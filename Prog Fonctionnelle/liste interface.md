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


Interface | Methode | Action | Terminal | Remarque | Exemple
---|---|---|---|---|---|
Predicate\<T> | filter | Filtrer une collection |
Consumer\<T> | foreach | Applique une action pour chaque élément | **action terminal**
BinaryOperator\<T> | reduce<br>_arg initValue : valeur initial, ex pour + c'est 0, mais pour un * c'est 1_ | réduction du nombre d'information de même type (**n à 1 object**) || _(int + int = int; double + double = double; ~~<span style="color: red">int + string = qqc)</span>~~_ | Elire 1 délégué parmis toute la classe
Function\<T, R> | apply | applique une action sur chaque élément et retourne un nouveau type (**n à n object**) | Non || exemple : transformer une liste de personne en liste de nom de personne
ToXFunction\<T> | applyAsX | | | Idem que précédemment, mais le type de retour est prédéfini
BiFunction<T1, T2, R> | apply; andThen|||(x,y) -> x^2 + y^2 <br>Si X et Y sont des ints, équivalent à : **IntBinaryOperator** |
Supplier\<T>| get | retourne un objet de type T | | |
Comparator\<T> | sort | trier une collection | | |


Méthode par défaut : se sont des méthodes supplémentaires des interfaces qui sont déjà implémentées de manière **universelles** dans les classes

Interface | Méthodes par défaut
---|---
List | stream, parallelStream, forEach
Comparator | reversed
Predicate | negate, and, or
Function | compose, andThen
set | stream


# Interface fonctionnel (qui ne sont <span style="color: red">pas</span> de programmation fonctionnel)
Interface | Méthode | Action | Remarque
---|---|---|---|
Iterable\<T> | | | Iterator n'est pas une IF, elle contient plusieurs méthodes
Runnable | run | Exécute une action (threadable) | |
Comparable\<T> | sort | trier une collection | |

# Utilitaires

Classe | Utilité | Exemples/Remarque
---|---|---
Collectors | permet diverses opérations de réductions | https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html
`Streams.stream(iterable)` | Stream sur un itérable | homemade du prof. <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// C'est très complexe à faire sinon</span> 

## Exemples Collectors

```java
// Accumulate names into a List
List<String> list = people.stream().map(Person::getName).collect(Collectors.toList());

// Group employees by department
Map<Department, List<Employee>> byDept
    = employees.stream()
            .collect(Collectors.groupingBy(Employee::getDepartment));

// Compute sum of salaries of employee
    int total = employees.stream()
        .collect(Collectors.summingInt(Employee::getSalary)));

// Autres méthodes
Collectors.summingInt(mapper) // mapper == par exemple toIntFunction
reducing(init, mapper, BinaryOperator)
reducing(init, binaryOperator)
Collectors.toList()
Collectors.toSet()
Collectors.toCollection(Supplier)
```



# BY SEB
Résumé des interfaces fonctionnelles :
```
┏━━━━━━━━━━━━━━━━━━━━━━━┯━━━━━━━━━━━━┯━━━━━━━━━┓
┃ Interface             │ Input      │ Output  ┃
┣━━━━━━━━━━━━━━━━━━━━━━━┿━━━━━━━━━━━━┿━━━━━━━━━┫
┃ Function<T, R>        │ T          │ R       ┃
┃ IntFunction<R>        │ int        │ R       ┃
┃ ToIntFunction<T>      │ T          │ int     ┃
┃ BiFunction<T, U, R>   │ (T, U)     │ R       ┃
┃ ToIntBiFunction<T, U> │ (T, U)     │ int     ┃
┠───────────────────────┼────────────┼─────────┨
┃ UnaryOperator<T>      │ T          │ T       ┃
┃ IntUnaryOperator      │ int        │ int     ┃
┃ BinaryOperator<T>     │ (T, T)     │ T       ┃
┃ IntBinaryOperator     │ (int, int) │ int     ┃
┠───────────────────────┼────────────┼─────────┨
┃ Supplier<T>           │ ()         │ T       ┃
┃ IntSupplier           │ ()         │ int     ┃
┠───────────────────────┼────────────┼─────────┨
┃ Consumer<T>           │ T          │ ()      ┃
┃ IntConsumer           │ int        │ ()      ┃
┃ BiConsumer<T, U>      │ (T, U)     │ ()      ┃
┠───────────────────────┼────────────┼─────────┨
┃ Predicate<T>          │ T          │ boolean ┃
┃ IntPredicate          │ int        │ boolean ┃
┃ BiPredicate<T, U>     │ (T, U)     │ boolean ┃
┗━━━━━━━━━━━━━━━━━━━━━━━┷━━━━━━━━━━━━┷━━━━━━━━━┛
```
Int peut être remplacé par Long ou Double