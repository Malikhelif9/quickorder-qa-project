# Cahier de Recette — QuickOrder V3.1

| Catégorie | ID | Titre | Objectif | Préconditions | Données | Étapes | Résultat attendu | Résultat obtenu | Statut |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Nominal** | **TC-NOM-01** | Connexion valide | Valider l'accès client | Compte actif | `alice@example.com` / `Password123!` | 1. Aller sur `/login`<br>2. Saisir identifiants<br>3. Valider | Connexion réussie | Connexion OK | **PASS** |
| **Nominal** | **TC-NOM-02** | Consultation du catalogue | Vérifier la liste des plats | Application en ligne | Aucune | 1. Accéder à l'accueil | Plats affichés | Catalogue affiché | **PASS** |
| **Nominal** | **TC-NOM-03** | Ajout d'article disponible | Ajouter un plat au panier | Produit en stock | *Couscous Poulet* | 1. Cliquer sur "Ajouter au panier" | Produit ajouté | Article ajouté | **PASS** |
| **Nominal** | **TC-NOM-04** | Validation de commande | Valider un achat complet | Panier non vide | Adresse valide | 1. Ouvrir le panier<br>2. Cliquer "Valider" | Commande créée | Commande enregistrée | **PASS** |
| **Nominal** | **TC-NOM-05** | API Catalogue `/api/products` | Vérifier le retour JSON | API accessible | `X-API-Key: quickorder-demo-key` | 1. Requête `GET /api/products` | Code HTTP 200 + JSON | HTTP 200 OK | **PASS** |
| **Nominal** | **TC-NOM-06** | Déconnexion | Vérifier la fermeture de session | Client connecté | Aucune | 1. Cliquer "Déconnexion" | Session fermée | Déconnexion OK | **PASS** |
| **Limite** | **TC-LIM-01** | Quantité maximale (99) | Tester l'ajout limite | Produit en stock | Quantité: `99` | 1. Saisir 99<br>2. Ajouter | Quantité 99 acceptée | Quantité ajoutée | **PASS** |
| **Limite** | **TC-LIM-02** | Mot de passe longueur min | Tester la limite 8 char | Inscription | `Pass123!` | 1. Saisir mdp 8 char<br>2. Valider | Accepté | Accepté | **PASS** |
| **Limite** | **TC-LIM-03** | Commande montant faible | Valider commande 1€ | Produit à 1€ | Quantité: `1` | 1. Commander article 1€ | Validation réussie | Commande validée | **PASS** |
| **Limite** | **TC-LIM-04** | Adresse longue (255 char) | Tester le champ d'adresse | Livraison | 255 fois 'A' | 1. Saisir 255 char<br>2. Valider | Adresse acceptée | Accepté | **PASS** |
| **Limite** | **TC-LIM-05** | Code promo jour limite | Valider coupon dernier jour | Coupon actif | `PROMO2026` | 1. Appliquer le code | Réduction appliquée | Réduction appliquée | **PASS** |
| **Limite** | **TC-LIM-06** | Réduction de quantité à 1 | Diminuer la quantité | Panier à 2 articles | Quantité: `1` | 1. Passer à 1 | Total recalculé | Prix inchangé | **FAIL** |
| **Erreur** | **TC-ERR-01** | Connexion mot de passe faux | Rejeter faux identifiants | Compte existant | `alice@example.com` / `FauxPass!` | 1. Connexion | Erreur HTTP 401 | HTTP 500 | **FAIL** |
| **Erreur** | **TC-ERR-02** | Validation panier vide | Bloquer commande 0 article | Panier vide | Aucune | 1. Valider panier vide | Action bloquée | Commande créée | **FAIL** |
| **Erreur** | **TC-ERR-03** | Quantité négative | Rejeter valeurs négatives | Article au panier | Quantité: `-2` | 1. Saisir `-2` | Saisie rejetée | Valeur négative acceptée | **FAIL** |
| **Erreur** | **TC-ERR-04** | API sans clé d'accès | Vérifier sécurité API | Endpoint sécurisé | Clé API absente | 1. Request sans header | HTTP 401 Unauthorized | HTTP 401 | **PASS** |
| **Erreur** | **TC-ERR-05** | Code promo inexistant | Rejeter faux code | Panier non vide | `FAUXCODE` | 1. Appliquer le code | Erreur "Code invalide" | Code appliqué | **FAIL** |
| **Erreur** | **TC-ERR-06** | Inscription email doublon | Vérifier unicité email | Email utilisé | `alice@example.com` | 1. Créer un compte | Erreur "Email utilisé" | Erreur affichée | **PASS** |
| **Règle Métier** | **TC-RGL-01** | Produit hors stock | Bloquer ajout plat épuisé | Plat *Tajine* (stock 0) | Hors stock | 1. Cliquer "Ajouter" | Bouton désactivé | Produit ajouté | **FAIL** |
| **Règle Métier** | **TC-RGL-02** | Suppression article panier | Retirer une ligne | Article au panier | Article unique | 1. Cliquer corbeille | Article retiré | Article reste présent | **FAIL** |
| **Règle Métier** | **TC-RGL-03** | Recalcul dynamique total | Vérifier mise à jour prix | Plat à 12€ | Quantité: 1 -> 3 | 1. Passer à 3 | Total passe à 36€ | Prix bloqué à 12€ | **FAIL** |
| **Règle Métier** | **TC-RGL-04** | Code promo expiré | Bloquer coupons périmés | Code expiré | `EXPIRE2025` | 1. Appliquer le code | Rejet "Code expiré" | Code accepté | **FAIL** |
| **Règle Métier** | **TC-RGL-05** | Rupture pendant commande | Contrôler stock à la fin | Stock à 0 en saisie | Produit au panier | 1. Valider commande | Erreur "Indisponible" | Commande validée | **FAIL** |
| **Règle Métier** | **TC-RGL-06** | Droits d'accès Admin API | Bloquer accès admin | Client connecté | `/api/admin/orders` | 1. Accéder à la route | HTTP 403 Forbidden | HTTP 403 Forbidden | **PASS** |