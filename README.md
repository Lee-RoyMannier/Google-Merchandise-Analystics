# Google-Merchandise-Analystics

## Monitoring des ventes Google

### Scénario
Je suis consultant Data engagé par Google pour mettre en place le monitoring des ventes de leurs produits.

L'objectif est de mieux suivre la tendance des ventes online / offline et de voir l'impact de leur campagne marketing sur le CA.

### Les objectifs de l'équipe marketing

3 grandes typologies d'objectifs :
- Le suivi des ventes du dernier mois, comparé au mois M-1, au global, par circuit de distribution, par catégorie de produit et par produit
- La valeur d'un panier avec son montant et le volume de produits vendus, au global et par circuit de distribution.
- Impact du marketing: avec le volume de dépenses marketing et le gain engendré, au global et par circuit de distribution

<details>
   <summary>Les KPIs</summary>

### Les KPIs
Etape 1 : SUIVI DES VENTES DU MOIS DERNIER

Box KPI:
  - Ventes totales du mois (avec évolution mois précédent)
  - Ventes cumulés sur l'année en cours
  - Ventes totales en ligne
  - Ventes totales hors ligne
  - Part du Online sur le total des ventes
  - Part du offline sur le total des ventes
Visualisations:
  - Evolution des ventes sur l'année
  - Evolution de la répartition Online/Offline des ventes
  - Ventes par catégorie de produit, ventilé par le circuit de distribution
  - Top des produits vendus en ligne
  - Top des produits vendus en physique

Etape 2 : SUIVI DU PANIER MOYEN

Box KPI:
  - Montant du panier moyen (avec évolution mois précédent)
  - Montant du panier moyen Online (avec évolution mois précédent)
  - Montant du panier moyen Offline (avec évolution mois précédent)
  - Nombre de commandes (avec évolution mois précédent)
  - Nombre de produits vendus (avec évolution mois précédent)
  - Nombre de produits par commande moyen (avec évolution mois précédent)

Visualisations:
  - Comparaison du montant du panier moyen en fonction du circuit de distribution + évolution dans le temps
  - Comparaison du nombre de produits vendus en fonction du circuit de distribution + évolution dans le temps
  - Comparaison du nombre de produits par panier en fonction du circuit de distribution + évolution dans le temps 
  - Comparaison du nombre de commandes totales en fonction du circuit de distribution + évolution dans le temps

Etape 3 : SUIVI DE LA PERFORMANCE MARKETING

Box KPI:
  - Montant total des dépenses marketing (avec évolution mois précédent)
  - Montant des dépenses marketing online (avec évolution mois précédent)
  - Montant des dépenses marketing offline (avec évolution mois précédent)
  - Rapport des gains par rapport aux dépenses marketing  (avec évolution mois précédent)
  - Rapport global des gains par rapport aux dépenses marketing online  (avec évolution mois précédent)
  - Rapport global des gains par rapport aux dépenses marketing offline  (avec évolution mois précédent)

Visualisations:
  - Evolution des dépenses marketing vs les ventes de chaque mois
  - Evolution des dépenses marketing online vs les ventes online de chaque mois
  - Evolution des dépenses marketing offline vs les ventes offline de chaque mois
  - Evolution du ratio gains/dépenses marketing circuit de distribution
</details>

## Les données
Les données proviennent du site Kaggle https://www.kaggle.com/datasets/jpallard/google-store-ecommerce-data-fake-retail-data

Ce Dataset simule un scénario de vente complet pour la boutique en ligne de Google, en y ajoutant des données hors ligne (retail) et de marketing.

📂 Contenu et Structure des Fichiers

Ce jeu de données est composé de plusieurs fichiers CSV qui permettent de reconstituer l'ensemble de l'activité commerciale :

1. online.csv (Ventes en Ligne)
Contient les données réelles des commandes importées manuellement de Google Analytics de la boutique publique Google Store.

Il représente l'activité e-commerce classique (trafic, conversions, produits vendus en ligne).

2. retail.csv (Ventes Hors Ligne/Retail)
Ce fichier est une version fortement modifiée d'un ensemble de données de détaillant britannique pour simuler les transactions et les ventes d'un point de vente physique (POS) du Google Store.

Il permet d'analyser et de comparer les performances des canaux en ligne et hors ligne (Omnichannel).

3. Marketing_Spend.csv (Dépenses Marketing)
C'est un fichier synthétique (fake) créé spécifiquement pour la modélisation.

Il contient les budgets publicitaires alloués aux campagnes en ligne et hors ligne.

