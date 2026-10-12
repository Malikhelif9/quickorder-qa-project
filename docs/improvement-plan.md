# Plan d'Amélioration — QuickOrder V3.1

Ce document détaille 6 propositions d'amélioration priorisées pour sécuriser la mise en production.

| N° | Amélioration proposée | Justification / Impact | Priorité |
| :--- | :--- | :--- | :--- |
| **1** | **Contrôle strict des stocks au Panier et à l'API** | Empêcher d'ajouter ou de commander des plats dont la quantité en BDD est à 0. | **P1 - Critique** |
| **2** | **Correction du JS du Panier (Prix & Suppression)** | Permettre la mise à jour dynamique du sous-total selon la quantité et rendre la suppression d'article fonctionnelle. | **P1 - Critique** |
| **3** | **Validation backend des commandes (`/api/orders`)** | Bloquer la création de commandes avec un panier vide (retourner une erreur HTTP 400). | **P2 - Majeur** |
| **4** | **Gestion conforme des d'erreurs API (`/api/login`)** | Retourner un code `401 Unauthorized` au lieu d'un `500 Internal Error` lors d'un mauvais mot de passe. | **P2 - Majeur** |
| **5** | **Recalcul dynamique de la note moyenne des plats** | Mettre à jour la moyenne globale d'un produit en base de données dès qu'un nouvel avis est validé. | **P3 - Moyen** |
| **6** | **Confirmation visuelle de commande** | Ajouter une page de succès affichant le récapitulatif et le numéro de commande unique après validation. | **P3 - Moyen** |