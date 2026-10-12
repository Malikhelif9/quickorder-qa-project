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

  ## Utilisateur 2
- **Profil** : Utilisateur occasionnel sur mobile.
- **Scénarios exécutés** :
  1. Ajout d'un plat *Tajine légumes* affiché hors stock.
  2. Tentative de suppression d'un article du panier.
  3. Validation de la commande.

### Problèmes observés
1. **Commande de produit épuisé** (Scénario 1) :
   - *Problème* : L'utilisateur a réussi à ajouter au panier et commander le plat malgré la mention "Hors stock".
   - *Verbatim* : « C'est écrit hors stock mais j'ai pu l'ajouter et valider la commande quand même. »
   - *Impact / Fréquence* : Critique (Constaté à chaque essai).

2. **Impossibilité de vider le panier** (Scénario 2) :
   - *Problème* : Le clic sur l'icône de suppression (corbeille) ne déclenche aucune action.
   - *Verbatim* : « Je clique sur supprimer mais le plat reste bloqué dans mon panier. »
   - *Impact / Fréquence* : Majeur (100 % des essais).



## Utilisateur 3
- **Profil** : Nouvel utilisateur / Client ponctuel pressé.
- **Scénarios exécutés** :
  1. Inscription et tentative de création de compte avec un email existant.
  2. Utilisation d'un code promo expiré (`EXPIRE2025`).
  3. Finalisation du paiement et recherche de la confirmation de commande.

### Problèmes observés
1. **Acceptation de coupon expiré** : L'utilisateur a saisi un code obsolète mais la réduction s'est appliquée.
   - *Verbatim* : « J'ai testé un vieux code promo trouvé sur Internet et l'application l'a accepté sans râler. »
   - *Impact / Fréquence* : Majeur (100 % des essais).
2. **Absence de page de confirmation de commande** : Après le clic sur "Valider", l'écran revient à l'accueil sans message explicite.
   - *Verbatim* : « J'ai payé mais je suis retombé direct sur l'accueil, je ne sais même pas si ma commande a été prise en compte ni quel est son numéro. »
   - *Impact / Fréquence* : Moyen (Systématique).


---

## Synthèse et Hypothèses d'Amélioration
- **Priorité 1** : Corriger le recalcul du total du panier et désactiver le bouton d'ajout pour les produits hors stock.
- **Priorité 2** : Rendre la suppression d'un article du panier fonctionnelle et lier le calcul des avis à la BDD.