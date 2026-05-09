# Projet : Équité Algorithmique, Interprétabilité et Robustesse

**Dataset** : German Credit (UCI) — prédiction du risque de crédit  
**Modèle de base** : XGBoost  
**Attributs sensibles** : genre, tranche d'âge

## Structure du projet

```
├── baseline_model.ipynb   # Tâche 1 — Modèle de référence XGBoost
├── task2_fairness.ipynb   # Tâche 2 — Équité (reweighing + seuil, from scratch)
├── task3_shap.ipynb       # Tâche 3 — Interprétabilité SHAP (TreeExplainer)
├── task4_robustness.ipynb # Tâche 4 — Robustesse (bruit, valeurs manquantes, distribution shift)
├── pyproject.toml         # Dépendances gérées par uv
└── uv.lock                # Lockfile — versions exactes pour reproductibilité
```

## Prérequis

Installer [uv](https://docs.astral.sh/uv/getting-started/installation/) :

```bash
# Linux / macOS
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## Lancement

```bash
# Cloner le dépôt
git clone <url-du-repo>
cd ethic-project

# Créer l'environnement et installer toutes les dépendances (une seule commande)
uv sync

# Lancer JupyterLab
uv run jupyter lab
```

Les notebooks s'ouvrent dans le navigateur. Les exécuter dans l'ordre :
1. `baseline_model.ipynb`
2. `task2_fairness.ipynb`
3. `task3_shap.ipynb`
4. `task4_robustness.ipynb`

## Exécuter un notebook en ligne de commande (sans interface)

```bash
uv run jupyter nbconvert --to notebook --execute task2_fairness.ipynb --output task2_fairness_executed.ipynb
uv run jupyter nbconvert --to notebook --execute task3_shap.ipynb     --output task3_shap_executed.ipynb
uv run jupyter nbconvert --to notebook --execute task4_robustness.ipynb --output task4_robustness_executed.ipynb
```

## Reproductibilité

- `uv.lock` fixe les versions exactes de toutes les dépendances → `uv sync` installe exactement les mêmes versions sur n'importe quelle machine.
- `RANDOM_STATE = 42` est utilisé dans tous les notebooks.
- Le dataset est téléchargé automatiquement depuis l'UCI Repository au premier lancement.

## Méthodes implémentées

| Tâche | Méthode | Implémentation |
|-------|---------|---------------|
| 2 — Équité | Reweighing | From scratch (NumPy) |
| 2 — Équité | Post-processing par seuil | From scratch (NumPy) |
| 2 — Équité | DPD, EOD | From scratch (NumPy) |
| 3 — Interprétabilité | SHAP TreeExplainer | Librairie `shap` |
| 4 — Robustesse | Bruit gaussien | From scratch (NumPy) |
| 4 — Robustesse | Valeurs manquantes | From scratch (NumPy) |
| 4 — Robustesse | Distribution shift | From scratch (NumPy) |
