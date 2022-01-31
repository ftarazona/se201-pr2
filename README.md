# SE201 - PR2

## Structure du dépôt 

- Le dossier `src`contient tout le code utilisé pour répondre aux questions.
- Le dossier `rapport` contient tous les fichiers utiliser dans la création du rapport (.md, images, Makefile pour la compilation en pdf)

## Fichiers sources

- Le code source et Makefile fournis se trouvent dans le dossier `src`. Nous avons modifier le Makefile afin de répondre plus facilement aux différentes questions. Vous pouvez taper `$make info` pour obtenir une liste des cibles possibles et leurs effets.


## Utilisation des Makefile pour MarkDown

Pour utiliser les Makefile compilant les fichiers .md (rapport et diagramme d'exécution), il faut procéder à quelques ajustements. Un argument de la ligne de commande utilisée est le chemin vers le pdf engine pdflatex. Cet argument est parfois optionnel, mais dans tous les cas il est propre à l'utilisateur.


