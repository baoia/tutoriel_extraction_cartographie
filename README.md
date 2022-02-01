# tutoriel_extraction_cartographie

Ce tutoriel vise cartographier un corpus de documents via l’identification des lieux cités dans les textes. Il démarre par l’extraction de documents océrisés et disponibles sur Gallica. Ceux-ci seront traités par une chaîne TAL (Traitement Automatique de la Langue) pour reconnaître les entités nommées de lieux utiles pour la cartographie (c’est-à-dire toutes les occurrences de lieux repérées). A partir de cette liste de lieux, l’outil d’alignement va faire concorder les entités en comparant les lieux avec d’autres bases de données dans lesquelles d’autres informations seront récupérées (données de géolocalisation : latitude et longitude, région). Le dernier outil de cartographie récupère ces informations géographiques pour placer les lieux sur une carte, exportable.

4 carnets sont nécessaires pour ce tutoriel.

BaOIA_gallica_txt.ipynb
BaOIA_reconnaissance_extraction_entites_lieux.ipynb
BaOIA_alignement_lieux.ipynb
BaOIA_cartographie_complète.ipynb OU BaOIA_cartographie_categorisée.ipynb
Préparation préalable : télécharger le dépôt Github (sur le bouton vert « code », cliquer sur « download ZIP »). Double-cliquer sur le fichier télécharger pour en extraire le contenu. À la base du compte Google Drive de travail, ajouter ce dossier.

Outil 1 : extraction des documents (Gallica)
Documents d’entrée : fichier Excel au format .XLSX. Ce fichier doit contenir AU MOINS les liens Gallica vers les documents OU les identifiants ark. Exemple : https://gallica.bnf.fr/ark:/12148/bpt6k63947766 OU bpt6k63947766. Un lien doit être indiqué par case, sur une colonne du fichier Excel. Ce n’est pas un problème si le fichier Excel contient d’autres informations (titre, auteur, date, etc.). Exemple de fichier Excel :


Ici, c’est la colonne D qui contient les liens vers Gallica.

Il faut ajouter ce document Excel (ici appelé « Corpus de Guides Paris ») au dossier contenant les scripts sur le Google Drive.

Ouvrir le premier carnet BaOIA_gallica_txt.ipynb.

-1ère cellule de code : cliquer pour lancer puis cliquer sur le lien généré pour s’authentifier à son compte Google Drive (Google Colab demande l’autorisation d’accéder aux fichiers). Cliquer sur son compte Google, puis sur autoriser. Ensuite, copier le lien généré sur la page et le coller dans la case apparue en dessous de la cellule de code en dessous de « Enter your authorization code » puis cliquer sur la touche enter de son clavier.

-2ème cellule de code : avant de lancer, remplir les champs demandés :

            -chemin_vers_le_dossier_de_travail : il est inutile de le changer si le dossier de travail est le même que celui téléchargé de Github contenant les carnets et le fichier Excel avec la liste des documents.

            -chemin_vers_le_fichiers_excel : il s’agit du chemin précédent (donc /content/drive/My Drive/tutoriel_extraction_cartographie-main/) auquel vient s’ajouter à la fin le nom du fichier excel avec sont format. Exemple : mon fichier excel se nomme Corpus de Guides Paris, donc le chemin final sera : /content/drive/My Drive/tutoriel_extraction_cartographie-main/Corpus de Guides Paris.xlsx

            -nom_de_la_feuille : un fichier Excel peut contenir plusieurs feuilles, il faut indiquer celle qui contient les liens. La feuille est indiquée en bas à gauche du fichier Excel. Dans notre exemple, la feuille de travail s’appelle « Guides Paris », c’est donc l’information exacte à indiquer dans la case.

            -lettre_de_la_colonne : c’est la lettre qui correspond à la colonne qui contient les liens. Ici, c’est la colonne D.

            -nom_dossier_telechargement : indiquer le nom du dossier souhaité dans lequel les fichiers textes extraits seront téléchargés. Ici, il est nommé « fichiers textes guides gallica ».

