# SM = Shared Memory

![](./Export/Mod%C3%A8le%20GPU.drawio.svg)

Très rapide, mais on en a très peux (48ko)

- Chaque thread partage la même instance de la mémoire partagée.
- On a donc pas 1 ins
- tance par "MP", mais par block
  - <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// Rappel : grid -> block -> thread</span> 

Il faut donc faire gaffe à ne pas la surcharger.

La shared memory est "matérielle", le tableau `tabSM` est logiciel
> allusion : Chaque block d'ingénieur à son armoire (orange), qui est accessible par tous les ingénieurs du block (orange) (`tabSM` est la "clé d'accès").
> (orange car les salles de cours sont orange)
> Si c'est un infirmier (block vert), ils recevrons les clés pour le "`tabSM`" du block des infirmiers (vert), mais pas celui des ingénieurs (orange)

> :orange: Pour la suite du cours chaque block orange == `tabSM` (mémoire partagée)


> Le block ingénieur fait la même chose que le block "infirmier", "chimiste", etc... mais tous avec leur propre `tabSM`
> --> **Programmation distribuée** **Massivement Parallèle**
> 


# Syntaxe

```cpp
__global__ void k()
{
    extern __shared__ float tabSM[]; // ⚠️ On ne mets rien dans les crochets
    // ⚠️ Ce n'est pas une déclaration de mémoire (on ne l'instancie pas), mais une "réception" de la variable
    // C'est le driver qui donne le pointeur du tableau, et chaque thread reçois un pointeur du tableau de la part du driver Nvidia
}
```

1. Le driver NVidia fait autant de `tabSM` que de block.
2. Le driver NVidia distribue le pointeur de `tabSM` à chaque thread du block

```cpp
__host__ void use()
{
    // Dans le host, on choisi la taille du `tabSM` (en octets (nombre de porte à notre "armoire")
    // n = nombre de cases dans le tableau
    // Actuellement n = nombre de thread par block (uniquement pour de la réduction)
    // n doit être une puissance de 2
    size_t sizeSM = n * sizeof(float);

    k <<<dg, db, sizeSM>>>();
}
```

# Avantages

- Mémoire plus rapide
- Code intégrallement sur le device (n'est plus géré par le Host)
- Respect des heuristiques
- On fait collaborer non pas chaque threads (128 "personnes différentes) mais chaque blocks (16 "personnes différentes") --> C'est plus simple de collaborer avec 16 personnes que 128

# Algorithme

> Imaginons que l'OFS est le `tabGM` et les armoires de la classe le `tabSM`
> Chaque personne (thread) de l'OFS effectue ses calculs et les envoie dans l'armoire.
> Pour regrouper les résultats, les ingénieurs collaborent et prennent les résultats directement dans l'armoire ou ils sont stockés. Ils ne doivent pas se déplacer jusqu'à l'OFS pour récupérer les résultats.


**Avant SM (on ne fait plus)**
1. Réduction IntraThread
   1. Prend les données à calculer et les réduits dans `tabGM`
2. Réduction avec `GM::memcpyDtoH_XXX` pour obtenir le résultat dans le Host

**Avec SM :**
1. Réduction IntraBlock
   1. Prend les données et les réduits dans `TabSM`
2. Réduction InterBlock
   1. Prend les données de `TabSM` et les réduits `ptrGMresult`

![](Export/schema-TP3_SliceSM.drawio.svg)

# Bibliothèque ReductionAdd
!!! info Pseudo Code

```cpp
__device__ void reductionInterBlock(float* tabSM, float* ptrResultGM)
{
    // Seul 1 "ingénieur" mets le résultat dans le `ptrResultGM` (par simplicité, on choisi le 1er thread du block :)
    if (TID_LOCAL == 0)
    {
        // *ptrResultGM = *ptrResultSM + tabSM[0];
        // C'est ce qu'on voudrait faire, mais on a un problème de concurrence --> 2 technique
        // 1. Utiliser un mutex
        // 2. Utiliser un atomicAdd (de Nvidia)

        atomicAdd(ptrResultGM, tabSM[0]);
        // (non sur de l'ordre, à vérifier)
        // Il n'y a pas d'atomicAdd pour les long (et d'autres types)
    }
}

__device__ void reductionIntraBlock(float* tabSM/*, int m*/)
// On a pas besoin de passer M, on peut le récupéré : chaque block dépose les valeurs dans leur case --> m = autant de thread par block
{
    int m  = Thread2D::getThreadBlock() // ⚠️ pas le bon nom de méthode, il faudrais rechercher la bonne
        >> 1; // On divise par 2

    // Ecrasements
    while (m > 0)
    {
        ecrasement(tabSM, m);
        m >>= 1; // On divise par 2

        // Problème de synchronisation, mais contrairement au TP 2, on peut utiliser `__syncthreads()`; car le nous travaillons sur un block, et comme `_syncthreads()` n'attend que les threads du même block, c'est bon !
        __syncthreads();
    }
}

__device__ void ecrasement(float* tabSM, int m)
{
    const int TID_LOCAL = Thread2D.get...();
    if (TID_LOCAL < m)
    {
        tabSM[TID_LOCAL] = tabSM[TID_LOCAL] + tabSM[TID_LOCAL + m];
    }
}

dg( , , 1)
db( , , 1)
```

!!! note ID d'un thread
    `tidLocal` == `tidLocalBlock` == `tidBlock`
    (pour correspondre en fonction du support)

## Contraintes :
dg :
- satisfaire heuristique 1 (H1)
- Nombre de block = nombre de multiprocesseur
db :
- satisfait heuristique 2 (H2)
- Doit être une puissance de 2
- égale à 1024

H2 :
- Le nombre de thread par block doit être un multiple du nombre de coeur par multiprocesseur (64)
  `[#nbThreadBlock] % [#nbCoreMP] == 0`
  - `[#nbThreadBlock]` == 64, 128, 256, 512, 1024
  - Le produit des 3 chiffres de db doivent donnée un des nombres ci-dessus
  Exemple : `db(64,1,1)`, `db(128,1,1)`, `db(32,2,1)`, `db(1024, 1, 1)`, `db(2, 512, 1)`

