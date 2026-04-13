# Génération de code

## Métadonnées
- **Catégorie** : code
- **Modèle cible** : GPT-4o | Claude 3.5 Sonnet | Gemini 1.5 Pro
- **Version** : 1.0
- **Auteur** : linguasfra-art
- **Date** : 2026-04-13

## Description
Génère un bloc de code propre, commenté et fonctionnel dans le langage demandé.
Adapté pour créer des fonctions utilitaires, des scripts ou des modules à partir
d'une description fonctionnelle en langage naturel.

## Paramètres du modèle
| Paramètre          | Valeur recommandée | Plage acceptable |
|--------------------|--------------------|-----------------|
| temperature        | 0.2                | 0.0 – 0.5       |
| max_tokens         | 2048               | 512 – 4096      |
| top_p              | 0.95               | 0.8 – 1.0       |
| frequency_penalty  | 0.0                | 0.0 – 1.0       |

> **Note :** Une température basse (0.2) favorise la précision et la reproductibilité
> du code plutôt que la créativité.

## Prompt système
```
Tu es un développeur senior expert en {{langage}} avec plus de 10 ans d'expérience.
Tu génères du code propre, lisible et bien commenté, conforme aux bonnes pratiques
du langage (conventions de nommage, gestion des erreurs, documentation des fonctions).
Tu fournis uniquement le code demandé, précédé d'une brève description (2-3 phrases)
et suivi d'exemples d'utilisation. Tu n'utilises pas de bibliothèques externes
sauf si elles sont explicitement demandées.
```

## Prompt utilisateur (template)
```
Écris une fonction en {{langage}} qui {{description_fonctionnelle}}.

Contraintes techniques :
- Style de code : {{style_code}}
- Gestion des erreurs : {{gestion_erreurs}}
- Commentaires : inclure des commentaires inline en français
{{contraintes_supplementaires}}

Fournis :
1. Le code complet avec commentaires
2. Un exemple d'utilisation avec des données fictives
3. Les cas limites à surveiller (edge cases)
```

## Variables

| Variable                    | Type    | Obligatoire | Description                                      | Exemple                          |
|-----------------------------|---------|-------------|--------------------------------------------------|----------------------------------|
| `{{langage}}`               | string  | Oui         | Langage de programmation cible                   | "Python 3.11"                    |
| `{{description_fonctionnelle}}` | string | Oui      | Ce que doit faire la fonction en langage naturel | "lit un fichier CSV et retourne un dictionnaire" |
| `{{style_code}}`            | string  | Non         | Convention de style à respecter                  | "PEP 8" / "Google Style"         |
| `{{gestion_erreurs}}`       | string  | Non         | Stratégie de gestion des erreurs                 | "lever des exceptions explicites"|
| `{{contraintes_supplementaires}}` | string | Non    | Contraintes additionnelles libres                | "- Sans dépendances externes"    |

## Exemples de test

### Exemple 1 — Lecture de fichier CSV en Python
**Variables utilisées :**
- `{{langage}}` = "Python 3.11"
- `{{description_fonctionnelle}}` = "lit un fichier CSV et retourne une liste de dictionnaires, une ligne = un dictionnaire"
- `{{style_code}}` = "PEP 8"
- `{{gestion_erreurs}}` = "lever des exceptions FileNotFoundError et ValueError avec messages explicites"
- `{{contraintes_supplementaires}}` = "- Utiliser uniquement la bibliothèque standard (csv, pathlib)"

**Résultat attendu :**
> Une fonction `lire_csv(chemin_fichier)` proprement typée, avec docstring,
> gestion des erreurs, et un bloc `if __name__ == "__main__"` démontrant l'usage.

---

### Exemple 2 — Formatage de date en JavaScript
**Variables utilisées :**
- `{{langage}}` = "JavaScript (ES2022)"
- `{{description_fonctionnelle}}` = "formate une date ISO 8601 en chaîne lisible selon une locale donnée"
- `{{style_code}}` = "Airbnb JavaScript Style Guide"
- `{{gestion_erreurs}}` = "retourner null si la date est invalide"
- `{{contraintes_supplementaires}}` = "- Utiliser l'API Intl.DateTimeFormat native"

**Résultat attendu :**
> Une fonction `formatDate(isoString, locale)` avec commentaires JSDoc et
> exemples pour les locales `fr-FR` et `pt-BR`.
