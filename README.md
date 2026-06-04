# PerfectMatch

PerfectMatch is a Django-based dating and matchmaking web application with a custom user system, profile management, swipe-style discovery, mutual matching, messaging, subscriptions, and compatibility testing.

## Overview

This project combines a Django backend with server-rendered HTML templates and a Bootstrap/Sass frontend. Users can:

- create an account and sign in
- complete a public and app-specific profile
- upload profile images
- browse suggested profiles
- like or dislike other users
- create mutual matches
- exchange messages
- take a compatibility test with a match
- manage notifications and subscriptions

## Tech stack

### Backend
- Python
- Django
- Custom `AbstractUser` model

### Frontend
- HTML templates
- JavaScript
- SCSS / CSS
- Bootstrap 5
- Sass build pipeline via npm

### Tooling
- npm
- `sass` for stylesheet compilation

## Repository structure

```text name=project-structure.txt
.
├── README.md
├── package.json
├── package-lock.json
└── PerfectMatch/
    ├── manage.py
    ├── PerfectMatch/
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── urls.py
    │   └── wsgi.py
    ├── static/
    │   ├── css/
    │   │   ├── styles.css
    │   │   └── styles.css.map
    │   ├── images/
    │   ├── js/
    │   │   ├── abonnement.js
    │   │   ├── discussions.js
    │   │   └── script.js
    │   └── scss/
    │       ├── styles.scss
    │       └── partials/
    ├── templates/
    │   ├── 403.html
    │   ├── 404.html
    │   └── 500.html
    ├── templates/
    └── utilisateurs/
        ├── admin.py
        ├── apps.py
        ├── context_processors.py
        ├── forms.py
        ├── models.py
        ├── tests.py
        ├── urls.py
        ├── views.py
        ├── migrations/
        └── templates/
            └── utilisateurs/
```

## Main features identified

### 1. Authentication and account management
The app includes registration, login, logout, and profile editing flows built around a custom user model.

Relevant files:
- `PerfectMatch/utilisateurs/models.py`
- `PerfectMatch/utilisateurs/forms.py`
- `PerfectMatch/utilisateurs/views.py`
- `PerfectMatch/utilisateurs/templates/utilisateurs/inscription.html`
- `PerfectMatch/utilisateurs/templates/utilisateurs/connecter_compte.html`

### 2. Custom user and profile system
The project defines:
- a custom `User` model extending `AbstractUser`
- a `UserProfile` model linked one-to-one with each user
- additional profile images through `ImagesUser`
- interests, biography, occupation, gender, and onboarding state

### 3. Matching workflow
Users can browse profiles returned by the API, then like or dislike them. If two users like each other, the match becomes mutual.

Relevant files:
- `PerfectMatch/utilisateurs/models.py`
- `PerfectMatch/utilisateurs/views.py`
- `PerfectMatch/static/js/script.js`

### 4. Compatibility test
A dedicated questionnaire computes a compatibility score for a match and stores it in the `Compatibilite` model.

Relevant files:
- `PerfectMatch/utilisateurs/forms.py`
- `PerfectMatch/utilisateurs/views.py`
- `PerfectMatch/utilisateurs/templates/utilisateurs/compatibilite_form.html`
- `PerfectMatch/utilisateurs/templates/utilisateurs/compatibilite_resultat.html`

### 5. Messaging and discussions
The app provides conversation endpoints and a discussion UI that fetches messages asynchronously.

Relevant files:
- `PerfectMatch/utilisateurs/models.py`
- `PerfectMatch/utilisateurs/views.py`
- `PerfectMatch/static/js/discussions.js`
- `PerfectMatch/utilisateurs/templates/utilisateurs/discussions.html`

### 6. Subscriptions
There is a subscription model and form flow for selecting and validating a subscription plan.

Relevant files:
- `PerfectMatch/utilisateurs/models.py`
- `PerfectMatch/utilisateurs/forms.py`
- `PerfectMatch/static/js/abonnement.js`
- `PerfectMatch/utilisateurs/templates/utilisateurs/abonement.html`

### 7. Frontend styling
The UI is heavily styled with SCSS and compiled CSS. Bootstrap has been customized through Sass partial imports and theme variables.

Relevant files:
- `PerfectMatch/static/scss/styles.scss`
- `PerfectMatch/static/scss/partials/`
- `PerfectMatch/static/css/styles.css`

## URL map
The main routes discovered in the project include:

- `/` → redirect to login
- `/connexion/` → login
- `/inscription/` → registration
- `/deconnexion/` → logout
- `/accueil/` → authenticated home page
- `/profil/` → user profile
- `/modif_profil/` → edit profile
- `/profilPerfectMatch/` → app-specific profile setup
- `/valider_abonement/` → subscription validation
- `/mes_matchs/` → mutual matches
- `/discussions/` → conversations
- `/notifications/` → notifications API response
- `/api/obtenir_profil/` → candidate profile feed
- `/api/action_like/` → like/dislike action
- `/api/discussions/` → conversation list
- `/api/messages/<user_id>/` → fetch conversation messages
- `/api/envoyer_message/<receiver_Id>/` → send a message
- `/compatibilite/<match_id>/` → compatibility test

## Setup

### 1. Clone the repository
```bash name=clone.sh
git clone https://github.com/Ozias22/PerfectMatch.git
cd PerfectMatch
```

### 2. Create and activate a virtual environment
```bash name=venv.sh
python -m venv .venv
```

Activate it:

- **Windows (PowerShell)**
  ```powershell name=activate-windows.ps1
  .\.venv\Scripts\Activate.ps1
  ```
- **macOS / Linux**
  ```bash name=activate-unix.sh
  source .venv/bin/activate
  ```

### 3. Install Python dependencies
A `requirements.txt` file is not currently present in the repository, so install Django and any media/image dependencies you use locally.

Example:
```bash name=install-python-deps.sh
pip install django pillow
```

> `Pillow` is typically required because the project uses `ImageField` in multiple models.

### 4. Install frontend dependencies
```bash name=install-node-deps.sh
npm install
```

### 5. Configure Django settings
This repository currently does **not** include `PerfectMatch/PerfectMatch/settings.py`, and `.gitignore` explicitly ignores it. Before running the project, create your own settings file.

At minimum, configure:
- `INSTALLED_APPS`
- `MIDDLEWARE`
- `TEMPLATES`
- `DATABASES`
- `LANGUAGES`
- `STATIC_URL`
- `MEDIA_URL`
- `MEDIA_ROOT`
- `AUTH_USER_MODEL = 'utilisateurs.User'`

You should also add the `utilisateurs.context_processors.navbar_notifications` context processor if you want notification data in templates.

### 6. Apply migrations
```bash name=migrate.sh
python PerfectMatch/manage.py makemigrations
python PerfectMatch/manage.py migrate
```

### 7. Run the development server
```bash name=runserver.sh
python PerfectMatch/manage.py runserver
```

Open the app in your browser at `http://127.0.0.1:8000/`.

## Frontend asset build
Compile SCSS to CSS with:

```bash name=build-css.sh
npm run build-css
```

Current npm script:

```json name=package.json-snippet
{
  "scripts": {
    "build-css": "sass PerfectMatch/static/scss/styles.scss PerfectMatch/static/css/styles.css"
  }
}
```

## Data model summary

The core models identified are:

- `User`: custom authentication model with additional fields such as profile photo, location, and birthday
- `UserProfile`: extended dating profile linked to each user
- `Match`: records likes and mutual matches between profiles
- `Message`: stores private messages between matched users/profiles
- `Abonement`: stores subscription information
- `Compatibilite`: stores compatibility test results
- `ImagesUser`: stores extra uploaded images for a user

## Important notes discovered during analysis

### Missing tracked settings file
The Django settings file is ignored in Git, so the repository is not runnable as-is without local configuration.

### No Python dependency manifest
There is no `requirements.txt` or equivalent Python dependency file in the repository.

### Existing package metadata still references another repository
`package.json` still contains references to `Ozias22/Projet-Web` instead of `Ozias22/PerfectMatch`, so the metadata should be updated.

### Large compiled frontend assets are committed
Compiled CSS and source maps are committed to the repository, which is fine for deployment but may be redundant during development if you prefer generating them in CI or locally.

### Some naming is still inconsistent
There are several French spellings such as `abonement` and `Compatibilite`, which reflect the current codebase and routes.

## Suggested next improvements

- add a `requirements.txt` file
- commit a safe example settings file such as `settings.example.py` or `.env.example`
- fix repository metadata in `package.json`
- document seed data or demo credentials if applicable
- add screenshots or GIFs of the UI
- improve automated tests in `PerfectMatch/utilisateurs/tests.py`
- document deployment steps

## Current status

The repository already contains the main building blocks of a full-stack matchmaking platform:
- custom authentication
- profile onboarding
- matching logic
- messaging
- subscriptions
- compatibility scoring
- responsive styling with Bootstrap and Sass

What is mainly missing is environment documentation and a few setup files, which this README helps clarify.