Lancer la cellule. Laisser la cellule s’exécuter (plusieurs minutes sont nécessaires pour télécharger les fichiers). Ici, pour 12 liens, la cellule s’exécute en 3m30s. Si un des liens ne correspond pas, ou est indisponible au téléchargement depuis Gallica

Dans le dossier de travail Google Drive, on peut voir que le dossier a été créé et qu’il contient les fichiers textes nommés avec leur date, leur titre et leur identifiant Gallica.

 / !\ Seuls les documents océrisés sont téléchargeables au format texte. Ainsi, si le nombre de documents présents dans le dossier de téléchargement est inférieur à celui du nombre de liens dans le fichier Excel, c’est que certains documents n’ont pas été océrisé par la BNF et donc que le texte n’est pas téléchargeable. En dessous du script s’affiche les documents concernés.

Documents de sortie : fichiers au format .TXT dans le dossier de téléchargement. Il est possible de les ouvrir et de les consulter. Ils contiennent uniquement le texte BRUT océrisé, il n’y a donc aucune indication bibliographique ou de mise en page. Ce format permet la recherche et l’extraction des entités nommées.

Outil 2 : recherche et extraction des entités nommées 
Documents d’entrée : dossier contenant un ou plusieurs fichiers .TXT. Ce sont les textes préalablement téléchargés.

Cet outil permet de repérer les noms de lieux cités dans les textes d’un corpus, ainsi que de les extraire. Un modèle préalablement entraîné sur un grand nombre de textes est utilisé pour la reconnaissance.

Ouvrir BaOIA_reconnaisance_extraction_entites_lieux.ipynb.

1ère cellule de code : elle permet, comme à chaque début de carnet de se connecter et d’autoriser l’accès à son Google Drive. Cette cellule permet aussi le téléchargement du modèle qui va permettre la reconnaissance des entités de lieux : ainsi il faut choisir la langue des textes pour la reconnaissance des entités (Français, Anglais, Allemand, Espagnol ou Italien). L’installation et donc l’exécution de la cellule sont plutôt longues.

La reconnaissance et l’extraction se font dans la cellule suivante. Trois champs doivent être préalablement remplis :

            -chemin_vers_le_dossier_de_travail : c’est celui téléchargé du Github dans lequel sont les scripts.

            -chemin_vers_le_dossier_de_fichiers_txt : c’est le dossier dans lequel les fichiers textes ont été préalablement téléchargés (en suivant l’outil précédant de téléchargement), le chemin devient donc : ‘/content/drive/My Drive/tutoriel_extraction_cartographie-main/fichiers textes guides gallica/’

            -nom_du_dossier_des_entites : indique le nom du dossier choisi dans lequel les listes d’entités de lieux vont être enregistrées. Ici, le nom est « entites lieux guides ».

Lancer la cellule, cette étape est plutôt longue. Par exemple, pour 7 documents, le temps d’exécution est de 12 minutes.

Il est possible d’aller jeter un œil aux documents créés qui contiennent les listes des lieux. Quand on regarde le détail des résultats trouvés on remarque un nombre d’erreurs de reconnaissance variable mais parfois conséquent. En fonction du résultat souhaité et du degré de précision, un temps de correction est possible : supprimer à la main les faux résultats. Plus le corpus est conséquent, moins les erreurs de reconnaissance prendront de l’importance et inversement : sur un corpus n’est composé que de trois ou quatre documents, les erreurs seront plus visibles. Le type de cartographie final est aussi important : pour la représentation de cartes de chaleurs ou de l’ensemble des lieux évoquées pour repérer des tendances, un taux d’erreur plus élevé est moins grave que pour celle d’un parcours, par exemple, ou chaque lieu a son importance. Ce sont des fichiers textes, il est possible de les modifier facilement comme tout document ; il est simplement important de conserver la structure (un seul lieu par ligne).

Documents de sortie : fichiers sous format TXT, un pour chaque document du corpus avec la liste des lieux détectés par le modèle Spacy entraîné.

