# Module 4 : NextJS & Déploiement (6h total)
## Séances 9, 10 et 11 - React/NextJS, Architecture et Production

---

# SÉANCE 9 : Introduction NextJS (2h - 30min CI + 1h30 TP)

## 📋 COURS THÉORIQUE (30min)

### 1. React en 10 minutes (10min)

**Concepts clés :**
```jsx
// Composant React (fonction)
function MonComposant() {
    return <h1>Hello World!</h1>;
}

// JSX = HTML dans JavaScript
const element = <div className="card">Bonjour</div>;

// Props (propriétés)
function Carte({ titre, description }) {
    return (
        <div>
            <h2>{titre}</h2>
            <p>{description}</p>
        </div>
    );
}

// Utilisation
<Carte titre="KaribConnect" description="Commerces locaux" />
```

**useState (état) :**
```jsx
import { useState } from 'react';

function Compteur() {
    const [count, setCount] = useState(0);
    
    return (
        <div>
            <p>Compteur: {count}</p>
            <button onClick={() => setCount(count + 1)}>
                Incrémenter
            </button>
        </div>
    );
}
```

---

### 2. NextJS App Router (15min)

**Structure d'un projet NextJS 14 :**
```
karibconnect-next/
├── app/
│   ├── layout.js          # Layout racine
│   ├── page.js            # Page d'accueil
│   ├── commerces/
│   │   ├── page.js        # Liste des commerces
│   │   └── [id]/
│   │       └── page.js    # Détail d'un commerce
│   └── ajouter/
│       └── page.js        # Formulaire d'ajout
├── components/
│   ├── Header.js
│   ├── CommerceCard.js
│   └── SearchForm.js
├── public/
│   └── images/
├── lib/
│   └── data.js            # Données et utilitaires
└── package.json
```

**Routing automatique :**
- `app/page.js` → `/`
- `app/commerces/page.js` → `/commerces`
- `app/commerces/[id]/page.js` → `/commerces/1`, `/commerces/2`...

**Server vs Client Components :**
```jsx
// Server Component (par défaut)
// S'exécute côté serveur
export default async function Page() {
    const data = await fetch('https://api.example.com/data');
    return <div>{data}</div>;
}

// Client Component (interactif)
'use client'; // Directive obligatoire

import { useState } from 'react';

export default function InteractiveButton() {
    const [clicked, setClicked] = useState(false);
    return <button onClick={() => setClicked(true)}>Cliquez</button>;
}
```

---

### 3. Différences avec le HTML/JS classique (5min)

| HTML/JS Classique | NextJS/React |
|-------------------|--------------|
| Manipulation DOM directe | Déclaratif (état → UI) |
| `document.querySelector()` | Props et State |
| Fichiers HTML séparés | Composants JSX |
| Plusieurs fichiers JS | Modules ES6 organisés |
| Déploiement manuel | Build automatique |

---

## 💻 TRAVAUX PRATIQUES (1h30)

### Exercice 1 : Setup NextJS (20min)

```bash
# Créer un nouveau projet NextJS
npx create-next-app@latest karibconnect-next

# Options recommandées :
# ✓ TypeScript? No
# ✓ ESLint? Yes
# ✓ Tailwind CSS? No (on utilise nos CSS)
# ✓ src/ directory? No
# ✓ App Router? Yes
# ✓ Import alias? Yes (@/*)

cd karibconnect-next

# Installer les dépendances
npm install

# Lancer le serveur de développement
npm run dev

# Ouvrir http://localhost:3000
```

**Structure de base créée :**
```
karibconnect-next/
├── app/
│   ├── favicon.ico
│   ├── globals.css
│   ├── layout.js
│   └── page.js
├── public/
├── .gitignore
├── next.config.js
├── package.json
└── README.md
```

**Nettoyer le projet :**
1. Supprimer le contenu de `app/page.js`
2. Vider `app/globals.css`
3. Copier nos CSS existants dans `app/styles/`

---

### Exercice 2 : Migration du layout (35min)

