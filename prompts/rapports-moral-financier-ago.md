# Rapports moral et financier d'AGO — Loi 1901

## Métadonnées
- **Catégorie** : gouvernance / rédaction administrative
- **Modèle cible** : GPT-4o | Claude 3.5 Sonnet | Gemini 1.5 Pro
- **Version** : 1.0
- **Auteur** : linguasfra-art
- **Date** : 2026-04-13

## Description
Rédige le rapport moral (présenté par le président) et le rapport financier
(présenté par le trésorier) destinés à l'assemblée générale ordinaire (AGO)
annuelle d'une association loi 1901. Les deux rapports sont soumis au vote
des membres pour approbation, avec délivrance d'un quitus au trésorier.

Le prompt intègre le cadre légal applicable, les distinctions entre obligations
selon la taille de l'association, la structure attendue par les financeurs publics
(subventions > 153 000 €) et les bonnes pratiques associatives.

## Cadre légal de référence

| Texte | Objet |
|---|---|
| Loi du 1er juillet 1901, art. 1 | Liberté contractuelle — statuts définissent les obligations de rapport |
| Loi du 1er juillet 1901, art. 5 | Déclaration préfecture si changement de dirigeants lors de l'AGO |
| Code de commerce, art. L612-4 | Rapport de gestion obligatoire si dépassement de 2 des 3 seuils |
| Décret du 16 août 1901 | Application de la loi 1901 |

### Obligations selon la taille de l'association

| Situation | Rapport moral | Rapport financier / comptes |
|---|---|---|
| Association standard (statuts silencieux) | Recommandé, non obligatoire légalement | Comptabilité simplifiée suffisante |
| Statuts ou règlement intérieur le prévoient | **Obligatoire** — responsabilité du président engagée | Selon statuts |
| Subventions publiques > 153 000 € / an | Fortement recommandé | **Comptes annuels obligatoires** (bilan + compte de résultat + annexe) + dépôt préfecture |
| 2 des 3 seuils dépassés (bilan > 1,55 M€ / CA > 3,1 M€ / > 50 salariés) | Obligatoire (rapport de gestion) | **Comptabilité commerciale obligatoire** + rapport commissaire aux comptes + dépôt greffe tribunal |

### Ce que comprend le rapport financier
- Compte de résultat (produits / charges → excédent ou déficit)
- Bilan simplifié (actif / passif au 31 décembre)
- Situation de trésorerie au jour de l'AGO
- Budget prévisionnel de l'exercice suivant
- Nature et provenance des fonds (cotisations, subventions, dons, prestations)
- Explication des dettes en cas de déficit et mesures correctives
- Vote d'approbation + **quitus** au trésorier

## Paramètres du modèle

| Paramètre          | Valeur recommandée | Plage acceptable | Notes |
|--------------------|--------------------|-----------------|-------|
| temperature        | 0.4                | 0.2 – 0.6       | Équilibre précision et registre institutionnel fluide |
| max_tokens         | 3000               | 1500 – 6000     | Selon richesse des données fournies |
| top_p              | 0.95               | 0.9 – 1.0       | |
| frequency_penalty  | 0.2                | 0.0 – 0.4       | Éviter répétitions stylistiques |
| presence_penalty   | 0.1                | 0.0 – 0.3       | Encourager diversité des formulations |

---

## Prompt système

```
Tu es un expert en gouvernance associative et rédaction de documents officiels
pour les associations loi 1901. Tu rédiges des rapports moraux et financiers
destinés à être présentés lors de l'assemblée générale ordinaire annuelle,
soumis au vote des membres et archivés dans les registres de l'association.

Cadre que tu appliques systématiquement :
- Rapport moral : présenté par le/la président(e), il rend compte des activités,
  de la gestion et des orientations de l'association pour l'exercice concerné.
  Structure attendue : rappel de l'objet et des valeurs, bilan des activités,
  difficultés rencontrées, partenariats, perspectives et remerciements.
- Rapport financier : présenté par le/la trésorier(ère), il expose les résultats
  financiers de l'exercice clos, la situation de trésorerie et le budget prévisionnel.
  Il se conclut par la demande de quitus.
- Ton : institutionnel, transparent, accessible aux membres non-spécialistes.
  Précis sur les chiffres, positif sur les réalisations, lucide sur les difficultés.
- Tu signales en fin de document les éventuelles obligations légales (dépôt préfecture,
  dépôt greffe, intervention commissaire aux comptes) selon les données fournies.
- Si les données financières sont insuffisantes pour un rapport complet, tu produis
  un rapport structuré avec des indications sur ce que l'auteur devra compléter,
  signalées par [À COMPLÉTER : ...].
```

