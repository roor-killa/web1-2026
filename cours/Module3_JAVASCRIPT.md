# Module 3 : JavaScript & Interactivité (5h total)
## Séances 6, 7 et 8 - DOM, Événements et API

---

# SÉANCE 6 : JavaScript Basics & DOM (2h - 25min CI + 1h35 TP)

## 📋 COURS THÉORIQUE (25min)

### 1. Introduction à JavaScript (8min)

**Variables et types de données**
```javascript
// Variables (ES6+)
const PI = 3.14159;           // Constante
let compteur = 0;             // Variable modifiable
var ancien = "à éviter";      // Ancienne syntaxe

// Types de données
let texte = "Martinique";     // String
let nombre = 42;              // Number
let decimal = 3.14;           // Number
let vrai = true;              // Boolean
let tableau = [1, 2, 3];      // Array
let objet = { nom: "Roor" };  // Object
let rien = null;              // Null
let indefini;                 // Undefined
```

**Fonctions**
```javascript
// Fonction classique
function saluer(nom) {
    return `Bonjour ${nom} !`;
}

// Arrow function (moderne)
const multiplier = (a, b) => a * b;

// Fonction avec paramètres par défaut
const afficher = (message = "Salut") => {
    console.log(message);
};
```

---

### 2. Le DOM (Document Object Model) (10min)

```javascript
// Sélectionner des éléments
const titre = document.getElementById('titre');
const boutons = document.querySelectorAll('.btn');
const premier = document.querySelector('.commerce-card');

// Modifier le contenu
titre.textContent = "Nouveau titre";
titre.innerHTML = "<strong>Titre important</strong>";

// Modifier les attributs
const image = document.querySelector('img');
image.src = "nouvelle-image.jpg";
image.alt = "Description";

// Modifier les styles
titre.style.color = "blue";
titre.style.fontSize = "2rem";

// Classes CSS
titre.classList.add('actif');
titre.classList.remove('cache');
titre.classList.toggle('visible');
titre.classList.contains('actif'); // true/false

// Créer des éléments
const div = document.createElement('div');
div.className = 'commerce-card';
div.textContent = "Nouveau commerce";

// Ajouter au DOM
document.body.appendChild(div);
const container = document.querySelector('.commerce-grid');
container.insertBefore(div, container.firstChild);
```

---

### 3. Événements (7min)

```javascript
// Écouter un événement
const bouton = document.querySelector('#rechercher');

bouton.addEventListener('click', function(event) {
    event.preventDefault(); // Empêcher le comportement par défaut
    console.log('Bouton cliqué !');
});

// Arrow function
bouton.addEventListener('click', (e) => {
    console.log('Coordonnées du clic:', e.clientX, e.clientY);
});

// Événements courants
input.addEventListener('input', (e) => {
    console.log('Valeur:', e.target.value);
});

formulaire.addEventListener('submit', (e) => {
    e.preventDefault();
    // Traiter le formulaire
});

document.addEventListener('DOMContentLoaded', () => {
    // Code à exécuter quand le DOM est prêt
});

window.addEventListener('scroll', () => {
    console.log('Position:', window.scrollY);
});
```

---

## 💻 TRAVAUX PRATIQUES (1h35)

### Exercice 1 : Formulaire de recherche interactif (35min)

**Créer `js/recherche.js` :**

```javascript
// Attendre que le DOM soit chargé
document.addEventListener('DOMContentLoaded', () => {
    // Éléments du formulaire
    const formulaireRecherche = document.querySelector('.search-form');
    const champRecherche = document.querySelector('#query');
    const selectVille = document.querySelector('#ville');
    const selectCategorie = document.querySelector('#categorie');
    const sliderRayon = document.querySelector('#rayon');
    const outputRayon = document.querySelector('#rayonValue');
    const btnRechercher = document.querySelector('button[type="submit"]');
    const btnReset = document.querySelector('button[type="reset"]');
    
    // Afficher la valeur du slider
    sliderRayon.addEventListener('input', (e) => {
        outputRayon.textContent = e.target.value;
    });
    
    // Recherche en temps réel (debounce)
    let timeoutId;
    champRecherche.addEventListener('input', (e) => {
        clearTimeout(timeoutId);
        
        const query = e.target.value;
        
        // Attendre 300ms après la dernière frappe
        timeoutId = setTimeout(() => {
            if (query.length >= 3) {
                rechercherCommerces(query);
            }
        }, 300);
    });
    
    // Soumission du formulaire
    formulaireRecherche.addEventListener('submit', (e) => {
        e.preventDefault();
        
        const criteres = {
            query: champRecherche.value,
            ville: selectVille.value,
            categorie: selectCategorie.value,
            rayon: sliderRayon.value
        };
        
        console.log('Recherche avec critères:', criteres);
        rechercherCommerces(criteres.query, criteres);
    });
    
    // Réinitialisation
    btnReset.addEventListener('click', () => {
        setTimeout(() => {
            afficherTousLesCommerces();
        }, 10);
    });
    
    // Fonction de recherche (à implémenter)
    function rechercherCommerces(query, criteres = {}) {
        console.log(`Recherche de "${query}"`, criteres);
        // TODO: Filtrer les commerces affichés
    }
    
    function afficherTousLesCommerces() {
        console.log('Afficher tous les commerces');
        // TODO: Réafficher tous les commerces
    }
});
```

