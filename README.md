# gestion-prompts

Bibliothèque personnelle de prompts AI organisée et versionnée — templates système/utilisateur avec variables, paramètres de modèles, descriptions et exemples de test.

---

## Structure du dépôt

```
gestion-prompts/
├── README.md          # Ce fichier — guide d'organisation
├── .gitignore         # Fichiers à exclure du suivi Git
├── LICENSE            # Licence MIT
└── prompts/
    ├── generation-code.md      # Prompt pour générer du code
    ├── generation-images.md    # Prompt pour générer des images
    └── generation-rapports.md  # Prompt pour générer des rapports
```

---

## Convention de nommage

Chaque fichier de prompt suit ce schéma :

```
[domaine]-[action].md
```

Exemples : `traduction-juridique.md`, `résumé-document.md`, `correction-email.md`

---

## Format d'un fichier de prompt

Chaque prompt est un fichier Markdown structuré ainsi :

```markdown
# Titre du prompt

## Métadonnées
- **Catégorie** : code | image | rapport | traduction | autre
- **Modèle cible** : GPT-4o | Claude 3.5 | Gemini 1.5 Pro | tous
- **Version** : 1.0
- **Auteur** : [votre nom]
- **Date** : AAAA-MM-JJ

## Description
Brève description de l'objectif du prompt et des cas d'usage typiques.

## Paramètres du modèle
| Paramètre       | Valeur recommandée | Plage acceptable |
|-----------------|-------------------|-----------------|
| temperature     | 0.7               | 0.0 – 1.0       |
| max_tokens      | 1024              | 512 – 4096      |
| top_p           | 1.0               | 0.8 – 1.0       |
| frequency_penalty | 0.0             | 0.0 – 2.0       |

## Prompt système
```
[Instruction de rôle et contexte permanent.
Définit le comportement de l'IA indépendamment de la requête utilisateur.]
```

## Prompt utilisateur (template)
```
[Corps de la requête avec variables entre doubles accolades.
Exemple : {{variable_nom}} sera remplacée à l'usage.]
```

## Variables

| Variable         | Type    | Obligatoire | Description                     | Exemple              |
|------------------|---------|-------------|---------------------------------|----------------------|
| `{{variable_1}}` | string  | Oui         | Description de la variable      | "valeur exemple"     |
| `{{variable_2}}` | string  | Non         | Description de la variable      | "valeur exemple"     |

## Exemples de test

### Exemple 1 — [Nom du cas]
**Variables utilisées :**
- `{{variable_1}}` = "..."
- `{{variable_2}}` = "..."

**Résultat attendu :**
> Description du type de réponse attendue.

---

## Utilisation des variables `{{variable}}`

Les variables utilisent la syntaxe `{{nom_variable}}` (doubles accolades). Elles permettent de créer des templates réutilisables dont seuls certains paramètres changent d'une utilisation à l'autre.

**Règles de nommage :**
- Minuscules avec underscores : `{{langue_cible}}`, `{{type_document}}`
- Noms explicites et concis
- Pas d'espaces ni de caractères spéciaux

**Substitution :**
Avant d'envoyer un prompt au modèle, remplacez manuellement (ou via script) toutes les occurrences `{{variable}}` par les valeurs réelles.

---

## Catégories disponibles

| Catégorie    | Description                                          |
|--------------|------------------------------------------------------|
| `code`       | Génération, révision et explication de code          |
| `image`      | Description et génération d'images (DALL·E, Midjourney, Stable Diffusion…) |
| `rapport`    | Rédaction de rapports, synthèses, comptes rendus     |
| `traduction` | Traduction et adaptation linguistique                |
| `autre`      | Tout autre cas d'usage                               |

---

## Ajouter un nouveau prompt

1. Créer un fichier `.md` dans `/prompts/` en respectant la convention de nommage
2. Utiliser le format décrit ci-dessus
3. Tester le prompt avec au moins un exemple
4. Committer avec un message descriptif :
   ```
   git add prompts/mon-nouveau-prompt.md
   git commit -m "feat: ajout prompt [domaine]-[action]"
   git push
   ```

---

## Licence

Ce dépôt est distribué sous licence [MIT](LICENSE).
