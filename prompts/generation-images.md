# Génération d'images

## Métadonnées
- **Catégorie** : image
- **Modèle cible** : DALL·E 3 | Stable Diffusion XL | Midjourney v6 | Flux
- **Version** : 1.0
- **Auteur** : linguasfra-art
- **Date** : 2026-04-13

## Description
Génère un prompt optimisé pour les modèles de création d'images à partir d'une
description du sujet, du style artistique et des paramètres visuels souhaités.
Ce prompt peut être utilisé directement dans DALL·E 3 (via ChatGPT ou API OpenAI),
Midjourney, ou adapté pour Stable Diffusion.

## Paramètres du modèle
| Paramètre      | Valeur recommandée | Plage acceptable | Notes                                  |
|----------------|--------------------|-----------------|----------------------------------------|
| temperature    | 0.8                | 0.5 – 1.0       | Favorise la créativité descriptive     |
| max_tokens     | 512                | 256 – 1024      | Les prompts images sont courts         |
| top_p          | 1.0                | 0.9 – 1.0       |                                        |

> **Paramètres spécifiques selon le modèle :**
> - **DALL·E 3** : `size` (1024x1024 / 1792x1024 / 1024x1792), `quality` (standard / hd), `style` (vivid / natural)
> - **Stable Diffusion** : `steps` (20–50), `cfg_scale` (7–12), `sampler` (DPM++ 2M Karras)
> - **Midjourney** : `--ar` (ratio), `--v 6`, `--style raw`, `--q 2`

## Prompt système
```
Tu es un expert en direction artistique et en rédaction de prompts pour modèles
de génération d'images. Tu maîtrises les techniques de description visuelle pour
DALL·E 3, Midjourney et Stable Diffusion. Tu rédiges des prompts riches, précis
et structurés qui maximisent la qualité du résultat visuel. Tes descriptions
incluent toujours : le sujet principal, l'ambiance/atmosphère, le style artistique,
l'éclairage, la palette de couleurs et la composition. Tu fournis le prompt en
anglais (plus efficace pour les modèles image) avec sa traduction française.
```

## Prompt utilisateur (template)
```
Crée un prompt de génération d'image pour le sujet suivant :

Sujet principal : {{sujet}}
Style artistique : {{style_artistique}}
Ambiance / atmosphère : {{ambiance}}
Palette de couleurs : {{palette_couleurs}}
Format / composition : {{composition}}
Modèle cible : {{modele_cible}}
Éléments à exclure : {{elements_negatifs}}

Fournis :
1. Le prompt optimisé en anglais (pour le modèle)
2. La traduction française du prompt
3. Le prompt négatif (negative prompt) si applicable
4. Les paramètres techniques recommandés pour {{modele_cible}}
```

## Variables

| Variable              | Type    | Obligatoire | Description                                    | Exemple                              |
|-----------------------|---------|-------------|------------------------------------------------|--------------------------------------|
| `{{sujet}}`           | string  | Oui         | Description du sujet ou de la scène principale | "Un port breton au lever du soleil"  |
| `{{style_artistique}}`| string  | Oui         | Style visuel ou référence artistique           | "aquarelle impressionniste"          |
| `{{ambiance}}`        | string  | Non         | Émotion ou atmosphère recherchée               | "calme, nostalgique, lumière dorée"  |
| `{{palette_couleurs}}`| string  | Non         | Couleurs dominantes ou ton général             | "tons bleus et orangés chauds"       |
| `{{composition}}`     | string  | Non         | Cadrage, angle, format                         | "grand angle, format 16:9, panorama" |
| `{{modele_cible}}`    | string  | Oui         | Modèle IA d'image à utiliser                   | "DALL·E 3" / "Midjourney v6"         |
| `{{elements_negatifs}}`| string | Non         | Ce que l'image ne doit pas contenir            | "personnes, texte, logo, flou"       |

## Exemples de test

### Exemple 1 — Illustration pour rapport professionnel
**Variables utilisées :**
- `{{sujet}}` = "Une salle de conférence moderne et lumineuse avec des personnes en réunion, vue de dessus"
- `{{style_artistique}}` = "illustration vectorielle flat design, style corporate"
- `{{ambiance}}` = "professionnel, dynamique, collaboratif"
- `{{palette_couleurs}}` = "bleu marine, blanc, accents dorés"
- `{{composition}}` = "vue isométrique, format carré 1:1"
- `{{modele_cible}}` = "DALL·E 3"
- `{{elements_negatifs}}` = "texte, logo, visages reconnaissables"

**Résultat attendu :**
> Un prompt anglais détaillé de type : *"Top-down isometric illustration of a modern
> bright conference room, flat design vector style, corporate aesthetic, navy blue
> and white color palette with golden accents, collaborative atmosphere, no text,
> no logos, no recognizable faces, square format..."* + paramètres DALL·E 3.

---

### Exemple 2 — Couverture de document de formation
**Variables utilisées :**
- `{{sujet}}` = "Une main tenant un stylo au-dessus d'un document juridique, sur un bureau en bois"
- `{{style_artistique}}` = "photographie professionnelle, haute résolution"
- `{{ambiance}}` = "sérieux, précis, institutionnel"
- `{{palette_couleurs}}` = "tons chauds naturels, bois, papier ivoire"
- `{{composition}}` = "gros plan macro, profondeur de champ, format 16:9"
- `{{modele_cible}}` = "Stable Diffusion XL"
- `{{elements_negatifs}}` = "texte illisible, distorsion des mains, flou excessif"

**Résultat attendu :**
> Prompt photo-réaliste avec paramètres SD XL (steps: 30, cfg: 8, sampler: DPM++)
> et negative prompt détaillé pour éviter les artefacts typiques.
