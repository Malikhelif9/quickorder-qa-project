# Stratégie de Test — QuickOrder QA (V3.1)

## 1. Contexte et Objectifs
Le présent document définit la stratégie de qualification de l'application **QuickOrder V3.1** (plateforme web et API REST de commande de repas). 
L'objectif est d'évaluer la qualité globale du produit, d'identifier les dysfonctionnements critiques avant la mise en production et de fournir une recommandation formelle de déploiement (Go / No-Go).

## 2. Périmètre de Test

### 2.1 En Périmètre (In-Scope)
- **Interface Web Client (`http://127.0.0.1:5000`)** :
  - Authentification (Connexion, Déconnexion, Inscription).
  - Navigation catalogue, filtres (végétarien, notes) et fiches produits.
  - Gestion du panier (ajout, modification de quantité, suppression, application de code promo).
  - Parcours de commande et validation.
- **API REST Swagger (`http://127.0.0.1:5000/docs/`)** :
  - Endpoints d'authentification (`/api/login`).
  - Endpoints catalogue (`/api/restaurants`, `/api/products`).
  - Endpoints commandes (`/api/orders`, `/api/coupons/validate`).
  - Validation de la clé d'API (`X-API-Key: quickorder-demo-key`).

### 2.2 Hors Périmètre (Out-of-Scope)
- Tests de charge et de montée en charge (Performance / Stress test).
- Tests d'accessibilité .
- Invalidation des cartes bancaires via un véritable PSP (Gateway de paiement tierce).
- Modifications du code source de l'application durant la phase d'audit.

## 3. Parcours Critiques Identifiés
1. **Inscription / Connexion utilisateur** : Accès sécurisé au compte.
2. **Recherche & Sélection de produits** : Contrôle de la disponibilité (gestion des stocks).
3. **Calcul et Gestion du Panier** : Recalcul dynamique du sous-total, application des promotions, suppression d'articles.
4. **Validation de Commande & Paiement** : Contrôle backend des paniers vides, enregistrement de la commande.

## 4. Types de Tests et Approche
- **Tests Fonctionnels UI** : Validation des parcours utilisateurs sur navigateur.
- **Tests API (Intégration & Sécurité)** : Contrôle des codes HTTP, des payloads JSON et de la gestion des erreurs d'authentification (`401`, `403`, `500`).
- **Tests aux Limites & Erreurs** : Saisie de quantités négatives, plafonds de caractères, codes promo expirés.
- **Tests de Règles Métier** : Vérification des contrôles de stock et du recalcul des notes moyennes.

## 5. Environnement & Outillage
- **Environnement** : Local (Python/Flask) — `http://127.0.0.1:5000`
- **Navigateur & Inspection** : Google Chrome, Chrome DevTools (Console, Network, LocalStorage).
- **Test API** : Swagger UI, Postman.
- **Gestion des TU & Bug Tracking** : GitHub (Markdown, Issues/Bug Reports).

## 6. Critères d'Entrée et de Sortie

### Critères d'entrée (Entry Criteria)
- Application QuickOrder V3.1 déployée et accessible localement.
- Base de données de test initialisée avec un jeu de données fonctionnel.
- Clé d'API valide (`quickorder-demo-key`).

### Critères de sortie (Exit Criteria)
- 100 % des 24 cas de test rédigés exécutés.
- Tous les bugs de sévérité **Bloquante** et **Majeure** documentés avec étapes de reproduction et preuves.
- Publication du rapport de synthèse et de la décision Go / No-Go.