**Créer `app/layout.js` :**
```jsx
import './globals.css';
import './styles/reset.css';
import './styles/variables.css';
import './styles/layout.css';
import './styles/components.css';

export const metadata = {
    title: 'KaribConnect - Commerces de Martinique',
    description: 'Découvrez les meilleurs commerces locaux de Martinique',
};

export default function RootLayout({ children }) {
    return (
        <html lang="fr">
            <body>
                <Header />
                <main>{children}</main>
                <Footer />
            </body>
        </html>
    );
}

function Header() {
    return (
        <header role="banner">
            <div className="container">
                <div className="logo">
                    <h1>🌴 KaribConnect</h1>
                    <p>Votre guide des commerces martiniquais</p>
                </div>
                
                <nav role="navigation" aria-label="Navigation principale">
                    <ul>
                        <li><a href="/">Accueil</a></li>
                        <li><a href="/commerces">Commerces</a></li>
                        <li><a href="/ajouter">Ajouter</a></li>
                        <li><a href="/favoris">Favoris</a></li>
                    </ul>
                </nav>
            </div>
        </header>
    );
}

function Footer() {
    return (
        <footer role="contentinfo">
            <div className="container">
                <section>
                    <h3>À propos</h3>
                    <p>Projet étudiant de l'Université des Antilles</p>
                </section>
                
                <section>
                    <h3>Contact</h3>
                    <address>
                        Email: <a href="mailto:contact@karibconnect.fr">contact@karibconnect.fr</a>
                    </address>
                </section>
                
                <small>&copy; 2026 KaribConnect - L1 Informatique UA</small>
            </div>
        </footer>
    );
}
```

**Améliorer avec le composant Link de Next :**
```jsx
import Link from 'next/link';

function Header() {
    return (
        <nav>
            <ul>
                <li><Link href="/">Accueil</Link></li>
                <li><Link href="/commerces">Commerces</Link></li>
                <li><Link href="/ajouter">Ajouter</Link></li>
            </ul>
        </nav>
    );
}
```

---

### Exercice 3 : Page d'accueil avec composants (35min)

**Créer `app/page.js` :**
```jsx
import Link from 'next/link';
import { commerces } from '@/lib/data';

export default function HomePage() {
    // Prendre seulement 3 commerces vedettes
    const commercesVedettes = commerces.slice(0, 3);
    
    return (
        <>
            <HeroSection />
            <SearchSection />
            <CommercesVedettes commerces={commercesVedettes} />
            <CategoriesSection />
        </>
    );
}

function HeroSection() {
    return (
        <section className="hero">
            <div className="container">
                <h2>Découvrez la Martinique autrement</h2>
                <p className="sous-titre">
                    Plus de 200 commerces locaux à Fort-de-France, Lamentin et Schoelcher
                </p>
                <Link href="/commerces" className="cta-button">
                    Commencer la recherche
                </Link>
            </div>
        </section>
    );
}

function SearchSection() {
    return (
        <section id="recherche" className="container">
            <h2>Recherche rapide</h2>
            <div className="search-quick">
                <input 
                    type="search" 
                    placeholder="Rechercher un commerce..."
                    className="search-input-large"
                />
                <button className="btn-primary">🔍 Rechercher</button>
            </div>
        </section>
    );
}

function CommercesVedettes({ commerces }) {
    return (
        <section className="container">
            <h2>Commerces à la une</h2>
            <div className="commerce-grid">
                {commerces.map(commerce => (
                    <CommerceCard key={commerce.id} commerce={commerce} />
                ))}
            </div>
            <div style={{ textAlign: 'center', marginTop: '2rem' }}>
                <Link href="/commerces" className="btn-secondary">
                    Voir tous les commerces →
                </Link>
            </div>
        </section>
    );
}

function CommerceCard({ commerce }) {
    const icones = {
        restaurant: '🍽️',
        alimentation: '🛒',
        services: '🔧',
        vetements: '👕',
    };
    
    return (
        <article className="commerce-card">
            <header>
                <h3>{icones[commerce.categorie]} {commerce.nom}</h3>
                <span className="categorie">{commerce.categorie}</span>
            </header>
            
            <div className="commerce-info">
                <p><strong>Ville:</strong> {commerce.ville}</p>
                <p>{commerce.description}</p>
            </div>
            
            <footer className="commerce-actions">
                <Link href={`/commerces/${commerce.id}`} className="btn-details">
                    Voir détails
                </Link>
            </footer>
        </article>
    );
}

function CategoriesSection() {
    const categories = [
        { nom: 'Restaurants', icone: '🍽️', count: 42 },
        { nom: 'Épiceries', icone: '🛒', count: 28 },
        { nom: 'Beauté', icone: '💇', count: 35 },
        { nom: 'Services', icone: '🔧', count: 51 },
    ];
    
    return (
        <section className="container">
            <h2>Explorer par catégorie</h2>
            <div className="categorie-grid">
                {categories.map(cat => (
                    <Link href={`/commerces?categorie=${cat.nom.toLowerCase()}`} key={cat.nom}>
                        <figure>
                            <span className="icone">{cat.icone}</span>
                            <figcaption>
                                <strong>{cat.nom}</strong>
                                <data>{cat.count} établissements</data>
                            </figcaption>
                        </figure>
                    </Link>
                ))}
            </div>
        </section>
    );
}
```

