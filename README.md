# template_bibliographie_fial-uclouvain
Un template LaTeX avec une page de garde ainsi que le style de bibliographie et de citation de la Faculté de philosophie, arts et lettres (UCLouvain), pour une utilisation avec LaTeX, réalisé avec le package biblatex.

## Utilisation

### Entrer les données bibliographiques

#### Où trouver les données bibliographiques

#### Les champs pour chaque type d'entrées (vérifier les données bibliographiques)

@article

* `issuetitle` et `issuesubtitle`, spécifie le titre du numéro spécial ou du dossier thématique.

### Citer dans le texte

### Compiler

À cause de l'utilisation d'une police très rarement utilisée en typographie (les petites capitales en gras de la page de garde fonctionnent avec latex, mais pas avec xelatex), il est nécessaire de compiler `page_de_garde_fial.tex` séparément de `main.tex` et avant ce dernier. Dans un terminal linux, il faut donc taper :

    pdflatex page_de_garde_fial.tex
    latexmk -pdf -xelatex main.tex

Une fois que la page de garde a été compilée une fois, il n'est plus nécessaire de la recompiler systématiquement (la deuxième commande intègre le pdf généré par la première au document final `main.pdf`).

Cependant, depuis l'ajout du fichier, `latexmkrc`, latexmk réalise la compilation de la page de garde automatiquement. La première commande est inutile, et la deuxième commande suffit. Sur [Overleaf](https://fr.overleaf.com/login), la compilation est automatique (l'utilisation d'overleaf plutôt qu'une installation locale de LaTeX est donc recommandée). Si vous ne voulez pas de page de garde, vous devrez supprimer le fichier `latexmkrc` qui ne sera plus d'aucune utilité.

## Conseils

* Sur git et LaTeX : https://github.com/dspinellis/latex-advice#use-third-party-latex-packages
* Sur l'intérêt de versionner ses travaux : https://geekographie.maieul.net/83
* Un excellent livre sur l'utilisation de LaTeX dans les sciences humaines. Disponible à cette adresse : https://geekographie.maieul.net/95. Notez qu'il n'est pas nécessaire de connaître tout sur tout de LaTeX (c'est impossible) pour pouvoir baliser son texte : les commandes de base suffisent et elles sont vraiment peu nombreuses. Il convient donc de ne pas se décourager face aux 300 pages de ce livre qu'il n'est pas nécessaire de lire en entier.

## Contribuer

Le style bibliographique n'est pas du tout au point, et il est difficile de penser qu'il le sera un jour, vu l'étendue des ambiguités que présentent les “normes” bibliographiques de la FIAL (voir le fichier guide_references_bibliographiques.pdf). Toute aide et toute connaissance sur biblatex est la bienvenue (je suis pas un expert de LaTeX, j'essaye juste de me dépatouiller avec la [documentation](http://mirrors.ibiblio.org/CTAN/macros/latex/contrib/biblatex/doc/biblatex.pdf), mais ça n'est pas toujours évident).

Pour contribuer :

1. Forkez le repo.
2. Créez votre branche fonctionnalité (`git checkout -b ma-nouvelle-fonctionnalite`).
3. Committez les changements (`git commit -am "Explication de ce que vous avez fait`).
4. Pushez ça sur la branche (`git push origin ma-nouvelle-fonctionnalite`).
5. Créez la nouvelle pull request.

À faire :

* Mettre le titre de dossier thématique entre guillemets et en romains.
* Ajouter la mention "dossier spécial". Voir pour utiliser titleaddon, ou bien créer un nouveau champ.
* Vérifier que l'affichage correspond aux consignes fial pour chaque type d'entrée possible (en dresser la liste).
* changer les mots clés anglais (dans, op. cit, etc.)
* Trouver le moyen que la mention d'édition s'affiche correctement (1\up{e} edition}
* Vérifier l'affichage d'un article type.
* S'arranger pour qu'il n'affiche pas les informations qui ne sont pas sencées figurer (ex : langue)
* Choisir le bon style de la famille verbose (trad1, 2 ou 3) pour la gestion des abbréviations de type op.cit. la plus proche de celui de la FIAL. Si besoin, redéfinir des macros pour que ça corresponde parfaitement. Les macros se trouvent dans cbx (/usr/local/texlive/2019/texmf-dist/tex/latex/biblatex/cbx/). Il y a encore un truc à lire dans le latex sciences humaines là-dessus (à la toute fin de la personnalisation des styles).
