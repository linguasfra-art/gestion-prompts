# Traduction juridique FR / PT / EN

## Métadonnées
- **Catégorie** : traduction
- **Modèle cible** : GPT-4o | Claude 3.5 Sonnet | Gemini 1.5 Pro
- **Version** : 1.0
- **Auteur** : linguasfra-art
- **Date** : 2026-04-13

## Description
Traduit des documents juridiques et administratifs entre le français, le portugais
(variantes européenne et brésilienne) et l'anglais (britannique ou américain).
Le prompt tient compte du type de document, de la juridiction d'origine et de
destination, du niveau de formalité requis et de la terminologie sectorielle
spécifique. Adapté à la traduction certifiée, aux documents judiciaires, aux actes
d'état civil, aux diplômes et attestations, aux textes réglementaires et aux contrats.

## Paramètres du modèle
| Paramètre          | Valeur recommandée | Plage acceptable | Notes                                      |
|--------------------|--------------------|------------------|--------------------------------------------|
| temperature        | 0.1                | 0.0 – 0.3        | Précision terminologique maximale          |
| max_tokens         | 4096               | 1024 – 8192      | Ajuster selon la longueur du document      |
| top_p              | 0.9                | 0.85 – 1.0       |                                            |
| frequency_penalty  | 0.0                | 0.0 – 0.2        | Conserver les répétitions terminologiques  |
| presence_penalty   | 0.0                | 0.0 – 0.1        | Ne pas varier la terminologie à l'identique|

> **Note critique :** Une temperature très basse (0.1) est impérative en traduction
> juridique pour garantir la cohérence terminologique et éviter toute paraphrase
> non contrôlée. Ne pas dépasser 0.3.

## Prompt système
```
Tu es un traducteur juridique certifié expert en droit français, droit brésilien
et droit portugais, avec une maîtrise de l'anglais juridique britannique et
américain. Tu traduis avec une fidélité absolue au document source, sans omettre
ni paraphraser aucun élément. Tu respectes scrupuleusement :
- La terminologie officielle de la juridiction cible ({{juridiction}})
- Les équivalences institutionnelles (ex. : "tribunal judiciaire" → équivalent exact
  dans la juridiction cible, avec note explicative entre crochets si nécessaire)
- Le niveau de formalité du document original
- Les conventions typographiques juridiques de la langue cible
  (majuscules institutionnelles, ponctuation, abréviations normalisées)

En cas d'intraduisibilité stricte d'un terme, tu conserves le terme source en
italique suivi de sa définition entre crochets : *terme source* [définition].
Tu signales toute ambiguïté ou lacune du document source par une note de traducteur :
[N.T. : …].
Tu ne reformules pas, tu ne simplifies pas, tu ne corriges pas le fond — uniquement
la forme pour conformité à la langue cible.
```

## Prompt utilisateur (template)
```
Traduis le document juridique suivant.

**Type de document** : {{document_type}}
**Langue source** : {{langue_source}}
**Langue cible** : {{langue_cible}}
**Juridiction d'origine** : {{juridiction}}
**Niveau de formalité** : {{niveau_formalite}}
**Terminologie spécifique à appliquer** : {{terminologie_specifique}}
**Variante linguistique cible** : {{variante_linguistique}}

---

DOCUMENT À TRADUIRE :
{{texte_source}}

---

Instructions complémentaires :
- Conserver la mise en forme structurelle du document (titres, articles, alinéas,
  numérotation) en adaptant aux conventions de la langue cible
- Fournir un glossaire des termes techniques traduits en fin de document
  (format : terme source | terme cible | note si intraduisibilité)
- Indiquer si une certification ou apostille est requise pour ce type de document
  dans la juridiction cible
{{instructions_supplementaires}}
```

## Variables

| Variable                    | Type    | Obligatoire | Description                                                  | Exemple                                           |
|-----------------------------|---------|-------------|--------------------------------------------------------------|---------------------------------------------------|
| `{{document_type}}`         | string  | Oui         | Nature juridique du document                                 | "jugement de divorce" / "acte de naissance" / "contrat de travail" / "diplôme d'État" |
| `{{langue_source}}`         | string  | Oui         | Langue du document original                                  | "français" / "portugais brésilien"                |
| `{{langue_cible}}`          | string  | Oui         | Langue de la traduction                                      | "portugais européen" / "anglais britannique"      |
| `{{juridiction}}`           | string  | Oui         | Juridiction d'origine et/ou de destination                   | "France → Brésil" / "Portugal → Royaume-Uni"      |
| `{{niveau_formalite}}`      | string  | Oui         | Registre de langue requis                                    | "très formel / acte officiel" / "formel / usage administratif" / "courant / communication interne" |
| `{{terminologie_specifique}}`| string | Non         | Domaine sectoriel ou glossaire à privilégier                 | "droit de la famille, apostille La Haye" / "droit commercial OHADA" / "médical-légal" |
| `{{variante_linguistique}}` | string  | Non         | Précision dialectale ou nationale                            | "portugais brésilien (PT-BR)" / "anglais américain (EN-US)" / "français canadien (FR-CA)" |
| `{{texte_source}}`          | string  | Oui         | Texte intégral du document à traduire                        | [coller le document ici]                          |
| `{{instructions_supplementaires}}` | string | Non   | Consignes additionnelles libres                              | "- Préserver les références légales (articles de loi) sans traduire les numéros" |

