# IF (Interface Fonctionnel)
Interface fonctionnel == 1 méthode

# Interfaces de <span style="color: green">programmation</span> fonctionnel

Pour les types simples, il existe des "IntXXX" ce qui remplace le **template** (exemple __IntBinaryOperator__) pour manipuler des int ; doube; bool; etc (gain de performance **énorme**)

<!-- #region NOTE BLOCK --> 
<div style="margin: 20px auto; padding: 10px; background-color: #ffd48a; border-left: 5px solid #8a5700;color: black; font-size: 2em">
<span> 📑 </span>Note<br>
<span style="font-size: 0.75em">

CF [exemple de type (exo 2022-04-10)](exo-2022-04-10.md)
</span></div>
<!-- #endregion NOTE BLOCK -->


Interface | Methode | Action | Remarque | Exemple
---|---|---|---|---|
Predicate\<T> | filter | Filtrer une collection |
Consumer\<T> | foreach | Applique une action pour chaque élément | **action terminal**
BinaryOperator\<T> | reduce<br>_arg initValue : valeur initial, ex pour + c'est 0, mais pour un * c'est 1_ | réduction du nombre d'information de même type (**n à 1 object**) | exemple élire 1 délégué parmis toute la classe<br><br>_(int + int = int; double + double = double; ~~<span style="color: red">int + string = qqc)</span>~~_
Function\<T, R> | map | applique une action sur chaque élément et retourne un nouveau type (**n à n object**) | exemple : transformer une liste de personne en liste de nom de personne<br><br>**Action <span style="color: green">non</span> terminale**
ToXFunction\<T> | | |  Idem que précédemment, mais le type de retour est prédéfini
BiFunction<T1, T2> ||||(x,y) -> x^2 + y^2 <br>Si X et Y sont des ints : **IntBinaryOperator**
Supplier<T>||||
Comparator<T>

# Interface fonctionnel (qui ne sont <span style="color: red">pas</span> de programmation fonctionnel)
Interface | Méthode | Action | Remarque
---|---|---|---|
Iterable<T> | | | Iterator n'est pas une IF, elle contient plusieurs méthodes
Runnable | run
Comparable<T> | sort
