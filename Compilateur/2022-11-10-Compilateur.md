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

## Automates à état finis non déterministe
NFA = Non Deterministic Finite Automata

![](Screen/2022-12-01-08-42-04.png)

### Exemple
![](Screen/2022-12-01-08-43-27.png)

## Automates à état finis déterministe
DFA = Deterministic Finite Automata
![](Screen/2022-12-01-08-44-43.png)

## NFA -> DFA
![](Screen/2022-12-01-08-45-34.png)

![](Screen/2022-12-01-08-46-06.png)

<!-- #region NOTE BLOCK --> 
<div style="margin: 20px auto; padding: 10px; background-color: #ffd48a; border-left: 5px solid #8a5700;color: black; font-size: 2em">
<span> 📑 </span>Note<br>
<span style="font-size: 0.75em">
Le déroulement des étapes est montré visuellement dans les slides 68-73
</span></div>

<!-- #endregion NOTE BLOCK -->

## Expressions régulières

### types pour les regex
De "mathématiquements", les regex ne sont pas vraiment des expressions régulières, mais elles se bases sur la théorie des expressions régulières.
![](Screen/2022-12-01-09-11-42.png)
> Il y a une erreur avec le schéma : les regex couvrent TOUT le type 3, en plus d'une partie du type 2
> palindrome : exemple : SUGUS, KAYAK, etc.

## Conclusion 
![](Screen/2022-12-01-09-22-44.png)

# Grammaire non contextuelles (type 2+3)
> slides 82+

![](Screen/2022-12-01-09-33-32.png)

![](Screen/2022-12-01-09-35-52.png)

![](Screen/2022-12-01-09-36-12.png)
> On constate qu'on a pas la priorité des opérations -->
> Deux arbres de dérivations différentes pour le même mot ==> **<span style="color: red">Grammaire ambiguüe</span>** 

![](Screen/2022-12-01-09-38-51.png)
> Rappel : 
> - Analyse décendante : LL
> - Analyse ascendante : LR