---

### Exercice 2 : Filtrage dynamique des commerces (40min)

**Données de commerces fictives - `js/data.js` :**

```javascript
const commerces = [
    {
        id: 1,
        nom: "La Savane Gourmande",
        categorie: "restaurant",
        ville: "fort-de-france",
        adresse: "45 Rue Victor Hugo",
        telephone: "0596123456",
        description: "Restaurant créole authentique. Spécialités : colombo, court-bouillon, accras.",
        services: ["livraison", "wifi"],
        prix: "moyen",
        note: 4.5
    },
    {
        id: 2,
        nom: "Bizouk Express",
        categorie: "alimentation",
        ville: "lamentin",
        adresse: "12 Avenue des Caraïbes",
        telephone: "0596234567",
        description: "Produits frais et locaux. Fruits, légumes pays, épices créoles.",
        services: ["livraison", "parking"],
        prix: "economique",
        note: 4.2
    },
    {
        id: 3,
        nom: "TechKarib Réparation",
        categorie: "services",
        ville: "schoelcher",
        adresse: "Zone Industrielle",
        telephone: "0596345678",
        description: "Réparation d'appareils électroniques. Diagnostic gratuit, garantie 3 mois.",
        services: ["parking"],
        prix: "moyen",
        note: 4.7
    },
    {
        id: 4,
        nom: "Chez Tatie Marie",
        categorie: "restaurant",
        ville: "fort-de-france",
        adresse: "Place de la Savane",
        telephone: "0596456789",
        description: "Cuisine créole traditionnelle. Ambiance familiale.",
        services: ["wifi"],
        prix: "economique",
        note: 4.8
    },
    {
        id: 5,
        nom: "Mode Karibbé",
        categorie: "vetements",
        ville: "lamentin",
        adresse: "Centre Commercial La Galleria",
        telephone: "0596567890",
        description: "Vêtements tendance et accessoires. Style caribéen moderne.",
        services: ["parking", "cb"],
        prix: "premium",
        note: 4.3
    }
];
```

