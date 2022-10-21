> <span style="font-size: 1.5em">📖</span> <span style="color: yellow; font-size: 1.3em;">Présentation `3250.1 0-Introduction aux compilateurs`</span>



Lecture d'un calcul

![](Screen/1.png)

Parcours en profondeur pour faire une pile, quand on a un opérateur, on dépile les 2 dernier nombres
> Pile après chaque états : 
> 1
> 123
> 123*
> 16
> 16+
> 7


Lexeur : Traduit la donnée `ici le calcul` en un arbre
--> diagramme d'état

Exemple en français :
Phrase (P) -> GN > GV

![](Screen/2.png)

`le chat` : GN
`mange` : GB

Partie scémentique : vérifie que l'ordre des données est correct
- `Le souris mange la chat` ne joue pas (le/là)
- `La souris mange le chat` ne joue pas (logique)
- `Le chat mange la souris` OK


----

Transpiler : compilateur d'une langage de haut niveau vers un autre

![](Screen/3.png)

![](Screen/2022-09-22-09-17-03.png)

<span style="color:red">Le linker est très important ! On l'oubli souvent</span>
![](Screen/2022-09-22-09-26-43.png)


----
> <span style="font-size: 1.5em">📖</span> <span style="color: yellow; font-size: 1.3em;">Présentation `3250.1 1-Analyse Lexicale`</span>









# REGEX

## Liste 
- .  n'importe quel caractère
- ^ début de ligne
- $ fin de ligne
- * répétition 0-n
- + 1-n
- ? 0-1
- {} répétion [spécifié] fois
- [] ensemble de caractères
- \ echapement
- | ou
- () groupe


[0-9] == \d
[^0-9] == \D
[0-9a-zA-Z] == \w
[^0-9a-zA-Z] == \W

## exemples
![](Screen/2022-09-22-10-51-26.png)
![](Screen/2022-09-22-10-52-24.png)
![](Screen/2022-09-22-10-53-17.png)




-----------
------------
------------

# Types de grammaires

Grammaire de type 3 et 2 : Arbres
Grammaire de type 1 et 0 : Graphes

Nous on fait du type 2

## grammaire type 3 
- automate d'état fini
- regex (lexical) (exemple lire une plaque de voiture)

> non-terminal -> terminal non-terminal
non-terminal -> terminal

## grammaire type 2
- automate d'état à pile
- (syntaxique) (permet exemple de faire des opérations
>non-terminal -> répétitions de terminal non-terminal
non-terminal -> terminal

## grammaire type 1
- automates linéaires bornés (on a des curseurs)
> terminaux plusieurs non-terminaux teminaux -> ...

## grammaire type 0
- machine de turing
- Lire des infos sur la bande, faire des opérations, écrire, etc.