Outil 3 : alignement des données et analyses statistiques
Documents d’entrée : fichiers TXT contenant la liste des lieux par document.

L’outil d’alignement a pour but d’identifier un lieux reconnu en l’alignant avec des bases de données extérieures : il est effectué en liant les informations avec la base Wikidata. L’alignement permet aussi d’extraire des informations sur les lieux détectés : avec cet outil, nous extrayons les données de géolocalisation spatiales, c’est à dire les coordonnées : latitude et longitude qui permettent le placement sur une carte ainsi que des descriptions rapides des lieux qui permettent de créer des cartes catégorisées. Un petit outil statistique permet de les comparer.

Ouvrir BaOIA_alignement_lieux.ipynb.

1ère cellule : elle permet de se connecter à son drive Google.

2ème cellule : la deuxième cellule lie les informations avec Wikidata et créée deux fichiers de données regroupant toutes les informations extraites pour chaque lieu. Avant de lancer la cellule, remplir les champs suivants :

-chemin_vers_les_listes_de_lieux: c’est le chemin vers le dossier contenant les listes de lieux précédemment extraites. En suivant les chemins prééxistant, le chemin est : /content/drive/MyDrive/tutoriel_extraction_cartographie-main/entites lieux guides

-Langue_pour_l_alignement: il convient de choisir la même langue que celle utilisée pour la reconnaissance, c’est la langue d’écriture des noms de lieux.

-nom_fichier_donnees_lieux: c’est le nom du fichier de sortie qui sera créée pour recenser tous les lieux et les informations. C’est aussi celui qui sera utilisé ensuite pour la cartographie. Il est un format .JSON (bien rajouter le suffixe de format de fichier), difficilement lisible à l’œil nu mais utilisable comme fichier de données. Ici, il s’appelle : données lieux corpus guides.json

-nom_fichier_excel_donnes_lieux: c’est le même fichier que le fichier json mais qui lui, sera lisible pour l’utilisateur, car il est créé au format Excel : bien rajouter le suffixe .XLSX.  Ici il s’appelle : donnees lieux corpus guides excel.xlsx

 Lancer la cellule : /!\ Cette étape est très longue !! / !\

3ème cellule : cette cellule est OPTIONNELLE. Elle permet simplement de connaître le nombre ainsi que la proportion de chaque « type de lieux » détecté. Par exemple : elle permet de voir que 50 communes ont été détectées, 3 parcs, 6 pays, etc. Le résultat s’affiche en dessous de la cellule. Ce sont les catégories qui seront utilisées pour la création de cartes catégorisées. Elle permet aussi de jeter un rapide coup d’œil sur les résultats obtenus par l’alignement : si par exemple on voit des types incohérents, cela peut signifier qu’il peut être judicieux d’effectuer quelques retouches à la main sur le document JSON. ou sur le document précédent et de relancer l’alignement.

Documents de sortie :

Un fichier Excel contenant la liste des lieux reconnus ainsi que des informations extraites de Wikidata : le type de lieu comme il est référencé, les coordonnées géographiques quand c’est un lieu précis reconnu (exemple : un pays n’aura pas de coordonnées géographiques car son aire géographique est trop large) ainsi qu’une brève description du lieu.
Un fichier de données au format .JSON contenant les mêmes informations que le fichier Excel précédent. Ce fichier est utile ensuite pour la création des cartes : c’est le fichier d’entrée des outils cartographiques.
Outil 4 : cartographie
Cartographie complète

Documents d’entrée : fichier .JSON contenant tous les lieux reconnus et alignés.

Ouvrir BaOIA_cartographie_complète.ipynb.

1ère cellule : elle permet de se connecter à son drive Google.

