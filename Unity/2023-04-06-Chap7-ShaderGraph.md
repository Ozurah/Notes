> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation [7. Shader Graph](http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/website/docs/cours/07-shadergraph/)</span>

!!! info Shader Graphe est abrégé en SD

Système sous forme de graphe.

Type de programamtion : data flow programming

![](Screen/2023-04-06-09-12-17.png)

et sur un matérial :
![](Screen/2023-04-06-09-14-28.png) _(lit shader est le nom que j'ai donné à mon SD_)


# Edition du SD

Si on veut colorer un pattern (ici Voronoi), il faut le multiplier par une couleur :

![](Screen/2023-04-06-09-21-28.png)

!!! info Voronoi
    Pattern de bruit, qui va créer des "cellules" de bruit. Les niveaux de dégradé est le même et dépend de la distance entre les cellules 

On peut ensuite relier notre voronoi coloré au fragment
![](Screen/2023-04-06-09-23-54.png)

!!! remarque 
    ![](Screen/2023-04-06-09-32-29.png)
    On peut voir un petit bug visuel, ceci peut être lié à plusieurs choses. Mais c'est surement les normales qui sont orientées dans le mauvais sens.
    Sa peut également être lié à la carte graphique

    Pour corriger le problème, peut être désactiver le `backface culling` dans le shader

    Correction dans mon cas : 
    Changer le type de matérial dans le `Graph Settings` de `Sprite Lit` à `Lit`
    ![](Screen/2023-04-06-09-52-33.png)

Pour animer la texture, on ajoute un node "Time". Ici on va utiliser le temps pour changer l'angle des cellules
![](Screen/2023-04-06-09-37-24.png)


Pour ajouter des propriétés modifiable dans l'éditeur, on ajoute dans le `blackboard` des propriétés :
![](Screen/2023-04-06-09-36-36.png)

et on le lie au shader :
![](Screen/2023-04-06-09-38-19.png)

![](Screen/2023-04-06-09-38-40.png)

# Appliquer le shader sur une forme

Le shader est appliqué sur un matérial, mais si on ne spécifie pas comment géré la surface, il peut y avoir des problèmes d'affichage. Exemple un cube affichera le même contenu sur chaque face, et un cercle il aura du mal.

Il faut donc ajouter une UV map pour spécifier les "points de coutures"