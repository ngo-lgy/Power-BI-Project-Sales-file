Imaginons qu'on reçoive un fichier .xlsx des ventes tous les mois ou toutes les semaines et qu'on veuille automatiser le reporting via Power BI. C'est dans ce cadre que s'inscrit le présent travail réalisé sur un fichier de ventes contenant les trois tables : Client3, Commandes1 et Produit2. Les objectifs de ce projet sont :

1 - Automatiser l'importation, le nettoyage et le traitement des données avec Power Query
2 - Créer un modèle de données, visualiser les données, créer des graphiques, créer des indicateurs, proposer une expérience interactive avec Power BI Desktop
3 - Créer des mesures avec le langage DAX, analyse de données
4 - Publier le rapport sur le Service Power BI pour que les collègues ou le client aient accès au rapport et puissent travailler avec

1 - Traitement des données avec Power Query

Dans cette section, on commence par charger le fichier ventes.xlsx dans Power BI, ce qui crée une connexion avec ce dernier. On choisit ensuite les trois tables Client3, Commandes1 et Produit2. On clique sur "Transformer les données" pour automatiser le processus de nettoyage dans l'éditeur Power Query.

Les tableaux (tables) dans Power Query sont appelés des requêtes, ce sont des copies des données au moment où elles ont été importées. On commence par renommer les différents tableaux (requêtes) en :

- Client3 pour Client

- Commandes1 pour Commandes

- Produit2 pour Produit

On commence le nettoyage des données par la table Client :

- On renomme la colonne "Client ID" en "Numéro de Client".

- On poursuit avec la table Commandes où l’on renomme la colonne "CDt" en "Numéro de Commande", "Dt" en "Date de Commande", "Livraison" en "Date de Livraison", "Client ID" en "Numéro de Client", "Produit ID" en "Numéro de Produit", "Qty" en "Quantité".

- On poursuit avec la table Produit où l’on renomme la colonne "Prod ID" en "Numéro de produit", "Cat" en "Catégorie", "Sous-cat" en "Sous-Catégorie".

Ensuite, on vérifie que le type des données des colonnes de chaque table est bien conforme.
On constate que dans la colonne Quantité de la table Commandes, le type de données est indéterminé, ce qui signifie que lors du chargement des données, Power Query n’a pas identifié explicitement le type de données à attribuer à cette colonne. Par conséquent, on définit le type de données en "Nombre entier". En outre, cette colonne contient des lignes contenant des erreurs. Ces erreurs sont dues au fait que dans le fichier Excel, il était indiqué "annulé" à ces emplacements précis. Et donc, quand Power Query essaie de les transformer en nombres, cela crée des erreurs. On supprime donc les lignes contenant ces erreurs. Ensuite, on constate que cette colonne contient également des cellules vides, ce qui signifie ici qu’aucune quantité n’a été expédiée. On choisit donc aussi de supprimer toutes les lignes contenant des cellules vides.

La colonne "Rabais" de la table Commandes a pour type de données "Nombre décimal", mais ici, le rabais correspond plutôt à un pourcentage. On modifie donc le type de données en "Pourcentage". On constate qu’il y a également des erreurs dans cette colonne. Ces erreurs sont dues au fait que dans le fichier Excel, il était indiqué "non" à ces emplacements. Le terme "non" signifie ici qu’aucun rabais n’a été appliqué. Donc, au lieu de supprimer les lignes contenant ces erreurs, on remplace la valeur "non" par "0" (0 %).

Après avoir géré le type de données et les erreurs, et après avoir constaté que la qualité des données est satisfaisante, on poursuit avec les transformations.

On commence par fusionner le nom et le prénom dans la table Client, en choisissant un espace comme séparateur, et en nommant la nouvelle colonne formée "Nom Complet".
Ensuite, on réalise les profilages statistiques. On constate que lors de l'affichage par profil de colonne effectué sur la colonne "Numéro de Client" de la table Client, il y a des différences entre le nombre total de lignes dans la table (810), le nombre de clients dans la base (793), et le nombre de clients qui apparaissent une seule fois (790). Cela suppose donc qu’il y a des doublons, c’est-à-dire des clients apparaissant plusieurs fois (visible aussi dans la distribution des valeurs), ce que l’on souhaite éviter. On supprime donc les doublons présents dans cette table.

Pour ces données, on constate qu’il n’y a plus de nettoyage ou de transformation forcément nécessaire. Le travail est terminé dans Power Query. On retourne donc dans Power BI. Pour cela, on clique sur "Accueil", puis sur "Fermer & Appliquer", ce qui applique les transformations aux données et les envoie dans Power BI Desktop.

2 - Créer un modèle de données, visualiser les données, créer des graphiques, créer des indicateurs, proposer une expérience interactive avec Power BI Desktop

De retour dans Power BI, on observe trois sections à gauche :

"Vue du modèle" qui permet de créer ou supprimer des relations entre les différents tableaux

