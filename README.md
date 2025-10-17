Concevez et analysez une base de données NoSQL

Projet pédagogique visant à concevoir un modèle de données NoSQL, charger des jeux de données dans une base MongoDB, puis réaliser des analyses à l’aide de requêtes (mongosh) et d’un notebook Python (PyMongo + Polars). Une présentation PDF synthétise la démarche et les résultats.

📂 Contenu du dépôt

requete_pymongo_polars.ipynb — Notebook Jupyter : connexion à MongoDB avec PyMongo, préparation/inspection de données et analyses avec Polars. 
GitHub

commande_requete_partie_2.txt — Ensemble de commandes et requêtes MongoDB (mongosh) utilisées pour l’exploration et l’agrégation. 
GitHub

KELLENI_Antoine_1_PPT_10_2025.pdf — Diaporama de présentation du projet (contexte, modèle, requêtes clés, résultats). 
GitHub

screenshot/ — Captures d’écran illustrant les étapes / résultats (ex. 7.png). 
GitHub

logo_OCR.jpg — Logo utilisé dans la présentation. 
GitHub

ℹ️ Aucun fichier de données brutes n’est versionné ; prévois un dossier data/ local si nécessaire.

🧰 Prérequis

MongoDB Community (ou Atlas) + mongosh

Python 3.10+

Packages Python : jupyter, pymongo, polars (et éventuellement python-dotenv)

🚀 Mise en place
# 1) Cloner le dépôt
git clone https://github.com/AntoineKelleni/Concevez-et-analysez-une-base-de-donnees-NoSQL
cd Concevez-et-analysez-une-base-de-donnees-NoSQL

# 2) Créer un environnement Python
python -m venv .venv && source .venv/bin/activate   # (Windows: .venv\Scripts\activate)

# 3) Installer les dépendances
pip install jupyter pymongo polars python-dotenv

# 4) Lancer Jupyter
jupyter notebook


Configure la variable d’environnement MONGODB_URI (ou adapte directement l’URI dans le notebook) :

mongodb://localhost:27017
# ou Atlas : mongodb+srv://<user>:<password>@<cluster>/?retryWrites=true&w=majority

💾 Chargement des données (exemple)

Si tu disposes de fichiers JSON/CSV, crée un dossier local data/ et importe avec mongoimport :

# CSV
mongoimport --uri "$MONGODB_URI" \
  --db netcites --collection logements \
  --type csv --headerline --file data/listings_Paris+(1).csv




🔎 Analyses et requêtes

Tu peux travailler de deux façons complémentaires :

1) Notebook Python : requete_pymongo_polars.ipynb

Connexion via PyMongo

Chargement d’échantillons / extraction de sous-ensembles

Transformations et agrégations Polars (groupby, joins, stats)

Visualisation rapide possible (ex. df.head(), stats descriptives)

2) Shell MongoDB : commande_requete_partie_2.txt

Filtres et projections (sélection de champs utiles)

Aggregations (pipeline $match, $project, $group, $sort, $limit, $lookup si besoin)

Conseillé : créer les index pertinents avant les agrégations coûteuses

db.logements.createIndex({ champ: 1 })
// Exemple de pipeline générique :
db.<collection>.aggregate([
  { $match: { /* critères */ } },
  { $project: { /* champs */ } },
  { $group: { _id: "$cle", total: { $sum: 1 } } },
  { $sort: { total: -1 } },
  { $limit: 10 }
])

🧱 Structure de collections (indicatif)

Le projet s’appuie sur MongoDB. Modélise tes collections selon les besoins métiers (documents imbriqués, références entre collections, etc.). Pense à :

Définir les clés d’accès (champs filtrants → index)

Documenter les schémas (même souples) dans le notebook ou la présentation

Garantir la cohérence (validations, formats, types)

🖼️ Captures & Présentation

Les images du dossier screenshot/ illustrent les étapes, commandes et résultats clés.

Le PDF KELLENI_Antoine_1_PPT_10_2025.pdf résume contexte, modèle, démarche d’analyse et insights principaux.
