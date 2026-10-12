# Bilan d'Exécution et Décision Go / No-Go — QuickOrder QA

## 1. Métriques de la campagne

La campagne de tests menée sur la version V3.1 a couvert l'interface Web et l'API REST Swagger.

- **Cas de test exécutés** : 24
- **Succès** : 11
- **Échecs** : 13
- **Bloqués** : 0
- **Ignorés** : 0

## 2. Anomalies critiques identifiées

L'analyse de l'application met en évidence 9 bugs majeurs :
1. **BUG-001** : Commande possible de produits en rupture de stock (*Tajine légumes*).
2. **BUG-002** : Impossibilité de supprimer un article du panier.
3. **BUG-003** : Prix total du panier fixe lors de la modification des quantités.
4. **BUG-004** : Création de commandes avec panier vide autorisée via l'API.
5. **BUG-005** : Absence de contrôle d'expiration sur les codes promo.
6. **BUG-006** : Erreur `500 Internal Error` au lieu de `401 Unauthorized` sur l'API login.
7. **BUG-007** : Quantités négatives acceptées dans le panier.
8. **BUG-008** : Absence de page de confirmation claire après validation.
9. **BUG-009** : Note moyenne des produits non mise à jour après l'ajout d'un avis.

## 3. Recommandation : Déconseillé

**Décision : REFUS DE MISE EN PRODUCTION**

L'application présente des risques majeurs d'erreurs de facturation (prix total fixe, panier vide) et d'incapacité à honorer les commandes (produits hors stock). 

**Prérequis au déblocage du GO :**
- Correction impérative des bugs **BUG-001, BUG-002, BUG-003, BUG-004**.
- Correction du statut HTTP de l'API (**BUG-006**).
- Exécution d'une campagne de non-régression validée à 100 % sur les cas nominaux.