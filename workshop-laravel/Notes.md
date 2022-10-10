> Syntaxe **Blade**:  
> @foreach
> @endforeach


>double {}
```php
<a href="{{route("books.create")}}"></a>

Sera traduit en : 
<a href="<?php echo e(route("books.create")); ?>"</a>
=>
<a href="/books/create"></a>
```


>return view : renvoie une vue sans changer l'URL
return redirect : envoie une requete pour changer l'URL


>\$book = Book::findorfail(\$id);
Génère une erreur géré par Laravel si l'id n'existe pas

------

> `Book::create($request->all());` request all n'est possible (provoque une erreur) pour éviter qu'un utilisateur non admin puisse modifier la requete pour ce mettre comme admin.
> all renvoie tous les champs ! (même admin) --> par sécurité on indique explicitement les champs autorisés
```php
    $book = new Book();
    $book->title = $request->title;
    $book->author = $request->author;
    $book->description = $request->description;
    $book->save();

    Book::create($book);
```

S'il on veut use le -all, il faut se protéger dans le modèle (Book.php) avec la fonction fillable
```php
    protected $fillable = ["title", "author", "description"];
```
(on précise quel champs sont autorisés)

Solution à choix.

----


# Conseils pour le projet
>Ne jamais mettre à jour une migration poussée sur le répo.
(en créer une nouvelle)

>Toujours valider les requêtes : utiliser les objets Request !

> Utiliser les collections Laravel !
(Eloquent les utilisent dans ses réponses)

> Attention aux `SELECT N+1`
> (Ne pas filtrer en PHP, mais lors de la requête SQL)
> 
> Ex. On a une table "Livre" et une table "Auteur" :
> on va faire une jointure
> <span style="color: red"> Et non pas</span> : requete pour obtenir les livres, puis pour chaque livre obtenu en PHP, requete pour obtenir l'auteur
>
> pour 10 lignes, ça marche bien, mais quand il y a bc de table/entrée, sa prend beaucoup de temps !! (et ça peut faire planter la page)
> <span style="color: red">Erreur de débutant !! Les profs sont strictes dessus !</span>  