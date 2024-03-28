# Boîte pour taquets francais
Design avec FreeCAD de boîtes à queue droite, adaptable sur des rails en CP de 18mm d'épaisseur, de 30mm à l'arrière et 48mm de hauteur à l'avant.

![La boîte assemblée](./boite-assemblée.png) "Boîte assemblée"


Dans FreeCAD, les activités se font dans des ateliers spécialisés, sélectionnables par le menu juste après les 3 icônes "Nouveau', "Ouvrir", "Sauver". Quatre d'entre eux seront utilisés dans la suite :
- Spreadsheet
- Part Design
- Part
- Laser Cut Interlocking, qui s'installe depuis le menu Tools > Addon manager

# Comment l'adapter à d'autres valeurs ?

Ouvrir le projet **Boite Taquets Fr V3.FCStd**

Dans FreeCAD, le design est paramétré grâce à une feuille de calcul ici nommée **dimensions**
Dans cette feuille de calcul, les cellules surlignées en jaune sont associées avec un **alias**, qui sert de référence à cette valeur, la syntaxe d'une référence est \<\<nom de la feuille de calcul\>\>.alias, par exemple \<\<dimensions\>\>.longueur.

Les dimensions sont celles de l'espace utile à l'intérieur de la boîte, les épaisseurs sont comptées en plus, vers l'extérieur.
Dans la vue du modèle, et de l'arbre de construction, il y a également le panneau inférieur, regroupant les valeurs numériques.
Lorsque qu'un champ numérique fait référence à une valeur de la feuille de calcul, il faut d'abord cliquer sur ƒx pour voir la formule la définissant.

Au cours du projet, il est parfois nécessaire d'alterner entre une utilsation précise de la souris pour dessiner, et le déplacement dans l'espace pour visualiser le modèle. En cliquant dans la barre de statut en bas le la fenètre de l'application, on peut changer ce mode de **CAD** mde précis, à **Gesture**, mode de navigation dans l'espace. Certaines cmmandes de dessins ne répondent pas dans un autre mode que CAD. 

Une exigence pour l'utilisation ultérieure du greffon "LC Interlocking" est que chaque panneau de la boîte soit défini comme un **corps** séparé dans l'atelier **Part Design**. On peut créer les 5 corps par avance puis les renommer au fur et à mesure. Chacun d'eux sera décrit grâce à une **esquisse**. Penser à sauvegarder à chaque étape complétée avec succès.

Le travail de design le plus complexe, avec l'atelier **Sketcher** est la saisie du profil des faces latérales, avec les crochets, qui doit spécifier toutes les contraintes de dimensions et d'angle.
Il faut cocher la case pour voir les messages du "solveur". Les contraintes redondantes sont mentionnées. le message __n DOFs__ signale l'insuffisance de contraintes, laissant encore n degrés de liberté non contraints, c'est à dire la possibilité de déformer le profil dessiné.

On procède ensuite au design des faces, en oubliant les queue droites qui seront générées plus tard. Les faces latérales sont typiquement dessinées avec une esquisse dans le plan YZ. Afin de ne pas se préoccuper des épaisseurs, il est possible de décaler la position de l'esquisse dans l'espace du projet de manière à ce que le (0,0) soit le coin bas gauche de la face. Attention ! chaque face est travaillée dans son repère local avec l'axe X horizontal, et l'axe Y vertical, et la profondeur est l'axe Z local. Si on replace ce repère dans le plan YZ, le X local devient le Y glogbal, le Y local devient le Z global, et la profondeur locale est le X global.

Il faut décrire les panneaux avec leur priorité dans l'assemblage comme pour un simple collage, le panneau qui est collé après, est plus large d'une épaissur, à chaque extrémité, deux épaisseurs en tout.

Pour cloner un panneau, on fait une simple copier-coller de l'original, en décochant la feuille de calcul qui reste unique, mais il faut ensuite décaler le plan de l'esquisse, généralement de la dimension du vide entre l'original et la copie, augmentée d'une épaisseur.

# Utilisation du greffon LC Interlocking
Lorsque les 5 corps sont prêts, il faut changer d'atelier pour **Part**, et il faut une transformation supplémentaire pour l'utilisation du greffon : On sélectionne les 5 corps, puis dasn le menu "Part", sélectionner **Part > Create a copy > Create simple copy**. On peut ensuite cacher les 5 corps originaux. **Attention** il ne faut pas les supprimer de l'arbre de construction, il faut seulement changer leur visibilité.

On peut ensuite passer dans l'atelier **Laser Cut Interlocking**, dans le menu qui lui est spécifique, on clique sur la 2e icône "Slots"
Dans cette étape, on fera de nombreux aller-retours entre l'onglet **Model**, et l'onglet **Tasks**.
Pour définir un assemblage, il faut selectionner toutes les copies simples des corps concernés par cet assemblage. 

Commençons par le fond, toutes les 5 copies sont concernées, on les sélectionne toutes.
1. On change pour l'onglet **Tasks**, on clique sur "Add same Parts", puis en déroulant le formulaire, vers le bas, on définit la tolérance d'assemblage 0,5mm par défaut mais qui peut s'affiner à 0,2mm, de même que la taille du faisceau Laser, ce sont des ajustements à trouver par l'expérience.
2. On change pour l'onglet **Model**, pour sélectionner tous les bords de panneaux qui vont être rallongés pour recevoir les queues droites. Pour cela on cache les corps qui recevront les encoches, l'avant, l'arrière et les deux flancs, en sélectionnant la copie du corps puis en appuyant sur la barre d'espace.
3. Avec la souris en mode CAD, on sélectionne les faces des bords avant et droit (Ctrl-Clic/Commande-Clic selon la machine). En mode Gesture on tourne la copie du fond pour exposer les deux autres faces, et compléter la sélection des quatre facettes des bords de la copie du fond en mode CAD.
4. On change pour l'onglet **Tasks**, on clique sur "Add same faces", puis en déroulant la formulaire vers le bas, on définit le nombre de queues droites sur les arêtes sélectionnées, 3 est un bon chiffre pour commencer. Si la découpe se fait au Laser, on peut décocher "Dog bones", qui sont utiles uniquement pour une fraiseuse CNC.
On clique sur "Preview" pour éxécuter la construction. De nouveaux corps avec le suffix _tab dans le nom sont crées.

Pour continuer et finir, on va travailler avec les 4 copies des faces avant-arrière, droite et gauche.
On cache les panneaux droit et gauche, on sélectionne les faces à l'extrémité des panneau avant et arrière, deux à gauche et deux à croite.

En suivant les même étapes, on obtient le résultat sauvegardé dans le projet **Boite Taquets Fr V3 fond.FCStd**

# Export en SVG
Dans l'onglet Model, on sélection les *_tab, et on clique sur la dernière icône du menu spécifique de "Laser Cut Interlocking", **Export**, on choisit comme format "Flattened SVG", et on obtient le plan de découpe.






