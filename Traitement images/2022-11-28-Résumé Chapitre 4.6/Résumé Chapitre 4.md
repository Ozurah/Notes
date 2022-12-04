---
# Configuration de Markdown Preview Enhanced
print_background: true # Pour l'export en HTML qu'il prenne le thème de la prévisu (par défaut c'est la prévisu de githublight)
title: Traitement d'image - Chapitre 4.6 &#58; Morphologie
puppeteer:
    format: A4
    printBackground : true
    displayHeaderFooter: true
    margin: # le Header/footer ne prend pas ces paramètres en compte
        top: 2cm
        right: 2cm
        bottom: 2cm
        left: 2cm

    # taille de police requis, car par défaut c'est 0pt
    # id header/footer sont réservés : ph pour page header, pf pour page footer
    headerTemplate: '
      <style>
          #ph, #pf {
              width: 100%;
              font-size: 10pt;
              font-family: "Times New Roman", Times, serif;
              border: 0px solid #c3c3c3;
              margin: 0px 1cm 0px;
          }
          #ph {
            border-bottom-width: 1px;
          }
          #pf {
              border-top-width: 1px;
          }
          #ph > div,
          #pf > div {
              display: flex;
              justify-content: space-between;
          }
      </style>

      <div id="ph">
          <div>
              <div>Allemann Jonas</div>
              <div>Traitement d&#39;images</div>
              <div>Résumé du chapitre 4.6</div>
          </div>
          <div>
              <div></div>
              <div></div>
              <div>Morphologie mathématiques I</div>
          </div>
      </div>
    '
    footerTemplate: ' 
      <div id="pf">
          <div class="child">
              <div></div>
              <div></div>
              <div>
                  <span class="pageNumber"></span>
                  /
                  <span class="totalPages"></span>
              </div>
          </div>
      </div>
    '
---

@import "style.less"

<h0>Traitement d'images - Morphologie mathématiques I</h0>

> Couvre les slides 1 à 39

# Définitions
## Terminologie

Terme | Définition
--|--
**Région** | Ensemble de pixels connexes d'une image binaire.<br> bit **0** = **background**<br> bit **1** = foreground (l'**objet**)
**Elément structurant** | Formes géométriques et de taille connues. Exemple les carrés ou les cercles.
**Point d'ancrage** | **Centre** de l'élément structurant.

> par la suite, ces termes sont indiqués de cette manière : <ref>exemple</ref>

## Formules
![](Screen/2022-11-26-12-33-55.png)

## Symboles
Symboles | Correspond à
--|--|--
⊖ | Erosion
⊕ | Dilatation
<span style="color: lightgray">X</span><sup>C</sup> | Complémentaire (inversion des couleurs)
∘ | Ouverture
• | Fermeture

# Introduction
> Chapitre 4.6.1 : Slides 6 à 16

<table>
<tr>
<td>

Le **but** de la morphologie est de :
- Boucher les trous
- Adoucir les bords
- Enlever les points de fonds

> Sur l'image, les mots clés importants de la morphologie
</td>

<td>

![](Screen/2022-11-26-12-20-08.png)
</td>
</tr>
</table>

<div style="page-break-after: always;"></div>

## Méthodologie

<table>
<tr>
<td>

1. On pose un <ref>élément structurant</ref> sur une <ref>région</ref>
2. On **déplace** cet élément pour que le <ref>point d'ancrage</ref> pour qu'il passe par la totalité des pixels de l'image.
</td>

<td>

![](Screen/2022-11-26-12-34-33.png)
</td>
</tr>

<tr>
<td>

3. Pour chaque positions, vérifier l'<ref>union</ref> et l'<ref>intersection</ref> de l'<ref>élément structurant</ref> et les objets de l'image.
4. Reporter les résultats **positifs** sur la nouvelle image (nommée `image résultat`).
</td>

<td>

![](Screen/2022-11-26-12-38-52.png)
![](Screen/2022-11-26-12-43-36.png)
</td>
</tr>

<tr>
<td>

5. Obtention du résultat
   - En cas d'inclusion totale : nous érodons l'ojet
   - En cas d'intersection non nulle : nous dilatons l'objet

> Pour la similitude, c'est comme si nous augmentons ou diminuons la taille de l'objet.
</td>

<td>

![](Screen/2022-11-26-12-56-27.png)

> Similitude sous Gimp : *réduire* ou *agrendir* 
> ![](Screen/2022-11-26-12-51-20.png)
</td>
</tr>
</table>

## Eléments structurants

Les <ref>éléments structurants</ref> *(`B` dans les images qui suivent)* sont convertis en tableaux 2D. Comme par exemple ceux-ci : 
![](Screen/2022-11-26-13-01-39.png)

Sur ces éléments, il est possible d'effectuer des **réfléxions** et des **translations**.
![](Screen/2022-11-26-13-02-45.png)


<div style="page-break-after: always;"></div>

# Morphologie binaire
> Chapitre 4.6.2 : Slides 17 à 39

<!-- #region VARIABLE BLOCK --> 
<div style="margin: 20px auto; padding: 10px; background-color: #ade9f7; border-left: 5px solid #00158a;color: black">
<span style="font-size: 1.5em"> 🔡 </span><b>Variables</b><br>

`A` image source
`B` Elément structurant
</div>

<!-- #endregion VARIABLE BLOCK -->

