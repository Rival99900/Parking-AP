# 🗺️ Plan du site — Parking-AP

> Application web de réservation de places de parking numérotées pour le personnel des ligues.
> Ce document décrit l'arborescence du site, les URLs de chaque page et les règles d'accès.

---

## 1. Vue d'ensemble

Le site est divisé en deux parties bien séparées :

- **Front-office** : espace réservé aux utilisateurs (personnel des ligues) dont l'inscription a été validée par un administrateur.
- **Back-office** : espace réservé à l'administrateur, seul utilisateur autorisé à y accéder.

Toutes les pages (sauf la connexion et le mot de passe oublié) nécessitent d'être **authentifié**.

---

## 2. Front-office (utilisateur)

| Page | URL | Accès | Description |
|---|---|---|---|
| Accueil | `/` | Public | Redirige vers `/login` (ou vers `/espace` si déjà connecté) |
| Connexion | `/login` | Public | Identification par email et mot de passe |
| Mot de passe oublié | `/mot-de-passe-oublie` | Public | Saisie de l'email pour recevoir un lien de réinitialisation |
| Réinitialisation | `/reinitialisation/{token}` | Public (avec jeton valide) | Choix d'un nouveau mot de passe |
| Tableau de bord | `/espace` | Utilisateur connecté | Affiche la place attribuée, ou le rang dans la file d'attente, ou le bouton « Réserver » |
| Demande de réservation | `/espace/reserver` | Utilisateur connecté | Lance la demande de place (attribution immédiate ou mise en file d'attente) |
| Historique | `/espace/historique` | Utilisateur connecté | Liste des places précédemment attribuées |
| Modifier mon mot de passe | `/espace/mot-de-passe` | Utilisateur connecté | Formulaire de changement de mot de passe |
| Aide | `/aide` | Utilisateur connecté | Documentation utilisateur accessible depuis l'application |
| Déconnexion | `/logout` | Utilisateur connecté | Ferme la session et redirige vers `/login` |

---

## 3. Back-office (administrateur)

| Page | URL | Accès | Description |
|---|---|---|---|
| Connexion admin | `/admin/login` | Public | Identification de l'administrateur |
| Tableau de bord | `/admin` | Admin | Vue synthétique : places libres/occupées, taille de la file d'attente |
| Liste des utilisateurs | `/admin/utilisateurs` | Admin | Validation des inscriptions, création, suppression |
| Édition d'un utilisateur | `/admin/utilisateurs/{id}` | Admin | Modification des informations, réinitialisation du mot de passe |
| Liste des places | `/admin/places` | Admin | Ajout, modification, activation/désactivation des places |
| File d'attente | `/admin/attente` | Admin | Consultation et modification de la position des personnes en attente |
| Historique des attributions | `/admin/historique` | Admin | Toutes les réservations passées et en cours |
| Attribution manuelle | `/admin/attribuer` | Admin | Attribuer une place précise à un utilisateur |
| Paramètres | `/admin/parametres` | Admin | Durée de réservation par défaut |
| Déconnexion | `/admin/logout` | Admin | Ferme la session admin |

---

## 4. Actions (envois de formulaires)

Ces URLs ne sont pas des pages à afficher mais des actions déclenchées par des boutons ou des formulaires.

| Action | URL | Méthode | Qui |
|---|---|---|---|
| Demander une place | `/espace/reserver` | POST | Utilisateur |
| Fermer sa réservation avant expiration | `/espace/reservation/{id}/fermer` | POST | Utilisateur |
| Quitter la file d'attente | `/espace/attente/quitter` | POST | Utilisateur |
| Valider une inscription | `/admin/utilisateurs/{id}/valider` | POST | Admin |
| Réinitialiser un mot de passe | `/admin/utilisateurs/{id}/reinitialiser` | POST | Admin |
| Fermer une réservation | `/admin/reservations/{id}/fermer` | POST | Admin |
| Déplacer une personne dans la file | `/admin/attente/{id}/deplacer` | POST | Admin |

---

## 5. Pages d'erreur

| Code | Cas | Comportement |
|---|---|---|
| **403** | Utilisateur non-admin qui tente d'accéder à `/admin/*` | Message « Accès refusé » |
| **404** | URL inexistante | Page « Page introuvable » avec lien vers l'accueil |
| **Redirection** | Utilisateur non connecté sur une page protégée | Redirection vers `/login` (ou `/admin/login` pour `/admin/*`) |

---

## 6. Règles d'accès résumées

- Un visiteur non connecté ne voit que `/login`, `/mot-de-passe-oublie` et `/reinitialisation/{token}`.
- Un utilisateur connecté n'accède qu'aux pages `/espace/*` et `/aide`.
- Seul l'administrateur accède aux pages `/admin/*`.
- Le bouton « Réserver » n'est utilisable que si l'utilisateur **n'est pas déjà en file d'attente** et **n'occupe pas déjà une place** (règle vérifiée côté serveur).

---

## 8. Correspondance avec les autres documents

- **MCD** : `docs/mcd/`
- **Maquettes** : `docs/maquettes/` (une maquette par page principale, en version desktop et mobile)
- **Liste des tâches** : `docs/taches.md`