"Affichage Table" qui permet d’avoir un aperçu des données sans retourner dans Power Query

"Affichage du rapport" qui permet de créer les graphiques et tableaux de bord

Avant de commencer l’élaboration du rapport, on vérifie les relations dans la "Vue du modèle" : on ajoute celles qui manquent et on supprime celles qui sont erronées.

On commence par ajouter des indicateurs au rapport par méthode implicite.

- À partir de la table Commandes, on ajoute trois indicateurs sur le rapport : une carte pour la quantité, une carte pour le nombre total de commandes, et une carte pour le nombre de clients ayant passé commande. On renomme ensuite les titres par défaut.

Ensuite, on croise les informations provenant des différentes tables. Cela nécessite que les relations entre les tables soient bien établies dans la "Vue du modèle".

- Par exemple, on affiche les quantités (table Commandes) par Segments (table Client), sous forme de graphique en anneau. On modifie les options d’affichage pour centrer la légende en haut.
Il faut bien s’assurer que les tables Commandes et Client sont reliées par "Numéro de Client" dans la Vue du modèle, sinon chaque segment affichera la quantité totale de commandes.

- Ensuite, on ajoute un graphique temporel pour visualiser l’évolution des quantités dans le temps (Date de Commande), affiché par mois.

On configure ensuite l’apparence et le positionnement des éléments du rapport. À noter que la réalisation de ces actions peut nécessiter une bonne maîtrise de Power BI Desktop. Voici ce que l’on fait :

- On homogénéise les tailles des trois cartes : 150 de hauteur et 300 de largeur

- On aligne les trois cartes à la même hauteur

- On espace les trois cartes de manière égale horizontalement

- On ajuste les visuels du bas pour qu’ils respectent les marges à gauche et à droite, et aient la même hauteur entre eux

- On modifie le titre du diagramme circulaire et on le centre horizontalement

- On modifie le titre du graphique temporel, et on désactive les titres des axes X et Y

- On active les marqueurs et les étiquettes de données sur le graphique temporel pour une meilleure lisibilité

- On insère un segment (filtre) permettant à l’utilisateur de filtrer l’ensemble du rapport selon la catégorie de produit (table Produit). On choisit le style vignette et on supprime le titre du segment
Il faut vérifier que les tables Produit et Commandes sont bien reliées, sinon le filtre n’aura aucun effet

- On ajoute un titre général au rapport, positionné en haut à gauche

- On sélectionne tous les visuels avec la souris ou "Ctrl + clic gauche" pour les grouper et les repositionner facilement, puis on les dissocie

- On ajoute un fond avec transparence pour améliorer l’aspect visuel du rapport

3 - Créer des mesures avec le langage DAX, analyse de données

Dans cette section, on génère du code DAX pour créer des mesures, puis les combiner avec d’autres mesures ou attributs afin de filtrer l’information ou produire des visualisations plus pertinentes.

- Mesure de base : création d’une mesure explicite dans la table Commandes à l’aide de la fonction SUM pour retourner la somme des quantités vendues

- Calcul du Chiffre d’Affaires Brut : création d’une mesure dans la table Commandes à l’aide de SUMX pour multiplier les quantités (Commandes) par le prix unitaire (Produit), et sommer les résultats

- On utilise cette mesure pour afficher le CA brut par Date de Commande sous forme d’histogramme empilé, affiché au niveau mensuel

- Rabais total : ajout d’une mesure dérivée de la précédente pour calculer le rabais total

- On affiche un tableau avec le CA brut et le rabais total par numéro de commande

- Chiffre d’Affaires Net : nouvelle mesure dans Commandes calculée en soustrayant le rabais total au CA brut

- On ajoute le CA net au tableau précédent

- On ajoute le CA net à l’histogramme du CA brut mensuel pour visualiser les différences mois par mois

- On affiche l’évolution du rabais total dans le temps sous forme d’histogramme

- On visualise le CA net par mois et par catégorie

- Indicateur filtré avec CALCULATE : création d’une mesure pour obtenir le CA net uniquement pour la catégorie "Technology", puis affichage sous forme d’histogramme groupé montrant le CA net général et celui de "Technology" par mois

- Titre dynamique : ajout d’interactivité en modifiant le titre d’un graphique selon le segment client sélectionné. On utilise SELECTEDVALUE pour créer une mesure, et on l’associe dans les options de titre via le bouton f(x)

Tous les graphiques créés dans cette section sont présentés ci-dessus.

4 - Publier le rapport sur le Service Power BI

- Pour publier le rapport, on se rend sur l’application en ligne Power BI et on le publie dans "Mon espace de travail personnel" pour un usage personnel (ex : premiers tests).

- Sinon, on crée un nouvel espace de travail à partir de l’onglet "Espace de travail", dans lequel on publie le rapport. On ajoute ensuite des personnes ou des groupes via l’option Gérer les accès.

