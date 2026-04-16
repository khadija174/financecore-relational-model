# 📊 Finance Data Pipeline Project

## 🧾 Description

Ce projet consiste à construire un pipeline de données complet pour analyser des transactions financières à l’aide de **PostgreSQL** et **Python (Pandas + SQLAlchemy)**.

Il couvre :

* La création de la base de données
* Le nettoyage et la transformation des données
* L’insertion optimisée dans PostgreSQL
* L’analyse via des requêtes SQL
* La création de vues (KPI)

---

## ⚙️ Technologies utilisées

* Python 🐍
* PostgreSQL 🐘
* SQLAlchemy
* Pandas
* dotenv

---

## 📁 Structure du projet

```
project_finance/
│
├── data/
│   └── financecore_clean.csv
│
├── scripts/
│   └── main.py
│
├── .env
├── requirements.txt
└── README.md
```

---

## 🔌 Configuration (ENV)

Créer un fichier `.env` :

```
DB_USER=your_user
DB_PASSWORD=your_password
DB_HOST=localhost
DB_PORT=5432
DB_NAME=your_db
```

---

## 🏗️ Étape 1 : Connexion à la base de données

Le projet utilise **SQLAlchemy** pour se connecter à PostgreSQL via des variables d’environnement sécurisées.

---

## 🧱 Étape 2 : Création des tables

Les tables suivantes sont créées :

* `agences`
* `segments_client`
* `clients`
* `produits`
* `transactions`

Relations :

* `transactions.client_id` → `clients.client_id`

---

## 📥 Étape 3 : Chargement des données

Les données sont chargées depuis :

```
financecore_clean.csv
```

Puis transformées en plusieurs tables :

* agences
* segments clients
* clients
* produits
* transactions

---

## 🔄 Étape 4 : Transformation des données

Traitements appliqués :

* Conversion des dates (`date_transaction`)
* Conversion des champs numériques
* Suppression des valeurs invalides
* Suppression des doublons (`transaction_id`)

---

## 📤 Étape 5 : Insertion des données

### Dimensions :

Insertion avec protection contre les doublons :

```sql
ON CONFLICT DO NOTHING
```

### Transactions :

* Chargement temporaire (`tmp_transactions`)
* Insertion finale avec gestion des conflits

---

## ⚠️ Bonnes pratiques appliquées

✔️ Utilisation de `ON CONFLICT`
✔️ Nettoyage des données avant insertion
✔️ Utilisation de tables temporaires
✔️ Séparation logique des étapes

---

## ❌ Erreurs évitées

* ❌ `DROP TABLE` sans contrôle
* ❌ `to_sql(if_exists="replace")` en production
* ❌ Duplication des données

---

## 📊 Étape 6 : Analyses (KPI)

### 🔝 Top transactions

* Nombre de transactions
* Montant total
* Moyenne

### 👤 Clients à faible solde

* Comparaison avec la moyenne globale

### ⚠️ Taux de défaut

* Basé sur les statuts :

  * Rejeté
  * Refusé
  * Défaut

---

## 🔗 Étape 7 : Jointures

Exemple :

```sql
clients LEFT JOIN segments_client
```

Avec nettoyage (`TRIM`, `LOWER`) pour éviter les erreurs de correspondance.

---

## 👁️ Étape 8 : Création des vues

### 📌 `vw_kpi_transactions`

* KPI par agence / produit / date

### 📌 `vw_kpi_taux_defaut`

* Taux de défaut par catégorie de risque

### 📌 `vw_kpi_performance_agence`

* Performance globale des agences

---

## 🚀 Exécution

```bash
python main.py
```

---

## 📈 Résultats

Le projet permet :

* Analyse des transactions financières
* Suivi des risques clients
* Monitoring des performances agences
* Création de KPIs exploitables

---

## 🔥 Améliorations possibles

* Dashboard (Streamlit / Power BI)
* Automatisation (Airflow)
* API (FastAPI)
* Data Warehouse (modèle étoile)

---

## 👨‍💻 Auteur

Projet réalisé dans un objectif d’apprentissage avancé en Data Engineering & Data Analysis.

---
