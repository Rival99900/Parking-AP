# 🅿️ Parking-AP — Application de réservation de places de parking

> Projet de groupe BTS SIO — application web de gestion et de réservation de places de parking numérotées pour le personnel des ligues.

![Branche](https://img.shields.io/badge/branche-main-lightgrey)

---

## 📑 Sommaire

1. [Contexte et objectifs](#1--contexte-et-objectifs)
2. [Périmètre fonctionnel](#2--périmètre-fonctionnel)
3. [Règles de gestion](#3--règles-de-gestion)
4. [Acteurs et droits d'accès](#4--acteurs-et-droits-daccès)
5. [Sécurité](#5--sécurité)
6. [Choix techniques](#6--choix-techniques)
7. [Organisation du dépôt](#7--organisation-du-dépôt)
8. [Documentation du projet](#8--documentation-du-projet)
9. [Avancement](#9--avancement)
10. [Méthode de travail](#10--méthode-de-travail)
11. [Installation et déploiement](#11--installation-et-déploiement)
12. [Équipe](#12--équipe)

---

## 1. 🎯 Contexte et objectifs

Le parking est un véritable labyrinthe et le **stationnement sauvage** y est fréquent. Pour y remédier, il a été décidé d'attribuer à chaque membre qui en fait la demande **une place de parking numérotée**.

L'application doit permettre :

- aux **membres du personnel des ligues** de demander une place et de suivre leurs réservations ;
- à un **administrateur** de gérer les places, les inscriptions et la file d'attente.

L'application est destinée à être hébergée sur un **serveur accessible depuis le réseau local**.

---

## 2. 🧩 Périmètre fonctionnel

### Espace utilisateur (front-office)

- Authentification par mot de passe
- Demande de réservation d'une place (attribution **immédiate**)
- Consultation de la place attribuée et de l'**historique** des places précédentes
- Consultation de son **rang dans la file d'attente**
- Clôture anticipée de sa réservation
- Modification du mot de passe et fonction « mot de passe perdu ? »
- Documentation utilisateur accessible depuis l'application

### Espace administrateur (back-office)

- Authentification par mot de passe
- Gestion des utilisateurs : validation ou création des inscriptions, réinitialisation des mots de passe
- Gestion de la liste des places
- Consultation et édition de la **file d'attente** (modification des positions)
- Consultation de l'**historique** des attributions
- **Attribution manuelle** d'une place
- Paramétrage de la **durée de réservation par défaut**

---

## 3. 📏 Règles de gestion

| N° | Règle |
|---|---|
| RG1 | Seul le personnel des ligues peut utiliser le service ; toute inscription doit être **validée (ou créée) par un administrateur**. |
| RG2 | Lors d'une demande, une place **libre** est attribuée **aléatoirement et immédiatement**. |
| RG3 | Une réservation **expire automatiquement** au bout d'une durée par défaut définie par l'administrateur. |
| RG4 | Si aucune place n'est libre, l'utilisateur est placé en **liste d'attente**. |
| RG5 | L'utilisateur **ne choisit pas la date** : les réservations sont toujours immédiates. |
| RG6 | Un utilisateur **ne peut pas faire de demande** s'il est déjà en file d'attente ou s'il occupe déjà une place. |
| RG7 | Une réservation peut être **fermée avant son expiration** par l'utilisateur ou par l'administrateur. |
| RG8 | Une fois la réservation expirée, l'utilisateur doit **refaire une demande** pour obtenir une nouvelle place. |
| RG9 | L'administrateur est le **seul utilisateur du back-office**. |

---

## 4. 👤 Acteurs et droits d'accès

| Acteur | Accès | Droits |
|---|---|---|
| **Visiteur** (non connecté) | `/login`, `/mot-de-passe-oublie` | S'identifier, demander la réinitialisation de son mot de passe |
| **Utilisateur** (personnel des ligues, inscription validée) | `/espace/*`, `/aide` | Réserver, consulter sa place / son historique / son rang, modifier son mot de passe |
| **Administrateur** | `/admin/*` | Gérer utilisateurs, places, file d'attente, historique, attributions et paramètres |

Le détail des URLs est disponible dans le [plan du site](docs/plan-du-site.md).

---

## 5. 🔐 Sécurité

Le front-office doit être sécurisé et n'accepter que les demandes du personnel des ligues. Mesures prévues :

- **Protection des accès** par mot de passe (utilisateur et administrateur)
- **Hachage des mots de passe** (jamais stockés en clair)
- **Contrôles de saisie côté serveur** (validation systématique des données reçues)
- **Contrôles de saisie côté client** (confort d'utilisation, jamais suffisants seuls)
- **Protection contre les injections** (requêtes préparées, échappement des sorties)
- **Contrôle des droits** sur chaque page : un utilisateur ne peut pas accéder au back-office
- **Jeton à durée limitée** pour la réinitialisation du mot de passe

---

## 6. 🛠️ Choix techniques

> ⚠️ Section **à confirmer par l'équipe**.

| Élément | Choix |
|---|---|
| Langage côté serveur | *À définir* |
| Base de données | SGBD relationnel *(à définir)* |
| Front | HTML / CSS, design **responsive** |
| Modélisation | MCD (Merise) |
| Maquettes | *Outil à définir* |
| Gestion de versions | Git / GitHub |
| Gestion de tâches | Asana |
| Hébergement | Serveur accessible depuis le réseau local |

---

## 7. 📁 Organisation du dépôt

```
Parking-AP/
├── README.md              ← ce fichier
├── .gitignore
├── docs/
│   ├── taches.md          ← liste des tâches et répartition
│   ├── plan-du-site.md    ← arborescence et URLs
│   ├── journal.md         ← journal de bord de l'équipe
│   ├── mcd/               ← MCD (fichier source + export image)
│   └── maquettes/         ← maquettes desktop et mobile
└── src/                   ← code de l'application
```

---

## 8. 📚 Documentation du projet

| Document | Description | Lien |
|---|---|---|
| Liste des tâches | Répartition des rôles et tâches par priorité | [docs/taches.md](docs/taches.md) |
| Plan du site | Arborescence, URLs, règles d'accès | [docs/plan-du-site.md](docs/plan-du-site.md) |
| Journal de bord | Suivi chronologique du travail | [docs/journal.md](docs/journal.md) |
| MCD | Modèle conceptuel de données | [docs/mcd/](docs/mcd/) |
| Maquettes | Maquettes des pages du front et du back-office | [docs/maquettes/](docs/maquettes/) |

---

## 9. 📈 Avancement

- [x] Création du dépôt GitHub
- [x] Liste des tâches (`docs/taches.md`)
- [x] Plan du site avec URLs (`docs/plan-du-site.md`)
- [ ] MCD et préparation de la base de données
- [ ] Maquettes (front-office et back-office, desktop et mobile)
- [ ] Relecture croisée de la documentation
- [ ] Création de la base de données
- [ ] Authentification et gestion des mots de passe
- [ ] Réservation, file d'attente et expiration automatique
- [ ] Espace administrateur
- [ ] Contrôles de saisie et protection contre les injections
- [ ] HTML / CSS / responsive
- [ ] Documentation utilisateur et technique

---

## 10. 🤝 Méthode de travail

- **Un seul dépôt** partagé par toute l'équipe, branche principale : `main`.
- **Commits fréquents** avec des messages clairs et à l'impératif, par exemple :
  - `Ajoute le plan du site`
  - `Corrige les cardinalités du MCD`
  - `Ajoute les maquettes du back-office`
- **Chaque membre commit ses propres livrables** : l'historique Git reflète la participation de chacun.
- **Suivi des tâches** sur Asana (`À faire` → `En cours` → `Terminé`), synchronisé avec `docs/taches.md`.
- **Journal de bord** mis à jour à chaque avancée significative.

---

## 11. 🚀 Installation et déploiement

1. Prérequis (serveur web, SGBD)
2. Récupération du projet : `git clone https://github.com/Rival99900/Parking-AP.git`
3. Création et import de la base de données
4. Configuration (identifiants de connexion à la base, durée de réservation par défaut)
5. Accès depuis le réseau local

---

## 12. 👥 Équipe

| Membre | Rôle |
|---|---|
| **Albert** | Dépôt GitHub, plan du site |
| **Ibrahima** | Préparation de la base de données, MCD |
| **Chris-Elliot** | Maquettes |

**Chef de projet :** *à désigner*

---

<sub>Projet réalisé dans le cadre de la formation BTS SIO — 2026.</sub>
