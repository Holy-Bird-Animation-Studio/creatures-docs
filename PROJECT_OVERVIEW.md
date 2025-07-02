# 🧠 Générateur de personnages stylisés personnalisés
**Mode SaaS – Multi-clients, multi-environnements**
*Juin 2025*

## 🎯 Objectif du projet
Système complet permettant de générer un personnage stylisé à partir :
- Photo prise sur place (caméra)
- Direction artistique prédéfinie
- Choix personnalisés (couleurs, attributs, passions)

**Résultats produits :**
- Image stylisée 2D
- Modèle 3D imprimable (.glb/.stl)
- Intégration dans univers commun en ligne

## 🏗️ Architecture cible (SaaS industrialisable)

### 1. Environnement utilisateur
- Interface React plein écran (borne tactile/desktop)
- Prise de photo, sélection couleurs/attributs
- Prévisualisation 2D + 3D

### 2. Backend API (FastAPI)
- Orchestration appels IA
- Gestion clients/environnements/logs
- Génération dynamique prompts

### 3. Intelligence Artificielle (locale)
- Stable Diffusion XL + LoRA par style + IP-Adapter
- Prompt templates dynamiques

### 4. Génération 3D
- Meshy API (image → .glb/.stl)
- Stockage temporaire local/S3

### 5. Base de données
- PostgreSQL : clients, environnements, générations

### 6. Infrastructure
- Docker + Docker Compose
- Cible future : Kubernetes/serverless GPU

## 🗂️ Structure multi-environnements
```
/environments/
├── clientA_env1/
│   ├── prompt.txt
│   ├── attributes.json
│   ├── lora/
│   └── style_dataset/
├── clientA_env2/
├── clientB_env1/
```

## 🚀 Phases de développement

### 🟡 Phase 1 — Initialisation technique
- Structure modulaire app/
- Backend FastAPI minimal
- Frontend React avec CameraCapture
- Structure environments/client_test/

### 🟢 Phase 2 — Test génération image stylisée
- Stable Diffusion XL local
- IP-Adapter + LoRA custom
- generation.py avec chargement dynamique
- API retour image base64

### 🔵 Phase 3 — Intégration Meshy API
- Appel API Meshy
- Récupération .glb/.stl
- Stockage /generated/
- Viewer 3D React

### 🟣 Phase 4 — Architecture multi-style
- load_environment(env_id)
- env_id dans appels API
- Support multiple LoRA/attributs

### ⚫ Phase 5 — Base de données et stockage
- PostgreSQL + SQLAlchemy
- Tables clients/environnements/générations
- Logging générations
- Option S3