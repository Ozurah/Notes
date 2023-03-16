> <span style="font-size: 1.5em">📖</span> <span style="color: orange; font-size: 1.3em;">Présentation [Introduction](https://unity3d.ch/docs/cours/00-introduction/)</span>

Unity est prévu pour le Temps réel (2 ou 3D).
Contrairement aux logiciels d'animation qui utilisent d'autres algorithmes


# Projet

Départ soit d'un projet vide, soit d'un template "URP" (conseillé car on est sur portable)
- Pipeline de rendu SRP (prend du temps à définir et c'est compliqué, tout est configurable)
- Unity propose deux pipeline de rendu préfait : URP et HDRP
  - URP est plus simple, plus rapide, plus léger (moins de gestion des reflexions, mais plus rapide pour par exemple la VR)
  - HDRP est plus complexe, plus lent, plus lourd. Plutôt pour des consoles de jeux très puissantes, comme la PS5. Quand la qualité visuel/calculs est primordiale.

Dans la hiérarchie des GameObjects, ceux qui sont bleus sont des instances d'un prefab (un modèle 3D). 
- Si on modifie le préfab directement, tous les objets prendrons ces modifications
- Si on modifie un objet directement, il ne sera pas modifié dans le préfab (il est possible d'appliquer les modifications au préfab)

# Raccourcis

Quand un objet est sélectionné
- `F` : focus sur l'objet (recentre la caméra sur l'objet, zoom, la caméra l'utilisera comme centre de rotation)