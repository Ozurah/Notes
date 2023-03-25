> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `3 CalibrageCamera`</span>

# Matrices
![](Screen/2023-03-20-13-09-34.png)

!!! info Formules
    Les formules et étapes sont expliqués de la slide 17 à 31

![](Screen/2023-03-20-13-11-17.png)
_slide 25_ 

**Paramètres intrinsèques** de la caméra :
- Pas besoin de calibrer cette matrice
- points internes de la caméra (focale, centre optique, etc.)
- 
**Paramètres extrinsèques** de la caméra :
- C'est ça qu'on va devoir calibrer
- Emplacement de la caméra par rapport à l'objet


# Mire de calibrage
![](Screen/2023-03-20-13-18-28.png)

Repère vert = repert de l'image en pixel
Rouge = Repère de l'image avec le calibrage (unité = mètres, ou "[unité]" (la taille du carré))
En jaune traitillé == coordonée en pixel du point dans l'image
En rouge traitillé == coordonées en [unité] du point dans l'image

# Distorsion non linéaire

## Radiale
![](Screen/2023-03-20-13-23-51.png)
![](Screen/2023-03-20-13-24-12.png)
![](Screen/2023-03-20-13-25-00.png)

## Tangentielle
![](Screen/2023-03-20-13-26-39.png)

## Risques d'une correction 
Corrigé une image distordue aura pour effet d'avoir de la perte d'information.

Pour corriger, on va étirer l'image pour avoir l'image non distordue. Une fois fait, on recadre l'image pour retirer les zones noires.

![](Screen/2023-03-20-13-29-55.png)