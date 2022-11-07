> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `4-5 Filtrage du bruit`</span>

![](Screen/2022-11-07-13-39-36.png)

# Bruit Additif

Pourquoier ajouter du bruit : uniquement à but de tests

bruiter : fait un histograme pas très lisse
bruiter puis ajouter un égalisage (matrice de 1) = flouté, l'histogramme est resséré


## Uniforme

![](Screen/2022-11-07-13-48-57.png)
![](Screen/2022-11-07-13-46-50.png)
Quand on "bruite" on rajoute des nouveaux de gris
Ici on corrige tout à 20%

## Gaussienne

![](Screen/2022-11-07-13-47-29.png)
![](Screen/2022-11-07-13-48-23.png)
La courbe inidique la quantité % de pixels qui sont corrigés

![](Screen/2022-11-07-13-49-57.png)


# Filtrage du bruit
![](Screen/2022-11-07-14-19-15.png)

Il faut éviter les "escalier" avec le filtre gaussien 

Si c'est bruité avec gaussien et poivre-sel, il faut retirer en 1er le minmax (poivre-sel) et ensuite le gaussien, pour réduire les "escaliers" provoqués par le poivre-sel

![](Screen/2022-11-07-14-24-29.png)

## Conclusion
![](Screen/2022-11-07-14-24-58.png)

C'est difficile et sa prend du temps de filtrer une image qui est bruitée.
Solution : rechercher à retirer le bruit à la base : luminosité, changer la camera, etc.
-  Acheter une caméra 10x plus cher coutera moins cher que payé un ingénieur

# Note
Filtre médiane ==> Trie d'un tableau ==> Grosse complexité (n log(n), n², ...)