**Créer `lib/data.js` (copier les données du JS classique) :**
```javascript
export const commerces = [
    {
        id: 1,
        nom: "La Savane Gourmande",
        categorie: "restaurant",
        ville: "fort-de-france",
        // ... reste des données
    },
    // ... autres commerces
];
```

---

# SÉANCE 10 : NextJS Avancé (2h - 20min CI + 1h40 TP)

## 📋 COURS THÉORIQUE (20min)

### 1. Server vs Client Components (10min)

**Server Components (défaut) :**
- Pas de JavaScript envoyé au client
- Parfait pour le contenu statique
- Peut accéder directement à la base de données
- Ne peut pas utiliser useState, useEffect, onClick

**Client Components :**
- JavaScript envoyé au navigateur
- Nécessaire pour l'interactivité
- Utilise useState, useEffect, événements
- Directive `'use client'` en haut du fichier

**Exemple pratique :**
```jsx
// components/SearchForm.js
'use client'; // Client Component car interactif

import { useState } from 'react';

export default function SearchForm({ onSearch }) {
    const [query, setQuery] = useState('');
    
    const handleSubmit = (e) => {
        e.preventDefault();
        onSearch(query);
    };
    
    return (
        <form onSubmit={handleSubmit}>
            <input 
                value={query}
                onChange={(e) => setQuery(e.target.value)}
                placeholder="Rechercher..."
            />
            <button type="submit">Rechercher</button>
        </form>
    );
}
```

---

### 2. Routes dynamiques (10min)

```jsx
// app/commerces/[id]/page.js
import { commerces } from '@/lib/data';

export default function CommercePage({ params }) {
    const commerce = commerces.find(c => c.id === parseInt(params.id));
    
    if (!commerce) {
        return <div>Commerce non trouvé</div>;
    }
    
    return (
        <div>
            <h1>{commerce.nom}</h1>
            <p>{commerce.description}</p>
        </div>
    );
}

// Générer les pages statiques
export async function generateStaticParams() {
    return commerces.map(commerce => ({
        id: commerce.id.toString(),
    }));
}
```

---

## 💻 TRAVAUX PRATIQUES (1h40)

### Exercice 1 : Composants réutilisables (35min)