**Système de filtrage - `js/filtres.js` :**

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const grille = document.querySelector('.commerce-grid');
    
    // Afficher tous les commerces au chargement
    afficherCommerces(commerces);
    
    // Fonction pour afficher les commerces
    function afficherCommerces(commercesAfficher) {
        // Vider la grille
        grille.innerHTML = '';
        
        // Si aucun résultat
        if (commercesAfficher.length === 0) {
            grille.innerHTML = `
                <div class="no-results">
                    <p>Aucun commerce trouvé 😞</p>
                    <p>Essayez d'élargir vos critères de recherche</p>
                </div>
            `;
            return;
        }
        
        // Créer les cartes
        commercesAfficher.forEach((commerce, index) => {
            const carte = creerCarteCommerce(commerce);
            carte.style.animationDelay = `${index * 0.1}s`;
            grille.appendChild(carte);
        });
    }
    
    // Fonction pour créer une carte commerce
    function creerCarteCommerce(commerce) {
        const article = document.createElement('article');
        article.className = 'commerce-card';
        article.dataset.id = commerce.id;
        
        const icones = {
            restaurant: '🍽️',
            alimentation: '🛒',
            services: '🔧',
            vetements: '👕',
            beaute: '💇',
            electronique: '📱'
        };
        
        article.innerHTML = `
            <header>
                <h3>${icones[commerce.categorie] || '📍'} ${commerce.nom}</h3>
                <span class="categorie">${commerce.categorie}</span>
                <div class="note">
                    ${'⭐'.repeat(Math.floor(commerce.note))} ${commerce.note}/5
                </div>
            </header>
            
            <div class="commerce-info">
                <p><strong>Ville:</strong> ${commerce.ville}</p>
                <p><strong>Adresse:</strong> ${commerce.adresse}</p>
                <p><strong>Téléphone:</strong> <a href="tel:+596${commerce.telephone.slice(1)}">${commerce.telephone}</a></p>
                <p>${commerce.description}</p>
                ${commerce.services.length > 0 ? `
                    <div class="services">
                        ${commerce.services.map(s => getServiceIcon(s)).join(' ')}
                    </div>
                ` : ''}
            </div>
            
            <footer class="commerce-actions">
                <a href="commerce.html?id=${commerce.id}" class="btn-details">Voir détails</a>
                <button class="btn-favoris" data-id="${commerce.id}">⭐ Favoris</button>
            </footer>
        `;
        
        return article;
    }
    
    // Icônes des services
    function getServiceIcon(service) {
        const icons = {
            livraison: '🚚 Livraison',
            parking: '🅿️ Parking',
            wifi: '📶 WiFi',
            cb: '💳 CB',
            accessible: '♿ PMR'
        };
        return `<span class="service-badge">${icons[service] || service}</span>`;
    }
    
    // Fonction de filtrage
    function filtrerCommerces(criteres) {
        return commerces.filter(commerce => {
            // Filtre par recherche textuelle
            if (criteres.query && criteres.query.length >= 3) {
                const query = criteres.query.toLowerCase();
                const rechercheDans = `${commerce.nom} ${commerce.description} ${commerce.categorie}`.toLowerCase();
                if (!rechercheDans.includes(query)) return false;
            }
            
            // Filtre par ville
            if (criteres.ville && commerce.ville !== criteres.ville) {
                return false;
            }
            
            // Filtre par catégorie
            if (criteres.categorie && commerce.categorie !== criteres.categorie) {
                return false;
            }
            
            // Filtre par services
            if (criteres.services && criteres.services.length > 0) {
                const aLesServices = criteres.services.every(s => 
                    commerce.services.includes(s)
                );
                if (!aLesServices) return false;
            }
            
            // Filtre par prix
            if (criteres.prix && criteres.prix.length > 0) {
                if (!criteres.prix.includes(commerce.prix)) return false;
            }
            
            return true;
        });
    }
    
    // Attacher le filtrage au formulaire
    const formulaire = document.querySelector('.search-form');
    
    formulaire.addEventListener('submit', (e) => {
        e.preventDefault();
        
        const criteres = {
            query: document.querySelector('#query').value,
            ville: document.querySelector('#ville').value,
            categorie: document.querySelector('#categorie').value,
            services: Array.from(document.querySelectorAll('input[name="services[]"]:checked'))
                .map(cb => cb.value),
            prix: Array.from(document.querySelectorAll('input[name="prix[]"]:checked'))
                .map(cb => cb.value)
        };
        
        const resultats = filtrerCommerces(criteres);
        afficherCommerces(resultats);
        
        // Afficher le nombre de résultats
        afficherNombreResultats(resultats.length);
    });
    
    function afficherNombreResultats(nombre) {
        let message = document.querySelector('.resultats-count');
        if (!message) {
            message = document.createElement('div');
            message.className = 'resultats-count';
            grille.before(message);
        }
        message.textContent = `${nombre} commerce${nombre > 1 ? 's' : ''} trouvé${nombre > 1 ? 's' : ''}`;
    }
    
    // Exposer globalement pour la recherche en temps réel
    window.rechercherCommerces = (query, criteres = {}) => {
        criteres.query = query;
        const resultats = filtrerCommerces(criteres);
        afficherCommerces(resultats);
    };
});
```

**CSS pour les nouveaux éléments :**
```css
.note {
    font-size: var(--text-sm);
    margin-top: var(--space-sm);
}

.services {
    display: flex;
    flex-wrap: wrap;
    gap: var(--space-xs);
    margin-top: var(--space-md);
}

.service-badge {
    background-color: var(--color-light-gray);
    padding: var(--space-xs) var(--space-sm);
    border-radius: var(--radius-sm);
    font-size: var(--text-xs);
}

