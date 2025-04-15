# Boîte pour taquets français
Design avec FreeCAD de boîtes à queues droites, adaptables sur des rails en CP de 18mm d'épaisseur, de 30mm à l'arrière et 48mm de hauteur à l'avant.

<img width="200" alt="image" src="https://github.com/TeamRepairCafeNice/Boite-pour-taquets-francais/assets/72799037/93402a38-45ab-4d43-832a-e1cead821e37">

Dans FreeCAD, les activités se font dans des ateliers spécialisés, sélectionnables par le menu juste après les 3 icônes "Nouveau', "Ouvrir", "Sauver". Quatre d'entre eux seront utilisés dans la suite :
- Spreadsheet
- Part Design
- Part
- Laser Cut Interlocking, qui s'installe depuis le menu Tools > Addon manager

# Comment l'adapter à d'autres dimensions ?
## Les étapes à suivre
1. Ouvrir le projet qui définit la géométrie et les panneaux, et leur disposition.
2. Éditer la feuille de calcul et modifier les dimensions souhaitées. Le modèle se recalcule automatiquement.
3. Préparer des copies des corps pour l'utilisation du greffon "LC Interlocking". 

## Les étapes en détail
1. Ouvrir **Boite Taquets Fr V3.FCStd**.
2. Dans FreeCAD, le design est paramétré grâce à une feuille de calcul ici nommée **dimensions**
Dans cette feuille de calcul, les cellules surlignées en jaune sont associées avec un **alias**, qui sert de référence à cette valeur, la syntaxe d'une référence est \<\<nom de la feuille de calcul\>\>.alias, par exemple \<\<dimensions\>\>.longueur.

> [!NOTE]  
> Les dimensions sont celles de l'espace utile à l'intérieur de la boîte, les épaisseurs sont comptées en plus, vers l'extérieur.

> [!NOTE]
> Dans la vue du modèle, et de l'arbre de construction, il y a également le panneau inférieur, regroupant les valeurs numériques.
> Lorsque qu'un champ numérique fait référence à une valeur de la feuille de calcul, il faut d'abord cliquer sur ƒx pour voir la formule la définissant.

> [!NOTE]  
> Au cours du projet, il est parfois nécessaire d'alterner entre une utilisation précise de la souris pour dessiner, et le déplacement dans l'espace pour visualiser le modèle. En cliquant dans la barre de statut en bas le la fenêtre de l'application, on peut changer ce mode, de : **CAD**, mode précis, à : **Gesture**, mode libre de navigation dans l'espace. Certaines commandes de dessins ne répondent pas dans un autre mode que CAD. 

3. Une exigence pour l'utilisation ultérieure du greffon "LC Interlocking" est que chaque panneau de la boîte soit défini comme un **corps** séparé dans l'atelier **Part Design**. On ne détaillera pas les opérations de design de la boîte. Lorsque les cinq corps sont prêts, il faut changer d'atelier pour **Part**, et une transformation supplémentaire est nécessaire pour l'utilisation du greffon : On sélectionne les cinq corps, puis dans le menu "Part", sélectionner **Part > Créer une copie > Créer une copie simple** . On peut ensuite cacher les cinq corps originaux.
> [!NOTE] 
> Il ne faut pas les supprimer de l'arbre de construction, il faut seulement changer leur visibilité.

# Utilisation du greffon LC Interlocking
## Les étapes à suivre
1. On selectionne toutes les copies de corps créées à l'étape précédente, et on indique au greffon de les prendre en compte. Dans le même formulaire on paramètre la tolérence et la précision du Laser.
2. On cache les copies de corps porteuses des encoches ou des mortaises, on sélectionne les toutes les faces qui vont être rallongées par les queues droites ou tenons, et on indique au greffon de les prendre en compte. Dans le même formulaire, on indique le nombre de tenons, et on désélectionne une option spécifique aux fraiseuses.
3. On clique sur "Preview", qui change la vue pour montrer le résultat.
4. On conclut l'opération en refermant le dialogue du greffon.

## Les étapes en détail
1. Dans la vue modèle, on selectionne les copies des corps, leurs noms ont un suffixe en 001. On peut ensuite passer dans l'atelier **Laser Cut Interlocking**, dans le menu qui lui est spécifique, on clique sur la 2e icône "Slots"
Dans cette étape, on fera de nombreux aller-retours entre l'onglet **Modèle**, et l'onglet **Tâches**.
Pour définir un assemblage, il faut selectionner toutes les copies simples des corps concernés par cet assemblage. 

Commençons par le fond, toutes les 5 copies sont concernées, on les sélectionne toutes.
1. On change pour l'onglet **Tâches**, on clique sur "Add same Parts", puis en déroulant le formulaire, vers le bas, on définit la tolérance d'assemblage 0,5mm par défaut mais qui peut s'affiner à 0,2mm, de même que la taille du faisceau Laser, ce sont des ajustements à trouver par l'expérience.
2. On change pour l'onglet **Modèle**, pour sélectionner tous les bords de panneaux qui vont être rallongés pour recevoir les queues droites. Pour cela on cache les corps qui recevront les encoches, l'avant, l'arrière et les deux flancs, en sélectionnant la copie du corps puis en appuyant sur la barre d'espace.
3. Avec la souris en mode CAD, on sélectionne les faces des bords avant et droit (Ctrl-Clic/Commande-Clic selon la machine). En mode Gesture on tourne la copie du fond pour exposer les deux autres faces, et compléter la sélection des quatre facettes des bords de la copie du fond en mode CAD.
4. On change pour l'onglet **Tâches**, on clique sur "Add same faces", puis en déroulant la formulaire vers le bas, on définit le nombre de queues droites sur les arêtes sélectionnées, 3 est un bon chiffre pour commencer. Si la découpe se fait au Laser, on peut décocher "Dog bones", qui sont utiles uniquement pour une fraiseuse CNC.
On clique sur "Preview" pour éxécuter la construction. De nouveaux corps avec le suffix _tab dans le nom sont crées.

Pour continuer et finir, on va travailler avec les 4 copies des faces avant-arrière, droite et gauche.
On cache les panneaux droit et gauche, on sélectionne les faces à l'extrémité des panneau avant et arrière, deux à gauche et deux à droite.



# Export en SVG
Dans l'onglet Model, on sélection les *_tab, et on clique sur la dernière icône du menu spécifique de "Laser Cut Interlocking", **Export**, on choisit comme format "Flattened SVG", et on obtient le plan de découpe.

![image](https://github.com/TeamRepairCafeNice/Boite-pour-taquets-francais/assets/72799037/4de3ce1b-a1ab-4aa9-929a-2e071f962350)




