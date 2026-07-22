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
- `healthyguru/index.html` + `healthyguru/styles.css` — landing page dédiée à l'app Healthy Guru, accessible via `/healthyguru` (light theme + accent crème)
- `athanorstudio_logo.png`, `healthyguru_icon.png`, `clashlist_icon.png` — assets
- `CNAME` — domaine GitHub Pages

## Design system
- Thème sombre : `bg: #0c0c0c`
- Accent crème/or : `#f8eac1`
- Animations fade-up au scroll
- Breakpoints responsive : 1024px / 768px / 480px

## Sections de l'index
1. Navbar (logo + Services / Apps / Company / Contact + hamburger mobile)
2. Hero — "We build and scale apps."
3. Services — 4 value cards (Transformation, Ownership, Data-Driven, Innovation)
4. Apps — grille `auto-fit minmax(340px, 1fr)` avec deux cartes :
   - Healthy Guru (4.6 ★, 500+ reviews, 150k+ installs) — carte cliquable (`<a class="app-card app-card-link">`) qui mène vers `/healthyguru`. CTA "Learn more →" en bas de carte. Le lien App Store n'est plus dans la carte (il est sur la page dédiée).
   - Clash List (Quiz Game, badge "Coming Soon" — pas encore de métriques ni de lien store)
5. Company — storytelling Athanor (fondé en 2024, fourneau alchimique)
6. Contact — titre seul (sous-titre retiré) + formulaire `mailto:` (pas de backend) → guillaume@athanor-studio.io
7. Footer

## Apps
- **Healthy Guru** — nutrition/fitness IA, Health & Fitness
  - https://apps.apple.com/fr/app/healthy-guru/id6575388387
  - Page dédiée : `/healthyguru` (dossier `healthyguru/`, light theme + **accent vert frais `#34b45a`** sur fonds mints doux, pour matcher l'app HG ; étoiles de notation en ambré `--star: #f5b301`). Design inspiré de solaia.app + micron-app.com. NB : cette page a sa PROPRE charte (verte), distincte du site studio racine (crème/or).
  - **Bilingue FR/EN** : détection auto via `navigator.language` (préfixe `fr` → français, sinon anglais) + toggle manuel `.lang-toggle` dans la navbar, choix mémorisé en `localStorage` (`hg-lang`). Tout le contenu traduisible porte un attribut `data-i18n="clé"` ; le dictionnaire `I18N = { en, fr }` est dans le `<script>` en bas de `index.html`. Pour éditer un texte, modifier la valeur dans les DEUX langues (les valeurs peuvent contenir du HTML inline, elles sont injectées via `innerHTML`). `<title>` et meta description sont aussi traduits.
  - Sections : navbar (logo HG + How it works / Features / Reviews / FAQ + toggle langue + Download) → Hero (headline + sous-titre + bouton App Store + ligne social proof + **chips de confiance** `.hero-trust` [Sans pub / Sans saisie manuelle / Confidentiel] + **trio de mockups iPhone décalés**) → **Comparison** (`.compare` : carte blanche "Les trackers basiques" ✕ vs carte noire "Healthy Guru" ✓ — inspirée de micron-app.com) → How it works (**stepper** façon micron-app : 3 cercles numérotés `.step-badge` + label "Étape X" `.step-label` + traits de liaison `.step::after`, centré, sans cartes) → Features (**4 cards** avec icône emoji : Plan sur mesure 🎯 / Suivi nutritionnel ultra-précis 📸 / Suivi d'activité 🏃⌚ / Suivi de progression 📈 — grille 2×2) → Reviews (titre + **ligne de note** `.reviews-rating` [⭐ 4.6 · 500+ avis · 150k+ installs, cliquable → App Store] + **3 témoignages** `<figure>` — note et avis regroupés dans UNE section façon micron-app, plus de bandeau dark séparé) → FAQ (5 questions `<details>`) → Final CTA → Footer.
  - **Mockups hero** = 3 faux iPhones (`.phone-left`/`.phone-center`/`.phone-right`) avec de **vrais screenshots** de l'app en WebP optimisé (~15-25 Ko chacun) : `screen-meal.webp` (gauche, détail repas scanné), `screen-home.webp` (centre, dashboard/anneau calories), `screen-recipes.webp` (droite, recettes). Sources originales : `~/Downloads/IMG_1045/1047/1043.PNG`, redimensionnées à 620px de large via `sips` puis encodées en WebP via `cwebp -q 78`. Pour mettre à jour un écran : refaire le même pipeline et écraser le `.webp`.
  - **⚠️ Positionnement / wording (important)** : l'app propose **4 façons de logger un repas** — scan photo IA, scan code-barres, base de données nutritionnelle, saisie manuelle. NE PAS réduire le discours au seul scan photo (ça donne une fausse impression d'imprécision). Toujours mettre en avant la **complétude** (4 méthodes) + la **précision** (micronutriments détaillés, valeurs ajustables, bases de données validées, recettes détaillées). Le hero est volontairement élargi ("Know exactly what you eat / Down to the micronutrient", pas centré photo). La colonne "Les trackers basiques" de la comparaison = saisie manuelle uniquement / calories seules / pas de micros — c'est ce que HG dépasse.
  - **Témoignages** = vrais avis App Store repris (Beyrima « Au top », Alexaa A, Millenium Otaku), traduits en EN dans le dictionnaire. Les originaux FR sont verbatim.
  - **Statut** : refonte façon solaia faite (bilingue + trio mockups avec vrais screenshots + science + vrais avis). Reste : review finale du contenu + balises OG/SEO + vérif métriques/notes. Ne pas considérer comme finale.
- **Clash List** — Quiz Game, "Challenge your friends in 45-second word duels."
  - Pas encore lancée. Carte affiche un badge `.status-badge` "Coming Soon" à la place des `app-metrics` + `app-links`. Quand l'app sortira, remplacer le `<span class="status-badge">` par les blocs métriques + store comme Healthy Guru.

## Contact
- Fondateur : Guillaume — guillaume@athanor-studio.io

## Notes / pièges connus
- Pas de backend : le formulaire ouvre le client mail via `mailto:`. Formspree envisagé plus tard.
- Le site se positionne comme un studio qui build et scale **ses propres apps**, pas un prestataire de service.
- L'`index.html` original (simple logo + email) a été perdu puis reconstruit à partir du `styles.css` — d'où l'importance de garder `styles.css` cohérent comme source du design.
