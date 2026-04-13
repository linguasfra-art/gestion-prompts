# PV et convocations de réunions — Loi 1901

## Métadonnées
- **Catégorie** : gouvernance / rédaction administrative
- **Modèle cible** : GPT-4o | Claude 3.5 Sonnet | Gemini 1.5 Pro
- **Version** : 1.0
- **Auteur** : linguasfra-art
- **Date** : 2026-04-13

## Description
Rédige des convocations et des procès-verbaux (PV) conformes à la loi du 1er
juillet 1901 pour les différentes instances d'une association : conseil
d'administration (CA), assemblée générale ordinaire (AGO), assemblée générale
extraordinaire (AGE), groupes de travail et sections locales.

Le prompt tient compte des exigences légales et jurisprudentielles (délai minimal
de convocation de 15 jours, mentions obligatoires du PV, vérification et mention
du quorum, obligations de publicité à la préfecture pour certains actes), ainsi
que des bonnes pratiques rédactionnelles associatives.

## Cadre légal de référence

| Texte | Objet |
|-------|-------|
| Loi du 1er juillet 1901 | Régime général des associations |
| Décret du 16 août 1901 | Application de la loi 1901 |
| Jurisprudence constante | Délai minimum de convocation : **15 jours** |
| Loi 1901, art. 5 | Obligation de déclaration en préfecture des modifications statutaires, changements de dirigeants, transfert de siège |

### Règles clés à intégrer dans chaque document

