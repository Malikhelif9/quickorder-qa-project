# Registre des Bug Reports — QuickOrder V3.1

---

### BUG-001 : Commande possible de produits en rupture de stock
- **Sévérité** : Critical (Bloquant) | **Priorité** : P1
- **Contexte** : Interface Web & API — Fiche Produit / Panier
- **Préconditions** : Produit *Tajine légumes* configuré avec un stock de 0 en BDD.
- **Étapes de reproduction** :
  1. Accéder au catalogue web.
  2. Sélectionner le produit *Tajine légumes* (affiché "Hors stock").
  3. Cliquer sur le bouton "Ajouter au panier".
  4. Ouvrir le panier et cliquer sur "Valider la commande".
- **Résultat attendu** : Le bouton d'ajout doit être désactivé ou l'action bloquée avec une erreur "Produit indisponible".
- **Résultat obtenu** : Le produit est ajouté au panier et la commande est validée en BDD.
- **Preuve** : Capture UI montrant le statut "Hors Stock" + Réponse API `201 Created` sur `/api/orders`.

---

### BUG-002 : Impossibilité de supprimer un article du panier
- **Sévérité** : Major (Majeur) | **Priorité** : P1
- **Contexte** : Interface Web — Page Panier
- **Préconditions** : Avoir au moins un article présent dans le panier.
- **Étapes de reproduction** :
  1. Accéder à la page Panier `/cart`.
  2. Cliquer sur l'icône Corbeille / "Supprimer" sur la ligne d'un article.
- **Résultat attendu** : L'article est retiré de la liste et le total est recalculé.
- **Résultat obtenu** : Aucun événement JS ne se déclenche, l'article reste bloqué dans le panier.
- **Preuve** : Logs DevTools Console (Erreur `Uncaught TypeError: removeItem is not defined`).

---

### BUG-003 : Prix total du panier fixe lors de la modification des quantités
- **Sévérité** : Critical (Bloquant) | **Priorité** : P1
- **Contexte** : Interface Web — Panier
- **Préconditions** : Un article présent au panier (ex: Couscous à 12 €).
- **Étapes de reproduction** :
  1. Aller sur le panier.
  2. Augmenter la quantité de 1 à 3 via le bouton `+` ou le champ numérique.
- **Résultat attendu** : Le sous-total de la ligne et le prix total passent à 36 €.
- **Résultat obtenu** : Le prix total reste bloqué à 12 €.
- **Preuve** : Capture d'écran du panier affichant Quantité = 3 et Total = 12,00 €.

---

### BUG-004 : Création de commandes avec panier vide autorisée via l'API
- **Sévérité** : Critical (Bloquant) | **Priorité** : P2
- **Contexte** : API REST — Endpoint `POST /api/orders`
- **Préconditions** : Clé d'API valide (`X-API-Key: quickorder-demo-key`).
- **Étapes de reproduction** :
  1. Envoyer une requête HTTP `POST /api/orders` avec le body JSON : `{"items": []}`.
- **Résultat attendu** : Code HTTP `400 Bad Request` avec le message "Le panier ne peut pas être vide".
- **Résultat obtenu** : Code HTTP `201 Created` et création d'une commande d'un montant de 0,00 €.
- **Preuve** : Payload de réponse API : `{"order_id": 104, "status": "pending", "total": 0.0}`.

---

### BUG-005 : Absence de contrôle d'expiration sur les codes promo
- **Sévérité** : Major (Majeur) | **Priorité** : P2
- **Contexte** : Interface Web & API — Endpoint `POST /api/coupons/validate`
- **Préconditions** : Un code promo expiré en base (ex: `EXPIRE2025`).
- **Étapes de reproduction** :
  1. Saisir le code `EXPIRE2025` dans le champ "Code promo" du panier.
  2. Appliquer le coupon.
- **Résultat attendu** : Rejet du code avec le message "Ce code promo est expiré".
- **Résultat obtenu** : Réduction appliquée avec succès sur le sous-total.
- **Preuve** : Réponse HTTP `200 OK` indiquant `{"valid": true, "discount": 0.20}`.

---

### BUG-006 : Erreur 500 Internal Error au lieu de 401 Unauthorized sur l'API login
- **Sévérité** : Major (Majeur) | **Priorité** : P2
- **Contexte** : API REST — Endpoint `POST /api/login`
- **Préconditions** : Aucune.
- **Étapes de reproduction** :
  1. Envoyer une requête `POST /api/login` avec un mot de passe erroné.
- **Résultat attendu** : Code HTTP `401 Unauthorized`.
- **Résultat obtenu** : Code HTTP `500 Internal Server Error` (Unhandled Exception backend).
- **Preuve** : Log réseau Swagger / Postman : `HTTP 500 Internal Server Error`.

---

### BUG-007 : Quantités négatives acceptées dans le panier
- **Sévérité** : Major (Majeur) | **Priorité** : P2
- **Contexte** : Interface Web — Panier
- **Préconditions** : Article présent au panier.
- **Étapes de reproduction** :
  1. Modifier manuellement la quantité de l'article en saisissant `-2`.
  2. Valider la modification.
- **Résultat attendu** : Saisie bloquée ou réinitialisée automatiquement à `1`.
- **Résultat obtenu** : La valeur négative est acceptée, entraînant un total négatif ou incohérent.
- **Preuve** : Capture d'écran montrant Quantité = `-2` et Total = `-24,00 €`.

---

### BUG-008 : Absence de page de confirmation claire après validation
- **Sévérité** : Minor (Mineur) | **Priorité** : P3
- **Contexte** : Interface Web — Parcours de commande
- **Préconditions** : Panier valide.
- **Étapes de reproduction** :
  1. Clic sur "Valider la commande".
- **Résultat attendu** : Redirection vers une page de succès avec numéro de commande unique et récapitulatif.
- **Résultat obtenu** : Redirection vers la page d'accueil sans notification visuelle claire.
- **Preuve** : Fil de navigation UI / absence d'URL `/order/success`.

---

### BUG-009 : Note moyenne des produits non mise à jour après l'ajout d'un avis
- **Sévérité** : Minor (Mineur) | **Priorité** : P3
- **Contexte** : Interface Web & BDD — Fiche Produit
- **Préconditions** : Produit avec une note initiale de 4.9 / 5.
- **Étapes de reproduction** :
  1. Publier un avis de 1 étoile sur le produit.
  2. Rafraîchir la page du produit.
- **Résultat attendu** : Recalcul de la moyenne globale en BDD et mise à jour de l'affichage.
- **Résultat obtenu** : L'avis est affiché mais la note moyenne globale reste inchangée à 4.9.
- **Preuve** : Inspection BDD / Fiche produit montrant l'écart entre les avis et la note moyenne.