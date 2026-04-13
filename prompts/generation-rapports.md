# Génération de rapports

## Métadonnées
- **Catégorie** : rapport
- **Modèle cible** : GPT-4o | Claude 3.5 Sonnet | Gemini 1.5 Pro
- **Version** : 1.0
- **Auteur** : linguasfra-art
- **Date** : 2026-04-13

## Description
Génère un rapport structuré, professionnel et complet à partir d'une liste de
données brutes ou d'un contexte fourni. Adapté aux rapports d'analyse, comptes
rendus de réunion, synthèses documentaires et rapports d'activité professionnelle.
Particulièrement utile pour la production de documents à remettre à des clients,
des institutions ou des équipes internes.

## Paramètres du modèle
| Paramètre          | Valeur recommandée | Plage acceptable | Notes                                  |
|--------------------|--------------------|-----------------|----------------------------------------|
| temperature        | 0.4                | 0.2 – 0.7       | Équilibre précision et fluidité rédact.|
| max_tokens         | 3000               | 1024 – 8192     | Ajuster selon longueur rapport souhait.|
| top_p              | 0.95               | 0.85 – 1.0      |                                        |
| frequency_penalty  | 0.3                | 0.0 – 0.8       | Évite les répétitions lexicales        |
| presence_penalty   | 0.2                | 0.0 – 0.5       | Encourage la diversité des tournures   |

## Prompt système
```
Tu es un rédacteur professionnel spécialisé dans la production de rapports formels
en {{langue_redaction}}. Tu maîtrises les normes rédactionnelles des documents
administratifs, juridiques et professionnels. Tu structures systématiquement tes
rapports avec une hiérarchie claire (titres, sous-titres, numérotation), un langage
précis et neutre, et des transitions logiques entre les sections. Tu adaptes
toujours le registre de langue au type de destinataire indiqué. Tu ne fais aucune
supposition non étayée par les données fournies et signales les lacunes d'information.
```

## Prompt utilisateur (template)
```
Rédige un rapport {{type_rapport}} sur le sujet suivant :

**Sujet** : {{sujet_rapport}}
**Destinataire** : {{destinataire}}
**Contexte** : {{contexte}}
**Données / informations à intégrer** :
{{donnees_brutes}}

**Structure demandée** :
{{structure_souhaitee}}

**Contraintes de forme** :
- Longueur approximative : {{longueur_souhaitee}}
- Niveau de langue : {{niveau_langue}}
- Format de sortie : {{format_sortie}}
- Mentions obligatoires : {{mentions_obligatoires}}
```

## Variables

| Variable               | Type    | Obligatoire | Description                                          | Exemple                                  |
|------------------------|---------|-------------|------------------------------------------------------|------------------------------------------|
| `{{langue_redaction}}` | string  | Oui         | Langue du rapport                                    | "français" / "portugais brésilien"       |
| `{{type_rapport}}`     | string  | Oui         | Nature du rapport                                    | "d'analyse" / "de synthèse" / "d'activité" |
| `{{sujet_rapport}}`    | string  | Oui         | Sujet principal ou titre                             | "Bilan de la session de formation 2025"  |
| `{{destinataire}}`     | string  | Oui         | Destinataire(s) et leur profil                       | "Direction administrative, non-spécialiste" |
| `{{contexte}}`         | string  | Oui         | Contexte de production du rapport                    | "Suite à 3 sessions de formation menées en janvier 2026" |
| `{{donnees_brutes}}`   | string  | Oui         | Faits, chiffres, observations à intégrer             | "- 24 participants\n- 3 formateurs\n- Taux de satisfaction : 87 %" |
| `{{structure_souhaitee}}` | string | Non       | Plan ou sections imposées                            | "1. Résumé exécutif\n2. Constats\n3. Recommandations" |
| `{{longueur_souhaitee}}`| string | Non         | Longueur cible                                       | "2 pages / 600 mots"                     |
| `{{niveau_langue}}`    | string  | Non         | Registre formel ou courant                           | "formel administratif"                   |
| `{{format_sortie}}`    | string  | Non         | Markdown, texte brut, HTML                           | "Markdown avec titres H2/H3"             |
| `{{mentions_obligatoires}}` | string | Non     | Éléments à faire apparaître impérativement           | "Date, référence dossier, signature"     |

## Exemples de test

### Exemple 1 — Rapport de synthèse de formation professionnelle
**Variables utilisées :**
- `{{langue_redaction}}` = "français"
- `{{type_rapport}}` = "de synthèse"
- `{{sujet_rapport}}` = "Session de formation à la traduction juridique assistée par IA — janvier 2026"
- `{{destinataire}}` = "Bureau de direction de l'association professionnelle, profil non technique"
- `{{contexte}}` = "Formation dispensée en ligne via webinaire, 3 séances de 2h chacune"
- `{{donnees_brutes}}` = "- 18 participants inscrits, 15 présents en moyenne\n- Intervenants : 2 traductrices certifiées\n- Outils abordés : DeepL Pro, ChatGPT, NotebookLM\n- Taux de satisfaction global : 91 %\n- Points forts cités : cas pratiques, exemples réels\n- Points d'amélioration : durée trop courte, exercices insuffisants"
- `{{structure_souhaitee}}` = "1. Contexte et objectifs\n2. Déroulement\n3. Résultats et retours\n4. Recommandations"
- `{{longueur_souhaitee}}` = "1 page / 400 mots environ"
- `{{niveau_langue}}` = "formel administratif"
- `{{format_sortie}}` = "Markdown"
- `{{mentions_obligatoires}}` = "Date du rapport, nom de l'association"

**Résultat attendu :**
> Un rapport en Markdown bien structuré avec 4 sections numérotées, un registre
> formel, une synthèse des données chiffrées et 2-3 recommandations concrètes.

---

### Exemple 2 — Compte rendu de réunion de bureau associatif
**Variables utilisées :**
- `{{langue_redaction}}` = "français"
- `{{type_rapport}}` = "compte rendu de réunion"
- `{{sujet_rapport}}` = "Réunion du bureau UNETICA — 10 avril 2026"
- `{{destinataire}}` = "Membres de l'association"
- `{{contexte}}` = "Réunion mensuelle ordinaire, tenue en visioconférence"
- `{{donnees_brutes}}` = "- Présents : 5 membres du bureau\n- Ordre du jour : cotisations 2026, organisation AG, charte déontologique mise à jour\n- Décisions : hausse cotisation de 5 %, AG fixée au 15 juin 2026, charte soumise au vote des membres"
- `{{structure_souhaitee}}` = "Participants — Points abordés — Décisions prises — Prochaine réunion"
- `{{longueur_souhaitee}}` = "court, 200-300 mots"
- `{{niveau_langue}}` = "formel institutionnel"
- `{{format_sortie}}` = "Markdown"
- `{{mentions_obligatoires}}` = "Date, lieu (visioconférence), secrétaire de séance"

**Résultat attendu :**
> Compte rendu concis et factuel, format tableau ou liste pour les décisions,
> sans reformulation excessive des débats.
