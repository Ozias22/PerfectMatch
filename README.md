# PerfectMatch

PerfectMatch est une application web de rencontre développée avec Django. Le projet combine un backend Python/Django, des templates HTML rendus côté serveur, une interface Bootstrap personnalisée avec Sass, ainsi que des interactions JavaScript pour le matching, la messagerie et les notifications.

## Aperçu du projet

L'application permet à un utilisateur de :

- créer un compte
- se connecter et se déconnecter
- compléter son profil utilisateur
- enrichir son profil PerfectMatch
- téléverser des images
- parcourir des profils proposés
- liker ou disliker d'autres profils
- obtenir des matchs mutuels
- échanger des messages
- effectuer un test de compatibilité
- consulter des notifications
- souscrire à un abonnement

## Stack technique

### Backend
- Python
- Django
- modèle utilisateur personnalisé basé sur `AbstractUser`

### Frontend
- HTML
- JavaScript
- SCSS / CSS
- Bootstrap 5
- Sass via npm

### Outils
- npm
- Sass

## Structure du dépôt

```text name=structure-du-projet.txt
.
├── README.md
├── requirements.txt
├── package.json
├── package-lock.json
└── PerfectMatch/
    ├── manage.py
    ├── PerfectMatch/
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── settings.example.py
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

## Fonctionnalités principales identifiées

### 1. Authentification et gestion de compte
Le projet gère l'inscription, la connexion, la déconnexion et la modification du profil à partir d'un modèle utilisateur personnalisé.

Fichiers concernés :
- `PerfectMatch/utilisateurs/models.py`
- `PerfectMatch/utilisateurs/forms.py`
- `PerfectMatch/utilisateurs/views.py`
- `PerfectMatch/utilisateurs/templates/utilisateurs/inscription.html`
- `PerfectMatch/utilisateurs/templates/utilisateurs/connecter_compte.html`

### 2. Profil utilisateur étendu
Le projet définit :
- un modèle `User` personnalisé
- un modèle `UserProfile` lié en one-to-one
- un système d'images supplémentaires avec `ImagesUser`
- des informations comme le genre, la bio, les centres d'intérêt et l'occupation

### 3. Système de matching
Les profils sont récupérés via une API interne, puis présentés sous forme de cartes. L'utilisateur peut liker ou disliker. Si deux utilisateurs se likent mutuellement, un match mutuel est créé.

Fichiers concernés :
- `PerfectMatch/utilisateurs/models.py`
- `PerfectMatch/utilisateurs/views.py`
- `PerfectMatch/static/js/script.js`

### 4. Test de compatibilité
Le projet inclut un questionnaire qui calcule un score de compatibilité et l'enregistre dans le modèle `Compatibilite`.

Fichiers concernés :
- `PerfectMatch/utilisateurs/forms.py`
- `PerfectMatch/utilisateurs/views.py`
- `PerfectMatch/utilisateurs/templates/utilisateurs/compatibilite_form.html`
- `PerfectMatch/utilisateurs/templates/utilisateurs/compatibilite_resultat.html`

### 5. Messagerie
Une interface de discussion et plusieurs endpoints JSON permettent d'afficher la liste des conversations, de récupérer les messages et d'en envoyer.

Fichiers concernés :
- `PerfectMatch/utilisateurs/models.py`
- `PerfectMatch/utilisateurs/views.py`
- `PerfectMatch/static/js/discussions.js`
- `PerfectMatch/utilisateurs/templates/utilisateurs/discussions.html`

### 6. Abonnements
Le projet contient un flux d'abonnement avec choix d'une formule et validation des informations de paiement.

Fichiers concernés :
- `PerfectMatch/utilisateurs/models.py`
- `PerfectMatch/utilisateurs/forms.py`
- `PerfectMatch/static/js/abonnement.js`
- `PerfectMatch/utilisateurs/templates/utilisateurs/abonement.html`

### 7. Interface et design
L'interface repose sur Bootstrap et un important travail de personnalisation via Sass, avec compilation vers un fichier CSS final.

Fichiers concernés :
- `PerfectMatch/static/scss/styles.scss`
- `PerfectMatch/static/scss/partials/`
- `PerfectMatch/static/css/styles.css`

## Routes principales

Les routes identifiées dans le projet sont :

- `/` → redirection vers la connexion
- `/connexion/` → connexion
- `/inscription/` → inscription
- `/deconnexion/` → déconnexion
- `/accueil/` → page d'accueil authentifiée
- `/profil/` → profil utilisateur
- `/modif_profil/` → modification du profil
- `/profilPerfectMatch/` → profil spécifique PerfectMatch
- `/valider_abonement/` → validation d'un abonnement
- `/mes_matchs/` → liste des matchs mutuels
- `/discussions/` → messagerie
- `/notifications/` → notifications
- `/api/obtenir_profil/` → récupération des profils proposés
- `/api/action_like/` → action like / dislike
- `/api/discussions/` → liste des discussions
- `/api/messages/<user_id>/` → récupération des messages
- `/api/envoyer_message/<receiver_Id>/` → envoi d'un message
- `/compatibilite/<match_id>/` → test de compatibilité

## Installation

### 1. Cloner le dépôt
```bash name=clone.sh
git clone https://github.com/Ozias22/PerfectMatch.git
cd PerfectMatch
```

### 2. Créer un environnement virtuel
```bash name=venv.sh
python -m venv .venv
```

Activation :

- **Windows (PowerShell)**
  ```powershell name=activate-windows.ps1
  .\.venv\Scripts\Activate.ps1
  ```
- **macOS / Linux**
  ```bash name=activate-unix.sh
  source .venv/bin/activate
  ```

### 3. Installer les dépendances Python
```bash name=install-python-deps.sh
pip install -r requirements.txt
```

### 4. Installer les dépendances frontend
```bash name=install-node-deps.sh
npm install
```

### 5. Créer le fichier de configuration Django
Le dépôt ne versionne pas `PerfectMatch/PerfectMatch/settings.py`. Un fichier d'exemple est maintenant fourni.

Copiez :

```bash name=settings-copy.sh
cp PerfectMatch/PerfectMatch/settings.example.py PerfectMatch/PerfectMatch/settings.py
```

Sous Windows :

```powershell name=settings-copy-windows.ps1
Copy-Item PerfectMatch/PerfectMatch/settings.example.py PerfectMatch/PerfectMatch/settings.py
```

Ensuite, adaptez si besoin :
- `SECRET_KEY`
- `DEBUG`
- `ALLOWED_HOSTS`
- la base de données
- les chemins statiques et média

Le fichier exemple inclut aussi :
- `AUTH_USER_MODEL = 'utilisateurs.User'`
- le context processor `utilisateurs.context_processors.navbar_notifications`
- une configuration SQLite par défaut

### 6. Appliquer les migrations
```bash name=migrate.sh
python PerfectMatch/manage.py makemigrations
python PerfectMatch/manage.py migrate
```

### 7. Lancer le serveur
```bash name=runserver.sh
python PerfectMatch/manage.py runserver
```

Puis ouvrir :

```text name=local-url.txt
http://127.0.0.1:8000/
```

## Compilation des assets frontend

Pour compiler le SCSS en CSS :

```bash name=build-css.sh
npm run build-css
```

Script actuel :

```json name=package-json-scripts.json
{
  "scripts": {
    "build-css": "sass PerfectMatch/static/scss/styles.scss PerfectMatch/static/css/styles.css"
  }
}
```

## Dépendances actuelles

### Python
Le fichier `requirements.txt` ajouté contient :
- `Django`
- `Pillow`

`Pillow` est nécessaire car le projet utilise plusieurs champs `ImageField`.

### Node.js
Le `package.json` mis à jour contient :
- `bootstrap`
- `sass`

Les métadonnées du dépôt ont aussi été corrigées pour pointer vers `Ozias22/PerfectMatch`.

## Résumé des modèles

Les principaux modèles du projet sont :

- `User` : utilisateur personnalisé avec email unique, photo de profil, pays, ville et date de naissance
- `UserProfile` : profil applicatif lié à un utilisateur
- `Match` : relation de like / match mutuel
- `Message` : messages entre utilisateurs
- `Abonement` : abonnement utilisateur
- `Compatibilite` : score de compatibilité entre deux utilisateurs
- `ImagesUser` : images supplémentaires du profil

## Points importants repérés pendant l'analyse

### Fichier `settings.py` absent du dépôt
Le projet ne peut pas être lancé directement après clonage sans créer un fichier `settings.py` local.

### Dépendances Python auparavant non documentées
Le dépôt ne contenait pas de `requirements.txt`, ce qui compliquait l'installation.

### Métadonnées npm incohérentes
Le `package.json` pointait vers un ancien dépôt nommé `Projet-Web`. Cela a été corrigé.

### CSS compilé versionné
Le dépôt contient déjà les fichiers CSS compilés et leur source map.

### Nommage métier mixte
Le projet garde plusieurs noms métier en français comme `abonement` et `compatibilite`, ce qui est cohérent avec le code existant.

## Améliorations possibles ensuite

- ajouter un `.env.example`
- créer un vrai `settings.py` de développement local séparé
- améliorer `tests.py`
- documenter un jeu de données de démonstration
- ajouter des captures d'écran
- corriger quelques incohérences de nommage dans le code

## Modifications effectuées dans cette étape

Les actions demandées ont été réalisées :

1. ajout de `requirements.txt`
2. nettoyage de `package.json`
3. ajout de `PerfectMatch/PerfectMatch/settings.example.py`
4. réécriture du README en français