.no-results {
    grid-column: 1 / -1;
    text-align: center;
    padding: var(--space-3xl);
    font-size: var(--text-xl);
    color: var(--color-gray);
}

.resultats-count {
    font-weight: 600;
    color: var(--color-primary);
    margin-bottom: var(--space-md);
}
```

---

### Exercice 3 : Bouton favoris avec localStorage (20min)

```javascript
// Gestion des favoris - js/favoris.js
document.addEventListener('DOMContentLoaded', () => {
    // Récupérer les favoris depuis localStorage
    function getFavoris() {
        const favoris = localStorage.getItem('karibconnect-favoris');
        return favoris ? JSON.parse(favoris) : [];
    }
    
    // Sauvegarder les favoris
    function saveFavoris(favoris) {
        localStorage.setItem('karibconnect-favoris', JSON.stringify(favoris));
    }
    
    // Vérifier si un commerce est en favori
    function estFavori(commerceId) {
        const favoris = getFavoris();
        return favoris.includes(commerceId);
    }
    
    // Ajouter/retirer des favoris
    function toggleFavori(commerceId) {
        let favoris = getFavoris();
        
        if (estFavori(commerceId)) {
            favoris = favoris.filter(id => id !== commerceId);
        } else {
            favoris.push(commerceId);
        }
        
        saveFavoris(favoris);
        return estFavori(commerceId);
    }
    
    // Écouter les clics sur les boutons favoris
    document.addEventListener('click', (e) => {
        if (e.target.classList.contains('btn-favoris')) {
            const commerceId = parseInt(e.target.dataset.id);
            const maintenant = toggleFavori(commerceId);
            
            // Mettre à jour le bouton
            if (maintenant) {
                e.target.textContent = '⭐ Retiré des favoris';
                e.target.classList.add('actif');
            } else {
                e.target.textContent = '⭐ Favoris';
                e.target.classList.remove('actif');
            }
            
            // Animation
            e.target.style.transform = 'scale(1.1)';
            setTimeout(() => {
                e.target.style.transform = 'scale(1)';
            }, 200);
        }
    });
    
    // Marquer les favoris au chargement
    function marquerFavoris() {
        const favoris = getFavoris();
        document.querySelectorAll('.btn-favoris').forEach(btn => {
            const commerceId = parseInt(btn.dataset.id);
            if (favoris.includes(commerceId)) {
                btn.textContent = '⭐ En favoris';
                btn.classList.add('actif');
            }
        });
    }
    
    // Appeler après le chargement des commerces
    setTimeout(marquerFavoris, 100);
});
```

---

# SÉANCE 7 : JavaScript Intermédiaire & API (2h - 15min CI + 1h45 TP)

## 📋 COURS THÉORIQUE (15min)

### 1. Fetch API et Promesses (15min)

```javascript
// Fetch basique
fetch('https://api.example.com/commerces')
    .then(response => response.json())
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.error('Erreur:', error);
    });

// Async/Await (moderne)
async function getCommerces() {
    try {
        const response = await fetch('https://api.example.com/commerces');
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Erreur:', error);
        return [];
    }
}

// Avec options
async function ajouterCommerce(commerce) {
    try {
        const response = await fetch('https://api.example.com/commerces', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(commerce)
        });
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Erreur lors de l\'ajout:', error);
        throw error;
    }
}
```

---

## 💻 TRAVAUX PRATIQUES (1h45)

### Exercice 1 : Intégration API publique (50min)

**Utiliser l'API Nominatim pour la géolocalisation :**

```javascript
// js/geolocalisation.js
class GeolocationService {
    constructor() {
        this.baseUrl = 'https://nominatim.openstreetmap.org';
    }
    
    // Rechercher une adresse
    async rechercherAdresse(query) {
        try {
            const url = `${this.baseUrl}/search?q=${encodeURIComponent(query)}&format=json&limit=5`;
            const response = await fetch(url);
            
            if (!response.ok) {
                throw new Error('Erreur de géocodage');
            }
            
            return await response.json();
        } catch (error) {
            console.error('Erreur:', error);
            return [];
        }
    }
    
    // Obtenir la position actuelle
    async getPositionActuelle() {
        return new Promise((resolve, reject) => {
            if (!navigator.geolocation) {
                reject(new Error('Géolocalisation non supportée'));
                return;
            }
            
            navigator.geolocation.getCurrentPosition(
                position => {
                    resolve({
                        lat: position.coords.latitude,
                        lon: position.coords.longitude
                    });
                },
                error => reject(error)
            );
        });
    }
    