2ème cellule : la deuxième cellule permet de créer la carte à partir de tous les lieux détectés. Deux champs sont à remplir avant de lancer la cellule :

            -nom_fichier_donnees_lieux : il s’agit du fichier de données au format .JSON créé précédemment. Si aucun des noms et des emplacements (dossiers) n’ont pas été changés, il n’est pas nécessaire de le modifier.

            -nom_carte : c’est le nom du fichier contenant la carte créée. C’est un fichier au format .HTML, c’est-à-dire qu’il s’ouvre dans un navigateur internet. Ce format permet de créer des cartes interactives, contrairement aux formats images. Il est important de conserver le suffixe de format .HTML dans le champ à remplir.

Lancer la cellule : la carte s’affiche en dessous, et la carte est créée dans le dossier de travail. Pour visualiser le fichier HTML, il faut d’abord le télécharger sur son ordinateur pour l’ouvrir.

3ème cellule : OPTIONNELLE : ajout de son propre fonds de carte (voir l’encadré / tutoriel précis pour cette étape à la toute fin)

Document de sortie : fichier contenant la carte et tous les points placés au format .HTML.

Cartographie catégorisée interactive

Documents d’entrée : fichier .JSON contenant tous les lieux reconnus et alignés.

Ouvrir BaOIA_cartographie_categorisee.ipynb.

1ère cellule : elle permet de se connecter à son drive Google.

2ème cellule : la deuxième cellule permet de créer la carte à partir des tous les lieux détectés. Deux champs sont à remplir avant de lancer la cellule :

            -nom_fichier_donnees_lieux : il s’agit du fichier de données au format .JSON créé précédemment. Si aucun des noms et des emplacements (dossiers) n’ont pas été changés, il n’est pas nécessaire de le modifier.

            -nom_carte : c’est le nom du fichier contenant la carte créée. C’est un fichier au format .HTML, c’est-à-dire qu’il s’ouvre dans un navigateur internet. Ce format permet de créer des cartes interactives, contrairement aux formats images. Il est important de conserver le suffixe de format .HTML dans le champ à remplir.

Lancer la cellule : la carte s’affiche en dessous, et la carte est créée dans le dossier de travail. Pour visualiser le fichier HTML, il faut d’abord le télécharger sur son ordinateur pour l’ouvrir.

3ème cellule : OPTIONNELLE : ajout de son propre fonds de carte (voir l’encadré / tutoriel précis pour cette étape à la toute fin)

Documents de sortie : fichier contenant la carte et tous les points placés au format .HTML.

*************************************************

Créer et ajouter son fond de carte :

Si l’on veut ajouter son propre fond de carte personnalisé :

1- Création d’un compte sur : https://mapwarper.net/

2- Téléchargement du fond de carte (la meilleure résolution possible est recommandée)

3- Sur Map Warper: dans l’onglet « Upload Map » il est possible de charger le fond de carte que l’on veut utiliser, et indiquer toutes les métadonnées nécessaires.

4- Dans l’onglet Rectify: il faut indiquer le plus de points identiques sur les deux cartes pour permettre la superposition du fond de carte chargé sur des données géolocalisées. Cliquer sur un point sur chaque carte, puis cliquer sur « add Control point » en dessous des cartes. Répéter l’opération le plus de fois possible pour obtenir un bon résultat. Dans l’encadré en dessous des deux fonds de carte, cliquer sur « Warp image » : le fond s’ajoute. Si le résultat n’est pas satisfaisant, il possible d’ajouter d’autres repères pour améliorer la qualité du nouveau fond de carte créé.

5- Se rendre dans l’onglet « Export ». Dans « Map services », copier le lien entier se situant après « Tiles (Google/OSM scheme) : », débutant par http et se terminant par .PNG.

6- Remplir ensuite les champs de la cellule contenu dans l’outil de cartographie utilisé :

            -nom_fichier_donnees_lieux : nom du fichier .JSON contenant l’ensemble des données géographiques.

            -lien_tiles_pour_fond_carte : il faut COLLER ici le lien précédemment copié sur le site dans l’onglet « Export ».

            -nom_carte_fond : c’est le nom de sortie que l’on veut donner au fichier au format .HTML créé.

Le fichier est téléchargé dans le dossier de travail. IL faut le télécharger sur so ordinateur pour ensuite l’ouvrir dans un navigateur internet.
