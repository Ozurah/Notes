> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `3250.1 5-Cours Langage Et Grammaires Formels`</span>

# Intro

Grammaire : ensemble de règles, 
G = {R, N, T, S}

- **Règle** (R) : ensemble de symboles
  - R : N =  {T, S}
  - > exemple 
    > P -> S
    > S -> E + E
- N : ensemble de **non terminaux** (S, E, P)
- T : ensemble de **terminaux** ( +, -, 0, 1, a, b, ...)
- S : **symbole de départ** (P)

![](Screen/2022-11-10-09-20-36.png)

## Application

![](Screen/2022-11-10-09-23-58.png)

# Généralités
## Termes

![](Screen/2022-11-10-09-27-07.png)
![](Screen/2022-11-10-09-28-44.png)
![](Screen/2022-11-10-09-29-27.png)
![](Screen/2022-11-10-09-30-11.png)

# Langage
![](Screen/2022-11-10-10-09-38.png)

> 1[rien], 01, 001, 0001, etc.
> Ce langage ce termine par `1`, et il contient entre 0 et n `0` avant
> Donc, le langage s'écrit : $L = \{0^n1 | n \geq 0\}$

## Classification des grammaires
Type :
- 0 : Grammaire générales
- 1 : Grammaire contextuelles
- 2 : Grammaire non contextuelles
- 3 : Grammaire régulière 
![](Screen/2022-11-10-10-17-29.png)

### Exemple Type 0
![](Screen/2022-11-10-10-19-04.png)

### Exemple Type 1
![](Screen/2022-11-10-10-20-50.png)

### Exemple Type 2 (celui qu'on fait habituellement)
![](Screen/2022-11-10-10-21-18.png)

### Exemple Type 3
![](Screen/2022-11-17-09-12-09.png)
![](Screen/2022-11-17-09-13-00.png)
![](Screen/2022-11-17-09-13-14.png)

# Automates à état finis (Grammaire de type 3)
![](Screen/2022-11-17-09-14-25.png)