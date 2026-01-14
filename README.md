# YouLogiX

API de gestion de colis — projet d'exemple (FastAPI + SQLAlchemy)

## Description

YouLogiX est une API minimale pour la gestion d'envois (expéditeurs, destinataires, colis,
livreurs, zones et historiques de statut). Le projet utilise FastAPI pour l'API et SQLAlchemy
pour l'ORM. Des factories et seeders simples ont été ajoutés pour peupler une base de données
de développement.

## Structure principale

- `app/` : code principal (models, routes, controllers, crud, factories, seeders)
- `requirements.txt` : dépendances Python
- `Dockerfile`, `docker-compose.yml` : configuration optionnelle pour conteneurisation

## Prérequis

- Python 3.10+ recommandé
- Une base de données configurée (voir `core/config.py` / variable `DATABASE_URL`)

## Installation rapide

1. Créer un environnement virtuel et l'activer :

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Unix/macOS
source .venv/bin/activate
```

2. Installer les dépendances :

```bash
pip install -r requirements.txt
```

3. Configurer la variable `DATABASE_URL` dans `.env` ou via `core/config.py`.

## Création des tables et seeders

Le projet contient des seeders et factories dans `app/seeders` et `app/factories`.
Pour créer les tables (si elles n'existent pas) et insérer des données d'exemple :

```bash
python -m app.seeders.run
```

Remarques :
- Le seeder tente d'utiliser le modèle `ClientExpediteur` si présent. Si votre dépôt n'inclut
	pas `app/models/ClientExpediteur.py`, le seeder crée des données de clients sous forme de
	dictionnaires (et vous pouvez ajouter le modèle si nécessaire).

## Lancer l'API en développement

```bash
uvicorn app.main:app --reload
```

Par défaut, quelques routes sont incluses :
- routes colis, livreur, destinataire (voir `app/routes`)

## Tests

Le projet contient `pytest` dans les dépendances. Ajouter des tests sous un dossier `tests/`.

## Docker

Le dépôt contient `Dockerfile` et `docker-compose.yml`. Vous pouvez construire et démarrer
avec :

```bash
docker compose build --no-cache
docker compose up
```

