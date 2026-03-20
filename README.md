# 🌍 Absolute SARL — Plateforme Immigration & Services

> **Plateforme  full-stack** développée pour une agence de conseil en immigration basée à Douala, Cameroun. Couvre l'intégralité du parcours client — du diagnostic d'orientation à la prise de rendez-vous — avec un back-office administratif complet.

[![Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)](https://www.typescriptlang.org)
[![Node.js](https://img.shields.io/badge/Node.js-20-green?logo=node.js)](https://nodejs.org)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-blue?logo=postgresql)](https://postgresql.org)
[![Prisma](https://img.shields.io/badge/Prisma-7-darkblue?logo=prisma)](https://prisma.io)
[![Déployé sur Vercel](https://img.shields.io/badge/Déployé-Vercel-black?logo=vercel)](https://vercel.com)

---

## 📌 Présentation du projet

**Absolute SARL** est une entreprise de services professionnels basée à Douala, Cameroun, spécialisée dans :
- 🇨🇦 L'immigration vers le Canada, la Belgique et la France
- 💻 Le marketing digital et l'infographie
- 📋 L'e-secrétariat et l'accompagnement administratif
- 🛒 Le commerce général

Cette plateforme a été conçue et développée de zéro pour digitaliser les opérations de l'entreprise, en remplaçant des processus manuels (WhatsApp, fichiers Excel) par une application web structurée, multilingue et sécurisée.

**Site en production :** [absolutesarl.com](https://absolutesarl.com)

---

## ✨ Fonctionnalités

### 👤 Espace Client
- **Interface multilingue** — Français, Anglais, Espagnol (next-intl)
- **Formulaire de diagnostic d'orientation en 6 étapes** avec logique conditionnelle et validation côté backend
- **Prise de rendez-vous** avec sélection de date, heure et motif
- **Espace client personnel** — suivi des diagnostics, rendez-vous et documents
- **Authentification complète** — inscription, connexion, vérification email par OTP, réinitialisation de mot de passe
- **Formulaire de contact** avec routing par sujet

### 🛠️ Back-office Administrateur
- **Tableau de bord** avec KPIs en temps réel (utilisateurs, diagnostics, messages, rendez-vous, articles)
- **Gestion des diagnostics** — fiche complète du candidat, workflow de statuts (NOUVEAU → LU → EN COURS → TRAITÉ → RÉSOLU → ARCHIVÉ), **export PDF**
- **Gestion des rendez-vous** — approbation / rejet avec notes internes
- **Gestion des messages de contact** — suivi de statut, notes d'équipe
- **Gestion des articles de blog** — contenu bilingue FR/EN, upload d'images Cloudinary
- **Gestion des utilisateurs** — rôles (ADMIN, EMPLOYÉ, CLIENT, PROSPECT)
- **Contrôle d'accès basé sur les rôles (RBAC)** — protection des routes au niveau middleware

---

## 🏗️ Stack Technique

### Frontend — `client-absolute-sarl`
| Technologie | Usage |
|---|---|
| Next.js 15 (App Router) | Framework principal |
| TypeScript | Langage |
| Tailwind CSS v4 | Styles |
| shadcn/ui | Bibliothèque de composants |
| Zustand + persist | Gestion d'état (authentification) |
| next-intl | Internationalisation (FR / EN / ES) |
| React Hook Form + Zod | Validation des formulaires |
| Framer Motion | Animations |
| Axios | Client HTTP |
| react-to-pdf | Export PDF |
| Cloudinary | Hébergement d'images |

### Backend — `server-absolute-sarl`
| Technologie | Usage |
|---|---|
| Node.js + Express | Serveur |
| TypeScript | Langage |
| Prisma ORM v7 | ORM base de données |
| PostgreSQL | Base de données |
| JWT | Authentification |
| express-validator | Validation des requêtes |
| Swagger JSDoc | Documentation API |
| @prisma/adapter-pg | Adaptateur driver PostgreSQL |

---

## 📁 Structure du projet

```
├── client-absolute-sarl/              # Frontend Next.js
│   ├── app/
│   │   └── [locale]/
│   │       ├── (public)/              # Pages publiques
│   │       ├── (client)/              # Pages espace client
│   │       └── (admin)/               # Back-office administrateur
│   ├── components/
│   │   ├── ui/                        # Composants shadcn/ui
│   │   ├── diagnostics/               # Modals & tableau diagnostics
│   │   └── messages/                  # Composants messages contact
│   ├── lib/                           # Fonctions API & utilitaires
│   ├── store/                         # Store Zustand (auth)
│   ├── types/                         # Interfaces TypeScript
│   └── messages/                      # Fichiers de traduction i18n
│
└── server-absolute-sarl/              # Backend Express
    ├── src/
    │   ├── controllers/               # Contrôleurs de routes
    │   ├── services/                  # Logique métier
    │   ├── routes/                    # Routeurs Express + Swagger
    │   ├── validators/                # Règles de validation
    │   ├── middleware/                # Guards auth & rôles
    │   ├── types/                     # DTOs TypeScript
    │   └── config/                    # Config DB & Swagger
    └── prisma/
        └── schema.prisma              # Schéma de base de données
```

---

## 🗄️ Schéma de base de données

Modèles principaux :
- **User** — rôles : `ADMIN | EMPLOYE | CLIENT | PROSPECT`
- **Diagnostic** — formulaire d'orientation 6 étapes (30+ champs), workflow de statuts, scores tests de langue
- **RendezVous** — rendez-vous avec statut `PENDING | APPROVED | REJECTED`
- **ContactMessage** — formulaire de contact avec suivi de statut
- **Blog** — articles bilingues (FR/EN) avec images Cloudinary
- **Conversation + ChatMessage** — messagerie (client ↔ équipe)
- **ClientContent** — documents privés du client

---

## 🚀 Installation locale

### Prérequis
- Node.js 20+
- PostgreSQL 16+
- Compte Cloudinary

### Backend
```bash
cd server-absolute-sarl
npm install
cp .env.example .env
# Remplir DATABASE_URL, JWT_SECRET, etc.
npx prisma migrate dev
npx prisma generate
npm run dev
```

### Frontend
```bash
cd client-absolute-sarl
npm install
cp .env.local.example .env.local
# Remplir NEXT_PUBLIC_API_URL, NEXT_PUBLIC_CLOUDINARY_*
npm run dev
```

### Variables d'environnement

**Backend `.env`**
```env
DATABASE_URL="postgresql://user:motdepasse@localhost:5432/absolute_sarl_db"
JWT_SECRET="votre-secret-jwt"
PORT=5000
```

**Frontend `.env.local`**
```env
NEXT_PUBLIC_API_URL=http://localhost:5000
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=votre-cloud-name
NEXT_PUBLIC_CLOUDINARY_UPLOAD_PRESET=votre-upload-preset
```

---

## 📡 Documentation API

La documentation Swagger est disponible sur `http://localhost:5000/api/docs` après démarrage du backend.

Principaux endpoints :
| Méthode | Route | Accès |
|---|---|---|
| POST | `/api/auth/register` | Public |
| POST | `/api/auth/login` | Public |
| POST | `/api/diagnostics` | Public (JWT optionnel) |
| GET | `/api/diagnostics` | ADMIN + EMPLOYÉ |
| GET | `/api/diagnostics/stats` | ADMIN |
| POST | `/api/rendezvous` | CLIENT |
| PATCH | `/api/rendezvous/:id/approve` | EMPLOYÉ + ADMIN |
| GET | `/api/blogs` | Public |
| POST | `/api/blogs` | EMPLOYÉ + ADMIN |
| GET | `/api/users` | ADMIN |

---

## 🔐 Flux d'authentification

```
Inscription → OTP Email → Vérification → JWT émis → Zustand + Cookie
                                                      ↓
                                          Middleware lit le cookie
                                          → Redirection par rôle
                                          (admin/* | client/* | /)
```

---

## 🌐 Déploiement

| Service | Plateforme |
|---|---|
| Frontend | Vercel |
| Backend | Render |
| Base de données | Render PostgreSQL |
| Images | Cloudinary |

---

## 📸 Captures d'écran
### Partie Prospect et client
![client](https://i.postimg.cc/TPLcMN9m/Capture-d-ecran-(207).png)
### Tableau de bord
![Dashboard](https://i.postimg.cc/28ShNXjk/Capture-d-ecran-(208).png)
### Formulaire diagnostic
![Formulaire](https://i.postimg.cc/N065H1GR/Capture-d-ecran-(213).png)
---

## 👨‍💻 Développé par

**[PHANUEL ARSÈNE ]** — Développeur Full-Stack  
📧 [votre@email.com](mailto:phanuel.alibia@gmail.com)  
🔗 [linkedin.com/in/votre-profil](https://www.linkedin.com/in/phanuel-tsopze-8a33a52a4/)  
🌐 [votre-portfolio.com](https://phanuel-alibia.com/)

---

## 📄 Licence

Ce projet a été développé pour **Absolute SARL** (Douala, Cameroun).  
Le code est partagé à titre de portfolio. Tous droits réservés.