## Exemples de test

### Exemple 1 — Traduction d'un extrait de jugement FR → PT-BR
**Variables utilisées :**
- `{{document_type}}` = "extrait de jugement civil"
- `{{langue_source}}` = "français"
- `{{langue_cible}}` = "portugais brésilien"
- `{{juridiction}}` = "Tribunal judiciaire de Toulouse → utilisation au Brésil (apostille requise)"
- `{{niveau_formalite}}` = "très formel / acte judiciaire officiel"
- `{{terminologie_specifique}}` = "procédure civile française, Code de procédure civile (CPC), équivalences droit brésilien (CPC/2015)"
- `{{variante_linguistique}}` = "portugais brésilien (PT-BR)"
- `{{texte_source}}` = "Par ces motifs, le tribunal, statuant publiquement, contradictoirement et en premier ressort, CONDAMNE M. [X] à payer à Mme [Y] la somme de 1 500 € (mille cinq cents euros) au titre de l'article 700 du Code de procédure civile..."
- `{{instructions_supplementaires}}` = "- Conserver les montants en euros avec équivalence indicative en BRL entre crochets\n- Préserver les références CPC françaises avec note de traducteur indiquant l'article brésilien équivalent"

**Résultat attendu :**
> Traduction fidèle avec : *jugement civil* → *sentença cível*, *article 700 CPC* conservé
> en référence avec note [N.T. : equivalente ao art. 85 do CPC/2015 (honorários
> advocatícios)], glossaire en fin de document, mention du besoin d'apostille
> Convention de La Haye.

---

### Exemple 2 — Traduction d'un diplôme universitaire FR → EN (usage UK)
**Variables utilisées :**
- `{{document_type}}` = "diplôme national de master"
- `{{langue_source}}` = "français"
- `{{langue_cible}}` = "anglais britannique"
- `{{juridiction}}` = "Ministère de l'Enseignement supérieur français → Royaume-Uni (NARIC/Ecctis recognition)"
- `{{niveau_formalite}}` = "très formel / document officiel d'État"
- `{{terminologie_specifique}}` = "système LMD, ECTS, équivalences UK (QAA Framework for Higher Education Qualifications)"
- `{{variante_linguistique}}` = "anglais britannique (EN-GB)"
- `{{texte_source}}` = "Le Président de l'Université Toulouse Capitole certifie que M. [X], né le [...] à [...], a satisfait aux épreuves du Diplôme national de Master mention Droit privé, spécialité Droit notarial, à l'issue de la deuxième année du cycle Master. Grade : Bien."
- `{{instructions_supplementaires}}` = "- Traduire 'Bien' selon l'échelle UK (Upper Second-Class Honours equivalent)\n- Conserver le nom de l'université en français avec traduction entre parenthèses"

**Résultat attendu :**
> Traduction certifiable avec *Diplôme national de Master* → *National Master's Degree*,
> mention de grade adaptée à l'échelle britannique, note sur l'équivalence FHEQ Level 7,
> glossaire LMD/ECTS → UK terminology.

---

### Exemple 3 — Traduction d'un acte d'état civil FR → PT-EU
**Variables utilisées :**
- `{{document_type}}` = "acte de naissance (extrait plurilingue)"
- `{{langue_source}}` = "français"
- `{{langue_cible}}` = "portugais européen"
- `{{juridiction}}` = "Mairie de Toulouse → utilisation au Portugal (Union européenne)"
- `{{niveau_formalite}}` = "très formel / acte d'état civil officiel"
- `{{terminologie_specifique}}` = "état civil français, Règlement UE n°2016/1191 (formulaires types plurilingues)"
- `{{variante_linguistique}}` = "portugais européen (PT-PT)"
- `{{texte_source}}` = "L'an deux mille [X], le [date], par-devant nous, officier de l'état civil de la commune de Toulouse (Haute-Garonne), a comparu [X], qui nous a déclaré que [Y], de sexe masculin/féminin, est né(e) le [date] à [lieu]..."
- `{{instructions_supplementaires}}` = "- Appliquer la terminologie du formulaire type multilingue UE (Annexe I du Règlement 2016/1191)\n- Signaler si une traduction certifiée est requise ou si le formulaire multilingue suffit dans le contexte UE"

**Résultat attendu :**
> Traduction conforme aux formulaires types UE avec terminologie standardisée,
> note sur la dispense de légalisation entre États membres, glossaire état civil
> FR/PT comparatif.
