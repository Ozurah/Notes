> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `09 Symmetric Encryption`</span>

# Ciphers
- Blocks cipher
  - pour le stockage
- Stream cipher
  - Pour le realtime

Le stream cipher est plus simple à implémenter

# Data Encryption Standard (DES)


Message de 64 bits + Clé de 64 bits
==> Cipher de 64 bits
<span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// La clé fait 56 bits, à la quel on rajoute 8 bits de parité (1 tous les 7 bits) = 64 bits</span>

16 étapes d'encryption

![](Screen/2022-12-07-10-26-56.png)



## S-Boxes (Substitution Boxes)
<span style="color: blue">1</span><span style="color: red">0111</span><span style="color: blue">0</span>  => 
- <span style="color: blue">10</span> => 2   => Ligne 2
- <span style="color: red">0111</span> => 7 => Colonne 7
- ==> la valeur est donc **1** (cf le tableau)

![](Screen/2022-12-07-10-38-01.png)

## Parity Check
Détection d'erreur
![](Screen/2022-12-07-10-47-03.png)

## Pourquoi pas le double DES ?
- Mieux que simple
- Mais plus faible, a cause du `meet-in-the-middle attack`

En regardant la clé `X` obtenue dans un sens, il est possible de trouver l'algorithme quand on récupère la clé `X` dans l'autre sens

![](Screen/2022-12-07-11-08-53.png)


------
------
> Slides 114+


![](Screen/2022-12-14-10-41-41.png)

- C'est pas une multiplication matricielle. mais une multiplication de cellules
  - (s00' = 02 * s00)

- On travail avec des bits : modulo 2
  - Raccourci pour faire une multiplication par 3 : (2 + 1) * sxy
  - Multiplication par 2 ==> décalage des bits à gauches selon l'algèbre modulo (juste après)

![](Screen/2022-12-14-10-46-02.png)
- `x^8 + x^4 + x^3 + x + 1` = `100011011
- 7*x^8 = x^8
- 8*x^8 = 0

# Stream Ciphers
- Facile à implémenter
- Sécurité forte, car beaucoup d'entropie (choses aléatoires entre tous les streams)
- Utiliser pour
  - Chiffrement
  - Génération de nombres aléatoires
- La clé n'est utilisée qu'une seule fois

## RC4
![](Screen/2022-12-14-11-03-20.png)