    // Calculer la distance entre deux points
    calculerDistance(lat1, lon1, lat2, lon2) {
        const R = 6371; // Rayon de la Terre en km
        const dLat = this.toRad(lat2 - lat1);
        const dLon = this.toRad(lon2 - lon1);
        
        const a = 
            Math.sin(dLat / 2) * Math.sin(dLat / 2) +
            Math.cos(this.toRad(lat1)) * Math.cos(this.toRad(lat2)) *
            Math.sin(dLon / 2) * Math.sin(dLon / 2);
        
        const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
        return R * c;
    }
    
    toRad(deg) {
        return deg * (Math.PI / 180);
    }
}

// Utilisation
const geoService = new GeolocationService();

// Bouton de géolocalisation
document.querySelector('#btn-geolocaliser')?.addEventListener('click', async () => {
    try {
        const position = await geoService.getPositionActuelle();
        console.log('Position:', position);
        
        // Filtrer les commerces à proximité
        const commercesProches = commerces.filter(commerce => {
            // Coordonnées fictives pour la démo
            const commerceLat = 14.6 + Math.random() * 0.1;
            const commerceLon = -61.0 + Math.random() * 0.1;
            
            const distance = geoService.calculerDistance(
                position.lat,
                position.lon,
                commerceLat,
                commerceLon
            );
            
            return distance < 5; // Moins de 5km
        });
        
        afficherCommerces(commercesProches);
    } catch (error) {
        alert('Impossible d\'obtenir votre position');
    }
});
```

---

### Exercice 2 : Soumission formulaire avec validation (35min)

```javascript
// js/formulaire-ajout.js
document.addEventListener('DOMContentLoaded', () => {
    const formulaire = document.querySelector('form[action="/api/commerces"]');
    
    if (!formulaire) return;
    
    // Validation en temps réel
    const inputs = formulaire.querySelectorAll('input[required], textarea[required], select[required]');
    
    inputs.forEach(input => {
        input.addEventListener('blur', () => {
            validerChamp(input);
        });
        
        input.addEventListener('input', () => {
            if (input.classList.contains('invalide')) {
                validerChamp(input);
            }
        });
    });
    
    function validerChamp(input) {
        const valide = input.checkValidity();
        
        if (!valide) {
            input.classList.add('invalide');
            input.classList.remove('valide');
            afficherErreur(input, input.validationMessage);
        } else {
            input.classList.remove('invalide');
            input.classList.add('valide');
            cacherErreur(input);
        }
        
        return valide;
    }
    
    function afficherErreur(input, message) {
        let erreur = input.nextElementSibling;
        
        if (!erreur || !erreur.classList.contains('erreur-message')) {
            erreur = document.createElement('span');
            erreur.className = 'erreur-message';
            input.after(erreur);
        }
        
        erreur.textContent = message;
    }
    
    function cacherErreur(input) {
        const erreur = input.nextElementSibling;
        if (erreur && erreur.classList.contains('erreur-message')) {
            erreur.remove();
        }
    }
    
    // Soumission du formulaire
    formulaire.addEventListener('submit', async (e) => {
        e.preventDefault();
        
        // Valider tous les champs
        let tousValides = true;
        inputs.forEach(input => {
            if (!validerChamp(input)) {
                tousValides = false;
            }
        });
        
        if (!tousValides) {
            alert('Veuillez corriger les erreurs dans le formulaire');
            return;
        }
        
        // Récupérer les données
        const formData = new FormData(formulaire);
        const commerce = Object.fromEntries(formData.entries());
        
        // Afficher un loader
        const btnSubmit = formulaire.querySelector('button[type="submit"]');
        const textOriginal = btnSubmit.textContent;
        btnSubmit.disabled = true;
        btnSubmit.innerHTML = '<span class="spinner"></span> Envoi en cours...';
        
        try {
            // Simuler un appel API
            await new Promise(resolve => setTimeout(resolve, 2000));
            
            console.log('Commerce à ajouter:', commerce);
            
            // Succès
            afficherNotification('Commerce ajouté avec succès !', 'success');
            formulaire.reset();
            
            // Rediriger après 2 secondes
            setTimeout(() => {
                window.location.href = 'index.html';
            }, 2000);
            
        } catch (error) {
            afficherNotification('Erreur lors de l\'ajout', 'error');
            btnSubmit.disabled = false;
            btnSubmit.textContent = textOriginal;
        }
    });
    
    function afficherNotification(message, type = 'info') {
        const notification = document.createElement('div');
        notification.className = `notification notification-${type}`;
        notification.textContent = message;
        
        document.body.appendChild(notification);
        
        setTimeout(() => {
            notification.classList.add('visible');
        }, 10);
        
        setTimeout(() => {
            notification.classList.remove('visible');
            setTimeout(() => notification.remove(), 300);
        }, 3000);
    }
});
```

**CSS pour la validation :**
```css
input.invalide,
textarea.invalide,
select.invalide {
    border-color: var(--color-error);
}

