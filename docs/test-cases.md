# Cahier de Recette — QuickOrder V3.1

## 1. Cas Nominaux (6)

| ID | Titre | Objectif | Préconditions | Données | Étapes | Résultat attendu | Résultat obtenu | Statut |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-NOM-01** | Connexion valide | Valider l'accès client | Compte actif | `alice@example.com` / `Password123!` | 1. Aller sur `/login`<br>2. Saisir identifiants<br>3. Valider | Connexion réussie, accès au profil | Connexion OK | **PASS** |
| **TC-NOM-02** | Consultation du catalogue | Vérifier la liste des plats | Application en ligne | Aucune | 1. Accéder à l'accueil | Plats affichés avec nom, prix, photo | Catalogue affiché | **PASS** |
| **TC-NOM-03** | Ajout d'article disponible | Ajouter un plat au panier | Produit en stock | *Couscous Poulet* | 1. Cliquer sur "Ajouter au panier" | Produit ajouté, sous-total mis à jour | Article ajouté | **PASS** |
| **TC-NOM-04** | Validation de commande | Valider un achat complet | Panier non vide | Adresse valide | 1. Ouvrir le panier<br>2. Cliquer "Valider" | Commande créée avec statut "Payée" | Commande enregistrée | **PASS** |
| **TC-NOM-05** | API Catalogue `/api/products` | Vérifier le retour JSON | API accessible | `X-API-Key: quickorder-demo-key` | 1. Requête `GET /api/products` | Code HTTP 200 + Liste produits JSON | HTTP 200 OK | **PASS** |
| **TC-NOM-06** | Déconnexion | Vérifier la fermeture de session | Client connecté | Aucune | 1. Cliquer "Déconnexion" | Session fermée, redirection `/login` | Déconnexion OK | **PASS** |

## 2. Cas Limites (6)

| ID | Titre | Objectif | Préconditions | Données | Étapes | Résultat attendu | Résultat obtenu | Statut |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-LIM-01** | Quantité maximale (99) | Tester l'ajout limite | Produit en stock | Quantité: `99` | 1. Saisir 99 en quantité<br>2. Ajouter au panier | Quantité 99 acceptée, total exact | Quantité ajoutée | **PASS** |
| **TC-LIM-02** | Mot de passe longueur min | Tester la limite de 8 caractères | Page d'inscription | `Pass123!` (8 char) | 1. Saisir mot de passe de 8 char<br>2. Valider | Accepté sans erreur de longueur | Accepté | **PASS** |
| **TC-LIM-03** | Commande d'un montant faible | Valider commande de 1€ | Produit à 1€ | Quantité: `1` | 1. Ajouter l'article à 1€<br>2. Commander | Validation réussie sans blocage | Commande validée | **PASS** |
| **TC-LIM-04** | Adresse longue (255 char) | Tester le champ d'adresse | Étape de livraison | Chaîne de 255 'A' | 1. Saisir 255 caractères<br>2. Valider | Adresse acceptée ou tronquée proprement | Accepté | **PASS** |
| **TC-LIM-05** | Code promo jour limite | Valider un coupon le dernier jour | Coupon actif | Code: `PROMO2026` | 1. Saisir le code dans le panier | Réduction appliquée | Réduction appliquée | **PASS** |
| **TC-LIM-06** | Réduction de quantité à 1 | Diminuer la quantité dans le panier | Panier avec 2 articles | Quantité: `1` | 1. Cliquer `-` pour passer à 1 | Quantité passe à 1, total recalculé | Prix inchangé | **FAIL** |

## 3. Cas d'Erreur (6)

| ID | Titre | Objectif | Préconditions | Données | Étapes | Résultat attendu | Résultat obtenu | Statut |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ERR-01** | Connexion mot de passe faux | Rejeter les identifiants invalides | Compte existant | `alice@example.com` / `FauxPass!` | 1. Tenter de se connecter | Erreur "Identifiants invalides" (HTTP 401) | HTTP 500 sur l'API | **FAIL** |
| **TC-ERR-02** | Validation panier vide | Bloquer les commandes à 0 article | Panier vide | Aucune | 1. Tenter de valider le panier vide | Action bloquée / Message d'erreur | Commande créée via API | **FAIL** |
| **TC-ERR-03** | Quantité négative | Rejeter les valeurs négatives | Article au panier | Quantité: `-2` | 1. Saisir `-2` dans la quantité | Rejet ou réinitialisation à 1 | Valeur négative acceptée | **FAIL** |
| **TC-ERR-04** | API sans clé d'accès | Vérifier la sécurité API | Endpoint sécurisé | Clé API absente | 1. Envoyer `POST /api/orders` sans header | Code HTTP 401 Unauthorized | HTTP 401 | **PASS** |
| **TC-ERR-05** | Code promo inexistant | Rejeter un faux code promo | Panier non vide | Code: `FAUXCODE` | 1. Appliquer le code `FAUXCODE` | Message "Code invalide" | Code appliqué / Erreur | **FAIL** |
| **TC-ERR-06** | Inscription email doublon | Vérifier l'unicité de l'email | Email déjà utilisé | `alice@example.com` | 1. Créer un compte avec cet email | Erreur "Email déjà utilisé" | Erreur affichée | **PASS** |

## 4. Règles Métier (6)

| ID | Titre | Objectif | Préconditions | Données | Étapes | Résultat attendu | Résultat obtenu | Statut |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-RGL-01** | Produit hors stock inestimable | Bloquer l'ajout d'un plat épuisé | Plat *Tajine légumes* (stock 0) | Produit hors stock | 1. Cliquer "Ajouter au panier" | Bouton désactivé, ajout impossible | Produit ajouté | **FAIL** |
| **TC-RGL-02** | Suppression d'article panier | Vérifier la suppression d'une ligne | Article au panier | Article unique | 1. Cliquer sur la corbeille | Article retiré, total mis à jour | Article reste présent | **FAIL** |
| **TC-RGL-03** | Recalcul dynamique du total | Vérifier la mise à jour du prix | Plat à 12€ | Quantité: 1 -> 3 | 1. Passer la quantité de 1 à 3 | Prix total passe à 36€ | Prix reste bloqué à 12€ | **FAIL** |
| **TC-RGL-04** | Code promo expiré | Bloquer les coupons périmés | Code expiré | Code: `EXPIRE2025` | 1. Appliquer le code expiré | Rejet "Code expiré" | Code accepté | **FAIL** |
| **TC-RGL-05** | Rupture pendant la commande | Contrôler le stock à la validation | Stock passe à 0 pendant la saisie | Produit en panier | 1. Valider la commande | Erreur "Produit non disponible" | Commande validée | **FAIL** |
| **TC-RGL-06** | Droits d'accès Admin API | Bloquer l'accès admin aux clients | Connecté en client | Route `/api/admin/orders` | 1. Accéder à la route admin | Refus HTTP 403 Forbidden | HTTP 403 Forbidden | **PASS** |