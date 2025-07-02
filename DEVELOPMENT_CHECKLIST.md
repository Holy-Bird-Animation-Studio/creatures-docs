# 📋 Checklist de développement - Générateur de personnages stylisés

## 🔧 Prérequis techniques à valider avant démarrage

### Environnement de développement
- [ ] Python 3.9+ installé
- [ ] Node.js 18+ installé
- [ ] Docker et Docker Compose disponibles
- [ ] GPU CUDA disponible (pour Stable Diffusion XL)
- [ ] Espace disque suffisant (≥20GB pour modèles IA)

### APIs externes
- [ ] Clé API Meshy obtenue et testée
- [ ] Limites/quotas Meshy API clarifiés
- [ ] Stratégie de fallback si API Meshy indisponible

## 🟡 Phase 1 — Initialisation technique (2-3 jours)

### Structure projet
- [ ] Créer dossier `app/` avec modules :
  - [ ] `app/api/` (routes FastAPI)
  - [ ] `app/core/` (config, database)
  - [ ] `app/services/` (generation, 3d)
  - [ ] `app/models/` (SQLAlchemy si Phase 5)
- [ ] Créer `frontend/` avec React + TypeScript
- [ ] Créer `environments/client_test/` avec :
  - [ ] `prompt.txt` (template de base)
  - [ ] `attributes.json` (couleurs, objets disponibles)
  - [ ] `lora/` (dossier pour LoRA custom)

### Backend minimal
- [ ] FastAPI avec endpoint `/generate-image` (POST)
- [ ] Gestion CORS pour frontend
- [ ] Structure de réponse standardisée
- [ ] Logging de base configuré

### Frontend minimal  
- [ ] Composant `CameraCapture` (accès webcam)
- [ ] Composant `AttributeSelector` (couleurs, passions)
- [ ] Composant `ImagePreview` (affichage résultat)
- [ ] Routing de base (page principale)

### Tests de base
- [ ] API health check fonctionnel
- [ ] Frontend build sans erreurs
- [ ] Communication frontend ↔ backend

## 🟢 Phase 2 — Génération image stylisée (5-7 jours)

### Installation IA locale
- [ ] Stable Diffusion XL via `diffusers` installé
- [ ] IP-Adapter pour conservation traits visage
- [ ] Test de génération basique (prompt simple)
- [ ] Mesure temps de génération sur hardware cible

### Intégration LoRA custom
- [ ] Mécanisme chargement LoRA dynamique
- [ ] LoRA test créé/obtenu pour `client_test`
- [ ] Validation qualité génération avec LoRA

### Service de génération
- [ ] `generation.py` avec classe `ImageGenerator`
- [ ] Chargement environnement depuis `environments/`
- [ ] Construction prompt dynamique :
  - [ ] Template base depuis `prompt.txt`
  - [ ] Injection attributs utilisateur
  - [ ] Injection données photo (IP-Adapter)
- [ ] Retour image en base64 via API

### Tests qualité
- [ ] Test avec plusieurs photos visages différents
- [ ] Test variation attributs (couleurs, objets)
- [ ] Validation cohérence style avec LoRA
- [ ] Performance : temps génération < 30s

## 🔵 Phase 3 — Génération 3D (3-4 jours)

### Intégration Meshy API
- [ ] Service `MeshyService` pour appels API
- [ ] Upload image stylisée vers Meshy
- [ ] Récupération URL .glb généré
- [ ] Gestion timeouts et erreurs API

### Stockage fichiers 3D
- [ ] Dossier `generated/` pour fichiers temporaires
- [ ] Download .glb depuis URL Meshy
- [ ] Nettoyage automatique fichiers anciens
- [ ] Endpoint API pour servir fichiers .glb

### Visualisation 3D frontend
- [ ] Composant `Model3DViewer` (Three.js ou React-Three-Fiber)
- [ ] Chargement et affichage .glb
- [ ] Contrôles rotation/zoom de base
- [ ] Bouton téléchargement modèle

