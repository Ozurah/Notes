> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation [3 Scripting](http://enseignement.pages.ing.he-arc.ch/isc/cours/niveau-3/3292.2-infographie-unity/website/docs/cours/03-scripting/)</span>

Recherche de GameObject à l'execution, avec `GameObject.Find(name)`, `GameObject.FindWithTag(tag)` et `GameObject.FindGameObjectsWithTag(tag)`.

Ces méthodes sont à utiliser dans le `Start` ou `Awake`, il faut éviter de le faire dans update. Car la recherche nécessite de parcourir tous les GameObjects de la scène (l'arborescence).


# Destruction
```csharp
Destroy(gameObject);
```

L'objet ne sera pas détruit directement. Unity va mettre un flag sur l'objet et le détruire à un moment donné (normalement avant la prochaine frame).

Unity va mettre tous les objets marqués dans une zone de la mémoire et les supprimer tous en même temps (gain de performance).

-->> Ne pas partir du principe qu'un objet détruit est détruit.


# Coroutines

Ne sont pas des threads, donc attention si la coroutine est gourmande elle peut "freeze" le main thread.