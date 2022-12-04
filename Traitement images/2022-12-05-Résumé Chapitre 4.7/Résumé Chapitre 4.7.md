---
# Configuration de Markdown Preview Enhanced
print_background: true # Pour l'export en HTML qu'il prenne le thème de la prévisu (par défaut c'est la prévisu de githublight)
title: Traitement d'image - Chapitre 4.7 &#58; Transformée de Fourier
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
              <div>Résumé du chapitre 4.7</div>
          </div>
          <div>
              <div></div>
              <div></div>
              <div>Transformée de Fourier</div>
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

<h0>Traitement d'images - Transformée de Fourier</h0>

> Couvre les slides 1 à 58

# Définitions

Jusqu'à maintenant, nous avons vu les `Transformations ponctuelles` et les `Transformations locales`.
![](Screen/2022-12-04-20-36-27.png)
~~> Dans ce chapitre, nous allons voir les `Transformations globales` qui sont des `Transformée de Fourier`

## Terminologie

Terme | Définition
--|--
**Basses fréquences** | Changements intensité lents
**Hautes fréquences** | Changements intensité rapides
**Domaine spatial** | L'image
**Domaine fréquentiel** | Le spectre


> par la suite, ces termes sont indiqués de cette manière : <ref>exemple</ref>

## Formules
Série de Fourier temporelle 1D
![](Screen/2022-12-04-20-44-55.png)

## Symboles
Symboles | Correspond à
--|--|--
$A(f_x, f_y)$ | Spectre
$\varphi(f_x, f_y)$ | Phase


# Fréquence dans une image
> Chapitre 4.7.1 : Slides 6 à 10

Un **signal périodique** peut être décomposé en une **somme de sinus**.

<ref>Basses fréquences</ref> | <ref>Hautes fréquences</ref>
--|--
![](Screen/2022-12-04-20-41-10.png) | ![](Screen/2022-12-04-20-41-22.png)

- Les <ref>basses fréquences</ref> sont présentes quand il y a de faibles changement d'intensité, les régions sont homogènes, il y a du flou.
- Les <ref>hautes fréquences</ref> sont présentes quand il y a de forts changements d'intensité, les contours, le bruit.

# Série de Fourier temporelle 1D
> Chapitre 4.7.2 : Slides 11 à 15
>
> Pour la compréhension des formules, voir la slide 13

Celle qui nous interesse est la transformée de Fouris discrète (DFT)
![](Screen/2022-12-04-20-50-37.png)

# Série de Fourier spatiale 2D
> Chapitre 4.7.3 : Slides 16 à 21

Domaine fréquentiel : **Spectre**, **Phase**

la composante continue corresponds aux flèches des valeurs du spectre ou de la phase.
Les zones de basses fréquences sont proches de l'origine.
Les zones de hautes fréquences sont loin de l'origine.

![](Screen/2022-12-04-22-51-48.png)

Relation entre plan spatial et fréquentiel :
![](Screen/2022-12-04-22-25-03.png)


# Transformée de Fourier discrète (DFT)
> Chapitre 4.7.4 : Slides 22 à 27

## Mise en forme du spectre

DC == Spectre centré
![](Screen/2022-12-04-22-55-51.png)

# Influences de paramètres sur le spectre
> Chapitre 4.7.5 : Slides 28 à 35

La composante continue est au centre du spectre.
![](Screen/2022-12-04-23-01-24.png)

## Fenêtre de Hanning
![](Screen/2022-12-04-23-03-16.png)
![](Screen/2022-12-04-23-03-30.png)

# Transformée de Fourier discrète inverse
> Chapitre 4.7.6 : Slides 36 à 39

Permet de retrouver l'image à partir du spectre et de la phase. L'image obtenue est plus "gris foncée" que l'image d'origine.

# Filtrage fréquentiel
> Chapitre 4.7.7 : Slides 41 à 53

## Fréquentiel vs Spatial
Le filtrage spatial correspond au noyau de convolution.
Alors que le filtrage fréquentiel correspond à la multiplication du spectre et de la phase par un masque.

## Passes-bas et passes-haut
![](Screen/2022-12-04-23-10-12.png)

Un filtre passe haut va inverser les couleurs et faire ressortir les contours. Le masque est un cercle noir sur fond blanc. Plus le cercle est grand, plus les contours principaux sont ressortis.
![](Screen/2022-12-04-23-12-52.png)

Un filtre passe bas va flouter l'image d'origine. Le masque est un cercle blanc sur fond noir. Plus le cercle est grand, moins l'image est floue.
![](Screen/2022-12-04-23-13-32.png)

## Filtrages sélectifs
Au lieu d'un cercle, le masque est un donut.

Le `coupe bande` est plus souvant utilisé que le `passe bande`.
![](Screen/2022-12-04-23-15-20.png)

Exemple du `coupe bande` :
![](Screen/2022-12-04-23-16-23.png)