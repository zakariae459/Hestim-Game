# Hestim Game

Application de bureau en Python qui calcule, de façon ludique, la relation entre deux personnes à partir de leurs prénoms. Le résultat est l'une des six lettres de **H‑E‑S‑T‑I‑M** (par exemple *Harmonieuse*, *Ennemi*…), accompagnée d'un pourcentage et d'un emoji.

Le projet comprend aussi un système de comptes complet : inscription avec vérification par e‑mail, connexion (y compris avec Google), mot de passe oublié, profil et historique des parties.

## Captures d'écran

<!-- Ajoutez vos captures dans un dossier screenshots/ puis décommentez les lignes ci-dessous -->
<!-- ![Écran de connexion](screenshots/connexion.png) -->
<!-- ![Écran de jeu](screenshots/jeu.png) -->

*À venir.*

## Fonctionnalités

- **Calcul de relation** : les lettres communes aux deux prénoms sont retirées, puis le nombre de lettres restantes désigne une lettre de HESTIM.
- **Comptes utilisateurs** : inscription, connexion, option « se souvenir de moi ».
- **Vérification par e‑mail** : code OTP envoyé à l'inscription, e‑mails de confirmation au format HTML.
- **Mot de passe oublié** : code de réinitialisation envoyé par e‑mail.
- **Connexion Google** (OAuth 2.0).
- **Historique des parties** : consultation, suppression, meilleur et pire « ami ».
- **Partage** du résultat ou de l'historique par e‑mail.
- **Ambiance** : vidéos d'arrière-plan et musique (avec bouton muet).

## Technologies

| Domaine | Outils |
|---|---|
| Langage | Python 3 |
| Interface | CustomTkinter, Tkinter, Pillow |
| Vidéo et son | OpenCV, Pygame |
| Base de données | MySQL ou MariaDB (`mysql-connector-python`) |
| E‑mails | SMTP Gmail (`smtplib`), modèles HTML |
| Authentification | Google OAuth (`google-auth-oauthlib`) |
| Divers | `pycountry` (liste des pays) |

## Installation

### Prérequis

- Python 3.10 ou plus récent
- Un serveur MySQL ou MariaDB (par exemple via WAMP ou XAMPP)

### Étapes

```bash
git clone <url-du-depot>
cd Hestim-Game
pip install customtkinter pillow opencv-python pygame mysql-connector-python google-auth-oauthlib pycountry
```

Créez ensuite la base de données (les tables sont créées automatiquement au premier lancement) :

```sql
CREATE DATABASE user_management CHARACTER SET utf8mb4;
```

Puis lancez le jeu :

```bash
python main.py
```

## Configuration

### Base de données

La connexion se règle avec des variables d'environnement :

| Variable | Valeur par défaut |
|---|---|
| `HESTIM_DB_HOST` | `localhost` |
| `HESTIM_DB_PORT` | `3307` |
| `HESTIM_DB_USER` | `root` |
| `HESTIM_DB_PASSWORD` | *(vide)* |

Exemple sous PowerShell, pour un MySQL sur le port 3306 :

```powershell
$env:HESTIM_DB_PORT = "3306"
$env:HESTIM_DB_PASSWORD = "votre_mot_de_passe"
python main.py
```

### Connexion Google

La connexion avec Google nécessite votre propre fichier `client_secret.json`, qui n'est pas fourni dans le dépôt :

1. Dans la [Google Cloud Console](https://console.cloud.google.com/), créez un projet.
2. Configurez l'écran de consentement OAuth.
3. Créez un identifiant **ID client OAuth** de type *Application de bureau*.
4. Téléchargez le fichier JSON, renommez-le `client_secret.json` et placez-le à la racine du projet.

Ce fichier est listé dans `.gitignore` : ne le publiez jamais.

### Envoi des e‑mails

Les e‑mails (code OTP, réinitialisation, confirmation) sont envoyés depuis un compte Gmail. Le compte d'envoi se règle avec deux variables d'environnement :

| Variable | Contenu |
|---|---|
| `HESTIM_EMAIL` | Adresse e‑mail d'envoi |
| `HESTIM_EMAIL_PASSWORD` | [Mot de passe d'application](https://myaccount.google.com/apppasswords) Gmail (pas votre vrai mot de passe) |

```powershell
$env:HESTIM_EMAIL = "votre.adresse@gmail.com"
$env:HESTIM_EMAIL_PASSWORD = "xxxx xxxx xxxx xxxx"
python main.py
```

Sans ces variables, le jeu se lance, mais les e‑mails ne partent pas.

### Médias

Les images, vidéos et musiques d'origine ne sont pas toutes incluses dans le dépôt. Si un fichier manque, l'application démarre quand même, avec un emplacement vide à la place.

## Structure du projet

```
├── main.py                     # Application complète (interface, logique, base de données)
├── *_template.html             # Modèles des e-mails HTML
├── logo hestim.png             # Logo utilisé dans les e-mails
├── assets/                     # Images
├── Adobe/                      # Vidéos et ressources graphiques
└── styles.css, index.html      # Pages HTML annexes
```

## Auteur

Zakariae SABHI, étudiant à **HESTIM**
Projet réalisé en 2024.
