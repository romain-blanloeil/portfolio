# CLAUDE.md

Repères pour Claude Code sur ce dépôt.

## Le projet

Portfolio personnel de Romain Blanloeil : infirmier pendant 20 ans, en reconversion, étudiant TSSR à l'ENI École Informatique de Nantes. Il recherche une alternance Bac+4 Administrateur Systèmes & Réseaux dès janvier 2027.

- Site en ligne : https://romain.blanloeil.com
- Public visé : recruteurs et entreprises pour l'alternance. Le ton reste sobre, factuel et professionnel.
- Langue du site : français.

## Stack et contraintes

- HTML5 / CSS3 pur, **sans framework, sans build, sans dépendance npm**. On ne les ajoute pas.
- Pas de JavaScript applicatif. Le menu mobile est en CSS pur (checkbox `#nav-toggle` et `:checked ~`). Seul le script Vercel Insights est présent, en bas de chaque page.
- Formulaire de contact : Formspree (`action` du `<form>` dans `index.html`).
- Hébergement : Vercel, **déploiement automatique à chaque push sur `main`**. Pousser sur `main` revient à mettre en ligne. On ne pousse jamais sans l'accord explicite de Romain.

## Structure

- `index.html` : page d'accueil en une seule page (sections `#accueil`, `#parcours`, `#competences`, `#projets`, `#contact`).
- `projets/*.html` : une page par projet (`homelab`, `rugby-app`, `portfolio`), avec des chemins relatifs en `../`.
- `css/style.css` : feuille de style unique. Les couleurs, polices et espacements passent par les variables de `:root` (`--teal`, `--ink`, `--paper`, `--font-display`…). On réutilise ces variables plutôt que d'écrire des valeurs en dur.
- `assets/img/` : images. `assets/cv-romain-blanloeil.pdf` : le CV.

La barre de navigation et le footer sont **dupliqués dans chaque page**. Une modification de l'un doit être reportée dans toutes les pages, en adaptant les chemins (`../index.html#…` depuis `projets/`).

## Conventions

- Caractères spéciaux en entités HTML dans le texte : `&amp;`, `&larr;`…
- Liens externes : `target="_blank" rel="noopener"`.
- Images : attribut `alt` en français, `width` et `height` renseignés, `loading="lazy"` hors du haut de page.
- Indentation : 2 espaces.

## Ajouter un badge de certification

Dans `index.html`, section `.certs`, liste `<ul class="badges">` : ajouter un `<li>` sur le modèle des badges existants.

- Image : `assets/img/badge-<nom>.png`, en **PNG 288×288 aux coins arrondis** (rayon d'environ 28 px, fond transparent), affichée en 96×96.
- Badges Claude Academy : partir du PDF officiel, dont l'image fait 3300×2250. Masquer le logo « Claude Academy » et la mention « ISSUED … », puis recadrer en carré sur la forme beige, soit la zone `(701, 176, 2601, 2076)` commune à tous les badges. Tous les badges Academy du site gardent ainsi le même cadrage.
- Lien : URL de vérification officielle (Credly, `academy.claude.com/verify/…`), avec un `title="Vérifier sur …"`.
- Légende : `Nom<br>mois abrégé année`, par exemple `nov. 2026`.
- Les certifications en projet apparaissent dans la même liste, sous forme de « badge fantôme » (`<div class="badge badge-todo">` avec un `.badge-slot` en pointillés et la légende `en projet`), placés après les badges obtenus. Une fois la certification obtenue, on remplace son badge fantôme par un vrai badge.

## Vérifier une modification

Aucun test automatisé. Servir le site en local et contrôler le rendu, en bureau comme en mobile :

```bash
python3 -m http.server 8000
```

## Licence

Le code est sous licence MIT. Les contenus (textes, photo, CV) sont © Romain Blanloeil. Ne pas réutiliser ni modifier ces contenus sans demande explicite.