**Créer `components/CommerceCard.js` :**
```jsx
import Link from 'next/link';

export default function CommerceCard({ commerce, showActions = true }) {
    const icones = {
        restaurant: '🍽️',
        alimentation: '🛒',
        services: '🔧',
        vetements: '👕',
        beaute: '💇',
        electronique: '📱'
    };
    
    return (
        <article className="commerce-card">
            <header>
                <h3>
                    {icones[commerce.categorie] || '📍'} {commerce.nom}
                </h3>
                <span className="categorie">{commerce.categorie}</span>
                {commerce.note && (
                    <div className="note">
                        {'⭐'.repeat(Math.floor(commerce.note))} {commerce.note}/5
                    </div>
                )}
            </header>
            
            <div className="commerce-info">
                <p><strong>Ville:</strong> {commerce.ville}</p>
                <p><strong>Adresse:</strong> {commerce.adresse}</p>
                <p><strong>Téléphone:</strong> 
                    <a href={`tel:+596${commerce.telephone.slice(1)}`}>
                        {commerce.telephone}
                    </a>
                </p>
                <p>{commerce.description}</p>
                
                {commerce.services && commerce.services.length > 0 && (
                    <div className="services">
                        {commerce.services.map(service => (
                            <ServiceBadge key={service} service={service} />
                        ))}
                    </div>
                )}
            </div>
            
            {showActions && (
                <footer className="commerce-actions">
                    <Link href={`/commerces/${commerce.id}`} className="btn-details">
                        Voir détails
                    </Link>
                    <FavorisButton commerceId={commerce.id} />
                </footer>
            )}
        </article>
    );
}

function ServiceBadge({ service }) {
    const icons = {
        livraison: '🚚 Livraison',
        parking: '🅿️ Parking',
        wifi: '📶 WiFi',
        cb: '💳 CB',
        accessible: '♿ PMR'
    };
    
    return (
        <span className="service-badge">
            {icons[service] || service}
        </span>
    );
}

// Ce composant doit être Client car il utilise localStorage
function FavorisButton({ commerceId }) {
    // TODO: implémenter dans l'exercice suivant
    return <button className="btn-favoris">⭐ Favoris</button>;
}
```

**Créer `components/SearchForm.js` :**
```jsx
'use client';

import { useState } from 'react';
import { useRouter } from 'next/navigation';

export default function SearchForm({ initialValues = {} }) {
    const router = useRouter();
    const [formData, setFormData] = useState({
        query: initialValues.query || '',
        ville: initialValues.ville || '',
        categorie: initialValues.categorie || '',
        rayon: initialValues.rayon || 5,
    });
    
    const handleChange = (e) => {
        const { name, value } = e.target;
        setFormData(prev => ({
            ...prev,
            [name]: value
        }));
    };
    
    const handleSubmit = (e) => {
        e.preventDefault();
        
        // Construire l'URL avec les paramètres
        const params = new URLSearchParams();
        Object.entries(formData).forEach(([key, value]) => {
            if (value) params.append(key, value);
        });
        
        // Naviguer vers la page de résultats
        router.push(`/commerces?${params.toString()}`);
    };
    
    return (
        <form className="search-form" onSubmit={handleSubmit}>
            <fieldset>
                <legend>Que recherchez-vous ?</legend>
                
                <div className="form-group">
                    <label htmlFor="query">Nom, produit ou service :</label>
                    <input 
                        type="search"
                        id="query"
                        name="query"
                        value={formData.query}
                        onChange={handleChange}
                        placeholder="Ex: Coiffeur, Restaurant créole..."
                    />
                </div>
            </fieldset>
            
            <fieldset>
                <legend>Où ?</legend>
                
                <div className="form-group">
                    <label htmlFor="ville">Ville :</label>
                    <select 
                        id="ville"
                        name="ville"
                        value={formData.ville}
                        onChange={handleChange}
                    >
                        <option value="">Toutes les villes</option>
                        <option value="fort-de-france">Fort-de-France</option>
                        <option value="lamentin">Lamentin</option>
                        <option value="schoelcher">Schoelcher</option>
                    </select>
                </div>
                
                <div className="form-group">
                    <label htmlFor="rayon">
                        Rayon: {formData.rayon} km
                    </label>
                    <input 
                        type="range"
                        id="rayon"
                        name="rayon"
                        min="1"
                        max="20"
                        value={formData.rayon}
                        onChange={handleChange}
                    />
                </div>
            </fieldset>
            
            <div className="form-actions">
                <button type="submit" className="btn-primary">
                    🔍 Rechercher
                </button>
                <button 
                    type="reset" 
                    className="btn-secondary"
                    onClick={() => setFormData({
                        query: '',
                        ville: '',
                        categorie: '',
                        rayon: 5
                    })}
                >
                    ↺ Réinitialiser
                </button>
            </div>
        </form>
    );
}
```

