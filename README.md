# Google-Merchandise-Analytics

## Monitoring des ventes Google

### Scénario
Je suis consultant Data engagé par Google pour mettre en place le monitoring des ventes de leurs produits.

L'objectif est de mieux suivre la tendance des ventes **Online** / **Offline** et de voir l'impact de leur campagne marketing sur le Chiffre d'Affaires (CA).

### Les objectifs de l'équipe marketing

Trois grandes typologies d'objectifs :

1.  **Suivi des Ventes :** Comparaison des ventes du dernier mois (M) par rapport à M-1, au global, par circuit de distribution, par catégorie de produit et par produit.
2.  **Analyse du Panier :** Montant et volume de produits vendus par commande (AOV), au global et par circuit de distribution.
3.  **Impact Marketing :** Analyse du volume de dépenses marketing et du gain engendré (ROI), au global et par circuit de distribution.

<details>
  <summary>🔍 Les Indicateurs Clés de Performance (KPIs) Détaillés</summary>

### Étape 1 : SUIVI DES VENTES DU MOIS DERNIER

**KPIs Cibles :**
* Ventes totales du mois (avec évolution mois précédent)
* Ventes cumulées sur l'année en cours
* Ventes totales en ligne et hors ligne
* Part du Online et du Offline sur le total des ventes

**Visualisations :**
* Évolution des ventes sur l'année.
* Évolution de la répartition Online/Offline des ventes.
* Ventes par catégorie de produit, ventilées par circuit de distribution.
* Top des produits vendus en ligne et en physique.

### Étape 2 : SUIVI DU PANIER MOYEN

**KPIs Cibles :**
* Montant du panier moyen (avec évolution mois précédent)
* Montant du panier moyen Online et Offline (avec évolution mois précédent)
* Nombre de commandes et Nombre de produits vendus (avec évolution mois précédent)
* Nombre de produits par commande moyen (avec évolution mois précédent)

**Visualisations :**
* Comparaison du montant du panier moyen en fonction du circuit de distribution et évolution dans le temps.
* Comparaison du nombre de commandes et de produits vendus en fonction du circuit de distribution et évolution dans le temps.

### Étape 3 : SUIVI DE LA PERFORMANCE MARKETING

**KPIs Cibles :**
* Montant total des dépenses marketing (avec évolution mois précédent)
* Montant des dépenses marketing online et offline (avec évolution mois précédent)
* Rapport des gains/dépenses marketing (ROI) au global et par canal (avec évolution mois précédent)

**Visualisations :**
* Évolution des dépenses marketing vs les ventes de chaque mois (total et par canal).
* Évolution du ratio Gains/Dépenses marketing par circuit de distribution.
</details>

## 💾 Les Données Source

Les données proviennent du site Kaggle : [Google Store Ecommerce Data + Fake Retail Data](https://www.kaggle.com/datasets/jpallard/google-store-ecommerce-data-fake-retail-data).

Ce Dataset simule un scénario de vente complet pour la boutique en ligne de Google, en y ajoutant des données hors ligne (retail) et de marketing.

### 📂 Contenu et Structure des Fichiers

1.  **`online.csv` (Ventes en Ligne) :** Données réelles importées de Google Analytics (activité e-commerce classique : trafic, conversions).
2.  **`retail.csv` (Ventes Hors Ligne/Retail) :** Données simulées pour les transactions des points de vente physiques (Omnichannel).
3.  **`Marketing_Spend.csv` :** Fichier synthétique contenant les budgets publicitaires alloués.
4.  **`KEY_SKU.csv` :** Table de liaison entre les codes stock et les SKU (Stock Keeping Units).

##  ETL et Transformation des données

### Fichier `KEY_SKU`
* Aucune modification n'a été effectuée.

### Fichier `Marketing_Spend`
* Les types de données des colonnes ont été reformatés (ex: nombres décimaux).

### Fichier `Online`
* **Nettoyage & Formatage :** Les colonnes ont été reformatées au bon format de donnée.
* **Lisibilité :** Les noms des colonnes ont été modifiés pour une meilleure compréhension métier.
* **Création de Colonnes Métriques :**
    * `Montant total` : Calculé à partir de la quantité des produits achetés et du prix de l'article.
    * `Origine` : Affectation de la valeur "Online".

### Fichier `Offline`
* **Nettoyage & Formatage :** Les colonnes ont été reformatées au bon format de donnée.
* **Enrichissement (Liaison Clé) :** Utilisation du `codestock` pour lier à `KEY_SKU` et à la table `Online`, afin d'obtenir les prix et noms de produits manquants.
    * *Gestion des données manquantes :* Retrait des doublons et uniformisation des prix des articles via le calcul de la moyenne par article.
* **Création de Colonnes Métriques :**
    * `Montant total` : Calculé à partir de la quantité des produits achetés et du prix de l'article.
    * `Origine` : Affectation de la valeur "Offline".

### Tables Finales

* **Table de Référence (Online + Offline) :** Jointure des tables Online et Offline pour une analyse consolidée.
* **Table des Commandes :** Regroupe par transaction : date d'achat, nombre de produits, prix total et canal de vente.

## 📊 Dashboard de Monitoring

<img width="1039" height="737" alt="Dashboard de monitoring des ventes Google" src="https://github.com/user-attachments/assets/50b0d9fa-26d7-4286-8e6b-f3981e885a66" />

## 🎯 Observations et Recommandations (Décembre)

### 📈 Analyse de la Performance Générale

* Le Chiffre d'Affaires (CA) total a enregistré une croissance de **+19%** en décembre, principalement tirée par une forte hausse des ventes en magasins physiques (**+23%**).
* La répartition du CA confirme une dominance marquée des canaux physiques : **85%** des ventes totales proviennent des magasins, contre **15%** pour le canal Online.
* Le canal Online a connu une croissance modeste de **+2%**.
* Les produits les plus vendus sont des **articles dérivés (goodies/vêtements)**.

### 🛒 Analyse Panier Moyen et Volume de Commandes

| Métrique | Évolution | Interprétation |
| :--- | :--- | :--- |
| **Panier Moyen (AOV)** | **Baisse de -5%** | La valeur moyenne des transactions diminue sur l'ensemble des canaux (Online : -13% ; Offline : -10%). |
| **Volume de Commandes** | **Croissance nette de +25%** | **Malgré l'érosion du Panier Moyen**, le nombre total de commandes a bondi de +25% ce mois-ci, sur tous les canaux, compensant la perte de valeur par un gain de volume important. |

### 📣 Campagne Marketing et Rentabilité (ROI)

* Le budget marketing global a été significativement accru en Décembre (**+23%**), principalement pour les magasins physiques (**+31%**).
* Malgré cet investissement, la **rentabilité globale du marketing est négative** :
    * Le **Retour sur Investissement (ROI)** global est de **-3%** (ratio Gain/Dépense de 0,97).
    * Le **canal Online** affiche une contre-performance critique (**ROI de -17%**).
    * Le **canal Offline** maintient un ROI quasi-neutre (**+1%**), ce qui suggère une meilleure efficience des dépenses physiques.

**Recommandation d'Action :** Une révision urgente de la stratégie d'acquisition Online est nécessaire pour identifier les campagnes non rentables et réallouer le budget vers les canaux plus performants (ou le Offline).
