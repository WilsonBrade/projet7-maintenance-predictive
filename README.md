# Projet 7 — Maintenance Prédictive

Hackathon IA & Cybersécurité 2026 — ISM Dakar — Groupe 10

## Le projet en bref

On construit un système qui détecte qu'un moteur d'avion va tomber en panne **avant** que ça arrive, à partir des données de ses capteurs (température, vibration, pression...). C'est ce qu'on appelle la maintenance prédictive.

Dataset utilisé : **NASA CMAPSS Turbofan Engine Dataset**.

## Structure du repo

```
projet7-maintenance-predictive/
│
├── data/
│   ├── raw/                    
│   └── processed/              
│
├── notebooks/                  
│   ├── 01_eda.ipynb            
│   ├── 02_feature_engineering.ipynb
│   └── 03_modeling.ipynb       
│
├── src/                        
│   ├── data_loader.py          
│   ├── preprocessing.py        
│   ├── features.py             
│   └── model.py                
│
├── app/
│   └── streamlit_app.py        
│
├── docs/
│   └── rapport.md              
│
└── requirements.txt            
```

## Rôle de chaque dossier

### `data/raw/`
Les fichiers originaux, **tels que téléchargés** sur Kaggle (`train_FD001.txt`, `test_FD001.txt`, `RUL_FD001.txt`).

⚠️ **Règle importante : on ne modifie jamais les fichiers ici.** Si on a besoin de transformer une donnée, on crée une nouvelle version dans `data/processed/`. Ça permet de toujours pouvoir revenir à la donnée d'origine si on a fait une erreur de manipulation.

### `data/processed/`
Les données nettoyées ou transformées : par exemple `train_with_rul.csv` (le fichier train avec le RUL calculé pour chaque ligne).

### `notebooks/`
C'est le **bac à sable**. Chacun peut expérimenter librement ici, tester des idées, faire des graphiques, essayer des trucs qui ne marchent pas. 

- `01_eda.ipynb` → exploration des capteurs, statistiques descriptives, visualisations
- `02_feature_engineering.ipynb` → calcul du RUL, création de nouvelles variables (moyennes glissantes, détection de rupture...)
- `03_modeling.ipynb` → entraînement et évaluation du modèle (Isolation Forest)

### `src/`
Le code **propre et réutilisable**. Dès qu'un bout de code marche dans un notebook et qu'on va s'en servir plusieurs fois (ou que quelqu'un d'autre dans l'équipe en a besoin), on le déplace ici sous forme de fonction, pour permettre aux de le réutiliser dans d'autres circonstances.

- `data_loader.py` → charger les fichiers bruts, nommer les colonnes
- `preprocessing.py` → nettoyage des données, calcul du RUL
- `features.py` → création de features (moyennes glissantes, tendances, ruptures)
- `model.py` → entraînement et évaluation du modèle

### `app/`
Le dashboard final, celui qu'on montrera au jury.

- `streamlit_app.py` → interface qui affiche l'état des capteurs et les alertes en direct

### `docs/`
La documentation écrite du projet.

- `rapport.md` → contexte, méthodologie, résultats — utile pour la présentation finale

### `requirements.txt`
La liste des bibliothèques Python nécessaires pour faire tourner le projet (pandas, scikit-learn, streamlit, etc.). Avant de commencer à coder, chacun installe les dépendances avec :

```bash
pip install -r requirements.txt
```

## Comment on travaille ensemble

1. On expérimente dans `notebooks/`
2. Quand un bout de code est stable et réutilisable, on le déplace dans `src/`
3. On ne touche jamais à `data/raw/`
4. On commit régulièrement avec un message claire pour que tout le monde voie l'avancement
5. Mettre des commentaires après les modifications pour permettre aux autres de suite les endroits modifiés
6. Faire un `git pull` avant de commencer à travailler pour récupérer les dernières modifications de groupes

## Le cycle Git à respecter
 
On travaille tous sur `main`, pas besoin de branches pour ce projet (on est peu nombreux et les tâches sont assez séparées). Par contre il faut respecter ce cycle à chaque session de travail, pour éviter les conflits :
 
```bash
git pull              # 1. récupérer les derniers changements des autres
# ... on travaille ...
git add .              # 2. préparer ce qu'on a modifié
git commit -m "message clair sur ce qu'on a fait"   # 3. décrire le changement
git push               # 4. envoyer sur GitHub
```
 
**Règle simple : pull avant, push après, jamais l'inverse.**
 
Toujours commencer une session par un `git pull`, même si on pense être à jour — ça évite 90% des conflits.
