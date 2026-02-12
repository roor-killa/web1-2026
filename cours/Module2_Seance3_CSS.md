# Module 2 : Stylisation CSS (5h total)
## Séances 3, 4 et 5 - CSS Fondamentaux, Layouts et Animations

---

# SÉANCE 3 : CSS Fondamentaux (2h - 20min CI + 1h40 TP)

## 📋 COURS THÉORIQUE (20min)

### 1. Introduction à CSS (5min)

**CSS = Cascading Style Sheets**
```css
/* Anatomie d'une règle CSS */
selecteur {
    propriete: valeur;
    autre-propriete: autre-valeur;
}
```

**3 façons d'intégrer CSS :**
```html
<!-- 1. CSS inline (à éviter) -->
<p style="color: blue;">Texte bleu</p>

<!-- 2. CSS interne (pour petits projets) -->
<style>
    p { color: blue; }
</style>

<!-- 3. CSS externe (recommandé) -->
<link rel="stylesheet" href="css/styles.css">
```

---

### 2. Sélecteurs CSS (10min)

```css
/* Sélecteur d'élément */
p { color: black; }

/* Sélecteur de classe */
.texte-important { font-weight: bold; }

/* Sélecteur d'ID (unique) */
#titre-principal { font-size: 2rem; }

/* Sélecteur descendant */
article p { line-height: 1.5; }

/* Sélecteur enfant direct */
nav > ul { margin: 0; }

/* Pseudo-classes */
a:hover { color: red; }
input:focus { border-color: blue; }
li:first-child { font-weight: bold; }

/* Pseudo-éléments */
p::first-line { font-variant: small-caps; }
h2::before { content: "→ "; }

/* Sélecteurs d'attribut */
input[type="email"] { border-color: green; }
a[href^="https"] { color: green; }
```

---

### 3. Box Model (5min)

```
┌─────────────────────────────────────┐
│          MARGIN (transparent)        │
│  ┌───────────────────────────────┐  │
│  │     BORDER (bordure)          │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │   PADDING (espacement)  │  │  │
│  │  │  ┌───────────────────┐  │  │  │
│  │  │  │   CONTENT         │  │  │  │
│  │  │  │   (contenu)       │  │  │  │
│  │  │  └───────────────────┘  │  │  │
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

```css
.box {
    /* Largeur totale = 300 + 20*2 + 2*2 + 10*2 = 364px */
    width: 300px;
    padding: 20px;
    border: 2px solid black;
    margin: 10px;
}

/* Alternative : box-sizing */
.box-modern {
    box-sizing: border-box; /* Largeur = 300px tout compris */
    width: 300px;
    padding: 20px;
    border: 2px solid black;
}
```

---

## 💻 TRAVAUX PRATIQUES (1h40)

### Exercice 1 : Créer la structure CSS (15min)

```
karibconnect/
├── css/
│   ├── reset.css          (normalisation)
│   ├── variables.css      (couleurs, tailles)
│   ├── layout.css         (structure générale)
│   ├── components.css     (composants réutilisables)
│   └── pages.css          (styles spécifiques pages)
├── index.html
└── ajouter-commerce.html
```

**1. Créer `css/reset.css` :**
```css
/* Reset CSS minimal */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html {
    font-size: 16px;
    line-height: 1.5;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
    color: #333;
    background-color: #fff;
}

img {
    max-width: 100%;
    height: auto;
    display: block;
}

a {
    text-decoration: none;
    color: inherit;
}

