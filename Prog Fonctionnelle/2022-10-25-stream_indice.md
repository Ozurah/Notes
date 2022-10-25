Les streams précédemment étudiée servait pour les données.
Maintenant nous allons voir les streams pour les indices.

# Contexte
Pour faire du parralelissme, ce qui dure long c'est les boucles !

```java
for (int i = 1; i < 1000000000; i++) {
    // ...
}
```

Une boucle `for` nous permet d'obtenir des indices.
Les streams d'indices permettront de remplacer les boucles `for`.

# `for` d'avant à maintenant

## `for` simple (++)
```java
list = ...
for (int i = 0; i < list.size; i++) {
    System.out.println(i);
}

// Remplacer par ce qu'on a vu précédemment (lambda)
IntConsumer print = i -> System.out::println(i);
list.forEach(print); // pas de gain de performance

// avec référence de variable
list.forEach(System.out::println); // pas de gain de performance

// Nouveauté : range  // gain de performance
IntConsumer print = i -> System.out::println(i);
IntStream.range(0, list.size()).forEach(print);

// ou en monoligne :
IntStream.range(0, list.size()).forEach(System.out::println);
```


## `for` avec un pas de 2 (+= 2) ==> streams infinis
```java

for(int i = 0; i < n; i = i + 2)
    {
    System.out.println(i);// affiche nombre paire
    }

// stream : lamda dans variable
UnaryOperator<Integer> inc2 = i -> i+2; // incrementer de 2
Consumer<Integer> print = System.out::println;

Stream // Stream<Integer>
    .iterate(0, inc2) // stream infinite
    .limit(n / 2) // warning n/2 : pour conserver la condition initial du for : i < n. Comme on incrémente de 2, on atteind la limite 2x plus vite
    .forEach(print);

// et sans variable :
IntStream // 10x plus rapide que Stream<Integer> car on a que des types simples et pas des objets
        .iterate(0, i -> i + 2) // stream infinite
        .limit(n / 2) // warning n/2 : pour conserver la condition initial du for : i < n. Comme on incrémente de 2, on atteind la limite 2x plus vite
        .forEach(System.out::println);
```

