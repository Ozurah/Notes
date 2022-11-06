> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `Pattern Lecteur rédacteur`
> https://docs.oracle.com/javase/7/docs/api/index.html?java/util/concurrent/locks/ReadWriteLock.html
> </span>

#  ReadWriteLock
https://docs.oracle.com/javase/7/docs/api/index.html?java/util/concurrent/locks/ReadWriteLock.html


Résumé : le vérou possède deux mode : 1 lecture, 1 écriture

Si le verou est en lecture, tout le monde peut lire les informations
Si le vérou est en écriture, seul 1 personne écrit. Personne d'autre que lui peut lire les informations


![](Screen/image.png.png)


## Cas1: Priorité <span style="color: red">Absolue</span> des lecteurs sur rédacteurs
![](Screen/2022-11-03-14-41-27.png)

##  Cas2: Priorité <span style="color: red">Relative</span> aux des lecteurs sur rédacteurs
(environ priorité égale)

![](Screen/2022-11-03-14-47-11.png)
![](Screen/2022-11-03-14-48-45.png)

## Cas3: Priorité aux rédacteurs

Il faut ajouter une variable représentant de nombre d’attente de rédacteurs permettant de bloquer les lecteurs si des rédacteurs sont en attente.

![](Screen/2022-11-03-14-57-47.png)

# StampedLock

Autre type de LecteurRedacteur, mais avec une optimisation comparé au précédent


