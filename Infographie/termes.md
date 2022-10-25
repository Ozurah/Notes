# divers
Vocabulaire importants : pages 316+
- discretiser des triangle en fonction des pixels : rasterisation
![](Top-left_triangle_rasterization_rule.gif) [source](https://en.wikipedia.org/wiki/Rasterisation)

<!-- #region IMPORTANT BLOCK --> 
<div style="margin: 20px auto; padding: 10px; background-color: #ff8a8a; border-left: 5px solid #8a0000;color: black; font-size: 2em">
<span style="letter-spacing: -30px; margin-right:50px">❗❗</span>Important<br>
<span style="font-size: 0.75em">
A se souvenir
</span></div>

# visualisation
<!-- #endregion IMPORTANT BLOCK -->

- CANVAS, "projection plan","front plan","viewport" :
  - C'est les 4 fois le même terme, on change juste en fonction du contexte 
  - Frustum : la pyramide tronquée (le volume)
  - ![](Screen/2022-09-30-17-46-25.png)
  - ![](Export/Canvas%20termes.drawio.svg)

- <span style="color: red">Les termes des repères (se souvenir d'au moins 4 !)</span>
  - ![](Screen/2022-09-30-17-47-38.png)


### Les matrices / repères
- repère monde : coord(0,0,0) (pas forcément un monde, mais peut être par exemple la coordonée initial sur Blender)
- M1 (MM) : repère modèle / matrice modèle : coordonnée de l'objet dans le monde
- M2 (VM) : Matrice de vue : permet de voir les objets (placement de la caméra)
- M3 (PM) : matrice de perspective : matrice identité; permet de définir les distances / angle de vue



Tout ces éléments sont géré par le **Vertex Shader**

### Vertex shader

Il est appelé sur chacun des vertex.

calcul la position des points

position finale = M3 * M2 * M1 * vec4(position, 1.0)
<span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// (l'ordre est important comme les poupée russe)</span>

<!-- #region IMPORTANT BLOCK --> 
<div style="margin: 20px auto; padding: 10px; background-color: #ff8a8a; border-left: 5px solid #8a0000;color: black; font-size: 2em">
<span style="letter-spacing: -30px; margin-right:50px">❗❗</span>Important<br>
<span style="font-size: 0.75em">
Un vec2, vec3, vec4, etc n'a que 1 seule Dimension !!

$$\begin{vmatrix}
X1\\
Y1\\
Z1\\
\end{vmatrix}$$

Une matrice est 2D :

$$\begin{vmatrix}
X1 & X2 & X3\\
Y1 & Y2 & Y3\\
Z1 & Z2 & Z3
\end{vmatrix}$$
</span></div>

<!-- #endregion IMPORTANT BLOCK -->

