# Athanor Studio Website - Project Memory

## Project
- **Site web** : Athanor Studio (app publishing company)
- **Repo GitHub** : https://github.com/AthanorStudio/website
- **Branche** : main
- **Hébergement** : GitHub Pages (CNAME configuré)
- **Stack** : HTML/CSS statique, pas de framework JS
- **Police** : Inter (Google Fonts)

## Fichiers
- `index.html` — page principale (landing page complète)
- `styles.css` — design system complet (tokens, composants, responsive)
- `privacy.html` — page de politique de confidentialité
- `healthyguru_icon.png` — icone de l'app Healthy Guru (téléchargée depuis l'App Store)
- `athanorstudio_logo.png` — logo Athanor Studio
- `CNAME` — configuration domaine GitHub Pages

## Structure du site (index.html)
1. **Navbar** — logo + liens (Services, Apps, Company, Contact) + hamburger mobile
2. **Hero** — titre "We build and scale apps.", sous-titre, bouton CTA
3. **Services (What We Do)** — 4 value cards en grille 2x2 :
   - Transformation
   - Ownership
   - Data-Driven
   - Innovation
   - Description : "We built our own tools and methodology to scale apps."
4. **Apps (Portfolio)** — carte Healthy Guru avec icone, métriques (4.6 rating, 500+ reviews, 150k+ installs), lien App Store
5. **Company** — storytelling Athanor (fondé en 2024, inspiration du fourneau alchimique)
6. **Contact** — formulaire (mailto:, pas de backend) + email guillaume@athanor-studio.io
7. **Footer** — logo, navigation, lien privacy

## App publiée
- **Healthy Guru** — app nutrition/fitness IA
  - App Store : https://apps.apple.com/fr/app/healthy-guru/id6575388387
  - Catégorie : Health & Fitness
  - Rating : 4.6, 500+ reviews, 150k+ installs
  - Développeur : Athanor Studio

## Design
- Thème sombre (bg: #0c0c0c)
- Accent couleur crème/or (#f8eac1)
- Animations fade-up au scroll
- Responsive (breakpoints: 1024px, 768px, 480px)

## Contact
- Email : guillaume@athanor-studio.io
- Fondateur : Guillaume

## Notes
- Le formulaire de contact utilise mailto: (ouvre le client mail). Pas de backend pour l'instant. Formspree envisagé pour plus tard.
- Le fichier index.html original (simple logo + email) a été perdu et reconstruit à partir du styles.css
- Le site parle d'Athanor comme un studio qui build et scale ses propres apps (pas un service pour d'autres)
