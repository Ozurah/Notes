> <span style="font-size: 1.5em">📖</span> <span style="color: yellow; font-size: 1.3em;">Présentation `1.2 Recherche Heuristique`</span>

Stratégie pour trouver une solution.
On a des piste/méthode/technique pour trouver une solution.

Comment : En ayant un score à chaque résultat

# Problème recherche aveugle
Pas d'historique des résultats

Complexité en espace
    - Nombre de nœuds à mémoriser croît de façon exponentielle (dans le cas de largeur d’abord)
    - Envisager l’élagage/taille (pruning) de l’espace de recherche par des heuristiques (recherches informées)

# Définition
![](Screen/2022-10-04-13-50-02.png)

Quand `h(s) = 0` la solution est trouvée

# Distance de manahttan
Déplacements horizontaux et verticaux

# Meilleur d'abord
 - Glouton

Caractéristiques :
- Complet : (Oui, sauf si y a des doubles) (pas de boucles car on a l'historique) 
- Temps : O(b^m) : exponentiel, mais possible d'améliorer en O(bm) en fonction de la heuristique choisie.
- Espace : O(b^m) : à cause de l'historique
- Optimal :

# Qu'est-ce qu'une bonne heuristique ?
Admissible si $h(s) \leq h^*(s) \leq h*(n)$ <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// h*(n) = coût optimal réel de n au but</span> 

![](Screen/2022-10-04-14-30-54.png)
h3 est **inadmissible**, car nous aurions **2** (case vide & case 1 sont mal placé), hors nous n'avons besoin que de **1** déplacement