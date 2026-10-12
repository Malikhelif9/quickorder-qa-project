# Matrice de Risques — QuickOrder QA

Cette matrice évalue les fonctionnalités de l'application selon la probabilité de défaillance (Risque) et leurs conséquences sur l'activité métier (Impact).

| Fonctionnalité / Parcours | Risque (Probabilité) | Impact (Conséquence) | Niveau de criticité |
| :--- | :--- | :--- | :--- |
| **Validation de la commande / Paiement** | Élevé | Critique | **CRITIQUE** (Priorité 1) |
| **Calcul du total du panier** | Élevé | Majeur | **MAJEUR** (Priorité 2) |
| **Gestion des stocks (Ajout d'articles)** | Élevé | Majeur | **MAJEUR** (Priorité 2) |
| **Authentification (Login / Inscription)** | Moyen | Majeur | **MAJEUR** (Priorité 2) |
| **Calcul de la note moyenne des produits** | Moyen | Moyen | **MOYEN** (Priorité 3) |
| **Affichage du catalogue / Recherche** | Faible | Mineur | **FAIBLE** (Priorité 4) |

**Analyse :** Les efforts de qualification et de correction doivent se concentrer en priorité sur la boucle d'achat (panier et commande) afin d'éviter tout préjudice financier ou opérationnel.