---

## Prompt utilisateur — Rapport moral

```
Rédige le rapport moral pour l'AGO de l'association suivante.

**Nom de l'association** : {{nom_association}}
**Exercice concerné** : {{exercice}}
**Présenté par** : {{presentateur_moral}}
**Objet statutaire** : {{objet_statutaire}}
**Valeurs de l'association** : {{valeurs}}
**Bilan des activités** : {{bilan_activites}}
**Activités non abouties / difficultés** : {{difficultes}}
**Partenaires publics et privés** : {{partenaires}}
**Évolutions internes** : {{evolutions_internes}}
**Perspectives pour {{exercice_suivant}}** : {{perspectives}}
**Remerciements** : {{remerciements}}
**Nombre de membres** : {{nb_membres}}
**Niveau de langue** : {{niveau_langue}}
{{instructions_supplementaires}}

Fournis :
1. Le rapport moral complet, prêt à lire en séance
2. Un encadré synthétique « Points clés à retenir » (3-5 bullet points)
3. La résolution à soumettre au vote (approbation du rapport moral)
```

---

## Prompt utilisateur — Rapport financier

```
Rédige le rapport financier pour l'AGO de l'association suivante.

**Nom de l'association** : {{nom_association}}
**Exercice concerné** : {{exercice}}
**Présenté par** : {{presentateur_financier}}
**Budget de l'exercice {{exercice}}** : {{budget}}
**Recettes réelles** : {{recettes_reelles}}
**Dépenses réelles** : {{depenses_reelles}}
**Résultat de l'exercice** : {{resultat_exercice}}
**Situation de trésorerie au jour de l'AGO** : {{tresorerie_actuelle}}
**Réserves et fonds associatif** : {{reserves}}
**Subventions perçues** : {{subventions}}
**Budget prévisionnel {{exercice_suivant}}** : {{budget_previsionnel}}
**Observations particulières** : {{observations_financieres}}
**Commissaire aux comptes** : {{commissaire_comptes}}
{{instructions_supplementaires}}

Fournis :
1. Le rapport financier complet avec tableau de synthèse recettes / dépenses
2. Le budget prévisionnel présenté de façon claire
3. La résolution d'approbation des comptes à soumettre au vote
4. La résolution de quitus au/à la trésorier(ère) à soumettre au vote
5. Une note sur les éventuelles obligations légales (dépôt, commissaire aux comptes)
   selon les données fournies
```

---

## Variables

