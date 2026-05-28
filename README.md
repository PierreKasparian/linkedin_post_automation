# Linkedin Post automatic creator

Récupère les newsletters [TLDR](https://tldr.tech/) depuis Gmail via IMAP et les fusionne en un seul fichier HTML navigable.

## Fonctionnement

Le script se connecte à Gmail, recherche les emails envoyés par `dan@tldrnewsletter.com` sur une période donnée, extrait leur contenu HTML et les concatène dans un fichier `tldr_aggregated_<N>_days.html`.

## Prérequis

- Python 3
- Un compte Gmail avec l'accès IMAP activé
- Un [mot de passe d'application Gmail](https://myaccount.google.com/apppasswords) (pas le mot de passe principal)

## Installation

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install python-dotenv
```

## Configuration

Crée un fichier `.env.local` à la racine du projet :

```env
TLDR_EMAIL_ACCOUNT=ton_adresse@gmail.com
TLDR_GMAIL_APP_PASSWORD=xxxx xxxx xxxx xxxx
```

## Utilisation

```bash
# Via le script shell (active le venv automatiquement)
./run.sh          # 7 derniers jours (défaut)
./run.sh 14       # 14 derniers jours

# Ou directement avec Python
source .venv/bin/activate
python3 tldr_aggregator.py --days 7
```

Le fichier HTML généré s'ouvre dans n'importe quel navigateur.
