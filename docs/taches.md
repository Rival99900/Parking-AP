# 📋 Liste des tâches — Parking-AP

> Application web de réservation de places de parking numérotées pour le personnel des ligues.
> Suivi des tâches en direct : **Asana** (projet « Projet Parking »).
> Bien sur les tâches peuvent changer.

---

## 👥 Équipe et responsabilités

| Membre | Rôle | Livrables |
|---|---|---|
| **Albert** | Dépôt GitHub + plan du site | Repo, structure des dossiers, README, `plan-du-site.md` |
| **Ibrahima** | Préparation de la BDD + MCD | MCD, règles de gestion, dictionnaire de données |
| **Chris-Elliot** | Maquettes | Maquettes desktop + mobile (front-office et back-office) |

> Chef de projet : *on réflechis*.

---

### 🔴 Priorité 1 — Dépôt GitHub *(Albert)*

- [x] Créer le dépôt GitHub du projet
- [x] Ajouter Ibrahima et Chris-Elliot comme collaborateurs
- [x] Créer l'arborescence :
  ```
  parking/
  ├── README.md
  ├── docs/
  │   ├── mcd/
  │   ├── maquettes/
  │   ├── plan-du-site.md
  │   └── taches.md
  └── src/
  ```
- [x] Rédiger le `README.md` (présentation, équipe, structure du repo)
- [x] Ajouter ce fichier `taches.md` dans `docs/`
- [ ] Vérifier que chaque membre a bien fait au moins un commit
- [x] Déposer l'adresse du repo (et la branche si autre que `master`) sur la plateforme

### 🔴 Priorité 1 — MCD + préparation de la BDD *(Ibrahima)*

- [ ] Lister les entités et attributs prochainement.
- [ ] Définir les associations et cardinalités
- [ ] Prévoir la gestion du mot de passe perdu (jeton de réinitialisation)
- [ ] Rédiger les règles de gestion, notamment :
  - une place est attribuée aléatoirement et immédiatement si elle est libre
  - la réservation expire automatiquement (durée par défaut fixée par l'administrateur)
  - si aucune place n'est libre, l'utilisateur passe en liste d'attente
  - impossible de demander une place si on est en attente ou si on en occupe déjà une
  - une réservation peut être fermée avant son expiration (par l'utilisateur ou l'admin)
- [ ] Exporter le MCD en image (PNG) + conserver le fichier source
- [ ] Déposer le tout dans `docs/mcd/`

### 🟠 Priorité 2 — Plan du site avec URLs *(Albert)*

- [ ] Lister les pages du **front-office** (connexion, mot de passe oublié, espace utilisateur, réservation, historique, changement de mot de passe, aide)
- [ ] Lister les pages du **back-office** (connexion admin, utilisateurs, places, file d'attente, historique, attribution manuelle, paramètres)
- [ ] Définir l'URL de chaque page
- [ ] Réaliser un schéma en arbre du site
- [ ] Rédiger `docs/plan-du-site.md`
- [ ] Vérifier la cohérence avec les maquettes de Chris-Elliot

### 🟠 Priorité 2 — Maquettes *(Chris-Elliot)*

- [ ] Choisir l'outil (Figma, draw.io, Balsamiq...)
- [ ] Front-office : connexion
- [ ] Front-office : tableau de bord (place attribuée / rang dans la file / bouton « Réserver »)
- [ ] Front-office : historique des places
- [ ] Front-office : changement de mot de passe et mot de passe oublié
- [ ] Back-office : liste des utilisateurs (validation, réinitialisation de mot de passe)
- [ ] Back-office : liste des places
- [ ] Back-office : file d'attente (modification des positions)
- [ ] Back-office : historique et attribution manuelle
- [ ] Prévoir une version **mobile** de chaque page (design responsive)
- [ ] Exporter en PNG/PDF dans `docs/maquettes/`

### 🟡 Priorité 3 — Revue finale *(toute l'équipe)*

- [ ] Relire ensemble le MCD, les maquettes et le plan du site
- [ ] Vérifier que les URLs du plan du site correspondent aux maquettes