| Variable | Type | Obligatoire | Prompt | Description | Exemple |
|---|---|---|---|---|---|
| `{{exercice}}` | string | Oui | Les deux | Année ou période de l'exercice clôturé | "2025" / "exercice 2025 (01/01 – 31/12/2025)" |
| `{{bilan_activites}}` | string | Oui | Moral | Résumé des activités réalisées durant l'exercice | "3 webinaires de formation (72 participants au total), refonte du site web, participation au congrès ETI de Lyon, 2 réunions régionales" |
| `{{budget}}` | string | Oui | Financier | Budget initial voté lors de la précédente AGO | "Recettes prévues : 18 500 € — Dépenses prévues : 17 800 €" |
| `{{nom_association}}` | string | Oui | Les deux | Dénomination officielle | "UNETICA" |
| `{{presentateur_moral}}` | string | Oui | Moral | Nom, prénom et qualité du présentateur | "M. [Prénom Nom], Président" |
| `{{presentateur_financier}}` | string | Oui | Financier | Nom, prénom et qualité du présentateur | "Mme [Prénom Nom], Trésorière" |
| `{{objet_statutaire}}` | string | Non | Moral | Objet de l'association tel que défini dans les statuts | "Défense du titre et du rôle des experts traducteurs-interprètes judiciaires, formation, déontologie" |
| `{{valeurs}}` | string | Non | Moral | Valeurs fondatrices de l'association | "Qualité, déontologie, service public de la justice, confraternité" |
| `{{difficultes}}` | string | Non | Moral | Activités non abouties et difficultés rencontrées | "Retard dans la refonte du règlement intérieur — reportée à 2026" |
| `{{partenaires}}` | string | Non | Moral | Partenaires publics et privés actifs sur l'exercice | "Ministère de la Justice (DACG), EULITA, cours d'appel de Toulouse et Bordeaux" |
| `{{evolutions_internes}}` | string | Non | Moral | Changements de gouvernance, effectifs, statuts… | "Renouvellement de 2 postes au CA, adoption d'une charte déontologique" |
| `{{perspectives}}` | string | Non | Moral | Projets et orientations pour l'exercice suivant | "Lancement d'une plateforme de formation en ligne, négociation tarifaire avec le ministère" |
| `{{remerciements}}` | string | Non | Moral | Membres, bénévoles, partenaires à remercier | "Membres du bureau, bénévoles de la commission formation, partenaires institutionnels" |
| `{{nb_membres}}` | string | Non | Moral | Nombre d'adhérents à jour de cotisation | "87 membres actifs au 31/12/2025" |
| `{{niveau_langue}}` | string | Non | Moral | Registre et niveau de langue | "formel institutionnel accessible" |
| `{{recettes_reelles}}` | string | Oui | Financier | Recettes effectivement encaissées (ventilées si possible) | "Cotisations : 12 400 € — Subvention région : 3 000 € — Formations : 2 800 €" |
| `{{depenses_reelles}}` | string | Oui | Financier | Dépenses effectivement réglées (ventilées si possible) | "Fonctionnement : 4 200 € — Formations : 3 500 € — Communication : 1 800 € — Frais de siège : 2 100 €" |
| `{{resultat_exercice}}` | string | Oui | Financier | Excédent ou déficit de l'exercice | "Excédent : 6 600 €" / "Déficit : -1 200 €" |
| `{{tresorerie_actuelle}}` | string | Non | Financier | Solde bancaire au jour de l'AGO | "14 200 € au 31/12/2025 — 15 800 € au jour de l'AGO (15/06/2026)" |
| `{{reserves}}` | string | Non | Financier | Fonds associatif et réserves accumulées | "Fonds associatif : 8 000 € — Réserves : 6 200 €" |
| `{{subventions}}` | string | Non | Financier | Détail des subventions publiques perçues | "Région Occitanie : 3 000 € — Aucune subvention > 153 000 €" |
| `{{budget_previsionnel}}` | string | Non | Financier | Budget prévisionnel pour l'exercice suivant | "Recettes prévues 2026 : 20 000 € — Dépenses prévues : 18 500 €" |
| `{{observations_financieres}}` | string | Non | Financier | Points d'attention, écarts budget/réel, dettes | "Hausse des frais de communication (+38 %) liée au lancement du nouveau site" |
| `{{commissaire_comptes}}` | string | Non | Financier | Nom du commissaire aux comptes si existant | "Néant — seuils non atteints" / "Cabinet Dupont & Associés, rapport joint" |
| `{{exercice_suivant}}` | string | Non | Les deux | Exercice à venir | "2026" |
| `{{instructions_supplementaires}}` | string | Non | Les deux | Consignes libres additionnelles | "- Mentionner le vote de la cotisation 2026 fixée à 120 €\n- Ajouter une mention sur la campagne de recrutement de membres" |

---

## Exemples de test

### Exemple 1 — Rapport moral UNETICA 2025 (exercice excédentaire)

**Variables utilisées :**
- `{{exercice}}` = "2025"
- `{{nom_association}}` = "UNETICA — Union nationale des experts traducteurs-interprètes près les cours d'appel"
- `{{presentateur_moral}}` = "M. [Prénom Nom], Président de l'UNETICA"
- `{{objet_statutaire}}` = "Défense du titre et du rôle des experts traducteurs-interprètes judiciaires, formation continue, déontologie, information des justiciables"
- `{{valeurs}}` = "Qualité de la justice, déontologie, service public, confraternité entre ETI, ouverture européenne"
- `{{bilan_activites}}` = "3 webinaires de formation (72 participants) ; révision et adoption d'une charte déontologique ; participation au congrès EULITA (Bruxelles) ; 2 réunions régionales (Toulouse, Lyon) ; refonte du site web ; courrier collectif au ministère de la Justice sur la revalorisation des tarifs ETI (CPP art. R.122)"
- `{{difficultes}}` = "Refonte du règlement intérieur reportée à 2026 (manque de disponibilité du groupe de travail) ; réponse toujours attendue du ministère sur le courrier tarifaire"
- `{{partenaires}}` = "Ministère de la Justice (DACG), EULITA, cours d'appel de Toulouse, Bordeaux et Lyon, CIPAV"
- `{{evolutions_internes}}` = "Renouvellement de 2 postes au CA lors de l'AGO 2025 ; nomination d'un référent déontologie"
- `{{nb_membres}}` = "87 membres actifs au 31/12/2025 (+9 % par rapport à 2024)"
- `{{perspectives}}` = "Relance de la négociation tarifaire avec le ministère ; lancement d'un module de formation en ligne ; préparation de la réforme du règlement intérieur ; développement des sections locales"
- `{{remerciements}}` = "Membres du bureau, groupe de travail formation (Marie M., Jean D., Sophie L.), adhérents actifs en régions, EULITA pour l'invitation au congrès"
- `{{niveau_langue}}` = "formel institutionnel, accessible à des ETI non spécialistes de la gouvernance"

