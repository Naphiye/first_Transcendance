# Transcendance
Transcendance est une plateforme web fullstack inspirée du jeu pong. Frontend en TypeScript/Tailwind avec React et i18n maison, backend Node.js/Fastify. Docker gère les conteneurs, la persistance, les uploads et les certificats TLS pour la sécurité.



Transcendance est une plateforme web fullstack inspirée du jeu de ping-pong en ligne et du réseau social de 42.
Frontend en TypeScript/Tailwind avec React et i18n maison, backend Node.js/Fastify.
Docker gère les conteneurs, la persistance, les uploads et les certificats TLS pour la sécurité.

Lancer le projet

Mode développement : 
```make dev```

Mode production :
```make prod```


## Variables d'environnement

Ce projet nécessite des variables d'environnement pour fonctionner.  
Créez un fichier `.env` à la racine du dossier backend en vous basant sur l'exemple ci-dessous.

### Exemple de `.env`

```env
# OAuth GitHub
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
GITHUB_URL=https://github.com/
GITHUB_API=https://api.github.com/

# JWT
JWT_SECRET=change_me_in_production

# Mot de passe par défaut pour le développement (NE PAS UTILISER EN PRODUCTION)
UNIVERSAL_PASSWORD=dev_password_only
FAKE_PASSWORD=fake_password_for_testing

# Gmail (optionnel)
GMAIL_APP_PASSWORD=your_gmail_app_password

# URL du frontend
# En développement : https://localhost:5173/
# En production : https://localhost:8080
LOCALHOST=https://localhost:5173/
```