---

### Exercice 2 : Page liste avec filtres (40min)

**Créer `app/commerces/page.js` :**
```jsx
import { commerces } from '@/lib/data';
import CommerceCard from '@/components/CommerceCard';
import SearchForm from '@/components/SearchForm';

export default function CommercesPage({ searchParams }) {
    // Filtrer les commerces selon les paramètres
    const commercesFiltres = filtrerCommerces(commerces, searchParams);
    
    return (
        <div className="container">
            <h1>Tous les commerces</h1>
            
            <SearchForm initialValues={searchParams} />
            
            <div className="resultats-header">
                <p className="resultats-count">
                    {commercesFiltres.length} commerce{commercesFiltres.length > 1 ? 's' : ''} trouvé{commercesFiltres.length > 1 ? 's' : ''}
                </p>
                <TriSelector />
            </div>
            
            {commercesFiltres.length === 0 ? (
                <NoResults />
            ) : (
                <div className="commerce-grid">
                    {commercesFiltres.map(commerce => (
                        <CommerceCard key={commerce.id} commerce={commerce} />
                    ))}
                </div>
            )}
        </div>
    );
}

function filtrerCommerces(commerces, params) {
    return commerces.filter(commerce => {
        // Filtre par recherche textuelle
        if (params.query) {
            const query = params.query.toLowerCase();
            const searchIn = `${commerce.nom} ${commerce.description} ${commerce.categorie}`.toLowerCase();
            if (!searchIn.includes(query)) return false;
        }
        
        // Filtre par ville
        if (params.ville && commerce.ville !== params.ville) {
            return false;
        }
        
        // Filtre par catégorie
        if (params.categorie && commerce.categorie !== params.categorie) {
            return false;
        }
        
        return true;
    });
}

function TriSelector() {
    return (
        <div className="tri-selector">
            <label>Trier par:</label>
            <select defaultValue="nom">
                <option value="nom">Nom (A-Z)</option>
                <option value="note">Note</option>
                <option value="ville">Ville</option>
            </select>
        </div>
    );
}

function NoResults() {
    return (
        <div className="no-results">
            <p>😞 Aucun commerce trouvé</p>
            <p>Essayez d'élargir vos critères de recherche</p>
        </div>
    );
}

export const metadata = {
    title: 'Tous les commerces - KaribConnect',
    description: 'Liste complète des commerces de Martinique',
};
```

---

### Exercice 3 : Page détail dynamique (25min)