4. KEY_SKU.csv (Clé de Produit)
Ce fichier sert de table de liaison.

Il établit le lien entre les codes stock et les SKU (Stock Keeping Units) des produits, permettant de joindre correctement les données des transactions aux descriptions de produits.

## Transformation des données

Fichier KEY_SKU:
   - Aucune modification n'a été effectué sur ce fichier

Fichier Marketing_Spend:
   - Les colonnes ont été reformaté pour coller au bon format de donnée (exemple: nombre décimal)

Fichier Online:
   - Les colonnes ont été reformaté pour coller au bon format de donnée (exemple: nombre décimal)
   - Les noms des colonnes ont été modifier pour être facilement compris par des personnes exterieurs
   - Création d'une colonne "Montont total" regroupant La quantité des produits achetés lors d'une trasnaction avec le prix de l'article, permettant ainsi d'avoir le montant de la commande
   - Création d'une colonne "Origine colonne" ayant comme valeur "Online" permettant de savoir quel canal de vente il s'agit.

Fichier Offline:
   - Les colonnes ont été reformaté pour coller au bon format de donnée (exemple: nombre décimal)
   - Les noms des colonnes ont été modifier pour être facilement compris par des personnes exterieurs
   - Cette table ne contenait pas les nom des produits ainsi que les prix, pour palier à cela, j'ai utiliser le codestock pour faire une liaison avec la table KEY_SKU, qui ma permit d'obtenir les SKU produits et ainsi faire une liaison avec les produits dans la table Online poiur obtenir toutes les informations manquante.
     Une fois cela fait, j'ai du retirer les doublons et uniformiser les prix des articles en faisant une moyenne des prix par article.
   - Création d'une colonne "Montont total" regroupant La quantité des produits achetés lors d'une trasnaction avec le prix de l'article, permettant ainsi d'avoir le montant de la commande
   - Création d'une colonne "Origine colonne" ayant comme valeur "Offline" permettant de savoir quel canal de vente il s'agit.

Création d'une table de référence, regroupant les ventes de tout les canaux de ventes (Online + Offline)
   - Cette table et une jointure des tables Online et Offline

Création d'une table de Commandes, regroupant pour chaque transaction, la date de l'achat, le nombre de produit acheté, le prix total et le canal de vente.

## Dashboard

<img width="1039" height="737" alt="image" src="https://github.com/user-attachments/assets/50b0d9fa-26d7-4286-8e6b-f3981e885a66" />

## Observation

### 📈 Analyse de la Performance Décembre

Le Chiffre d'Affaires (CA) total a enregistré une croissance de +19% en décembre, principalement tirée par une forte hausse des ventes en magasins physiques (+23% sur la période).

La répartition du CA confirme une dominance marquée des canaux physiques : 85% des ventes totales proviennent des magasins, contre 15% pour le canal Online.

Le canal Online a connu une croissance modeste de +2%, ce qui est un indicateur de l'efficacité potentielle de la campagne marketing digitale, mais son impact reste marginal.

Globalement, la tendance des ventes totales est positive sur l'ensemble des canaux. On note que les produits les plus vendus sont des articles dérivés (goodies/vêtements) qui soutiennent l'image de la marque.

🛒 Analyse du Panier Moyen et du Volume de Commandes

| Métrique | Évolution          | Interprétation |
| :--------------- |:---------------:| -----:|
| Panier Moyen (AOV)	| Baisse de -5% |	La valeur moyenne des transactions diminue sur l'ensemble des canaux (Online : -13% ; Offline : -10%).|
| Volume de Commandes | Croissance nette de +25% | Malgré l'érosion du Panier Moyen, le nombre total de commandes a bondi de +25% ce mois-ci, sur tous les canaux.|

### 📣 Campagne Marketing et Rentabilité (ROI)

Le budget marketing global a été significativement accru en Décembre, enregistrant une hausse de +23%. Cette augmentation est principalement portée par les dépenses pour les magasins physiques (+31%), tandis que le budget Online a augmenté plus modérément (+12%).

Malgré cet investissement accru, la rentabilité globale du marketing est négative :

Le Retour sur Investissement (ROI) global s'établit à -3% (ratio Gain/Dépense de 17,3).

Cette contre-performance est accentuée par le canal Online (ROI de -17%).

Le canal Offline maintient un ROI quasi-neutre (+1%), ce qui suggère que les dépenses physiques ont été plus efficientes.

Recommandation d'Action : Une révision urgente de la stratégie d'acquisition Online est nécessaire pour identifier les campagnes non rentables et réallouer le budget vers les canaux plus performants ou le Offline.