button {
    font-family: inherit;
    cursor: pointer;
}
```

**2. Créer `css/variables.css` :**
```css
:root {
    /* Couleurs principales - Palette caribéenne */
    --color-primary: #00A9E0;        /* Bleu lagon */
    --color-secondary: #FF6B35;      /* Corail */
    --color-accent: #FFD23F;         /* Soleil */
    
    /* Couleurs neutres */
    --color-dark: #1A1A1A;
    --color-gray: #6B7280;
    --color-light-gray: #F3F4F6;
    --color-white: #FFFFFF;
    
    /* Couleurs sémantiques */
    --color-success: #10B981;
    --color-warning: #F59E0B;
    --color-error: #EF4444;
    --color-info: #3B82F6;
    
    /* Typographie */
    --font-base: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    --font-heading: 'Poppins', sans-serif;
    
    /* Tailles */
    --text-xs: 0.75rem;    /* 12px */
    --text-sm: 0.875rem;   /* 14px */
    --text-base: 1rem;     /* 16px */
    --text-lg: 1.125rem;   /* 18px */
    --text-xl: 1.25rem;    /* 20px */
    --text-2xl: 1.5rem;    /* 24px */
    --text-3xl: 1.875rem;  /* 30px */
    --text-4xl: 2.25rem;   /* 36px */
    
    /* Espacements */
    --space-xs: 0.25rem;   /* 4px */
    --space-sm: 0.5rem;    /* 8px */
    --space-md: 1rem;      /* 16px */
    --space-lg: 1.5rem;    /* 24px */
    --space-xl: 2rem;      /* 32px */
    --space-2xl: 3rem;     /* 48px */
    --space-3xl: 4rem;     /* 64px */
    
    /* Bordures */
    --radius-sm: 4px;
    --radius-md: 8px;
    --radius-lg: 12px;
    --radius-full: 9999px;
    
    /* Ombres */
    --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
    --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
    --shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.15);
    
    /* Transitions */
    --transition-fast: 150ms ease;
    --transition-base: 300ms ease;
    --transition-slow: 500ms ease;
    
    /* Largeurs max */
    --container-sm: 640px;
    --container-md: 768px;
    --container-lg: 1024px;
    --container-xl: 1280px;
}
```

---

### Exercice 2 : Styliser le header et la navigation (30min)

**Créer `css/layout.css` :**

```css
/* Container principal */
.container {
    max-width: var(--container-xl);
    margin: 0 auto;
    padding: 0 var(--space-md);
}

/* Header */
header[role="banner"] {
    background: linear-gradient(135deg, var(--color-primary), #0080B3);
    color: var(--color-white);
    padding: var(--space-lg) 0;
    box-shadow: var(--shadow-md);
    position: sticky;
    top: 0;
    z-index: 1000;
}

header .logo h1 {
    font-family: var(--font-heading);
    font-size: var(--text-3xl);
    font-weight: 700;
    margin-bottom: var(--space-xs);
}

/* Navigation */
nav[role="navigation"] {
    margin-top: var(--space-md);
}

nav ul {
    list-style: none;
    display: flex;
    gap: var(--space-lg);
    flex-wrap: wrap;
}

nav a {
    color: var(--color-white);
    font-weight: 500;
    padding: var(--space-sm) var(--space-md);
    border-radius: var(--radius-md);
    transition: background-color var(--transition-base);
}

nav a:hover,
nav a:focus {
    background-color: rgba(255, 255, 255, 0.2);
}

nav a:focus {
    outline: 2px solid var(--color-white);
    outline-offset: 2px;
}

/* Section Hero */
.hero {
    background: linear-gradient(
        to bottom,
        rgba(0, 169, 224, 0.05),
        transparent
    );
    padding: var(--space-3xl) 0;
    text-align: center;
}

.hero h2 {
    font-size: var(--text-4xl);
    color: var(--color-dark);
    margin-bottom: var(--space-md);
    font-weight: 700;
}

.hero .sous-titre {
    font-size: var(--text-xl);
    color: var(--color-gray);
    margin-bottom: var(--space-xl);
}

/* Bouton CTA */
.cta-button {
    display: inline-block;
    background-color: var(--color-secondary);
    color: var(--color-white);
    padding: var(--space-md) var(--space-2xl);
    border-radius: var(--radius-lg);
    font-weight: 600;
    font-size: var(--text-lg);
    box-shadow: var(--shadow-lg);
    transition: all var(--transition-base);
}

.cta-button:hover {
    background-color: #E55A2A;
    transform: translateY(-2px);
    box-shadow: var(--shadow-xl);
}

/* Footer */
footer[role="contentinfo"] {
    background-color: var(--color-dark);
    color: var(--color-white);
    padding: var(--space-2xl) 0 var(--space-lg);
    margin-top: var(--space-3xl);
}

footer h3 {
    color: var(--color-accent);
    margin-bottom: var(--space-md);
}

footer a {
    color: var(--color-light-gray);
    transition: color var(--transition-fast);
}

footer a:hover {
    color: var(--color-accent);
}

footer small {
    display: block;
    text-align: center;
    margin-top: var(--space-xl);
    padding-top: var(--space-lg);
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    color: var(--color-gray);
}
```

---

### Exercice 3 : Cartes de commerces (30min)

**Créer `css/components.css` :**

```css
/* Grille de commerces */
.commerce-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: var(--space-xl);
    margin-top: var(--space-xl);
}

