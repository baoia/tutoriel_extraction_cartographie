# Tutoriel complet : de l’extraction documentaire à la cartographie

Ce tutoriel vise à cartographier un corpus de documents via l’identification des lieux cités dans les textes. Il démarre par l’extraction de documents déjà océrisés et disponibles sur Gallica. Ceux-ci seront traités par une chaîne TAL (Traitement Automatique de la Langue) pour reconnaître les entités nommées de lieux utiles pour la cartographie à savoir, toutes les occurrences de lieux repérées. À partir de cette liste de lieux, l’outil d’alignement va faire concorder les entités en comparant les lieux avec d’autres bases de données dans lesquelles d’autres informations seront récupérées (données de géolocalisation : latitude et longitude, région). Le dernier outil de cartographie récupère ces informations géographiques pour placer les lieux sur une carte exportable.

## Structure du dépôt

```
tutoriel_extraction_cartographie
    ├── fichiers_crees_exemples/                            # Fichiers produits par le tutoriel à partir des guides de voyage
        ├── entites lieux guides/
            ├── DIV_barack.txt
            └── Lieux_barack.tkt
        ├── fichiers textes guides gallica/
            ├── 1876_Paris_illustré_en_1870_et_1876._Guide_de_l_ét_bpt6k63947766_texte_brut.txt
            ├── ...
            └── _Guide_pratique_de_l_étranger_dans_Paris_et_se_bpt6k97689245_texte_brut.txt
        ├── carte_complète.html
        └── carte_creee.html
    ├── BAOIA_cartographie_categorisee.ipynb                # Notebook pour la réalisation d'une carte catégorisée selon les types de lieux
    ├── BAOIA_cartographie_complète.ipynb                   # Notebook pour la réalisation d'une carte complète
    ├── BaOIA_alignement_lieux.ipynb                        # Notebook pour l'alignement des lieux avec Wikidata
    ├── BaOIA_gallica_txt.ipynb                            # Notebook pour l'extraction de l'océrisation de Gallica
    └── BaOIA_reconnaissance_extraction_entites.ipynb       # Notebook pour la reconnaissance et l'extraction des entités nommées
```

## Tutoriel

Le tutoriel entier est disponible sur le site du projet à l'adresse suivante : [https://baoia.huma-num.fr/contact/tutoriel-complet-de-lextraction-documentaire-a-la-cartographie/](https://baoia.huma-num.fr/contact/tutoriel-complet-de-lextraction-documentaire-a-la-cartographie/).
