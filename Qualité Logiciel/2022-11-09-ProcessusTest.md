> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `Chapitre 05 - Processus AQ`</span>
> Page 14+


![](Screen/2022-11-09-08-45-34.png)

Tailloring : customisation des méthodologies pour simplifier / garder que ce qu'on a besoin


![](Screen/2022-11-09-08-49-27.png)

Matrice de risque : 
- Description
- Probabilité
- Gravité (impact sur le projet)
- Difficulté à corriger
- Détectabilité : si le risque est détectable ou non (exemple une intrusion)

Mitigation : Une fois la matrice des risques faite, on décrit des action servant à limiter l'appariation d'un risque

Change and configuration management :
- Le client viens vers nous (quand on est bien avancé dans le projet) et nous demande de changer des fonctionnalités (gros changement comparé au cahier des charges)
- Comment réagir :
  - Qualifié, faire une étude
  - Refaire un nouveau cahier des charges
  - <span style="color: red">Ne pas faire le changement sans ça</span>
  - Protocoler la séance (Procès verbal décisionnel)
    - Si sur wiki gitlab, ajouter une mention `"en cas de non requête dans les 2 semaines après publication du PV, elle est considérée comme acceptée"`



> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `Chapitre 06 - Planification des tests`</span>

![](Screen/2022-11-16-09-04-11.png)

- **Efficacité** : On a des résultats à la fin
- **Efficiance** : Qu'utilise-t-on pour être efficace
- **Suitability** : Test adapté au contexte


<!-- #region NOTE BLOCK --> 
<div style="margin: 20px auto; padding: 10px; background-color: #ffd48a; border-left: 5px solid #8a5700;color: black; font-size: 2em">
<span> 📑 </span>Note<br>
<span style="font-size: 0.75em">
Slides 29+ juste vu de manière rapide (pas dans les détails -> pas pour le quizz)
</span></div>

<!-- #endregion NOTE BLOCK -->


![](Screen/2022-11-30-09-14-12.png)

Les critères sont :
- Les données de tests, exemples
  - Blackbox :  fichiers d'entrées / sortie attendue
  - Tests unitaires : in = arguments, out = valeur de retour, stacktrace d'échec, etc