## Erosion et Dilatation
> Slides 17 à 25

L'érosion et la dilation sont des opérations qui permettent de modifier la taille des objets. L'une ajoute de la "matière", l'autre en enlève.

### Erosion

L'**érosion** (`⊖`) à pour but de supprimer les pixels des bords de l'objet. C'est une opération qui **réduit** l'objet.

Notations : **A ⊖ B** = $E^B(A)$ = $\{ \vec{x} \mid B_x \subseteq A\}$


Les effets de l'érosions :
- Les parties plus petites que l'élément structurant sont **supprimées**
  ![](Screen/2022-11-26-14-02-26.png)
- Les autres parties sont **diminuées**
  ![](Screen/2022-11-26-14-04-47.png)
- Les trous sont **agrandis**
  ![](Screen/2022-11-26-14-05-40.png)
- Les objets peuvent se **séparer**
  ![](Screen/2022-11-26-14-06-17.png)

> La **connexité** des objets n'est **pas conservée**

### Dilatation

La **dilatation** (`⊕`) à pour but d'**ajouter** des pixels aux bords l'objet. C'est une opération qui **agrandit** l'objet.

Notations : **A ⊕ B** = $D^B(A)$ = $\{ \vec{x} \mid B_x \cap A \neq \emptyset \}$

Les effets de la dilatation :
- Les objets sont **agrandis**
  ![](Screen/2022-11-26-14-13-23.png)
- Les trous sont **diminués**
  ![](Screen/2022-11-26-14-15-56.png)
- Les objets peuvent **fusionner**
  ![](Screen/2022-11-26-14-16-34.png)

> La **connexité** des objets n'est en générale **pas conservée**

### Dualité

$A ⊖ B = (A^C ⊕ B)^C$
$A ⊕ B = (A^C ⊖ B)^C$

![](Screen/2022-11-26-14-28-32.png)


<div style="page-break-after: always;"></div>

## Ouverture et fermeture
> Slides 26 à 33

![](Screen/2022-11-26-14-33-25.png)

> Qu'est-ce qu'une isthmes : c'est des petites parcelles reliées à la terre ferme, exemple l'île saint-pierre du lac de bienne
> ![](Screen/2022-11-26-14-59-20.png)

### Ouverture

L'**ouverture** (∘) c'est : une **érosion** suivie d'une **dilatation**.

Notations : **A ∘ B** = (A ⊖ B) ⊕ B = $O^B(A)$

Exemple :
![](Screen/2022-11-26-14-37-26.png)

![](Screen/2022-11-26-14-38-54.png)

⤷ Les trous sont comblés sans modifier la forme générale de l'objet.

#### Propriétés :
- **Lisse** les formes
- **Elimine** les composantes connexes plus petites que l'<ref>élément structurant</ref>
- **Supprime** les
  - Petites iles (tâches)
  - Les isthmes
- **Conserve** souvant la taille et la forme
- Ne **préserve pas** la **connexité**
- Est idempotente (non itérative) : A ∘ B = A ∘ B ∘ B


### Fermeture

La **fermeture** (•) c'est : une **dilatation** suivie d'une **érosion**.

Notations : **A • B** = (A ⊕ B) ⊖ B = $F^B(A)$

Exemple :
![](Screen/2022-11-26-14-44-05.png)
![](Screen/2022-11-26-14-51-56.png)
⤷ Les tâches sont retirée, les objets proches fusionnent entre eux, sans pour autant modifier la forme générale de l'objet.

#### Propriétés :
- **Elimine** les trous plus petites que l'<ref>élément structurant</ref>
- **Supprime** les
  - Petits lacs (trous)
  - Les détroits (espaces faibles entre 2 objets)
  - Les golfes étroits (espaces faibles entre 2 isthmes)
- Ne **préserve pas** la **connexité** (soude les éléments proches)
- Est idempotente (non itérative) : A • B = A • B • B


## Applications
> Slides 34 à 39

Pour résumés l'utilité des opérations mentionnées précédemment, nous avons :

| Opération | Utilité | Exemple
--- | --- | ---
<ref>Région</ref>,<br>XOR sur l'érosion, dilatation | Déterminer les contours | ![](Screen/2022-11-26-15-37-17.png)
Erosion | Séparer des objets se touchant | ![](Screen/2022-11-26-16-15-29.png)
Dilatation | Augmenter la visibilité | ![](Screen/2022-11-26-16-16-30.png)
Ouverture | Filtrer le bruit selon la taille<br>(Eliminer les petites tâches) | ![](Screen/2022-11-26-15-37-54.png)
Ouverture puis fermeture | Enlever le bruit | ![](Screen/2022-11-26-16-17-32.png)

- **<ref>Région</ref>, XOR sur l'érosion, dilatation**
  - Déterminer les contours
    ![](Screen/2022-11-26-15-37-17.png)
- **Erosion**
  - Séparer des objets se touchant
    ![](Screen/2022-11-26-16-15-29.png)
- **Dilatation**
  - Augmenter la visibilité
    ![](Screen/2022-11-26-16-16-30.png)
- **Ouverture** 
  - Filtrer le bruit selon la taille<br>(Eliminer les petites tâches)
    ![](Screen/2022-11-26-15-37-54.png)
- **Ouverture puis fermeture**
  - Enlever le bruit
    ![](Screen/2022-11-26-16-17-32.png)