/* Carte commerce */
.commerce-card {
    background-color: var(--color-white);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-md);
    overflow: hidden;
    transition: all var(--transition-base);
    border: 1px solid var(--color-light-gray);
}

.commerce-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-xl);
    border-color: var(--color-primary);
}

.commerce-card header {
    background: linear-gradient(135deg, var(--color-primary), #0080B3);
    color: var(--color-white);
    padding: var(--space-lg);
}

.commerce-card h3 {
    font-size: var(--text-xl);
    margin-bottom: var(--space-sm);
}

.commerce-card .categorie {
    background-color: rgba(255, 255, 255, 0.2);
    padding: var(--space-xs) var(--space-sm);
    border-radius: var(--radius-sm);
    font-size: var(--text-sm);
    display: inline-block;
}

.commerce-info {
    padding: var(--space-lg);
}

.commerce-info p {
    margin-bottom: var(--space-md);
    line-height: 1.6;
}

.commerce-info strong {
    color: var(--color-dark);
    font-weight: 600;
}

.commerce-actions {
    padding: var(--space-lg);
    background-color: var(--color-light-gray);
    display: flex;
    gap: var(--space-md);
}

/* Boutons */
.btn-details,
.btn-favoris {
    flex: 1;
    padding: var(--space-sm) var(--space-md);
    border-radius: var(--radius-md);
    font-weight: 500;
    text-align: center;
    transition: all var(--transition-base);
    border: none;
}

.btn-details {
    background-color: var(--color-primary);
    color: var(--color-white);
}

.btn-details:hover {
    background-color: #0080B3;
}

.btn-favoris {
    background-color: var(--color-white);
    color: var(--color-gray);
    border: 1px solid var(--color-gray);
}

.btn-favoris:hover {
    background-color: var(--color-accent);
    color: var(--color-dark);
    border-color: var(--color-accent);
}

/* Catégories */
.categorie-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: var(--space-lg);
    list-style: none;
    margin-top: var(--space-lg);
}

.categorie-grid a {
    display: block;
    text-align: center;
    padding: var(--space-xl);
    background-color: var(--color-white);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-sm);
    transition: all var(--transition-base);
}

.categorie-grid a:hover {
    transform: scale(1.05);
    box-shadow: var(--shadow-md);
}

.categorie-grid .icone {
    font-size: 3rem;
    display: block;
    margin-bottom: var(--space-md);
}

.categorie-grid strong {
    display: block;
    font-size: var(--text-lg);
    color: var(--color-dark);
    margin-bottom: var(--space-xs);
}

.categorie-grid data {
    color: var(--color-gray);
    font-size: var(--text-sm);
}
```

---

### Exercice 4 : Formulaires stylisés (25min)

```css
/* Formulaires */
.search-form,
form {
    background-color: var(--color-white);
    padding: var(--space-xl);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-md);
    margin: var(--space-xl) 0;
}