input.valide,
textarea.valide,
select.valide {
    border-color: var(--color-success);
}

.erreur-message {
    color: var(--color-error);
    font-size: var(--text-sm);
    display: block;
    margin-top: var(--space-xs);
}

.notification {
    position: fixed;
    top: 20px;
    right: 20px;
    padding: var(--space-md) var(--space-lg);
    border-radius: var(--radius-md);
    box-shadow: var(--shadow-xl);
    opacity: 0;
    transform: translateX(400px);
    transition: all var(--transition-base);
    z-index: 10000;
}

.notification.visible {
    opacity: 1;
    transform: translateX(0);
}

.notification-success {
    background-color: var(--color-success);
    color: white;
}

.notification-error {
    background-color: var(--color-error);
    color: white;
}
```

---

### Exercice 3 : Tri et pagination (20min)

```javascript
// js/tri-pagination.js
class CommercePagination {
    constructor(commerces, parPage = 9) {
        this.commerces = commerces;
        this.parPage = parPage;
        this.pageActuelle = 1;
        this.triActuel = 'nom';
        this.ordreActuel = 'asc';
    }
    
    trier(critere, ordre = 'asc') {
        this.triActuel = critere;
        this.ordreActuel = ordre;
        
        this.commerces.sort((a, b) => {
            let valA = a[critere];
            let valB = b[critere];
            
            if (typeof valA === 'string') {
                valA = valA.toLowerCase();
                valB = valB.toLowerCase();
            }
            
            if (ordre === 'asc') {
                return valA > valB ? 1 : -1;
            } else {
                return valA < valB ? 1 : -1;
            }
        });
        
        this.pageActuelle = 1;
    }
    
    getPage(numero) {
        this.pageActuelle = numero;
        const debut = (numero - 1) * this.parPage;
        const fin = debut + this.parPage;
        return this.commerces.slice(debut, fin);
    }
    
    getNombrePages() {
        return Math.ceil(this.commerces.length / this.parPage);
    }
    
    afficherPagination(container) {
        const nbPages = this.getNombrePages();
        container.innerHTML = '';
        
        // Bouton précédent
        if (this.pageActuelle > 1) {
            const btnPrev = this.creerBoutonPage('← Précédent', this.pageActuelle - 1);
            container.appendChild(btnPrev);
        }
        
        // Numéros de page
        for (let i = 1; i <= nbPages; i++) {
            if (i === 1 || i === nbPages || (i >= this.pageActuelle - 2 && i <= this.pageActuelle + 2)) {
                const btn = this.creerBoutonPage(i, i);
                if (i === this.pageActuelle) {
                    btn.classList.add('actif');
                }
                container.appendChild(btn);
            } else if (i === this.pageActuelle - 3 || i === this.pageActuelle + 3) {
                const ellipsis = document.createElement('span');
                ellipsis.textContent = '...';
                ellipsis.className = 'pagination-ellipsis';
                container.appendChild(ellipsis);
            }
        }
        
        // Bouton suivant
        if (this.pageActuelle < nbPages) {
            const btnNext = this.creerBoutonPage('Suivant →', this.pageActuelle + 1);
            container.appendChild(btnNext);
        }
    }
    
    creerBoutonPage(text, page) {
        const btn = document.createElement('button');
        btn.textContent = text;
        btn.className = 'pagination-btn';
        btn.onclick = () => {
            const commerces = this.getPage(page);
            afficherCommerces(commerces);
            this.afficherPagination(document.querySelector('.pagination'));
            window.scrollTo({ top: 0, behavior: 'smooth' });
        };
        return btn;
    }
}

// Utilisation
const pagination = new CommercePagination(commerces, 6);

