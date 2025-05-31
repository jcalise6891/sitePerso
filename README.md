# 🚀 Site Personnel Laravel

Un site personnel moderne développé avec Laravel et une architecture Docker complète pour un développement et déploiement efficaces.

## 📋 Objectif du Projet

Créer un site personnel professionnel avec une architecture moderne, évolutive et facilement déployable. Le projet remplace une ancienne version Symfony par une stack Laravel plus adaptée aux besoins actuels.

## 🛠️ Technologies Utilisées

### Backend
- **Laravel 11** - Framework PHP moderne
- **PHP 8.3-FPM** - Version PHP optimisée pour les performances
- **MySQL 8** - Base de données relationnelle
- **Composer** - Gestionnaire de dépendances PHP

### Frontend
- **Vite** - Build tool moderne pour le développement frontend
- **Node.js 20** - Runtime JavaScript
- **npm** - Gestionnaire de packages JavaScript

### Infrastructure & DevOps
- **Docker & Docker Compose** - Containerisation complète
- **Traefik v2.10** - Reverse proxy et load balancer
- **Nginx Alpine** - Serveur web haute performance
- **Mailhog** - Testing des emails en développement

### Outils de Développement
- **Git** - Contrôle de version
- **GitHub Actions** - CI/CD (à venir)
- **Custom Bash Aliases** - Commandes de développement optimisées

## 🏗️ Architecture

```
📦 sitePerso/
├── 🐳 docker/
│   ├── nginx/           # Configuration Nginx
│   ├── php/            # Dockerfile PHP-FPM
│   └── traefik/        # Configuration Traefik
├── 🎨 laravel/         # Application Laravel
│   ├── app/
│   ├── public/
│   ├── resources/
│   └── ...
├── 🔧 .env             # Variables Docker Compose
├── 🔧 .env.local       # Variables Docker dev
├── 🔧 .env.prod        # Variables Docker prod
└── 📋 docker-compose.yml
```

## 🚀 Installation & Configuration

### Prérequis
- Docker & Docker Compose
- Git
- Un éditeur de texte

### 1. Cloner le projet
```bash
git clone [URL_DU_REPO]
cd sitePerso
```

### 2. Configuration de l'environnement

#### Fichier hosts
Ajouter dans `/etc/hosts` :
```
127.0.0.1 local.jcalise.fr
```

#### Fichiers d'environnement
Les fichiers `.env`, `.env.local`, `.env.prod` et `laravel/.env` sont déjà configurés.

### 3. Lancement du projet
```bash
# Installation des alias (optionnel mais recommandé)
cp .bash_aliases ~/.bash_aliases
source ~/.bashrc

# Démarrage des containers
docker-compose up -d

# Installation des dépendances Laravel
docker-compose exec app composer install

# Configuration Laravel
docker-compose exec app cp .env.local .env
docker-compose exec app php artisan key:generate
docker-compose exec app php artisan migrate

# Correction des permissions
docker-compose exec app chmod -R 777 storage bootstrap/cache
```

## 🌐 Accès aux Services

### Développement
- **Site principal** : http://local.jcalise.fr
- **Mailhog** : http://local.jcalise.fr:8025
- **Traefik Dashboard** : http://localhost:8080

### Production
- **Site principal** : https://jcalise.fr
- **Mailhog** : https://mail.jcalise.fr

## 🔧 Commandes Utiles

### Aliases disponibles
```bash
# Docker
dcu                 # docker-compose up -d
dcd                 # docker-compose down
dcl                 # docker-compose logs -f

# Laravel Artisan
art migrate         # php artisan migrate
art-clear          # Clear tous les caches
art tinker         # php artisan tinker

# Développement
app                # Entrer dans le container PHP
site               # cd ~/sitePerso
fix-perms          # Corriger les permissions
status             # Voir l'état des containers
```

### Commandes Docker complètes
```bash
# Redémarrage complet
docker-compose down && docker-compose up -d

# Logs en temps réel
docker-compose logs -f app

# Accès au container
docker-compose exec app bash
```

## 📁 Structure Laravel

```
laravel/
├── app/
│   ├── Http/Controllers/
│   ├── Models/
│   └── ...
├── resources/
│   ├── views/
│   ├── js/
│   └── css/
├── routes/
│   ├── web.php
│   └── api.php
├── database/
│   ├── migrations/
│   └── seeders/
└── public/
    └── index.php
```

## 🔄 Workflow de Développement

### Environnement Local
1. Développement sur `local.jcalise.fr`
2. Tests avec Mailhog
3. Utilisation des alias pour les commandes fréquentes

### Déploiement
1. Push sur la branche `main`
2. GitHub Actions (à configurer)
3. Déploiement automatique sur le VPS

## 🎯 Fonctionnalités Prévues

- [ ] **Authentification** - Système de login/register
- [ ] **Portfolio** - Présentation des projets
- [ ] **Blog** - Articles et actualités
- [ ] **Contact** - Formulaire de contact avec Mailhog
- [ ] **Admin Panel** - Interface d'administration
- [ ] **API REST** - Endpoints pour applications externes
- [ ] **Tests** - Tests unitaires et fonctionnels
- [ ] **CI/CD** - Pipeline de déploiement automatique

## 🐛 Dépannage

### Problèmes fréquents

**Erreur de permissions**
```bash
docker-compose exec app chmod -R 777 storage bootstrap/cache
```

**Cache Laravel**
```bash
docker-compose exec app php artisan cache:clear
docker-compose exec app php artisan config:clear
```

**Base de données**
```bash
docker-compose exec app php artisan migrate:fresh
```

**Rebuild complet**
```bash
docker-compose down
docker-compose up -d --build --force-recreate
```

## 📝 Notes de Développement

### Environnements
- **Local** : `.env.local` → `local.jcalise.fr`
- **Production** : `.env.prod` → `jcalise.fr`

### Base de Données
- **Host** : `mysql` (nom du service Docker)
- **Database** : `laravel`
- **User** : XXX
- **Password** : XXX

## 🤝 Contribution

1. Fork le projet
2. Créer une branche feature (`git checkout -b feature/nouvelle-fonctionnalite`)
3. Commit les changements (`git commit -m 'Ajout nouvelle fonctionnalité'`)
4. Push vers la branche (`git push origin feature/nouvelle-fonctionnalite`)
5. Ouvrir une Pull Request

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 👨‍💻 Auteur

**JCalise**
- Site : [jcalise.fr](https://jcalise.fr)
- GitHub : [@jcalise6891](https://github.com/jcalise6891)

---

*Développé avec ❤️ et Laravel*