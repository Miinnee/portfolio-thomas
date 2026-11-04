# Portfolio Thomas Chassang — Astro

Refonte à partir de la base AstroPaper transmise et de la version Nuxt précédente. **Le ZIP AstroPaper fourni étant incomplet** (imports `@/config`, `@/i18n`, assets manquants), ce projet conserve l'approche statique et éditoriale d'Astro avec une architecture autonome.

## Démarrer

Node.js 20.3+ (ou 22) :

```bash
npm install
npm run dev
```

Pour générer la version de production : `npm run build`.

## Modifier les contenus

- **Profil, contacts, dates** : `src/data/site.ts`
- **Ajouter un projet** : créer `src/content/projects/mon-projet.md` en copiant la structure d'un projet existant ; sa page `/projets/mon-projet/` et sa carte apparaissent automatiquement.
- **Illustrations de projet** : déposer une image dans `public/projects/` puis ajuster `cover:` dans le Markdown. Les SVG inclus sont des **illustrations temporaires**, et non des captures de projets.
- **Design, bleu / gris / cyan** : `src/styles/site.css`
- **Page d'accueil** : `src/pages/index.astro`
- **URL du site** : `astro.config.mjs` (`site`).

Le CV est fourni dans `public/CV-Thomas-Chassang.pdf`. Le portfolio n'affiche pas l'adresse personnelle ni le numéro de téléphone, par discrétion.

Les liens GitHub individuels proviennent de la **version Nuxt de référence** et n'ont pas pu être tous vérifiés en direct : contrôle conseillé avant publication. Les informations sur le stage sont issues de la lettre datée du 1er octobre 2026.
