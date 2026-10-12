# Audit Qualité & Tests — QuickOrder V3.1

Ce dépôt contient l'audit de qualité logicielle, la stratégie de test, le cahier de recette, ainsi que les rapports d'anomalies réalisés sur l'application **QuickOrder V3.1** dans le cadre du projet académique *Tests et qualité des solutions numériques*.

> **Consultation du projet** :
> Veuillez basculer sur la branche **`deposit`** pour consulter l'ensemble du travail d'audit et les livrables réalisés. La branche **`master`** a été utilisée uniquement pour le développement initial de l'application.

---

## Synthèse de l'Audit QA

- **Statut de la campagne** : 24 cas de test exécutés (11 PASS / 13 FAIL).
- **Décision - Non validé** : Refus de mise en production en raison de dysfonctionnements bloquants sur le panier, la gestion des stocks et la facturation.
- **Anomalies identifiées** : 9 bugs majeurs/critiques répertoriés et documentés.

---

## Livrables de l'Audit (`docs/`)

Tous les documents d'audit et de qualification sont centralisés dans le dossier `docs/` :

- **`docs/test-strategy.md`** : Stratégie de test, périmètre (UI/API), parcours critiques et critères de sortie.
- **`docs/risk-matrix.md`** : Matrice des risques fonctionnels et techniques priorisée.
- **`docs/test-cases.xlsx`** : Cahier de recette (24 cas de test : nominaux, limites, erreurs et règles métier).
- **`docs/execution-report.md`** : Bilan d'exécution de la campagne et justification de la décision Go/No-Go.
- **`docs/bug-reports/`** : Fiches d'anomalies détaillées et reproductibles (BUG-001 à BUG-009).
- **`docs/user-feedback.md`** : Synthèse des tests utilisateurs (3 profils, verbatims et métriques d'impact).
- **`docs/improvement-plan.md`** : Plan de 6 améliorations priorisées pour débloquer la mise en production.

---

## Présentation & Lancement de QuickOrder

QuickOrder est une application web de commande de repas développée avec **Python, Flask, Flask-SQLAlchemy et SQLite**.

### Comptes de démonstration

| Rôle | Email | Mot de passe |
|---|---|---|
| Client | `alice@example.com` | `Password123!` |
| Client | `bob@example.com` | `Password123!` |
| Admin | `admin@quickorder.local` | `Admin123!` |

### Démarrage rapide

#### Option A — Python + environnement virtuel

**Windows PowerShell :**
```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python seed.py
python run.py