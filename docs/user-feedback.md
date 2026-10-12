# Retours Utilisateurs (User Feedback) — QuickOrder QA

## Utilisateur 1
- **Profil** : Client régulier d'applications de livraison de repas.
- **Scénarios exécutés** :
  1. Recherche d'un plat végétarien et ajout au panier.
  2. Modification de la quantité dans le panier.
  3. Tentative d'ajout d'un avis sur un plat.

### Problèmes observés
1. **Prix total fixe** : L'utilisateur a augmenté la quantité à 3, mais le prix est resté celui d'un seul plat.
   - *Verbatim* : « Je comprends pas, j'en prends 3 mais le prix ne change pas, c'est gratuit ou c'est un bug ? »
   - *Impact / Fréquence* : Bloquant (100 % des essais).
2. **Avis non mis à jour** : L'utilisateur a mis 1 étoile à un plat, mais la note globale est restée à 4.9.
   - *Verbatim* : « J'ai mis une mauvaise note mais la moyenne ne bouge pas du tout. »
   - *Impact / Fréquence* : Majeur (Fréquent).

---

## Utilisateur 2
- **Profil** : Utilisateur occasionnel sur mobile.
- **Scénarios exécutés** :
  1. Ajout d'un plat *Tajine légumes* affiché hors stock.
  2. Tentative de suppression d'un article du panier.
  3. Validation de commande.

### Problèmes observés
1. **Commande de produit épuisé** : L'utilisateur a réussi à ajouter et commander le *Tajine légumes*.
   - *Verbatim* : « C'est écrit hors stock mais j'ai pu l'ajouter et valider la commande quand même. »
   - *Impact / Fréquence* : Critique (Constaté à chaque essai).
2. **Impossibilité de vider le panier** : Clic sur la corbeille sans effet.
   - *Verbatim* : « Je clique sur supprimer mais le plat reste bloqué dans mon panier. »
   - *Impact / Fréquence* : Majeur (100 % des essais).

---

## Synthèse et Hypothèses d'Amélioration
- **Priorité 1** : Corriger le recalcul du total du panier et désactiver le bouton d'ajout pour les produits hors stock.
- **Priorité 2** : Rendre la suppression d'un article du panier fonctionnelle et lier le calcul des avis à la BDD.