**Créer `app/commerces/[id]/page.js` :**
```jsx
import { commerces } from '@/lib/data';
import { notFound } from 'next/navigation';
import Link from 'next/link';

export default function CommercePage({ params }) {
    const commerce = commerces.find(c => c.id === parseInt(params.id));
    
    if (!commerce) {
        notFound();
    }
    
    return (
        <div className="container">
            <nav className="breadcrumb">
                <Link href="/">Accueil</Link>
                {' > '}
                <Link href="/commerces">Commerces</Link>
                {' > '}
                <span>{commerce.nom}</span>
            </nav>
            
            <article className="commerce-detail">
                <header className="commerce-header">
                    <h1>{commerce.nom}</h1>
                    <div className="commerce-meta">
                        <span className="categorie-badge">{commerce.categorie}</span>
                        <span className="note-large">
                            {'⭐'.repeat(Math.floor(commerce.note))} {commerce.note}/5
                        </span>
                    </div>
                </header>
                
                <div className="commerce-content">
                    <section className="commerce-info-section">
                        <h2>Informations</h2>
                        <dl className="info-list">
                            <dt>📍 Adresse</dt>
                            <dd>{commerce.adresse}, {commerce.ville}</dd>
                            
                            <dt>📞 Téléphone</dt>
                            <dd>
                                <a href={`tel:+596${commerce.telephone.slice(1)}`}>
                                    {commerce.telephone}
                                </a>
                            </dd>
                            
                            {commerce.email && (
                                <>
                                    <dt>✉️ Email</dt>
                                    <dd>
                                        <a href={`mailto:${commerce.email}`}>
                                            {commerce.email}
                                        </a>
                                    </dd>
                                </>
                            )}
                        </dl>
                    </section>
                    
                    <section>
                        <h2>Description</h2>
                        <p className="description-large">{commerce.description}</p>
                    </section>
                    
                    {commerce.services && commerce.services.length > 0 && (
                        <section>
                            <h2>Services disponibles</h2>
                            <ul className="services-list">
                                {commerce.services.map(service => (
                                    <li key={service}>{getServiceLabel(service)}</li>
                                ))}
                            </ul>
                        </section>
                    )}
                    
                    <section className="actions-section">
                        <Link href={`tel:+596${commerce.telephone.slice(1)}`} className="btn-primary">
                            📞 Appeler
                        </Link>
                        <Link href="/commerces" className="btn-secondary">
                            ← Retour à la liste
                        </Link>
                    </section>
                </div>
            </article>
        </div>
    );
}

function getServiceLabel(service) {
    const labels = {
        livraison: '🚚 Livraison à domicile',
        parking: '🅿️ Parking disponible',
        wifi: '📶 WiFi gratuit',
        cb: '💳 Paiement par carte',
        accessible: '♿ Accessible PMR'
    };
    return labels[service] || service;
}

// Générer toutes les pages statiques
export async function generateStaticParams() {
    return commerces.map(commerce => ({
        id: commerce.id.toString(),
    }));
}

// Métadonnées dynamiques
export async function generateMetadata({ params }) {
    const commerce = commerces.find(c => c.id === parseInt(params.id));
    
    if (!commerce) {
        return {
            title: 'Commerce non trouvé',
        };
    }
    
    return {
        title: `${commerce.nom} - KaribConnect`,
        description: commerce.description,
    };
}
```

---

# SÉANCE 11 : Finalisation & Déploiement (2h - 15min CI + 1h45 TP)

## 📋 COURS THÉORIQUE (15min)

### Déploiement sur Vercel (15min)

**Pourquoi Vercel ?**
- Créé par l'équipe NextJS
- Déploiement gratuit et illimité
- CI/CD automatique avec Git
- URLs de prévisualisation pour chaque commit
- Performance optimale (CDN global)

**Processus de déploiement :**
1. Push le code sur GitHub
2. Connecter le repo à Vercel
3. Build et déploiement automatiques
4. URL de production générée

---

## 💻 TRAVAUX PRATIQUES (1h45)

### Exercice 1 : Fonctionnalités finales (45min)

**Créer `components/FavorisButton.js` :**
```jsx
'use client';

import { useState, useEffect } from 'react';

export default function FavorisButton({ commerceId }) {
    const [estFavori, setEstFavori] = useState(false);
    
    // Charger l'état depuis localStorage
    useEffect(() => {
        const favoris = getFavoris();
        setEstFavori(favoris.includes(commerceId));
    }, [commerceId]);
    
    const toggleFavori = () => {
        let favoris = getFavoris();
        
        if (favoris.includes(commerceId)) {
            favoris = favoris.filter(id => id !== commerceId);
        } else {
            favoris.push(commerceId);
        }
        
        saveFavoris(favoris);
        setEstFavori(!estFavori);
    };
    
    return (
        <button 
            className={`btn-favoris ${estFavori ? 'actif' : ''}`}
            onClick={toggleFavori}
        >
            {estFavori ? '⭐ En favoris' : '☆ Favoris'}
        </button>
    );
}

function getFavoris() {
    if (typeof window === 'undefined') return [];
    const favoris = localStorage.getItem('karibconnect-favoris');
    return favoris ? JSON.parse(favoris) : [];
}

function saveFavoris(favoris) {
    localStorage.setItem('karibconnect-favoris', JSON.stringify(favoris));
}
```

