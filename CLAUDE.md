# Athanor Studio Website

Site vitrine d'Athanor Studio (app publishing company). Source de vérité du contexte projet : `memory.md`.

## Stack
- HTML/CSS statique pur, pas de framework, pas de build
- Police : Inter (Google Fonts)
- Hébergement : GitHub Pages, domaine via `CNAME`
- Repo : https://github.com/AthanorStudio/website (branche `main`)

## Fichiers
- `index.html` — landing page (navbar, hero, services, apps, company, contact, footer)
- `styles.css` — design system (tokens, composants, responsive)
- `privacy.html` — politique de confidentialité
- `athanorstudio_logo.png`, `healthyguru_icon.png` — assets
- `CNAME` — domaine GitHub Pages
- `memory.md` — contexte détaillé du projet (à lire en premier)

## Design system
- Thème sombre : `bg: #0c0c0c`
- Accent crème/or : `#f8eac1`
- Animations fade-up au scroll
- Breakpoints responsive : 1024px / 768px / 480px

## Sections de l'index
1. Navbar (logo + Services / Apps / Company / Contact + hamburger mobile)
2. Hero — "We build and scale apps."
3. Services — 4 value cards (Transformation, Ownership, Data-Driven, Innovation)
4. Apps — carte Healthy Guru (4.6 ★, 500+ reviews, 150k+ installs, lien App Store)
5. Company — storytelling Athanor (fondé en 2024, fourneau alchimique)
6. Contact — formulaire `mailto:` (pas de backend) → guillaume@athanor-studio.io
7. Footer

## App publiée
- **Healthy Guru** — nutrition/fitness IA, Health & Fitness
  - https://apps.apple.com/fr/app/healthy-guru/id6575388387

## Contact
- Fondateur : Guillaume — guillaume@athanor-studio.io

## Notes / pièges connus
- Pas de backend : le formulaire ouvre le client mail via `mailto:`. Formspree envisagé plus tard.
- Le site se positionne comme un studio qui build et scale **ses propres apps**, pas un prestataire de service.
- L'`index.html` original (simple logo + email) a été perdu puis reconstruit à partir du `styles.css` — d'où l'importance de garder `styles.css` cohérent comme source du design.
