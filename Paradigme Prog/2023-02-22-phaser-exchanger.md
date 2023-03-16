> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `Phaser&Exchanger`</span>

# Phaser

"Fusion" entre une barrière cyclique et le CountDownLatch.

Permet de le configurer comme un CountDownLatch ou comme un CyclicBarrier.

## Comme barrière cyclique

```java
Phaser phaser = new Phaser(1);
phaser.register();
phaser.arriveAndAwaitAdvance();
```

## Comme CountDownLatch

```java
Phaser phaser = new Phaser(1);
phaser.register();
phaser.arriveAndDeregister();
```

# Exchanger
Permet d'échanger des objets entre 2 thread, sans synchronisation explicite.

Exemple d'échange entre 2 threads :

```java
Exchanger<String> exchanger = new Exchanger<>();
new Thread(() -> {
    try {
        String message = exchanger.exchange("Hello");
        System.out.println("Thread 1 : " + message);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}).start();

new Thread(() -> {
    try {
        String message = exchanger.exchange("World");
        System.out.println("Thread 2 : " + message);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}).start();

// Output :
// Thread 1 : World
// Thread 2 : Hello
```

et si on a 3 threads :

```java
Exchanger<String> exchanger = new Exchanger<>();
new Thread(() -> {
    try {
        String message = exchanger.exchange("Hello");
        System.out.println("Thread 1 : " + message);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}).start();

new Thread(() -> {
    try {
        String message = exchanger.exchange("World");
        System.out.println("Thread 2 : " + message);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}).start();

new Thread(() -> {
    try {
        String message = exchanger.exchange("!");
        System.out.println("Thread 3 : " + message);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}).start();

// Output :
// Thread 1 : World
// Thread 2 : Hello
// Thread 3 : !
```

On remarque que le 3eme à son propre message.
Pourquoi ? :
- chaque appel à la méthode exchange échange l'objet courant avec l'objet reçu en paramètre. 
- Ainsi, dans ce cas, le troisième thread échange l'objet "!" avec lui-même, car il n'y a pas d'autre thread en attente à ce moment-là. Cela explique pourquoi le troisième thread affiche son propre message.