**Créer `app/favoris/page.js` :**
```jsx
'use client';

import { useState, useEffect } from 'react';
import { commerces } from '@/lib/data';
import CommerceCard from '@/components/CommerceCard';
import Link from 'next/link';

export default function FavorisPage() {
    const [commercesFavoris, setCommercesFavoris] = useState([]);
    
    useEffect(() => {
        const favorisIds = getFavoris();
        const favoris = commerces.filter(c => favorisIds.includes(c.id));
        setCommercesFavoris(favoris);
    }, []);
    
    if (commercesFavoris.length === 0) {
        return (
            <div className="container">
                <h1>Mes favoris</h1>
                <div className="empty-state">
                    <p>😊 Vous n'avez pas encore de favoris</p>
                    <Link href="/commerces" className="btn-primary">
                        Découvrir les commerces
                    </Link>
                </div>
            </div>
        );
    }
    
    return (
        <div className="container">
            <h1>Mes favoris ({commercesFavoris.length})</h1>
            <div className="commerce-grid">
                {commercesFavoris.map(commerce => (
                    <CommerceCard key={commerce.id} commerce={commerce} />
                ))}
            </div>
        </div>
    );
}

function getFavoris() {
    if (typeof window === 'undefined') return [];
    const favoris = localStorage.getItem('karibconnect-favoris');
    return favoris ? JSON.parse(favoris) : [];
}
```

**Créer `app/ajouter/page.js` :**
```jsx
'use client';

import { useState } from 'react';
import { useRouter } from 'next/navigation';

export default function AjouterPage() {
    const router = useRouter();
    const [loading, setLoading] = useState(false);
    
    const handleSubmit = async (e) => {
        e.preventDefault();
        setLoading(true);
        
        const formData = new FormData(e.target);
        const data = Object.fromEntries(formData);
        
        try {
            // Simuler un appel API
            await new Promise(resolve => setTimeout(resolve, 1500));
            
            console.log('Commerce ajouté:', data);
            
            // Rediriger vers la page d'accueil
            router.push('/?success=commerce-ajoute');
        } catch (error) {
            alert('Erreur lors de l\'ajout du commerce');
        } finally {
            setLoading(false);
        }
    };
    
    return (
        <div className="container">
            <h1>Ajouter un commerce</h1>
            <p>Remplissez ce formulaire pour référencer votre établissement</p>
            
            <form onSubmit={handleSubmit} className="form-ajouter">
                {/* Informations générales */}
                <section>
                    <h2>1️⃣ Informations générales</h2>
                    
                    <div className="form-group">
                        <label htmlFor="nom">Nom du commerce *</label>
                        <input 
                            type="text"
                            id="nom"
                            name="nom"
                            required
                            placeholder="Ex: La Savane Gourmande"
                        />
                    </div>
                    
                    <div className="form-group">
                        <label htmlFor="categorie">Catégorie *</label>
                        <select id="categorie" name="categorie" required>
                            <option value="">Sélectionnez</option>
                            <option value="restaurant">Restaurant</option>
                            <option value="alimentation">Alimentation</option>
                            <option value="vetements">Vêtements</option>
                            <option value="services">Services</option>
                        </select>
                    </div>
                    
                    <div className="form-group">
                        <label htmlFor="description">Description *</label>
                        <textarea 
                            id="description"
                            name="description"
                            required
                            rows="4"
                            placeholder="Décrivez votre commerce..."
                        />
                    </div>
                </section>
                
                {/* Coordonnées */}
                <section>
                    <h2>2️⃣ Coordonnées</h2>
                    
                    <div className="form-group">
                        <label htmlFor="adresse">Adresse *</label>
                        <input type="text" id="adresse" name="adresse" required />
                    </div>
                    
                    <div className="form-row">
                        <div className="form-group">
                            <label htmlFor="ville">Ville *</label>
                            <select id="ville" name="ville" required>
                                <option value="">Sélectionnez</option>
                                <option value="fort-de-france">Fort-de-France</option>
                                <option value="lamentin">Lamentin</option>
                                <option value="schoelcher">Schoelcher</option>
                            </select>
                        </div>
                        
                        <div className="form-group">
                            <label htmlFor="telephone">Téléphone *</label>
                            <input 
                                type="tel"
                                id="telephone"
                                name="telephone"
                                required
                                pattern="0[5-7][0-9]{8}"
                            />
                        </div>
                    </div>
                </section>
                
                <div className="form-actions">
                    <button 
                        type="submit" 
                        className="btn-primary"
                        disabled={loading}
                    >
                        {loading ? 'Envoi en cours...' : '✅ Publier'}
                    </button>
                </div>
            </form>
        </div>
    );
}
```

