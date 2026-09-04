# Athanor Studio Website

Site vitrine d'Athanor Studio (app publishing company).

## Stack
- HTML/CSS statique pur, pas de framework, pas de build
- Police : Inter (Google Fonts)
- Hébergement : GitHub Pages, domaine via `CNAME`
- Repo : https://github.com/AthanorStudio/website (branche `main`)

## Fichiers
- `index.html` — landing page Athanor Studio (navbar, hero, services, apps, company, contact, footer)
- `styles.css` — design system du site studio (dark, tokens, composants, responsive)
- `privacy.html` — politique de confidentialité
- `healthyguru/index.html` + `healthyguru/styles.css` — landing page dédiée à l'app Healthy Guru, accessible via `/healthyguru` (light theme + **accent vert frais**, charte propre distincte du studio). `healthyguru/screen-*.webp` = screenshots réels de l'app (mockups + CTA).
- `climbr/index.html` + `climbr/styles.css` — page dédiée à l'app Climbr, accessible via `/climbr` (thème **sable / encre / terre brûlée**, la palette « Grès » de l'app). `climbr/screen-*.webp` = vrais écrans de l'app, `climbr/iphone.webp` = le boîtier iPhone 17 Pro Max (capturé dans le Simulateur de Xcode, écran transparent) posé par-dessus chaque écran en CSS.
- `athanorstudio_logo.png`, `healthyguru_icon.png`, `clashlist_icon.png`, `climbr_icon.png` — assets
- `CNAME` — domaine GitHub Pages
- `og-image.png` (racine, thème sombre studio) + `healthyguru/og-image.png` (thème vert app) + `climbr/og-image.png` (sable, généré avec Pillow) — images de partage 1200×630, générées via une carte HTML rendue en Chrome headless puis redimensionnée avec `sips`. Balises Open Graph/Twitter + `canonical` + `theme-color` dans les deux `<head>`.
- `robots.txt` + `sitemap.xml` — SEO de base (racine).

## Design system
- Thème sombre : `bg: #0c0c0c`
- Accent crème/or : `#f8eac1`
- Animations fade-up au scroll
- Breakpoints responsive : 1024px / 768px / 480px