fieldset {
    border: 1px solid var(--color-light-gray);
    border-radius: var(--radius-md);
    padding: var(--space-lg);
    margin-bottom: var(--space-lg);
}

legend {
    font-weight: 600;
    color: var(--color-dark);
    padding: 0 var(--space-sm);
}

.form-group {
    margin-bottom: var(--space-lg);
}

label {
    display: block;
    font-weight: 500;
    color: var(--color-dark);
    margin-bottom: var(--space-sm);
}

input[type="text"],
input[type="email"],
input[type="tel"],
input[type="url"],
input[type="search"],
input[type="number"],
input[type="date"],
input[type="time"],
select,
textarea {
    width: 100%;
    padding: var(--space-md);
    border: 2px solid var(--color-light-gray);
    border-radius: var(--radius-md);
    font-size: var(--text-base);
    transition: all var(--transition-base);
}

input:focus,
select:focus,
textarea:focus {
    outline: none;
    border-color: var(--color-primary);
    box-shadow: 0 0 0 3px rgba(0, 169, 224, 0.1);
}

input:invalid {
    border-color: var(--color-error);
}

/* Range slider */
input[type="range"] {
    width: 100%;
    height: 8px;
    border-radius: var(--radius-full);
    background: var(--color-light-gray);
    outline: none;
}

input[type="range"]::-webkit-slider-thumb {
    appearance: none;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: var(--color-primary);
    cursor: pointer;
}

/* Checkboxes et radios */
.checkbox-group,
.radio-group {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
}

input[type="checkbox"],
input[type="radio"] {
    margin-right: var(--space-sm);
    width: 18px;
    height: 18px;
}

/* Boutons de formulaire */
.form-actions {
    display: flex;
    gap: var(--space-md);
    margin-top: var(--space-xl);
}

.btn-primary,
.btn-secondary {
    padding: var(--space-md) var(--space-xl);
    border-radius: var(--radius-md);
    font-weight: 600;
    font-size: var(--text-base);
    border: none;
    cursor: pointer;
    transition: all var(--transition-base);
}

.btn-primary {
    background-color: var(--color-primary);
    color: var(--color-white);
    flex: 1;
}

.btn-primary:hover {
    background-color: #0080B3;
    transform: translateY(-1px);
    box-shadow: var(--shadow-md);
}

.btn-secondary {
    background-color: transparent;
    color: var(--color-gray);
    border: 2px solid var(--color-light-gray);
}

.btn-secondary:hover {
    border-color: var(--color-gray);
    background-color: var(--color-light-gray);
}

/* Messages d'aide */
small {
    display: block;
    color: var(--color-gray);
    font-size: var(--text-sm);
    margin-top: var(--space-xs);
}
```

---

## ✅ Checkpoints TP Séance 3

- [ ] Variables CSS créées et utilisées
- [ ] Header sticky avec navigation fonctionnelle
- [ ] Cartes commerces avec hover effects
- [ ] Formulaire stylisé avec focus states
- [ ] Code CSS organisé en fichiers séparés

---

# SÉANCE 4 : Layouts Modernes (2h - 15min CI + 1h45 TP)

## 📋 COURS THÉORIQUE (15min)

### 1. Flexbox (7min)

```css
/* Container flex */
.flex-container {
    display: flex;
    
    /* Direction */
    flex-direction: row | column | row-reverse | column-reverse;
    
    /* Retour à la ligne */
    flex-wrap: nowrap | wrap | wrap-reverse;
    
    /* Alignement horizontal (axe principal) */
    justify-content: flex-start | center | flex-end | space-between | space-around | space-evenly;
    
    /* Alignement vertical (axe secondaire) */
    align-items: stretch | flex-start | center | flex-end | baseline;
    
    /* Espacement */
    gap: 1rem;
}

