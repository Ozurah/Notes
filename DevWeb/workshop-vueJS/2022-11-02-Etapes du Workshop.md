# Setup

# Extension pour le navigateur
https://devtools.vuejs.org/guide/installation.html
![](Screen/2022-11-02-15-11-51.png)
et après dans les outils de développement :
![](Screen/2022-11-02-15-11-31.png)


## Extensions VSC : 
https://marketplace.visualstudio.com/items?itemName=Tobermory.es6-string-html
Utile pour les balises HTML dans du PHP (colorisation syntaxique)

Colorisation syntaxique pour les éléments `Vue` dans les fichiers `.html`
https://github.com/johnsoncodehk/volar

Intégration de VueJS au projet : `<script src="https://unpkg.com/vue@3.2.37"></script>`


# init

**`Main.js`** :
```js
const app = Vue.createApp({
    data: function () {
        return {
            title: "Achat de café Nespresso",
            description: "Hello world",
            image: "assets/images/colombia.png",
            link: "https://www.nespresso.com/fr/fr/produits/cafe-en-grains/colombia",
        }
    }
});
```

**`index.html`** :
```html
 <div id="app">
    <h1>
      <a :href="link">
        {{ title }} <!-- on récupère la variable title -->
      </a>
    </h1>
    <p>{{ description }}</p>
    <img v-bind:src="image" height="200" />
  </div>

  <script src="./main.js"></script>

  <script> // Une nouvelle balise, c'est important ! (ne pas utiliser celle avec le src main.js)
    const mountedApp = app.mount('#app') // Notre objet Vue sera dans cette balise
  </script>
```

## Explication éléments
- `{{ }}` : mention qu'il s'agit d'utiliser une variable
- Dans les attributs, `v-bind:` permet à vue de comprendre que c'est une variable qui est indiqué
  - simplification explicite de`v-bind:` en `:`

# Conditions

- `v-if` sont bien, mais va charger et décharger le HTML.
On utilise le `v-show` qui va juste modifier le CSS (l'élément est toujours présent dans le DOM)

```html
<p v-if="inStock > 5">
    En stock
</p>
<p v-else-if="inStock <= 5 && inStock > 0">
    Plus que {{ inStock }} en stock
<p v-else>
    En rupture de stock
</p>

<p v-show="inStock > 5">
    Test
</p>
```

# Listes

- `v-for` : boucle sur une liste, pas très performant s'il y a beaucoup de données

`:key` est important pour `vue` afin d'optimiser l'affichage en rendant les éléments uniques. Utile quand il y a beaucoup de donnée, ou de l'animation. <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// Ce mot clé  ne sert que pour `vue`.</span> 

```html
<ul>
    <li v-for="detail in details">{{ detail }}</li>
</ul>

<div v-for="image in carouselImages" :key="image.id">
    {{image.text}}
</div>
```

# Bouton

`v-on` permet de déclencher une action lors d'un événement (click, mouseover, etc.), peut être simplifié par `@`

```html
<div>
    Panier ({{cart}})
</div>

<button v-on:click="cart += 1">
    Ajouter au panier
</button>
```

On remarque qu'appuyer sur le bouton va automatiquement update la valeur du panier

# Méthodes

**`main.js`** : 
```js
const app = Vue.createApp({
    data: function () {
        return {
            // ... les données au format dict
        }
    },
    methods: {
        //addToCart: function () {      // Ancienne syntaxe
        addToCart() {                   // Nouvelle syntaxe
            this.cart += 1
        }
    }
});
```

et on update le bouton d'avant en lui passant la méthode qu'on vient de créer :

**`index.html`** :
```html
<button v-on:click="addToCart()">
    Ajouter au panier
</button>
```

# Styles

3 manières de modifier le style :

**universelle** : 
```html	
<li v-for="detail in details" :key="detail.id" :style="{color: detail.color}">
    {{detail.text}}
</li>
```

via un **objet `style` dans le `main.js`**
```js
data: function () {
    return {
        // ... les données au format dict
        styles:
        {
            roundButton: {
                borderRadius: "20px",
                padding: "10px",
                backgroundColor: "rgb(0, 114, 180)",
                color: "white",
                cursor: "pointer"
            }
        },
    }
```

avec le **CSS normal** (exemple sur le bouton désactivé prend la classe "disabledButton")

index.html :
```html
<button v-on:click="addToCart" :style="styles.roundButton" :disabled="inStock <= 0" :class="{disabledButton: inStock <= 0}">{{stringCart}}</button>
```

pour la couleur du background, on peut utilisé aussi bien `background-color` que `backgroundColor`


# Computed properties

- Permet de créer des variables qui sont calculées à partir d'autres variables
Exemple pour la concatenation de texte, vue va mettre le résultat en mémoire comme ça il n'y a pas besoin de recalculer à chaque fois

**`main.js`**
```js
const app = Vue.createApp({
    data: function () {
        return {
            // ...
    },
    methods: {
        // ...
    },
    computed:
    {
        title() {
            return this.action + " " + this.brand;
        }
    }

});
```

# Composants

on commence dans le main.js; mais par la suite se sera déplacé dans un `.vue`

1. on créé la structure de l'objet dans le **`main.js`**
```js
app.component('product-display', {
    template:
    /*html*/
    `
    <h1>Super titre</h1>
    `,
    data() {
      return {
      }
    },
    methods: {
    },
    computed: {
    }
  });
```

2. on l'utilise dans le **`index.html`**
```html
<product-display></product-display>
```
      