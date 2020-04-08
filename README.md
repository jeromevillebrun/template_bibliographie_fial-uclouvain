# template_bibliographie_fial-uclouvain
Un template LaTeX avec une page de garde ainsi que le style de bibliographie et de citation de la Faculté de philosophie, arts et lettres (UCLouvain), pour une utilisation avec LaTeX, réalisé avec le package biblatex.

## Compiler

À cause l'utilisation d'une police très rarement utilisée en typographie (les petites capitales en gras de la page de garde fonctionnent avec latex, mais pas avec xelatex), il est nécessaire de compiler `page_de_garde_fial.tex` séparément de `main.tex` et avant ce dernier. Dans un terminal linux, il faut donc taper :

    pdflatex page_de_garde_fial.tex
    latexmk -pdf -xelatex main.tex

Une fois que la page de garde a été compilée une fois, il n'est plus nécessaire de la recompiler systématiquement (la deuxième commande intègre le pdf généré par la première au document final `main.pdf`).

La compilation automatique sur [Overleaf](https://fr.overleaf.com/login) ne devrait donc pas fonctionner pour le moment. Il faudrait, à l'occasion, ajouter un fichier `latexmkrc`, mais je ne sais pas comment on fait.

## Conseils

Il existe un excellent livre (libre) sur l'utilisation de LaTeX dans les sciences humaines. Disponible à cette adresse : https://geekographie.maieul.net/95

## Contribuer

Le style bibliographique n'est pas du tout au point, et il est difficile de penser qu'il le sera un jour, vu l'étendue des ambiguités que présentent les normes bibliographiques de la FIAL (voir le fichier guide_references_bibliographiques.pdf). Toute aide et toute connaissance sur biblatex est la bienvenue (je suis pas un expert de LaTeX, j'essaye juste de me dépatouiller avec la documentation, mais ça n'est pas toujours évident).

Pour contribuer :

1. Forkez le repo.
2. Créez votre branche fonctionnalité (`git checkout -b ma-nouvelle-fonctionnalite`).
3. Committez les changements (`git commit -am "Explication de ce que vous avez fait`).
4. Pushez ça sur la branche (`git push origin ma-nouvelle-fonctionnalite`).
5. Créez la nouvelle pull request.
