<!-- #region NOTE BLOCK --> 
<div style="margin: 20px auto; padding: 10px; background-color: #ffd48a; border-left: 5px solid #8a5700;color: black; font-size: 2em">
<span> 📑 </span>Note<br>
<span style="font-size: 0.75em">

Cette version n'est pas la plus optimale.
Cours du [2023-03-14](2023-03-14-Labo-SliceSM.md) pour la version optimale.
</span></div>

<!-- #endregion NOTE BLOCK -->



# Réduction additive (`Réduction +`) inplace

Pour nos algorithmes, on va travailler avec `n = 2^k`, avec `n == nombre de thread` (choisi par nous)

Puissance de 2 implique la possibilité de couper le tableau par 2 de sûre.

On répète l'opération `m` fois :
`m = n/2 = n >> 1` (il n'y a pas plus rapide qu'un opérateur de décalage de bits)
Tant que `m > 0` :

![algo réduction additive avec écrasement](./Export/algo-reduction-additive.svg)
> On remarque qu'a chaque fois on a besoin de moins de thread pour la mise en place du parallélisme.
> Les autres sont mis au "chômage"
> On vois que le thread "vert" va travailler 1x de plus que le bleu, 2x de plus que le rouge et orange, etc.

> Algorithmes récursif sont bienb moins performants.
> Ici on cherche la performance, donc on utilise un algorithme itératif.

## Algorithme CPP

```cpp
void reduce(float* tab, int n)
{
	int m = n >> 1;

	while (m > 0)
	{
		ecrasement(tab, m);
		m = m >> 1;
	}
}


void ecrasement (float* tab, int m)
{
	for (int i = 0; i < m; i++)
	{
		tab[i] = tab[i] + tab[i + m]
	}
}
```

## Problèmes de concurrence

Si l'on reprend le schéma, on remarque qu'il y a un problème de concurrence. On ne peut pas passer au `m` suivant tant que l'écrasement précédent n'est pas terminé.

Mais l'algorithme est naif, simple à comprendre et à implémenter. :D

## Algorithme CUDA

> Version non fonctionnelle, voir les explications plus bas

```cpp
// Etape 1 : ajout des parties CUDA
__global__ void reduce(float* tab, int n)
{
    // Chaque thread va executer le code ici
    // Il faut donc s'assurer que le contenu est correct, OK ici (avec synchronisation)

    int m = n >> 1;

    while (m > 0)
    {
        ecrasement(tab, m);
        m = m >> 1;

        // Ici il faut rajouter le fait d'attendre que tous les threads aient fini leur travail (écrasement en cours)
        __syncthreads();
    }
}

__device__ void ecrasement (float* tab, int m)
{
    // Chaque thread va executer le code ici
    // Il faut donc s'assurer que le contenu est correct, 
    // Ici il faut retirer la boucle for et remplacer par l'ID du thread

    const int TID = Thread2D.getTID();
    if (TID < m)
    {
        tab[TID] = tab[TID] + tab[TID + m];
    }
}
```

### Malheureusement, ça ne marche pas

`syncthreads()` ne fonctionne pas comme attendu. En pratique `syncthreads()` n'attend **que les** thread du **même** bloc.

> On imagine les filière infirmière, ingénieur, etc comme des blocs de thread. `__syncthreads()` appelé dans un bloc `ingénieur` n'attendra que sur les thread du bloc `ingénieur`, il n'attendra pas les `infirmières`.

==>> Il n'est pas possible de synchroniser coté device...

### Solution
Faire fonctionner `reduce` coté host et `ecrasement` comme global.

```cpp
// Etape 1 : ajout des parties CUDA
__host__ void reduce(float* tabGM, int n)
{
    // Ce code n'est plus executé par tous les threads
    // Il faut ajouter les instructions "dg db"

    dim3 dg(m, 1, 1);
    dim3 db(1, 1, 1); // On emploie que 1 coeur par multiprocesseur --> beaucoup de chômeur
    // Si on mettrait dg(1,1,1) et db(m,1,1) on aurait un seul thread qui ferait tout le travail. De plus "m" ne pourrais pas être supérieur à 1024 (taille max d'un bloc)
    // Comme amélioration, on pourrait factoriser "m" par a et b, et mettre dg(a,1,1) et db(b,1,1) pour avoir a*b threads. Si on fait ça, il faut aussi adapter le code pour réduire des fois dg, des fois db.

    int m = n >> 1;

    while (m > 0)
    {
        // Note : Il faut éviter de transmettre de l'information sur le PSIe (arguments)... ici tab et m ont une taille négligeable (une 12ène d'octets) donc c'est bon
        ecrasement<<<dg,db>>>(tabGM, m);
        // Pas de problème de concurrence ici, car on est coté host :
        // Barrière de synchronisation implicite, le driver NVidia va attentre que le kernel précédant soit terminé (donc qu'un seul kernel (global) à la fois, si un kernel est en cours, on attend qu'il soit terminé)
        // De même, si on a un "memcopy" on veut copier les résultats du kernel, donc un memcopy attend que le kernel soit terminé avant de passer à la suite du code

        m = m >> 1;

        dg.x = dg.x / 2; // On est coté host, ici on aura pas bc de performance à perdre, car l'host est par nature lent
    }
}

__global__ void ecrasement (float* tabGM, int m)
{
    // Chaque thread va executer le code ici
    // Il faut donc s'assurer que le contenu est correct, 
    // Ici il faut retirer la boucle for et remplacer par l'ID du thread

    const int TID = Thread2D.getTID();
    if (TID < m)
    {
        tabGM[TID] = tabGM[TID] + tabGM[TID + m];
    }
}
```