/* Élément flex */
.flex-item {
    flex: 1; /* flex-grow: 1, flex-shrink: 1, flex-basis: 0 */
    flex-basis: 300px; /* largeur de base */
}
```

### 2. Grid (8min)

```css
/* Container grid */
.grid-container {
    display: grid;
    
    /* Définir les colonnes */
    grid-template-columns: 200px 1fr 200px;
    grid-template-columns: repeat(3, 1fr);
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    
    /* Définir les lignes */
    grid-template-rows: auto 1fr auto;
    
    /* Espacement */
    gap: 1rem;
    column-gap: 2rem;
    row-gap: 1rem;
}

/* Élément grid */
.grid-item {
    /* Placement */
    grid-column: 1 / 3; /* de la colonne 1 à 3 */
    grid-row: 2 / 4;
    
    /* Ou par nom de zone */
    grid-area: header;
}

/* Template areas */
.layout {
    display: grid;
    grid-template-areas:
        "header header header"
        "sidebar main main"
        "footer footer footer";
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
```

---

## 💻 TRAVAUX PRATIQUES (1h45)

### Exercice 1 : Layout responsive avec Grid (40min)

**Créer un layout adaptatif pour la page d'accueil :**

```css
/* Layout principal */
main {
    display: grid;
    grid-template-columns: 1fr;
    gap: var(--space-2xl);
    max-width: var(--container-xl);
    margin: 0 auto;
    padding: var(--space-xl);
}

/* Section avec sidebar */
.section-with-sidebar {
    display: grid;
    grid-template-columns: 1fr;
    gap: var(--space-xl);
}

/* Responsive : tablette et desktop */
@media (min-width: 768px) {
    .section-with-sidebar {
        grid-template-columns: 300px 1fr;
    }
    
    .commerce-grid {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media (min-width: 1024px) {
    .commerce-grid {
        grid-template-columns: repeat(3, 1fr);
    }
    
    .categorie-grid {
        grid-template-columns: repeat(4, 1fr);
    }
}

/* Footer en 3 colonnes */
footer[role="contentinfo"] {
    display: grid;
    grid-template-columns: 1fr;
    gap: var(--space-xl);
    max-width: var(--container-xl);
    margin: 0 auto;
    padding: var(--space-2xl) var(--space-md);
}

@media (min-width: 768px) {
    footer[role="contentinfo"] {
        grid-template-columns: repeat(3, 1fr);
    }
}
```

---

### Exercice 2 : Navigation flexbox (30min)

```css
/* Navigation responsive */
nav ul {
    display: flex;
    flex-direction: column;
    gap: var(--space-sm);
}

@media (min-width: 768px) {
    nav ul {
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }
}

/* Menu burger pour mobile */
.menu-toggle {
    display: block;
    background: none;
    border: none;
    color: var(--color-white);
    font-size: var(--text-2xl);
    cursor: pointer;
}

@media (min-width: 768px) {
    .menu-toggle {
        display: none;
    }
}

/* Navigation cachée sur mobile */
.nav-hidden {
    display: none;
}

@media (min-width: 768px) {
    .nav-hidden {
        display: flex;
    }
}
```

---

### Exercice 3 : Galerie d'images responsive (35min)

```css
/* Galerie photo Grid auto-responsive */
.photo-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: var(--space-md);
    padding: var(--space-xl);
}

.photo-gallery img {
    width: 100%;
    height: 250px;
    object-fit: cover;
    border-radius: var(--radius-md);
    transition: transform var(--transition-base);
}

.photo-gallery img:hover {
    transform: scale(1.05);
}

/* Layout complexe : Masonry-like */
.masonry-grid {
    columns: 1;
    column-gap: var(--space-md);
}

@media (min-width: 640px) {
    .masonry-grid {
        columns: 2;
    }
}

@media (min-width: 1024px) {
    .masonry-grid {
        columns: 3;
    }
}

.masonry-item {
    break-inside: avoid;
    margin-bottom: var(--space-md);
}
```

---

# SÉANCE 5 : CSS Avancé & Animations (1h - 100% TP)

## 💻 TRAVAUX PRATIQUES (1h)

### Exercice 1 : Animations et transitions (30min)

```css
/* Animation d'apparition */
@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.commerce-card {
    animation: fadeIn 0.5s ease-out;
    animation-fill-mode: backwards;
}

/* Délai progressif pour chaque carte */
.commerce-card:nth-child(1) { animation-delay: 0s; }
.commerce-card:nth-child(2) { animation-delay: 0.1s; }
.commerce-card:nth-child(3) { animation-delay: 0.2s; }

/* Animation de pulsation */
@keyframes pulse {
    0%, 100% {
        transform: scale(1);
    }
    50% {
        transform: scale(1.05);
    }
}

.cta-button {
    animation: pulse 2s infinite;
}

.cta-button:hover {
    animation: none;
}

/* Skeleton loading */
@keyframes shimmer {
    0% {
        background-position: -1000px 0;
    }
    100% {
        background-position: 1000px 0;
    }
}

.skeleton {
    background: linear-gradient(
        90deg,
        #f0f0f0 25%,
        #e0e0e0 50%,
        #f0f0f0 75%
    );
    background-size: 1000px 100%;
    animation: shimmer 2s infinite;
}

/* Transition de couleur au scroll */
header {
    transition: background-color var(--transition-base);
}

header.scrolled {
    background-color: rgba(0, 169, 224, 0.95);
    backdrop-filter: blur(10px);
}
```

---

### Exercice 2 : Micro-interactions (30min)

```css
/* Badge notification avec animation */
.notification-badge {
    position: relative;
}

.notification-badge::after {
    content: attr(data-count);
    position: absolute;
    top: -8px;
    right: -8px;
    background-color: var(--color-error);
    color: white;
    border-radius: var(--radius-full);
    padding: 2px 6px;
    font-size: var(--text-xs);
    font-weight: 600;
    animation: bounce 0.5s ease;
}

@keyframes bounce {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.2); }
}