### Tests 3D
- [ ] Pipeline complet photo → image stylisée → 3D
- [ ] Qualité modèles 3D générés acceptable
- [ ] Performance chargement viewer 3D

## 🟣 Phase 4 — Multi-environnements (2-3 jours)

### Gestion environnements dynamiques
- [ ] Fonction `load_environment(env_id)` 
- [ ] Paramètre `env_id` dans toutes routes API
- [ ] Chargement LoRA spécifique par environnement
- [ ] Validation environnement existe avant génération

### Frontend multi-environnements
- [ ] Sélecteur environnement dans interface
- [ ] Adaptation attributs disponibles par environnement
- [ ] Prévisualisation style par environnement

### Tests environnements multiples
- [ ] Créer 2-3 environnements test différents
- [ ] Validation génération différente par environnement
- [ ] Commutation environnement sans restart

## ⚫ Phase 5 — Base de données (3-4 jours)

### Setup PostgreSQL
- [ ] Docker Compose avec PostgreSQL
- [ ] SQLAlchemy configuré
- [ ] Models : `Client`, `Environment`, `Generation`
- [ ] Migrations avec Alembic

### Logging et persistance
- [ ] Sauvegarde chaque génération en DB
- [ ] Métadonnées : env_id, attributs, temps génération
- [ ] Endpoint historique générations
- [ ] Statistiques usage par environnement

### Stockage fichiers (optionnel)
- [ ] Intégration S3 ou stockage cloud
- [ ] Migration fichiers locaux vers cloud
- [ ] URLs signées pour téléchargement sécurisé

## 🟠 Phase 6 — Interface d'administration (4-5 jours)

### Structure admin interface
- [ ] Créer dossier `admin/` avec pages React
- [ ] Routing admin séparé du frontend client
- [ ] Authentification admin (JWT)
- [ ] Dashboard principal avec métriques

### Gestion clients et environnements
- [ ] Page CRUD clients
- [ ] Liste/création environnements par client
- [ ] Éditeur prompts templates en temps réel
- [ ] Upload et gestion fichiers LoRA
- [ ] Prévisualisation attributs disponibles

### Monitoring et statistiques
- [ ] Graphiques générations par client/environnement
- [ ] Temps de traitement moyen
- [ ] Taille fichiers générés
- [ ] Logs d'erreurs centralisés
- [ ] Alertes seuils d'usage

### API endpoints admin
- [ ] `POST /api/admin/clients` (création client)
- [ ] `PUT /api/admin/clients/{id}` (mise à jour client)
- [ ] `POST /api/admin/environments` (création environnement)
- [ ] `PUT /api/admin/environments/{env_id}` (édition prompt/attributs)
- [ ] `POST /api/admin/environments/{env_id}/lora` (upload LoRA)
- [ ] `GET /api/admin/stats` (statistiques globales)
- [ ] `GET /api/admin/generations` (historique complet)

### Configuration système
- [ ] Paramètres modèles IA (steps, guidance_scale)
- [ ] Quotas par client (générations/jour)
- [ ] Gestion cache modèles
- [ ] Configuration stockage (local/S3)

## 🚀 Déploiement et finalisation

### Docker & Production
- [ ] Dockerfile optimisé pour app
- [ ] Docker Compose production-ready
- [ ] Variables d'environnement sécurisées
- [ ] Monitoring et logs centralisés

### Tests complets
- [ ] Tests end-to-end pipeline complet
- [ ] Tests charge (génération simultanée)
- [ ] Tests récupération après panne
- [ ] Documentation API complète

## ❓ Questions à clarifier avant démarrage

1. **Hardware cible** : Spécifications GPU disponible ?
2. **Volumétrie** : Nombre générations/jour attendu ?
3. **Styles** : Combien d'environnements/styles différents prévus ?
4. **Budget** : Limites coût API Meshy ?
5. **Délais** : Échéance pour version MVP ?
6. **Données** : Exemples de LoRA/styles à implémenter ?