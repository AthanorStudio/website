# Athanor Studio Website

Site vitrine d'Athanor Studio (app publishing company).

## Stack
- HTML/CSS statique pur, pas de framework, pas de build
- Police : **Inter** seule (300/400/500/600), Google Fonts. Un display serif (Marcellus) avait été essayé le 5 septembre 2026 puis retiré le jour même — le premium passe par la graisse et le tracking, pas par un serif.
- Hébergement : GitHub Pages, domaine via `CNAME`
- Repo : https://github.com/AthanorStudio/website (branche `main`)

## Fichiers
- `index.html` — landing page Athanor Studio (navbar, hero, practice, apps, company, contact, footer)
- `styles.css` — design system du site studio (dark éditorial, tokens, composants, responsive)
- `privacy.html` — politique de confidentialité
- `healthyguru/index.html` + `healthyguru/styles.css` — landing page dédiée à l'app Healthy Guru, accessible via `/healthyguru` (light theme + **accent vert frais**, charte propre distincte du studio). `healthyguru/screen-*.webp` = screenshots réels de l'app (mockups + CTA).
- `climbr/index.html` + `climbr/styles.css` — page dédiée à l'app Climbr, accessible via `/climbr` (thème **sable / encre / terre brûlée**, la palette « Grès » de l'app). `climbr/screen-*.webp` = vrais écrans de l'app, `climbr/iphone.webp` = le boîtier iPhone 17 Pro Max (capturé dans le Simulateur de Xcode, écran transparent) posé par-dessus chaque écran en CSS.
- **Marque** — `athanor-mark.svg` (source vectorielle), `athanor-mark.png` (512px crème, transparent), `athanor-mark-ink.svg` + `athanor-mark-ink.png` (version encre pour fonds clairs), `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` (180px, tuile sombre). Voir « Logo » plus bas.
- `athanorstudio_logo.png` — **ancien** logo (bitmap opaque, wordmark gravé dedans). N'est plus référencé par aucune page ; conservé comme archive.
- `healthyguru_icon.png`, `clashlist_icon.png`, `climbr_icon.png` — icônes des apps
- `CNAME` — domaine GitHub Pages
- `og-image.png` (racine, thème sombre studio) + `healthyguru/og-image.png` (thème vert app) + `climbr/og-image.png` (sable, généré avec Pillow) — images de partage 1200×630, générées via une carte HTML rendue en Chrome headless puis redimensionnée avec `sips`. Balises Open Graph/Twitter + `canonical` + `theme-color` dans les deux `<head>`.
- `robots.txt` + `sitemap.xml` — SEO de base (racine).

## Logo
La marque est **« l'œuf dans le fourneau »** (refonte du 5 septembre 2026) : un triangle en contour — le signe alchimique du feu, donc l'athanor — avec un disque plein suspendu dans sa moitié basse, l'œuf philosophique. Géométrie exacte, en 100 unités :
```
triangle : M50 9 L91 87 L9 87 Z   (contour, stroke-width 3.2, linejoin miter)
disque   : cx 50, cy 63, r 11     (plein)
```
- **Dans les pages HTML**, la marque est un `<symbol id="mark">` inline en haut du `<body>`, appelé via `<svg class="mark"><use href="#mark"/></svg>`. Elle hérite de `currentColor` — c'est ce qui permet de la teinter (crème dans la navbar, `opacity .5` en grand dans Company).
- **Le wordmark « ATHANOR STUDIO » est du texte**, pas une image : Inter 500, `text-transform: uppercase`, `letter-spacing: .24em`.
- **Épaisseurs optiques** : les icônes petites utilisent un trait ÉPAISSI (favicon `stroke-width: 8.5` + `r: 14`, apple-touch `5.6`/`12.5`). Ne pas se contenter de réduire le SVG 3.2 — il disparaît.
- Les PNG sont générés par un script Pillow (suréchantillonnage ×8 puis LANCZOS), pas par un export manuel : triangle extérieur rempli, triangle intérieur évidé, disque par-dessus. L'offset se fait par homothétie autour de l'incentre `(50, 62.23)`, rayon inscrit `24.77`.
- ⚠️ **Le crème `#f8eac1` est invisible sur fond clair.** Pour l'App Store, la presse ou tout fond papier, utiliser la version encre : `athanor-mark-ink.svg` / `athanor-mark-ink.png` (encre chaude `#17140f`, même géométrie). Le site n'utilise QUE la version crème — l'encre existe uniquement pour ce qu'on envoie à l'extérieur.
- Six directions avaient été proposées avant l'arbitrage (Ignis, Quadratura, Athanor, Sigillum, Gradus, Lumen) ; c'est « Athanor » qui a été retenue.

