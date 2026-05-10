# VéloSahel — Dashboard Ventes, Stocks & Satisfaction Client | Power BI

> **Distribution vélos & accessoires · Afrique de l'Ouest**  
> 3 axes de pilotage · Alertes rupture dynamiques · Star Schema · Démo YouTube 54 min

🇬🇧 [English version available here](README.md)

---

## Problème Business

Une entreprise de distribution de vélos et accessoires opérant en Afrique de l'Ouest
pilotait son activité depuis des fichiers Excel épars — aucune vue consolidée sur les
ventes, les stocks critiques, ni la satisfaction client.

**3 questions sans réponse pour la direction :**

| Axe | Question |
|---|---|
| Ventes | Quelle est la performance par produit, période et client ? |
| Stocks | Quels produits sont en rupture ou en sur-stock critique ? |
| Satisfaction | Comment évolue la note client et quels signaux faibles détecter ? |

**Mission :** Centraliser le pilotage en un outil unique, actualisable et
lisible par le management — avec alertes automatiques sur les ruptures.

---

## Dashboard — 2 Vues

| Vue Direction | Alertes Stock |
|:-:|:-:|
| ![Direction](Direction.png) | ![Alerte Stock](Alerte%20Stock%24.png) |

**Vue Direction :** Performance commerciale par catégorie produit · Tendances CA ·
Top produits · Évolution satisfaction client · KPIs synthétiques direction

**Vue Alertes Stock :** Produits sous seuil critique · Fréquences de
réapprovisionnement recommandées · Alertes dynamiques colorées par niveau de risque

---

## Démonstration Complète

[![Voir sur YouTube](https://img.youtube.com/vi/VAYAVpYkcMg/maxresdefault.jpg)](https://youtu.be/VAYAVpYkcMg)

▶️ **[Démo complète — 54 minutes](https://youtu.be/VAYAVpYkcMg)**

---

## Modèle de Données — Star Schema

```
[Inventaire]     [Avis-Clients]
      └──────────────┘
              │
         [Ventes]          ← Table de faits
              │
        [Calendrier]       ← Table date DAX
```

**3 sources consolidées :** `Ventes.csv` · `Inventaire.csv` · `Avis-Clients.csv`

---

## Mesures DAX Implémentées

| Mesure | Description |
|---|---|
| `CA_Total` | Chiffre d'affaires global et par catégorie produit |
| `Quantité_Vendue` | Volume global, par produit et par période |
| `Note_Moyenne_Satisfaction` | Pondérée par volume de transactions |
| `Taux_Rupture_Stock` | % produits sous le seuil d'alerte défini |
| `Alertes_Conditionnelles` | Indicateurs visuels basés sur seuils métier |

**Logique d'alerte stock :**
```dax
Alerte_Stock =
VAR StockRestant = [Stock_Actuel]
VAR SeuilAlerte  = [Seuil_Reappro]
RETURN
SWITCH(TRUE(),
    StockRestant = 0,              "Rupture critique",
    StockRestant <= SeuilAlerte,   "Réapprovisionnement urgent",
    StockRestant <= SeuilAlerte*2, "Stock à surveiller",
    "Stock OK"
)
```

---

## Recommandations Livrées à la Direction

- Identification des produits en rupture critique avec fréquences de réapprovisionnement calculées
- Classement des catégories par performance CA et tendance (hausse / baisse / stable)
- Signaux faibles satisfaction client — catégories sous le seuil de note acceptable
- Règles métier documentées pour un dashboard maintenable par l'équipe interne

---

## Stack Technique

- **Power BI Desktop** — rapport, visualisations, navigation multi-pages
- **Power Query / M** — nettoyage, transformation, consolidation des 3 sources CSV
- **DAX** — mesures calculées, KPIs, intelligence temporelle
- **Star Schema** — modélisation relationnelle optimisée

---

## Installation

```bash
git clone https://github.com/bouba02/PowerBI-Analyse-Ventes-Stocks-Satisfaction.git
```

Ouvrir `SahelVelo Dashboard.pbix` dans Power BI Desktop.  
Si les sources ne se chargent pas : `Accueil → Transformer les données → Paramètres de la source` → rediriger vers les CSV du dossier cloné.

---

## Structure du Repository

```
VeloSahel/
├── README.md
├── README_FR.md
├── SahelVelo Dashboard.pbix
├── SahelVelo Dashboard.pdf
├── Ventes.csv
├── Inventaire.csv
├── Avis-Clients.csv
├── Direction.png
└── Alerte Stock.png
```

---

## Auteur

**Boubacar Nikiema** — Data Analyst & Consultant BI

Spécialisé en dashboards opérationnels, Sales & Supply Chain analytics et pilotage
de la performance avec Power BI, SQL, Python et Excel. Basé au Maroc, j'interviens
auprès d'entreprises en Afrique et en Europe francophone.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-boubacar--nikiema-blue?logo=linkedin)](https://linkedin.com/in/boubacar-nikiema)
[![YouTube](https://img.shields.io/badge/YouTube-BoubacarDataAnalyst-red?logo=youtube)](https://youtube.com/@BoubacarDataAnalyst)
[![Email](https://img.shields.io/badge/Email-nikiemaboubacar%40gmail.com-gray?logo=gmail)](mailto:nikiemaboubacar@gmail.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-data.ngroupmediadigital.com-green)](https://data.ngroupmediadigital.com)

---

*Données simulées · Code : MIT License*
