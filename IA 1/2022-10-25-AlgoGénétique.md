> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation [Chapitre 1.3 - Algorithmes génétiques](https://cyberlearn.hes-so.ch/mod/resource/view.php?id=1895081)</span>

# Gain

![](Screen/2022-10-25-13-45-19.png)

Pour trouver le maximum global, les solutions sont :
- Dérivé (rarement possible en IA)
- Brutforce (impossible, trop de combinaisons et imaginons qu'il faut 1 minute par combinaison...)
- Brutforce avec une logique (ex. dichotomie et un pas défini)
- Solution : **s'insprier de la nature**

# Sélection naturelle
![](Screen/2022-10-25-13-51-08.png)
![](Screen/2022-10-25-13-52-52.png)
![](Screen/2022-10-25-13-54-21.png)

# Codage
![](Screen/2022-10-25-13-54-49.png)

Type de codage :
- binaire
- Alphabete
- Arbre

![](Screen/2022-10-25-14-01-35.png)
![](Screen/2022-10-25-14-02-37.png)

> Explication de la sélection, mutation, croisement : https://kushalmukherjee.medium.com/a-brief-introduction-to-genetic-algorithm-and-its-use-in-feature-selection-using-deap-81c7e2a3d3b9#:~:text=results%20than%20others.-,Genetic%20operators,-In%20genetic%20algorithms
# Sélections

![](Screen/2022-10-25-15-41-29.png)

**Fitnesse** : Il s'agit d'une méthode qui attribut un score à un individu. Plus le score est élevé, plus l'individu est adapté à la solution.

Par convention c'est fitnesse max; mais la librairie `DEAP` que nous utiliserons permet d'avoir un fitness min.

![](Screen/2022-10-25-14-04-32.png)

# Mutations
![](Screen/2022-10-25-14-29-20.png)
![](Screen/2022-10-25-14-29-41.png)

# Croisements
![](Screen/2022-10-25-14-30-04.png)


# ---

anytime : fournis une solution à tout moment, même si c'est pas la meilleure (exemple on a une réponse après la 1ère itération)