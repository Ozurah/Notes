Récupéré le contneu d'une map plusieurs techniques (pour grouper):

- `.collect(Collectors.toMap( {1}  ,  {2}   ))`
  - {1} : keyMapper
  - {2} : valueMapper
  - ![](Export/Collect-ToMap.svg)
  - chaque valeur (distincte) contient une entrée dans la map
- `.collect(Collectors.groupingBy( {1}  ,  {2}   ))`
  - {1} : functionClassifier <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// Créé les clusters</span> 
  - {2} : valueCollector
  - ![](Export/Collect-GroupingBy.svg)
  - Chaque valeur ayant le même classifier sont regroupé à la suite dans une string
- `.collect(Collectors.partitionningBy( {1}  ,  {2}   ))`
  - {1} : predicatClassifier // on l'utilise quand c'est binaire
  - {2} : valueCollector


Pour dégrouper : `.flatMap( {1}  )`
- {1} : function <span style="color: #46b7ae; font-style: italic; font-size: 0.85rem">// Exemple Arrays::stream</span> 