/* Tooltip */
[data-tooltip] {
    position: relative;
}

[data-tooltip]::before {
    content: attr(data-tooltip);
    position: absolute;
    bottom: 100%;
    left: 50%;
    transform: translateX(-50%) translateY(-8px);
    background-color: var(--color-dark);
    color: var(--color-white);
    padding: var(--space-sm) var(--space-md);
    border-radius: var(--radius-md);
    font-size: var(--text-sm);
    white-space: nowrap;
    opacity: 0;
    pointer-events: none;
    transition: opacity var(--transition-base), transform var(--transition-base);
}

[data-tooltip]:hover::before {
    opacity: 1;
    transform: translateX(-50%) translateY(-4px);
}

/* Loading spinner */
.spinner {
    width: 40px;
    height: 40px;
    border: 4px solid var(--color-light-gray);
    border-top-color: var(--color-primary);
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
}

@keyframes spin {
    to { transform: rotate(360deg); }
}

/* Effet de ripple sur les boutons */
.btn-ripple {
    position: relative;
    overflow: hidden;
}

.btn-ripple::after {
    content: "";
    position: absolute;
    top: 50%;
    left: 50%;
    width: 0;
    height: 0;
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.5);
    transform: translate(-50%, -50%);
    transition: width 0.6s, height 0.6s;
}

.btn-ripple:active::after {
    width: 300px;
    height: 300px;
}
```

---

## 📝 Livrables Module 2

1. **CSS complet** :
   - `reset.css`, `variables.css`, `layout.css`, `components.css`
   - Site entièrement stylisé et responsive
   - Au moins 5 animations différentes

2. **Commit Git** : `"Module 2: CSS complet - layouts et animations"`

3. **Documentation** :
   - Guide de style (couleurs, typographie)
   - Liste des composants réutilisables

---

## 🎯 Prochaine séance

**Module 3 - JavaScript : Interactivité**
- DOM manipulation
- Événements
- Filtres dynamiques
- API Fetch