## Design system
- **Fond chaud, pas gris** : `--ink: #0b0a08` (page), `#121110` (section alternée), `#161412` (cartes). Le noir neutre `#0c0c0c` d'avant faisait paraître le crème terne — le noir chaud le fait lire comme de l'or.
- **Texte** : `--fg: #f4f1ea` (blanc chaud, jamais `#fff`), puis `--fg-soft` 60 % et `--fg-mute` 38 %.
- **Accent crème/or** : `#f8eac1` — réservé aux chiffres, à la marque et aux états de survol. Jamais un mot coloré au milieu d'un titre.
- **Les filets sont le dispositif structurant principal** (`--rule` à 10 %), pas les boîtes. Le seul bloc encadré du site, ce sont les deux cartes d'apps.
- **Typo, tout en Inter** : titres en 600 avec un tracking serré (`-0.03em`, et `-0.042em` sur le hero — c'est ce serrage qui fait le premium en sans-serif) ; corps en 300/400 ; labels et eyebrows en 500 capitales, `letter-spacing: .18em` (`.24em` pour le wordmark) ; chiffres en 600 + `font-variant-numeric: tabular-nums`.
- ⚠️ **L'échelle typo est calée pour Inter.** Inter a une hauteur d'x bien supérieure à celle d'un serif d'affichage : à corps égal il paraît plus gros. `--fs-display` plafonne donc à 4.5rem et `--fs-h2` à 2.5rem. Si un jour un serif revient, il faudra REMONTER ces valeurs, pas juste changer `--font-display`.
- Grain de film en `body::after` (turbulence SVG en data-URI, `opacity: .028`) — c'est ce qui empêche les aplats de paraître plastique.
- Animations fade-up au scroll, avec `html:not(.js) .fade-up { opacity: 1 }` : **si le JS ne tourne pas, le contenu reste visible** (l'ancienne version le laissait à `opacity: 0`).
- Breakpoints responsive : 1024px / 768px / 480px, plus un palier 400px pour resserrer les gouttières des métriques.

## Sections de l'index
(Refonte éditoriale du 5 septembre 2026 : la **mise en page** est nouvelle, mais **les textes sont ceux d'origine** — ils ont été restaurés après coup, à la demande. Tout est désormais **aligné à gauche**, plus rien n'est centré. Les ancres n'ont pas bougé : `#services`, `#apps`, `#company`, `#contact`.)
1. Navbar (marque SVG + wordmark texte + Services / Apps / Company / Contact + hamburger mobile). Le filet du bas n'apparaît qu'au scroll.
2. Hero — marque, titre « We build and scale apps. », sous-titre d'origine, `Get in Touch →`, puis un **rail de stats** séparé par des filets : 150k+ Installs / 4.6 App Store rating / 2024 Founded (seul ajout de contenu conservé).
3. Services (`#services`, fond `--ink-raise`) — label « Scale », titre « What We Do », puis **4 lignes `<dl>` séparées par des filets** (Transformation, Ownership, Data-Driven, Innovation). Ce ne sont plus des cartes, et les numéros 01–04 ont sauté : ce sont des facettes, pas une séquence. Le CSS s'appelle encore `.practice-row` / `.practice-term` / `.practice-def`.
4. Apps — label « Portfolio », titre « Our Apps », grille `auto-fit minmax(360px, 1fr)` avec deux cartes : Healthy Guru et Climbr (Clash List retirée de l'accueil le 4 septembre 2026, son icône reste dans le dépôt) :
   - Healthy Guru (4.6 ★, 500+ reviews, 150k+ installs) — carte cliquable (`<a class="app-card">`, la classe `app-card-link` a disparu à la refonte) vers `/healthyguru`. Métriques séparées par des filets verticaux, CTA "Learn more →" en bas. Le lien App Store n'est pas dans la carte (il est sur la page dédiée).
   - Climbr (Sports · Bouldering, badge "Coming Soon") — carte cliquable vers `/climbr`.
5. Company — grande marque à gauche (`opacity .5`), texte d'origine à droite sous le titre « Athanor Studio ». Le paragraphe parle du fourneau alchimique, ce qui tombe juste puisque le logo le représente.
6. Contact — « Get in Touch » + l'adresse mail en **lien discret** (`clamp(1.0625rem, 1.8vw, 1.375rem)`, soulignement animé au survol). Elle avait d'abord été posée en très grand corps (jusqu'à 38px) : elle concurrençait le titre de section juste au-dessus, elle a été ramenée à une taille de lien.
   - Le formulaire a été SUPPRIMÉ. Il était en `action="mailto:" method="post"` : un `mailto:` n'envoie rien, il ouvre au mieux un brouillon dans le client mail du visiteur, qu'il doit envoyer lui-même — donc il faut un client configuré (or la plupart des gens sont sur Gmail dans un onglet), il n'y a aucun retour ni validation, et `POST` est la variante la moins bien supportée des deux (`GET` passe les données dans l'URL, ce que les clients comprennent). Pour un vrai formulaire il faut un service tiers (Formspree, gratuit jusqu'à 50 messages/mois) — ça demande un compte côté Guillaume.
   - Le CSS `.contact-lede` et `.contact-meta` est resté en place, inutilisé, si jamais on veut rajouter du contenu ici.
7. Footer — marque + wordmark + tagline « Transforming apps into success stories. », colonnes Navigation et Legal, barre du bas (© + mail). Les anciens liens LinkedIn/Twitter en `href="#"` ont été retirés.

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
- **Climbr** — carnet de bloc en salle (Sports), app d'Athanor Studio **en ligne depuis le 10 septembre 2026** : https://apps.apple.com/fr/app/climbr-progression-escalade/id6803155208. Carte « Now on the App Store » sur l'index, cliquable vers `/climbr` ; pas encore de métriques (notes, avis) à afficher.
  - Page dédiée : `/climbr` (dossier `climbr/`), **français uniquement** — l'app est en français. Sections : navbar (bouton « Télécharger ») / hero (titre « Ton carnet de bloc. », sous-titre « Scanne ton bloc, note tes essais et suis ta progression. », trio de vrais écrans dans le vrai boîtier) / Fonctions (4 cartes) / Comment ça marche (3 gestes) / CTA sombre (App Store + mail, sans téléphone) / Support (`#support`, une seule carte) / footer.
  - **Le trio du hero reprend la couverture Instagram du 10 septembre 2026** : même boîtier trois fois, les côtés à `scale(0.8)` centrés verticalement sur le central, recouverts de 10 px seulement. ⚠️ À 86 % et recouverts d'un sixième, les côtés se lisaient comme des téléphones plus étroits — c'est ce qui a été refusé sur Instagram. Les posts et le script qui les rend sont dans `~/Desktop/Climbr/instagram/`.
  - **Réseaux de l'app** : https://www.instagram.com/climbr.application et https://www.tiktok.com/@climbr.application, dans le pied de page seulement (le Support ne garde que la carte « Nous écrire », choix du 10 septembre 2026).
  - **Mail de l'app : `climbr@athanor-studio.io`** (CTA et Support). Le studio, lui, est joignable sur `contact@athanor-studio.io` (index). `privacy.html` porte `climbr@athanor-studio.io` (choix du 10 septembre 2026). ⚠️ Sa section Climbr ne nomme PAS le fournisseur du modèle de détection — « our backend » seulement — et déclare Mixpanel et Tenjin, ajoutés à l'app le 9 septembre.
  - `climbr/og-image.png` est régénérée avec Pillow depuis les captures App Store (logo, titre, pastille « Disponible sur l'App Store », trio).
  - Sert d'**URL marketing** (`/climbr/`) et d'**URL d'assistance** (`/climbr/#support`) dans App Store Connect ; la politique de confidentialité reste `/privacy.html`.
  - Quand il y aura des avis : remplacer le `status-badge` de l'index par les métriques comme Healthy Guru.
  - Les textes viennent de la fiche App Store (nom « Climbr – Progression Escalade », sous-titre « Scanne ton bloc avec une photo »). Tutoiement, comme Healthy Guru.
- **Clash List** — Quiz Game, "Challenge your friends in 45-second word duels."
  - Pas encore lancée. Carte affiche un badge `.status-badge` "Coming Soon" à la place des `app-metrics` + `app-links`. Quand l'app sortira, remplacer le `<span class="status-badge">` par les blocs métriques + store comme Healthy Guru.

## Contact
- Fondateur : Guillaume — contact@athanor-studio.io (studio), climbr@athanor-studio.io (Climbr)

## Notes / pièges connus
- Pas de backend, et **plus de formulaire** : le contact se fait par un lien `mailto:` direct. Si un vrai formulaire est souhaité un jour, il faudra Formspree ou équivalent — un `<form action="mailto:">` ne marche pas.
- `privacy.html` partage `styles.css` et la même navbar/footer que l'index : **toute refonte du chrome doit être répercutée dans les deux fichiers** (ils ne partagent pas de template).
- L'`og-image.png` de la racine se régénère avec le pipeline « carte HTML → Chrome headless `--screenshot` en 2400×1260 → `sips -z 630 1200` ». Rendre en 2× puis réduire, sinon le texte bave.
- ⚠️ Chrome headless **clampe le viewport à 500 px minimum** sur macOS : une capture en `--window-size=390` rend la page à 500 px puis rogne à 390, ce qui donne une fausse impression de débordement. Pour vraiment mesurer, injecter une sonde `scrollWidth`/`getBoundingClientRect` et lire le résultat via `--dump-dom`.
- Le site se positionne comme un studio qui build et scale **ses propres apps**, pas un prestataire de service.
- L'`index.html` original (simple logo + email) a été perdu puis reconstruit à partir du `styles.css` — d'où l'importance de garder `styles.css` cohérent comme source du design.