**Convocation :**
- Délai minimum : **15 jours** avant la date de réunion (jurisprudence ; les
  statuts peuvent prévoir un délai plus long, généralement jusqu'à 1 mois)
- Délai calculé à partir de la **date d'envoi** (non de réception)
- Non-respect du délai → risque d'**annulation des délibérations** par le tribunal
- Mentions obligatoires : dénomination et siège de l'association, type de réunion,
  date/heure/lieu, ordre du jour complet, pièces annexes, nom et qualité du signataire

**Procès-verbal :**
- Obligation légale uniquement si les statuts ou le règlement intérieur le prévoient ;
  fortement recommandé dans tous les cas (bonne pratique de gestion)
- Mentions à inclure : dénomination et siège, date/heure/lieu, type de réunion,
  identité du président et du secrétaire de séance, mode de convocation et date
  d'envoi, liste des membres présents et représentés (avec qualité), vérification
  du quorum, ordre du jour, résumé des débats par point, résolutions votées avec
  résultats détaillés (pour / contre / abstentions), heure de clôture, signatures
- PV signé par le **président** et le **secrétaire** de séance (au minimum)
- Rédiger sans blanc, ni rature, sur feuillets numérotés ou registre dédié

**Quorum :**
- Non obligatoire par la loi 1901 — défini par les **statuts ou le règlement intérieur**
- Modes courants : 1/10, 1/4, 1/3, 1/2 ou majorité absolue des membres
- Calcul : membres présents seuls, ou présents + représentés par procuration
  (si les statuts le prévoient)
- Si quorum non atteint : **ajournement** et convocation d'une nouvelle réunion
  (délai de 15 jours minimum)

**Publicité en préfecture (obligatoire) :**
- Modification du nom ou de l'objet de l'association
- Transfert du siège social
- Modification des statuts
- Changement de dirigeants
- Transfert de propriété d'un bien immobilier

## Paramètres du modèle

| Paramètre          | Valeur recommandée | Plage acceptable | Notes                                         |
|--------------------|--------------------|-----------------|-----------------------------------------------|
| temperature        | 0.2                | 0.1 – 0.4       | Documents formels : précision maximale        |
| max_tokens         | 2048               | 1024 – 4096     | Ajuster selon longueur de l'ordre du jour     |
| top_p              | 0.95               | 0.9 – 1.0       |                                               |
| frequency_penalty  | 0.1                | 0.0 – 0.3       | Éviter les répétitions de formules            |

---

## Prompt système

```
Tu es un juriste spécialisé en droit des associations loi 1901, expert en rédaction
de documents de gouvernance associative : convocations, procès-verbaux (PV),
comptes rendus de réunion. Tu produis des documents formels, directement
exploitables, conformes à la loi du 1er juillet 1901, au décret du 16 août 1901
et à la jurisprudence applicable.

Cadre légal que tu maîtrises et appliques systématiquement :
- Délai minimal de convocation : 15 jours avant la date de réunion (calculé à
  partir de la date d'envoi).
- Mentions obligatoires des convocations et PV (cf. jurisprudence et bonnes
  pratiques associatives).
- Quorum : non imposé par la loi 1901, mais tu vérifies sa mention et sa
  conformité si des règles statutaires sont indiquées.
- Obligations de publicité en préfecture pour les actes modificatifs (statuts,
  dirigeants, siège).

Pour chaque document produit, tu :
- Appliques scrupuleusement les mentions légales et les bonnes pratiques.
- Adaptes le registre au type d'instance (CA, AGO, AGE, groupe de travail,
  section locale).
- Signales en fin de document les éventuelles obligations déclaratives en
  préfecture si les décisions prises le nécessitent.
- Fournis une note de vigilance si un élément fourni présente un risque juridique
  (délai trop court, quorum non précisé dans les statuts, ordre du jour incomplet).
```

---

## Prompt utilisateur — Convocation

```
Rédige une convocation pour la réunion suivante.

**Type de réunion** : {{type_reunion}}
**Nom de l'association** : {{nom_association}}
**Siège social** : {{siege_social}}
**Date, heure et lieu de la réunion** : {{date_heure_lieu}}
**Date d'envoi prévue** : {{date_envoi}}
**Ordre du jour** : {{ordre_du_jour}}
**Quorum requis** : {{quorum}}
**Mode de convocation** : {{mode_convocation}}
**Pièces jointes à la convocation** : {{pieces_jointes}}
**Signataire** : {{signataire}}
{{instructions_supplementaires}}

Fournis :
1. La convocation complète, prête à envoyer
2. Une note de vigilance si le délai de convocation est inférieur à 15 jours
   ou si l'ordre du jour est susceptible d'entraîner une déclaration en préfecture
```

---

## Prompt utilisateur — Procès-verbal

```
Rédige le procès-verbal de la réunion suivante.

**Type de réunion** : {{type_reunion}}
**Nom de l'association** : {{nom_association}}
**Siège social** : {{siege_social}}
**Date, heure et lieu** : {{date_heure_lieu}}
**Président de séance** : {{president_seance}}
**Secrétaire de séance** : {{secretaire_seance}}
**Mode et date de convocation** : {{mode_convocation_date}}
**Membres présents** : {{membres_presents}}
**Membres représentés** : {{membres_representes}}
**Membres absents excusés** : {{membres_absents}}
**Quorum requis et constaté** : {{quorum}}
**Ordre du jour** : {{ordre_du_jour}}
**Résumé des débats et décisions par point** : {{debats_decisions}}
**Heure de clôture** : {{heure_cloture}}
**Signataires** : {{signataires}}
{{instructions_supplementaires}}

Fournis :
1. Le procès-verbal complet, formaté, prêt à signer
2. Un rappel des résolutions adoptées (liste récapitulative)
3. Une note sur les éventuelles obligations déclaratives en préfecture
```

---

## Variables

| Variable                  | Type    | Obligatoire | Utilisation          | Description                                                    | Exemple |
|---------------------------|---------|-------------|----------------------|----------------------------------------------------------------|---------|
| `{{type_reunion}}`        | string  | Oui         | Convocation + PV     | Type d'instance et nature de la réunion                        | "Conseil d'administration — réunion ordinaire" / "Assemblée générale ordinaire" / "Assemblée générale extraordinaire" / "Groupe de travail Formation" / "Section locale Occitanie" |
| `{{nom_association}}`     | string  | Oui         | Convocation + PV     | Dénomination officielle de l'association                       | "UNETICA — Union nationale des experts traducteurs-interprètes près les cours d'appel" |
| `{{siege_social}}`        | string  | Oui         | Convocation + PV     | Adresse complète du siège social                               | "12 rue des Fleurs, 75001 Paris" |
| `{{date_heure_lieu}}`     | string  | Oui         | Convocation + PV     | Date, heure et lieu précis de la réunion                       | "Lundi 20 avril 2026 à 18h00 — salle B, Maison des Associations, Toulouse / ou en visioconférence Zoom [lien]" |
| `{{ordre_du_jour}}`       | string  | Oui         | Convocation + PV     | Liste numérotée des points à l'ordre du jour                   | "1. Approbation du PV de la dernière réunion\n2. Bilan financier T1 2026\n3. Préparation de l'AG annuelle\n4. Questions diverses" |
| `{{quorum}}`              | string  | Oui         | Convocation + PV     | Règle de quorum applicable et résultat constaté (pour le PV)  | "Quorum statutaire : 1/2 des membres — 8 membres présents ou représentés sur 14 → quorum atteint" / "Aucun quorum prévu aux statuts" |
| `{{date_envoi}}`          | string  | Conditionnel| Convocation          | Date d'envoi prévue de la convocation                         | "3 avril 2026" |
| `{{mode_convocation}}`    | string  | Non         | Convocation          | Mode d'envoi de la convocation                                 | "courrier électronique avec accusé de réception" / "lettre recommandée AR" |
| `{{pieces_jointes}}`      | string  | Non         | Convocation          | Documents annexés à la convocation                             | "Rapport moral, rapport financier, projet de budget 2026" |
| `{{signataire}}`          | string  | Oui         | Convocation          | Nom, prénom et qualité du signataire                           | "M. Jean Dupont, Président de l'UNETICA" |
| `{{president_seance}}`    | string  | Conditionnel| PV                   | Identité du président de séance                                | "M. Jean Dupont, Président" |
| `{{secretaire_seance}}`   | string  | Conditionnel| PV                   | Identité du secrétaire de séance                               | "Mme Marie Martin, Secrétaire générale" |
| `{{mode_convocation_date}}`| string | Conditionnel| PV                   | Mode de convocation et date d'envoi (pour mention dans le PV) | "Convocation par email du 3 avril 2026 (délai : 17 jours)" |
| `{{membres_presents}}`    | string  | Conditionnel| PV                   | Liste des membres présents avec qualité                        | "Jean Dupont (Président), Marie Martin (Secrétaire générale), Paul Durand (Trésorier)…" |
| `{{membres_representes}}` | string  | Non         | PV                   | Membres absents représentés par procuration                    | "Sophie Lefèvre (membre), représentée par Jean Dupont (pouvoir annexé)" |
| `{{membres_absents}}`     | string  | Non         | PV                   | Membres absents excusés                                        | "Pierre Bernard (excusé)" |
| `{{debats_decisions}}`    | string  | Conditionnel| PV                   | Résumé des échanges et décisions par point de l'ordre du jour  | "Point 1 : Le PV de la réunion du 10 mars est approuvé à l'unanimité. Point 2 : Le trésorier présente un bilan excédentaire…" |
| `{{heure_cloture}}`       | string  | Conditionnel| PV                   | Heure de fin de séance                                         | "20h45" |
| `{{signataires}}`         | string  | Conditionnel| PV                   | Nom, prénom et qualité des signataires du PV                   | "Le Président, Jean Dupont / La Secrétaire de séance, Marie Martin" |
| `{{instructions_supplementaires}}` | string | Non | Convocation + PV    | Consignes libres additionnelles                                | "- Mentionner la possibilité de vote par procuration\n- Ajouter les modalités de connexion Zoom" |

---

## Types de réunions couverts

| Type de réunion          | Particularités rédactionnelles |
|--------------------------|-------------------------------|
| **Conseil d'administration (CA)** | Ordre du jour fixé par le bureau ; PV signé par le président et le secrétaire ; pas d'obligation de publicité préfectorale sauf changement de dirigeants |
| **Assemblée générale ordinaire (AGO)** | Délai de convocation ≥ 15 jours ; quorum statutaire vérifié ; PV récapitulatif des votes ; publicité préfectorale si changement de dirigeants |
| **Assemblée générale extraordinaire (AGE)** | Même délai minimum 15 jours ; requiert souvent un quorum renforcé et une majorité qualifiée ; obligatoirement déposé en préfecture si modification statutaire ou dissolution |
| **Groupe de travail** | Réunion interne, moins formelle ; PV allégé (compte rendu) ; pas d'obligation de quorum ni de publicité |
| **Section locale** | Fonctionnement calé sur les statuts nationaux ou le règlement intérieur ; PV transmis au siège pour archivage |

---

## Exemples de test

### Exemple 1 — Convocation CA ordinaire (UNETICA)
**Variables utilisées :**
- `{{type_reunion}}` = "Conseil d'administration — réunion ordinaire"
- `{{nom_association}}` = "UNETICA — Union nationale des experts traducteurs-interprètes près les cours d'appel"
- `{{siege_social}}` = "[adresse du siège UNETICA]"
- `{{date_heure_lieu}}` = "Lundi 4 mai 2026 à 18h00 — en visioconférence Zoom (lien transmis séparément)"
- `{{date_envoi}}` = "15 avril 2026 (délai : 19 jours)"
- `{{ordre_du_jour}}` = "1. Approbation du PV du CA du 10 mars 2026\n2. Point sur les listes d'experts — cours d'appel de Toulouse et Bordeaux\n3. Préparation de l'AG annuelle 2026 (date, ordre du jour, logistique)\n4. Budget prévisionnel S2 2026\n5. Questions diverses"
- `{{quorum}}` = "Quorum statutaire : majorité des membres du CA (7 sur 12)"
- `{{mode_convocation}}` = "courrier électronique avec accusé de réception"
- `{{pieces_jointes}}` = "PV du CA du 10 mars 2026, tableau de suivi des listes d'experts"
- `{{signataire}}` = "M. [Prénom Nom], Président de l'UNETICA"

**Résultat attendu :**
> Convocation formelle complète, en-tête association, objet, date/heure/lieu,
> ordre du jour numéroté, mention du délai de convocation (19 jours — conforme),
> mention des pièces jointes, formule de politesse adaptée à des membres
> professionnels ETI. Pas de note de vigilance (délai respecté, pas de
> décision modificatrice à l'ordre du jour).

---

### Exemple 2 — PV d'AGO avec quorum atteint
**Variables utilisées :**
- `{{type_reunion}}` = "Assemblée générale ordinaire 2026"
- `{{nom_association}}` = "UNETICA"
- `{{date_heure_lieu}}` = "Samedi 15 juin 2026 à 10h00 — Salle de conférence, Paris 9e"
- `{{president_seance}}` = "M. [Prénom Nom], Président"
- `{{secretaire_seance}}` = "Mme [Prénom Nom], Secrétaire générale"
- `{{mode_convocation_date}}` = "Convocation par email du 29 mai 2026 (délai : 17 jours)"
- `{{membres_presents}}` = "32 membres présents (liste en annexe)"
- `{{membres_representes}}` = "8 membres représentés par procuration (pouvoirs en annexe)"
- `{{membres_absents}}` = "5 membres excusés"
- `{{quorum}}` = "Quorum statutaire : 1/3 des membres à jour de cotisation (45 membres sur 134) — 40 présents ou représentés → quorum largement atteint"
- `{{ordre_du_jour}}` = "1. Approbation du PV de l'AG 2025\n2. Rapport moral du président\n3. Rapport financier et approbation des comptes 2025 — quitus au trésorier\n4. Renouvellement partiel du CA (3 postes)\n5. Cotisations 2027\n6. Questions diverses"
- `{{debats_decisions}}` = "[résumé des échanges par point]"
- `{{heure_cloture}}` = "12h30"
- `{{signataires}}` = "Le Président / La Secrétaire de séance"

**Résultat attendu :**
> PV complet avec vérification formelle du quorum en introduction, résolutions
> numérotées avec résultats de vote (pour/contre/abstentions), liste récapitulative
> des décisions en fin de document, note sur l'obligation de déclaration en
> préfecture pour le renouvellement partiel du CA (changement de dirigeants).

---

### Exemple 3 — Convocation AGE avec modification statutaire
**Variables utilisées :**
- `{{type_reunion}}` = "Assemblée générale extraordinaire"
- `{{ordre_du_jour}}` = "1. Modification de l'article 3 des statuts (objet de l'association)\n2. Modification de l'article 12 (modalités de vote par correspondance)\n3. Ratification"
- `{{quorum}}` = "Quorum statutaire AGE : 2/3 des membres à jour de cotisation"
- `{{instructions_supplementaires}}` = "- Préciser l'obligation de dépôt en préfecture après le vote\n- Mentionner le délai de 3 mois pour la déclaration"

**Résultat attendu :**
> Convocation AGE avec mentions renforcées sur la nature extraordinaire de la
> réunion, quorum qualifié requis, note de vigilance systématique sur l'obligation
> de déclaration en préfecture dans les 3 mois suivant la modification statutaire
> (loi 1901, art. 5 et décret 1901).
