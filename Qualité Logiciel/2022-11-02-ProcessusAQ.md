> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation `Chapitre 05 : Processus AQ`</span>


# QA / QC
QA = Quality Assurance
QC = Quality Control

![](Screen/2022-11-02-08-24-01.png)

# Types de processus de développement

![](Screen/2022-11-02-08-25-00.png)


# Méthologies

- Processus en **cascade** (Waterfall)
  - Gros problème : les tests sont fait très tard, et donc très risqué
  - ![](Screen/2022-11-02-08-26-19.png)
- Processus en **V**
  - Waterfall, mais corrige l'injection des tests (branche de gauche)
  - Mais le rendu du client se fait toujours très tard
  - ![](Screen/2022-11-02-08-37-24.png)
- Processus adaptatifs ou itératifs
  - Cycles de développements très cours (**Sprints**)
  - Avoir toutes les 3 semaines une version utilisable et fonctionnelle
    - ![](Screen/2022-11-02-08-40-22.png)
    - difficulté : on a des feedbacks tout le temps, il faut donc bien géré entre "nouveauté" et "correction clients"
  - Processus **Agiles**
    - Toutes les fonctionnalités souhaités, puis séance client pour choisir les fonctionnalités du sprint en cours
    - **Scrum** : ![](Screen/2022-11-02-08-44-20.png)
    - Users Story : déscription d'une fonctionnalité
      - 1. `Rôle` ("en tant qu'utilisateur", "en tant que ...")
      - 2. `Done`, critères pour valider la fonctionnalités (80% tests, effectue ceci, etc.)
    - Efficace pour des équipes de 5 à 7