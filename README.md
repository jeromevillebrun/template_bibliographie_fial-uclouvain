# template_bibliographie_fial-uclouvain
Un template LaTeX avec une page de garde ainsi que le style de bibliographie et de citation de la Faculté de philosophie, arts et lettres (UCLouvain), pour une utilisation avec LaTeX, réalisé avec le package biblatex.

## Utilisation

L'utilisation d'[Overleaf](https://fr.overleaf.com/login) est recommandée. Il s'agit d'un éditeur LaTeX en ligne, très user friendly et proposant plein de chouettes fonctionnalités (raccourcis clavier, synchronisation de la bibliographie avec Zotero ou Mendeley, autocomplétion très avancée, compilation automatique, travail à plusieurs sur le même document, documentation vulgarisée sur LaTeX, etc.). Il suffit de créer un compte gratuit. Il n'est ainsi pas nécessaire d'installer LaTeX sur votre ordinateur. À ma connaissance, la seule raison de ne pas l'utiliser est si vous éprouvez régulièrement des difficultés à vous connecter à internet.

### Les titres

La documentation de biblatex paragraphe 2.2.2 répertorie tous les champs définis. Il en existe plusieurs pour les titres. Il est important de bien les comprendre pour être capable de gérer aisément des cas complexes.

* `title` : le titre de l'élément que l'on veut référencer.
* `maintitle` : lorsque l'on a un publication en plusieurs volumes, on renseigne le titre de l'ensemble dans ce champ.
* `booktitle` : si `title` indique le titre d'un travail qui fait partie d'une publication plus grande, on indique dans `booktitle` le titre de cette publication. Par exemple, lorsque l'on cite un article d'ouvrage collectif, on y indique le titre de l'ouvrage collectif. Cependant, si cet ouvrage collectif est en plusieurs volumes, `booktitle` sera destiné à accueillir le titre du volume dans lequel se trouve l'article.

### vérifier les données bibliographiques

[Ce billet de blog](https://serialmentor.com/blog/2015/10/2/Bibtex) donne des pistes pour vérifier que les données trouvées sur internet au format BibTeX sont correctes.

@book

Pour les monographies.

* `edition` indique la mention d'édition. Si c'est un chiffre, biblatex l'indiquera automatiquement sous la forme "2e éd." (avec le "e" en exposant). Il est aussi possible de l'indiquer sous forme littérale (par exemple "2e édition revue et corrigée"). Dans ce cas, on met le "e" en exposant avec la commande `\up{e}`. Pour rappel, c'est aussi dans ce champ que l'on peut spécifier la mention "réimpr. anast." si l'on a affaire à une réimpression anastatique. On peut également y spécifier des mentions apparaissant sur la page de titre comme "trad. du russe par Prénom Nom"
* `publisher` pour la maison d'édition.
* `editor` pour l'éditeur scientifique. Normalement, on préfèrera choisir entre utiliser `editor` ou `author`, le comportement de biblatex n'étant peut-être pas celui attendu dans le cas où l'on utilise les deux champs à la fois.
* `series` pour la collection. C'est un champ par défaut de biblatex, de type "litteral string" : il est imprimé tel quel. Si l'ouvrage est dans plusieurs collections, il faut donc les séparer par des "/" soi-même.

@mvbook

Pour citer un volume en particulier d'une monographie en plusieurs volumes. `@book` aura exactement le même comportement que `@mvbook`, même dans ce cas, mais `@mvbook` est l'entrée qui est faite pour, et c'est une bonne pratique que de l'utiliser (pour des raisons de tri dans les bibliographies).

* `volume` pour indiquer le numéro de tome/volume utilisé. Si vous mettez seulement un numéro, latex ajoutera automatiquement la mention "t.". Si vous ajouter la mention "vol." (ou toute autre chaine de caractère), latex imprimera le champ tel quel.
* `volumes` pour le nombre de tomes/volumes de l'ouvrage entier. Même chose que pour le précédent : si on ne met que le chiffre, il ajoute automatiquement "t." ; si on ajoute "vol.", il imprime le champ tel quel.
* `maintitle` et `mainsubtitle` doivent être utilisés dans ce même cas pour spécifier le titre de l'ensemble.
* `title` sera utilisé pour le titre spécifique au volume cité s'il en a un.

@thesis

Pour les thèses et les mémoires.

* `institution` est utilisé pour le nom de l'université.
* `date` doit être impérativement utilisé pour l'année scolaire (date doit toujours être privilégié à `year` de toute façon quelque soit l'entrée. Ex : "date = {2019/2020}". Il faut absolument utiliser le "/" et non "-", qui sera mis automatiquement dans le document. L'utilisation du tiret n'est pas la bonne syntaxe et pourrait poser des problèmes dans le tri de la bibliographie, si celle-ci est trié par dates.
* `type` est utilisé pour la mention obligatoire "Mémoire de maîtrise en Histoire" en fin de référence. Il peut être imprimé tel quel, ou on peut aussi utiliser une *localisation key* (voir section 4.9.2.13 de la documentation biblatex).

@collection

Il est destiné aux ouvrages collectifs, et se comporte exactement comme `@book`. Pour les articles d'ouvrages collectifs, utiliser `@incollection`.

@proceedings

Il est destiné aux actes de colloque, et se comporte exactement comme `@book`. Pour les articles d'actes de colloque, utiliser `@inproceedings`, qui se comporte exactement comme `@incollection`.

@reference

Il est destiné aux dictionnaires, bibliographies et encyclopédies, et se comporte exactement comme `@book`. Pour les articles d'ouvrage de référence, utiliser `@inreference`, qui se comporte exactement comme `@incollection`.

@article

* `issuetitle` et `issuesubtitle`, spécifie le titre du numéro spécial ou du dossier thématique. Ils sont rarement repris dans les bases de données en ligne.
* `issuetitleaddon` spécifie la mention du type de numéro spécial telle qu'affichée sur la page de titre (ex : "dossier thématique", "numéro spécial", etc.). C'est un champ inventé pour l'occasion (pas un champ intégré de base à biblatex). Il faut donc systématiquement l'ajouter pour chaque entrée de type @article ou @periodical.

### Citer dans le texte

Utiliser la commande `\autocite[prenote][postnote]{clé_de_citation}` pour citer un document du fichier `.bib`. Celle-ci créera une note de bas de page à l'endroit de la citation. On la préfère à `\footcite{}` puisqu'elle permet d'utiliser le même texte avec un autre style bibliographique (qui aurait comme option une citation en fin d'ouvrage, par exemple). `prenote` est un bout de texte à afficher avant la référence (comme par exemple "Cf.", mais aussi un texte plus long pour faire une note explicative). `postnote` est un bout de texte à afficher après la référence, par exemple pour préciser un numéro de page → le numéro seul suffit : le "p.~" est ajouté automatiquement si la postnote est un numéro.

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

Les styles (bibliographiques et de citation) ne sont pas du tout au point. Toute aide et toute connaissance sur biblatex est la bienvenue (je suis pas un expert de LaTeX, j'essaye juste de me dépatouiller avec la [documentation](http://mirrors.ibiblio.org/CTAN/macros/latex/contrib/biblatex/doc/biblatex.pdf), mais ça n'est pas toujours évident).

Pour contribuer :

1. Forkez le repo.
2. Créez votre branche fonctionnalité (`git checkout -b ma-nouvelle-fonctionnalite`).
3. Committez les changements (`git commit -am "Explication de ce que vous avez fait`).
4. Pushez ça sur la branche (`git push origin ma-nouvelle-fonctionnalite`).
5. Créez la nouvelle pull request.

Si vous désirez aider, mais que vous n'avez pas envie d'apprendre comment fonctionne les macros biblatex, vous pouvez aussi...

* Tester le style et identifier ce qu'il faut modifier, intervertir, s'il y a des choses à ajouter, etc. (ouvrir une [issue](https://github.com/jeromevillebrun/template_bibliographie_fial-uclouvain/issues))
* Identifier quel style de citation (parmi [verbose-trad1](http://mirrors.ibiblio.org/CTAN/macros/latex/exptl/biblatex/doc/examples/74-style-verbose-trad1-biber.pdf), [verbose-trad2](http://ctan.math.utah.edu/ctan/tex-archive/macros/latex/contrib/biblatex/doc/examples/75-style-verbose-trad2-bibtex.pdf) et [verbose-trad3](http://ctan.math.washington.edu/tex-archive/macros/latex/exptl/biblatex/doc/examples/76-style-verbose-trad3-bibtex.pdf)) qui correspond le mieux à la gestion des op.cit., ibid., etc. de la [norme FIAL](https://github.com/jeromevillebrun/template_bibliographie_fial-uclouvain/blob/master/guide_references_bibliographiques.pdf).
* Identifier les éventuelles modifications qu'il faudrait opérer sur le style choisi pour qu'il corresponde parfaitement à la norme FIAL.

Todolist :

* Je bloque complètement pour implémenter le référencement des sources éditées. Dans le style donné aux bac1 histoire, il n'y a que deux exemples, alors que c'est un type d'entrée qui comporte plein de cas de figures (que je ne connait pas tous à cause de mon manque d'expérience). Je ne sais pas comment faire pour que nom des auteurs antiques et médiévaux soient entièrement en petites capitales, mais pas ceux des auteurs modernes. De plus, la manière d'afficher le nom de l'éditeur scientifique est totalement absurde et incohérente avec les autres types d'entrées (Prénom avant le nom et mention "éd." avant le nom au lieu de après et entre parenthèses). Quelles-sont les règles non écrites utilisées en pratique pour référencer les sources éditées ? Que signifie le "pour la suite de la référence, se conformer aux directives de la faculté" ? Pour pouvoir automatiser quelque chose, il faut déjà avoir une idée claire de ce qui doit être fait, et c'est là que ce document d'uniformisation est un échec.
* Choisir le bon style de la famille verbose (trad1, 2 ou 3) pour la gestion des abbréviations de type op.cit. la plus proche de celui de la FIAL. Si besoin, redéfinir des macros pour que ça corresponde parfaitement. Les macros se trouvent dans cbx (/usr/local/texlive/2019/texmf-dist/tex/latex/biblatex/cbx/). Il y a encore un truc à lire dans le latex sciences humaines là-dessus (à la toute fin de la personnalisation des styles).
* S'arranger pour qu'il n'affiche pas les informations qui ne sont pas sencées figurer dans certains types d'entrées (ex : langue).