---

### Exercice 2 : Optimisations et build (30min)

**Optimiser les images - `next.config.js` :**
```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
    images: {
        domains: ['images.unsplash.com'], // Si vous utilisez des images externes
    },
};

module.exports = nextConfig;
```

**Utiliser le composant Image de Next :**
```jsx
import Image from 'next/image';

function CommerceImage({ src, alt }) {
    return (
        <Image 
            src={src}
            alt={alt}
            width={400}
            height={300}
            className="commerce-image"
            loading="lazy"
        />
    );
}
```

**Tester le build de production :**
```bash
# Build de production
npm run build

# Analyser la taille des bundles
npm run build -- --analyze

# Tester en local
npm run start
```

---

### Exercice 3 : Déploiement Vercel (30min)

**Étape 1 : Préparer le projet**
```bash
# Vérifier que tout fonctionne
npm run build
npm run start

# S'assurer que .gitignore contient :
# node_modules/
# .next/
# .env*.local

# Commit final
git add .
git commit -m "Projet KaribConnect prêt pour le déploiement"
git push origin main
```

**Étape 2 : Déployer sur Vercel**
1. Créer un compte sur https://vercel.com
2. Cliquer sur "Add New Project"
3. Importer le repository GitHub
4. Configurer :
   - Framework Preset: Next.js
   - Build Command: `npm run build`
   - Output Directory: `.next`
5. Cliquer sur "Deploy"

**Étape 3 : Configuration du domaine (optionnel)**
- Aller dans Settings > Domains
- Ajouter un domaine personnalisé ou utiliser le domaine Vercel gratuit
- Format: `karibconnect-votre-groupe.vercel.app`

**Étape 4 : Variables d'environnement (si nécessaire)**
```
# Dans Vercel Dashboard > Settings > Environment Variables
NEXT_PUBLIC_API_URL=https://api.karibconnect.com
```

---

## 📝 LIVRABLES FINAUX

### Critères d'évaluation finale

**Code source (25%) :**
- [ ] Structure NextJS propre et organisée
- [ ] Composants réutilisables
- [ ] Code commenté et lisible
- [ ] Pas de warnings ni erreurs

**Fonctionnalités (20%) :**
- [ ] Page d'accueil avec hero et commerces vedettes
- [ ] Liste des commerces avec filtres
- [ ] Pages détails dynamiques
- [ ] Système de favoris fonctionnel
- [ ] Formulaire d'ajout complet

**UI/UX (10%) :**
- [ ] Design cohérent et professionnel
- [ ] Responsive (mobile, tablette, desktop)
- [ ] Animations et transitions fluides
- [ ] Accessibilité (navigation clavier, ARIA)

**Présentation (5%) :**
- [ ] Démo de 5 minutes
- [ ] Explication des choix techniques
- [ ] Retour d'expérience

---

## Projet terminé !

Vous avez créé une application web moderne complète avec :
- ✅ HTML5 sémantique
- ✅ CSS3 avancé et responsive
- ✅ JavaScript interactif
- ✅ NextJS et React
- ✅ Déploiement en production

**Prochaines étapes possibles :**
- Intégrer une vraie API backend (Laravel, Node.js) (en L2)
- Ajouter un système d'authentification
- Implémenter une carte interactive (Google Maps, Leaflet)
- Créer une version mobile (React Native)
- Ajouter un tableau de bord administrateur
- Intégrer un système de notation et avis