## Sections de l'index
1. Navbar (logo + Services / Apps / Company / Contact + hamburger mobile)
2. Hero — "We build and scale apps."
3. Services — 4 value cards (Transformation, Ownership, Data-Driven, Innovation)
4. Apps — grille `auto-fit minmax(340px, 1fr)` avec deux cartes : Healthy Guru et Climbr (Clash List retirée de l'accueil le 4 septembre 2026, son icône reste dans le dépôt) :
   - Healthy Guru (4.6 ★, 500+ reviews, 150k+ installs) — carte cliquable (`<a class="app-card app-card-link">`) qui mène vers `/healthyguru`. CTA "Learn more →" en bas de carte. Le lien App Store n'est plus dans la carte (il est sur la page dédiée).
   - Climbr (Sports · Bouldering, badge "Coming Soon") — carte cliquable vers `/climbr`.
5. Company — storytelling Athanor (fondé en 2024, fourneau alchimique)
6. Contact — titre seul (sous-titre retiré) + formulaire `mailto:` (pas de backend) → guillaume@athanor-studio.io
7. Footer

## Apps
- **Healthy Guru** — nutrition/fitness IA, Health & Fitness
  - https://apps.apple.com/fr/app/healthy-guru/id6575388387
  - Page dédiée : `/healthyguru` (dossier `healthyguru/`, light theme + **accent vert frais `#34b45a`** sur fonds mints doux, pour matcher l'app HG ; étoiles de notation en ambré `--star: #f5b301`). Design inspiré de solaia.app + micron-app.com. NB : cette page a sa PROPRE charte (verte), distincte du site studio racine (crème/or).
  - **Bilingue FR/EN** : détection auto via `navigator.language` (préfixe `fr` → français, sinon anglais) + toggle manuel `.lang-toggle` dans la navbar, choix mémorisé en `localStorage` (`hg-lang`). Tout le contenu traduisible porte un attribut `data-i18n="clé"` ; le dictionnaire `I18N = { en, fr }` est dans le `<script>` en bas de `index.html`. Pour éditer un texte, modifier la valeur dans les DEUX langues (les valeurs peuvent contenir du HTML inline, elles sont injectées via `innerHTML`). `<title>` et meta description sont aussi traduits.
  - **Ordre des sections** (l'alternance des fonds clair/`.section-cream` est volontaire, pour ne jamais avoir deux fonds crème collés) :
    1. **Navbar** — logo HG + How it works / Features / Reviews / FAQ + toggle langue + Download
    2. **Hero** — en haut : ligne étoiles + note `.hero-social` (⭐ 4,6 · 150 000+ utilisateurs…) qui remplace l'ancien eyebrow ; puis titre "La nutrition, jusqu'au micronutriment." (2ᵉ ligne en `.ink-soft`) + sous-titre + bouton App Store + **2 chips** `.hero-trust` [Sans pub / Tes données restent privées] ; à droite **trio de mockups iPhone décalés** (`.phones`)
    3. **Features** (`#features`, fond crème) — **4 cards** icône emoji, grille 2×2 : Plan sur mesure 🎯 / Suivi nutritionnel ultra-précis 📸 / Suivi d'activité ⌚ / Suivi de progression 📈
    4. **Comparison** (`.compare`) — carte blanche "Les trackers basiques" ✕ vs carte noire "Healthy Guru" ✓ (inspirée micron-app.com)
    5. **How it works** (`#how`, fond crème) — titre "3 étapes simples" + **stepper** façon micron-app : 3 cercles numérotés `.step-badge` + label "Étape X" `.step-label` + traits de liaison `.step::after`, centré. Étapes : Définis tes objectifs → Enregistre tes repas → Suis ta progression
    6. **Reviews** (`#reviews`) — titre + **ligne de note** `.reviews-rating` (⭐ 4,6 · 500+ avis sur l'App Store, cliquable → App Store) + **3 témoignages** `<figure>` (note et avis regroupés dans UNE section façon micron-app, plus de bandeau dark)
    7. **FAQ** (`#faq`, fond crème) — 5 questions `<details>`
    8. **Final CTA** (`.final-cta`) — **carte contenue** `.final-cta-card` (fond dégradé + texture grille `::before`) façon micron-app : texte + bouton App Store à gauche, **mockup iPhone qui déborde en bas** à droite (`screen-home.webp`)
    9. **Footer**
  - **Mockups hero** = 3 faux iPhones (`.phone-left`/`.phone-center`/`.phone-right`) avec de **vrais screenshots** de l'app en WebP optimisé (~15-25 Ko chacun) : `screen-meal.webp` (gauche, détail repas scanné), `screen-home.webp` (centre, dashboard/anneau calories), `screen-recipes.webp` (droite, recettes). Sources originales : `~/Downloads/IMG_1045/1047/1043.PNG`, redimensionnées à 620px de large via `sips` puis encodées en WebP via `cwebp -q 78`. Pour mettre à jour un écran : refaire le même pipeline et écraser le `.webp`.
  - **⚠️ Positionnement / wording (important)** : l'app propose **4 façons de logger un repas** — scan photo IA, scan code-barres, base de données nutritionnelle, saisie manuelle. NE PAS réduire le discours au seul scan photo (ça donne une fausse impression d'imprécision). Toujours mettre en avant la **complétude** (4 méthodes) + la **précision** (micronutriments détaillés, valeurs ajustables, bases de données validées, recettes détaillées). Le hero est volontairement élargi ("La nutrition, jusqu'au micronutriment." / "Nutrition, down to the micronutrient.", pas centré photo). La colonne "Les trackers basiques" de la comparaison = saisie manuelle uniquement / calories seules / pas de micros — c'est ce que HG dépasse. **Ton FR = tutoiement** partout (chaleureux/coach, cohérent avec les apps conso FR).
  - **Témoignages** = vrais avis App Store repris (Beyrima « Au top », Alexaa A « s'améliore chaque semaine », Kiwak_. « Très bonne application »), traduits en EN dans le dictionnaire — les originaux FR sont verbatim. Récupérables via le flux `https://itunes.apple.com/fr/rss/customerreviews/id=6575388387/sortby=mosthelpful/json`.
  - **Responsive du trio de mockups** : largeur fixe → géré par `transform: scale()` par palier (>1440 pleine taille / 1201-1440 `.phones` 0.85 / bascule 1 colonne ≤1200 / 820 → 0.82 / 600 → 0.64 / 400 → 0.52) + `min-width:0` sur les cellules du hero pour éviter tout débordement horizontal.
  - **Partage/SEO** : image OG dédiée `healthyguru/og-image.png` (carte verte : logo + accroche + mockup dashboard) + balises OG/Twitter/canonical/theme-color dans le `<head>`. Régénérable via le pipeline « carte HTML → Chrome headless `--screenshot` → `sips -z 630 1200` » (voir historique).
  - **Statut** : refonte complète faite et **déployée en live** (bilingue, trio vrais screenshots, features/comparaison/stepper/avis/CTA carte, thème vert, responsive, OG/SEO). Reste UNIQUEMENT : vérif des métriques 4,6★/500+ et des notes d'avis dans App Store Connect (laissées telles quelles).
- **Climbr** — carnet de bloc en salle (Sports), app d'Athanor Studio en cours de soumission (V1, septembre 2026). Pas encore de lien App Store : carte « Coming Soon » sur l'index, cliquable vers `/climbr`.
  - Page dédiée : `/climbr` (dossier `climbr/`), **français uniquement** — l'app est en français. Sections : navbar / hero (titre « Ton suivi de bloc, en un clin d'œil. », trio de vrais écrans dans le vrai boîtier) / Fonctions (4 cartes = les 4 titres des captures App Store) / Comment ça marche (3 gestes) / CTA sombre (mail) / Support (`#support`) / footer.
  - Sert d'**URL marketing** (`/climbr/`) et d'**URL d'assistance** (`/climbr/#support`) dans App Store Connect ; la politique de confidentialité reste `/privacy.html`.
  - Quand l'app sort : remplacer les deux `.store-badge.soon` par un lien App Store, et sur l'index remplacer le `status-badge` par les métriques comme Healthy Guru.
  - Les textes viennent de la fiche App Store (nom « Climbr – Progression Escalade », sous-titre « Scanne ton bloc avec une photo »). Tutoiement, comme Healthy Guru.
- **Clash List** — Quiz Game, "Challenge your friends in 45-second word duels."
  - Pas encore lancée. Carte affiche un badge `.status-badge` "Coming Soon" à la place des `app-metrics` + `app-links`. Quand l'app sortira, remplacer le `<span class="status-badge">` par les blocs métriques + store comme Healthy Guru.

## Contact
- Fondateur : Guillaume — guillaume@athanor-studio.io

## Notes / pièges connus
- Pas de backend : le formulaire ouvre le client mail via `mailto:`. Formspree envisagé plus tard.
- Le site se positionne comme un studio qui build et scale **ses propres apps**, pas un prestataire de service.
- L'`index.html` original (simple logo + email) a été perdu puis reconstruit à partir du `styles.css` — d'où l'importance de garder `styles.css` cohérent comme source du design.