**Résultat attendu :**
> Rapport structuré en 6-7 parties (objet/valeurs, bilan activités, partenariats,
> vie interne, perspectives, remerciements), ton présidentiel mesuré, encadré
> « Points clés », résolution d'approbation prête à soumettre au vote.

---

### Exemple 2 — Rapport financier UNETICA 2025 (exercice excédentaire)

**Variables utilisées :**
- `{{exercice}}` = "2025"
- `{{nom_association}}` = "UNETICA"
- `{{presentateur_financier}}` = "Mme [Prénom Nom], Trésorière de l'UNETICA"
- `{{budget}}` = "Recettes budgétées : 18 500 € — Dépenses budgétées : 17 800 € — Excédent prévu : 700 €"
- `{{recettes_reelles}}` = "Cotisations membres : 12 400 € — Subvention Région Occitanie : 3 000 € — Formations (inscriptions) : 2 800 € — Divers : 200 € — Total : 18 400 €"
- `{{depenses_reelles}}` = "Fonctionnement bureau : 4 200 € — Organisation formations : 3 500 € — Communication et site web : 2 500 € — Frais de siège et assurance : 2 100 € — Congrès EULITA : 800 € — Divers : 300 € — Total : 13 400 €"
- `{{resultat_exercice}}` = "Excédent : 5 000 €"
- `{{tresorerie_actuelle}}` = "14 200 € au 31/12/2025"
- `{{reserves}}` = "Fonds associatif : 8 000 € — Réserves antérieures : 1 200 € — Report à nouveau 2025 : 5 000 €"
- `{{subventions}}` = "Région Occitanie : 3 000 € — Aucune subvention dépassant le seuil de 153 000 €"
- `{{budget_previsionnel}}` = "Recettes 2026 : 20 500 € (hausse cotisations votée à 120 €, nouvelles formations) — Dépenses 2026 : 18 800 € (règlement intérieur, module e-learning) — Excédent prévisionnel : 1 700 €"
- `{{observations_financieres}}` = "Hausse des dépenses communication (+38 % vs budget) liée au lancement du nouveau site — compensée par une hausse des inscriptions aux formations (+12 %)"
- `{{commissaire_comptes}}` = "Néant — seuils légaux non atteints (art. L612-4 C. com.)"

**Résultat attendu :**
> Rapport financier avec tableau synthétique budget/réel, analyse des écarts,
> présentation claire de la trésorerie, budget prévisionnel 2026 commenté,
> résolution d'approbation des comptes, résolution de quitus à la trésorière,
> note confirmant l'absence d'obligation de dépôt au greffe et d'intervention
> de commissaire aux comptes pour cet exercice.

---

### Exemple 3 — Rapport financier en situation de déficit avec plan de redressement

**Variables utilisées :**
- `{{exercice}}` = "2025"
- `{{resultat_exercice}}` = "Déficit : -2 200 €"
- `{{tresorerie_actuelle}}` = "3 100 € au 31/12/2025 (en baisse de 2 200 € vs N-1)"
- `{{observations_financieres}}` = "Déficit lié à l'annulation tardive d'une subvention régionale attendue (4 000 €) et à des frais de déplacement sous-estimés. Plan de redressement proposé : suspension temporaire de 2 postes de dépenses non essentiels, campagne de recrutement ciblée pour augmenter les cotisations de 15 %"
- `{{budget_previsionnel}}` = "Recettes 2026 : 17 000 € — Dépenses 2026 : 15 500 € — Retour à l'équilibre prévu au S2 2026"

**Résultat attendu :**
> Rapport transparent sur la situation déficitaire, explication factuelle des
> causes, présentation du plan de redressement, budget prévisionnel 2026 avec
> retour à l'équilibre, ton rassurant mais lucide, résolutions adaptées à la
> situation (approbation des comptes + quitus malgré déficit + adoption du
> plan de redressement).
