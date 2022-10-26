> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `Algebric Structures`</span>

<span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// P == Nombre premier</span> 


$GF(P) = {0,1,2,..., P-1}$ <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// c'est un modulo</span> 
toutes les valeurs entres 1 et P-1 sont obtenable par la partie multiplicative du groupe :
- GF(7) = { <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// On choisi un nombre entre 2 et p, ici on a choisi 3</span> 
  - $3^1 \% 7 = 3$
  - $3^2 \% 7 = 2$ 
  - $3^3 \% 7 = 6$ <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// (2 * 3) % 7 = 6 // on prend la valeur précédente, et on multiplie par 3</span> 
  - $3^4 \% 7 = 4$ <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// (6 * 3) % 7 = 6</span> 
  - $3^5 \% 7 = 5$ <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// (4 * 3) % 7 = 5</span> 
  - $3^6 \% 7 = 1$
  - On obtient tous les nombres sauf le 0
- }

Pour $GF(N)$, c'est un peu plus compliqué :
- plus de complément dans l'exercice 1 du devoirs de la semaine 5

# Identité de Bézout
gcd(a,b) = d
ax + by = d
==> Si et uniquement si le GCD == 1, alors : 
ax + by = 1
ax % b = 1
-> x est la multiplicative inverse de a modulo b
-->> $x = a^{-1} \% b$
$x \% b = a^{-1} \% b$


---
$k^{p-1} * k \% p = 1 * k$
-->
$k^{p} \% p = k$
$k^{p-1} \% p = 1$

$k^{p-2} \% p = k^{-1} \% p$


---

Astuce pour calculer sans faire la puissance : 
$5^{75} \% 2017$

On sait que le résultat ne dépassera pas 2016
on décompose l'exposant dans la forme d'euler :
![](Screen/2022-10-19-11-28-21.png)


# Nombre de racine primitives

$\varphi(\varphi(n)) \rightarrow \varphi(\varphi(p)) = \varphi(p-1)$ 