// Tri
document.querySelector('#tri-nom')?.addEventListener('click', () => {
    pagination.trier('nom', 'asc');
    afficherCommerces(pagination.getPage(1));
    pagination.afficherPagination(document.querySelector('.pagination'));
});

document.querySelector('#tri-note')?.addEventListener('click', () => {
    pagination.trier('note', 'desc');
    afficherCommerces(pagination.getPage(1));
    pagination.afficherPagination(document.querySelector('.pagination'));
});
```

---

# SÉANCE 8 : JavaScript Moderne & Optimisations (1h - 100% TP)

## 💻 TRAVAUX PRATIQUES (1h)

### Exercice 1 : Modules ES6 (20min)

**Réorganiser le code en modules - `js/modules/Commerce.js` :**

```javascript
export class Commerce {
    constructor(data) {
        Object.assign(this, data);
    }
    
    getNote() {
        return '⭐'.repeat(Math.floor(this.note)) + ` ${this.note}/5`;
    }
    
    getPrixSymbole() {
        return '€'.repeat(['economique', 'moyen', 'premium'].indexOf(this.prix) + 1);
    }
    
    getDistance(lat, lon) {
        // Calcul de distance
        return Math.random() * 10; // km (fictif)
    }
    
    toCard() {
        return `
            <article class="commerce-card" data-id="${this.id}">
                <header>
                    <h3>${this.nom}</h3>
                    <span class="categorie">${this.categorie}</span>
                    <div class="note">${this.getNote()}</div>
                </header>
                <div class="commerce-info">
                    <p><strong>Ville:</strong> ${this.ville}</p>
                    <p>${this.description}</p>
                </div>
            </article>
        `;
    }
}
```

**`js/modules/api.js` :**
```javascript
export const API_BASE = 'https://api.karibconnect.local';

export async function fetchCommerces(filters = {}) {
    const params = new URLSearchParams(filters);
    const response = await fetch(`${API_BASE}/commerces?${params}`);
    return response.json();
}

export async function createCommerce(data) {
    const response = await fetch(`${API_BASE}/commerces`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data)
    });
    return response.json();
}
```

**`js/app.js` (point d'entrée) :**
```javascript
import { Commerce } from './modules/Commerce.js';
import { fetchCommerces } from './modules/api.js';

async function init() {
    const data = await fetchCommerces();
    const commerces = data.map(d => new Commerce(d));
    // ...
}

init();
```

---

### Exercice 2 : Performance et optimisations (30min)

```javascript
// Debounce utility
function debounce(func, wait) {
    let timeout;
    return function executedFunction(...args) {
        const later = () => {
            clearTimeout(timeout);
            func(...args);
        };
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
    };
}

// Throttle utility
function throttle(func, limit) {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}

// Lazy loading des images
function lazyLoadImages() {
    const images = document.querySelectorAll('img[data-src]');
    
    const imageObserver = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                const img = entry.target;
                img.src = img.dataset.src;
                img.removeAttribute('data-src');
                imageObserver.unobserve(img);
            }
        });
    });
    
    images.forEach(img => imageObserver.observe(img));
}

// Scroll infini
function initInfiniteScroll(loadMore) {
    const observer = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
            loadMore();
        }
    }, { rootMargin: '200px' });
    
    const sentinel = document.querySelector('.infinite-scroll-sentinel');
    if (sentinel) {
        observer.observe(sentinel);
    }
}

// Optimisation de la recherche
const rechercheOptimisee = debounce((query) => {
    // Recherche API
    fetch(`/api/search?q=${query}`)
        .then(r => r.json())
        .then(data => afficherResultats(data));
}, 300);

// Optimisation du scroll
const handleScroll = throttle(() => {
    const scrolled = window.scrollY > 100;
    document.body.classList.toggle('scrolled', scrolled);
}, 100);

window.addEventListener('scroll', handleScroll);
```

---

## 📝 Livrables Module 3

1. **JavaScript complet** :
   - Filtrage et recherche dynamiques
   - Gestion des favoris (localStorage)
   - Validation de formulaires
   - Tri et pagination
   - Code modulaire (ES6 modules)

2. **Commit Git** : `"Module 3: JavaScript interactif complet"`

---

## Prochaine séance

**Module 4 - NextJS : Application moderne**
- Introduction à React et NextJS
- Migration vers NextJS
- Composants et routing
- Déploiement sur Vercel
