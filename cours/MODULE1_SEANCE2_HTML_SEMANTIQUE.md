# Module 1 - Séance 2 : HTML Sémantique & Formulaires Avancés
## Durée : 2h (15min CI + 1h45 TP)

---

## 📋 COURS THÉORIQUE (CI) - 15 minutes

### 1. HTML Sémantique : Pourquoi et comment ? (7min)

**Balises sémantiques vs balises génériques**

❌ **Mauvais (div soup) :**
```html
<div class="header">
    <div class="nav">
        <div class="menu-item">Accueil</div>
    </div>
</div>
```

✅ **Bon (sémantique) :**
```html
<header>
    <nav>
        <a href="#accueil">Accueil</a>
    </nav>
</header>
```

**Balises sémantiques HTML5 :**
```
┌─────────────────────────────┐
│         <header>            │  En-tête de page/section
│    <nav> Navigation </nav>  │  Menu de navigation
├─────────────────────────────┤
│         <main>              │  Contenu principal unique
│  ┌─────────────────────┐   │
│  │   <article>         │   │  Contenu autonome
│  │     <section>       │   │  Section thématique
│  │     </section>      │   │
│  │     <aside>...</aside>  │  Contenu complémentaire
│  │   </article>        │   │
│  └─────────────────────┘   │
│         </main>             │
├─────────────────────────────┤
│         <footer>            │  Pied de page
└─────────────────────────────┘
```

**Les 3 piliers de la sémantique :**
1. **Accessibilité** : lecteurs d'écran comprennent la structure
2. **SEO** : Google valorise le contenu bien structuré
3. **Maintenabilité** : code plus lisible pour les développeurs

---

### 2. Formulaires HTML5 : Types d'input modernes (8min)

**Types d'input HTML5 :**
```html
<!-- Texte classique -->
<input type="text">

<!-- Email avec validation native -->
<input type="email" required>

<!-- Téléphone -->
<input type="tel" pattern="[0-9]{10}">

<!-- URL -->
<input type="url">

<!-- Nombre avec min/max -->
<input type="number" min="0" max="100" step="5">

<!-- Date -->
<input type="date" min="2026-01-01">

<!-- Heure -->
<input type="time">

<!-- Couleur -->
<input type="color">

<!-- Recherche -->
<input type="search">

<!-- Range (slider) -->
<input type="range" min="0" max="5">
```

**Attributs de validation :**
- `required` : champ obligatoire
- `pattern` : regex de validation
- `min` / `max` : valeurs limites
- `maxlength` : nombre de caractères max
- `placeholder` : texte d'aide
- `autocomplete` : suggestions du navigateur

**Organisation d'un formulaire :**
```html
<form action="/submit" method="POST">
    <fieldset>
        <legend>Informations personnelles</legend>
        
        <label for="nom">Nom :</label>
        <input type="text" id="nom" name="nom" required>
        
        <label for="email">Email :</label>
        <input type="email" id="email" name="email" required>
    </fieldset>
    
    <button type="submit">Envoyer</button>
</form>
```

---

## 💻 TRAVAUX PRATIQUES (TP2) - 1h45

### Objectif
Améliorer la sémantique de KaribConnect et créer des formulaires avancés.

---

### Exercice 1 : Refactoring sémantique (30min)

**1.1 Optimiser la structure de la page d'accueil**

Transformer votre `index.html` actuel en version ultra-sémantique :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Annuaire des commerces locaux de Martinique">
    <title>KaribConnect - Découvrez les commerces martiniquais</title>
</head>
<body>
    
    <!-- En-tête principal du site -->
    <header role="banner">
        <div class="logo">
            <h1>🌴 KaribConnect</h1>
        </div>
        
        <nav role="navigation" aria-label="Navigation principale">
            <ul>
                <li><a href="#accueil">Accueil</a></li>
                <li><a href="#commerces">Commerces</a></li>
                <li><a href="#ajouter">Ajouter un commerce</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>

    <!-- Contenu principal -->
    <main id="contenu-principal">
        
        <!-- Section hero avec call-to-action -->
        <section class="hero" aria-labelledby="titre-hero">
            <h2 id="titre-hero">Découvrez la Martinique autrement</h2>
            <p class="sous-titre">
                Plus de 200 commerces locaux à Fort-de-France, 
                Lamentin et Schoelcher
            </p>
            <a href="#recherche" class="cta-button">Commencer la recherche</a>
        </section>

        <!-- Formulaire de recherche -->
        <section id="recherche" aria-labelledby="titre-recherche">
            <h2 id="titre-recherche">Trouvez votre commerce</h2>
            <!-- Le formulaire sera ajouté dans l'exercice suivant -->
        </section>

        <!-- Grille de commerces -->
        <section id="commerces-vedettes" aria-labelledby="titre-vedettes">
            <h2 id="titre-vedettes">Commerces à la une</h2>
            
            <div class="commerce-grid">
                <!-- Chaque commerce est un article autonome -->
                <article class="commerce-card" itemscope itemtype="http://schema.org/LocalBusiness">
                    <header>
                        <h3 itemprop="name">La Savane Gourmande</h3>
                        <span class="categorie" itemprop="category">Restaurant créole</span>
                    </header>
                    
                    <div class="commerce-info">
                        <p itemprop="address" itemscope itemtype="http://schema.org/PostalAddress">
                            <strong>Adresse :</strong>
                            <span itemprop="streetAddress">45 Rue Victor Hugo</span>,
                            <span itemprop="addressLocality">Fort-de-France</span>
                        </p>
                        
                        <p>
                            <strong>Téléphone :</strong>
                            <a href="tel:+596596000000" itemprop="telephone">0596 00 00 00</a>
                        </p>
                        
                        <p itemprop="description">
                            Restaurant créole authentique au cœur de Fort-de-France. 
                            Spécialités : colombo, court-bouillon, accras.
                        </p>
                    </div>
                    
                    <footer class="commerce-actions">
                        <a href="commerce.html?id=1" class="btn-details">Voir les détails</a>
                        <button class="btn-favoris" aria-label="Ajouter aux favoris">
                            ⭐ Favoris
                        </button>
                    </footer>
                </article>

                <!-- Répétez pour les autres commerces -->
            </div>
        </section>

        <!-- Catégories populaires -->
        <section id="categories" aria-labelledby="titre-categories">
            <h2 id="titre-categories">Explorer par catégorie</h2>
            
            <nav aria-label="Catégories de commerces">
                <ul class="categorie-grid">
                    <li>
                        <a href="#restaurants">
                            <figure>
                                <span class="icone" aria-hidden="true">🍽️</span>
                                <figcaption>
                                    <strong>Restaurants</strong>
                                    <data value="42">42 établissements</data>
                                </figcaption>
                            </figure>
                        </a>
                    </li>
                    <!-- Autres catégories... -->
                </ul>
            </nav>
        </section>
    </main>

    <!-- Pied de page -->
    <footer role="contentinfo">
        <section class="footer-about">
            <h3>À propos de KaribConnect</h3>
            <p>
                Projet étudiant de l'Université des Antilles 
                pour promouvoir les commerces locaux.
            </p>
        </section>
        
        <section class="footer-contact">
            <h3>Contactez-nous</h3>
            <address>
                Email : <a href="mailto:contact@karibconnect.fr">contact@karibconnect.fr</a><br>
                Tél : <a href="tel:+596596000000">0596 00 00 00</a>
            </address>
        </section>
        
        <small>&copy; 2026 KaribConnect - L1 Informatique UA</small>
    </footer>

</body>
</html>
```

**Points clés à noter :**
- Attributs ARIA pour l'accessibilité
- Microdata schema.org pour le SEO
- Structure hiérarchique claire (h1 > h2 > h3)
- Balises sémantiques partout

**✅ Checkpoint :** Valider le HTML sur https://validator.w3.org

---

### Exercice 2 : Formulaire de recherche avancé (35min)

**Créer un formulaire de recherche avec tous les types d'inputs modernes :**

```html
<section id="recherche" aria-labelledby="titre-recherche">
    <h2 id="titre-recherche">Trouvez votre commerce idéal</h2>
    
    <form class="search-form" action="/search" method="GET" role="search">
        
        <!-- Recherche textuelle -->
        <fieldset>
            <legend>Que recherchez-vous ?</legend>
            
            <div class="form-group">
                <label for="query">
                    Nom, produit ou service :
                </label>
                <input 
                    type="search" 
                    id="query" 
                    name="q" 
                    placeholder="Ex: Coiffeur, Restaurant créole..."
                    autocomplete="off"
                    aria-describedby="query-help"
                >
                <small id="query-help">
                    Saisissez au moins 3 caractères pour lancer la recherche
                </small>
            </div>
        </fieldset>

        <!-- Localisation -->
        <fieldset>
            <legend>Où ?</legend>
            
            <div class="form-group">
                <label for="ville">Ville :</label>
                <select id="ville" name="ville" required>
                    <option value="">Sélectionnez une ville</option>
                    <optgroup label="Centre">
                        <option value="fort-de-france">Fort-de-France</option>
                        <option value="lamentin">Lamentin</option>
                        <option value="schoelcher">Schoelcher</option>
                    </optgroup>
                    <optgroup label="Sud">
                        <option value="ducos">Ducos</option>
                        <option value="riviere-salee">Rivière-Salée</option>
                        <option value="trois-ilets">Trois-Îlets</option>
                    </optgroup>
                    <optgroup label="Nord">
                        <option value="trinite">Trinité</option>
                        <option value="robert">Robert</option>
                    </optgroup>
                </select>
            </div>

            <div class="form-group">
                <label for="rayon">Rayon de recherche :</label>
                <input 
                    type="range" 
                    id="rayon" 
                    name="rayon" 
                    min="1" 
                    max="20" 
                    value="5"
                    step="1"
                    oninput="rayonValue.textContent = this.value"
                >
                <output id="rayonValue">5</output> km
            </div>
        </fieldset>

        <!-- Catégorie et filtres -->
        <fieldset>
            <legend>Précisez votre recherche</legend>
            
            <div class="form-group">
                <label for="categorie">Catégorie :</label>
                <select id="categorie" name="categorie">
                    <option value="">Toutes catégories</option>
                    <option value="alimentation">🛒 Alimentation</option>
                    <option value="restaurant">🍽️ Restaurants</option>
                    <option value="vetements">👕 Vêtements</option>
                    <option value="electronique">📱 Électronique</option>
                    <option value="beaute">💇 Beauté & Bien-être</option>
                    <option value="services">🔧 Services</option>
                    <option value="sante">⚕️ Santé</option>
                    <option value="loisirs">🎮 Loisirs</option>
                </select>
            </div>

            <!-- Fourchette de prix -->
            <div class="form-group">
                <label>Gamme de prix :</label>
                <div class="checkbox-group">
                    <label>
                        <input type="checkbox" name="prix[]" value="economique">
                        € Économique
                    </label>
                    <label>
                        <input type="checkbox" name="prix[]" value="moyen">
                        €€ Moyen
                    </label>
                    <label>
                        <input type="checkbox" name="prix[]" value="premium">
                        €€€ Premium
                    </label>
                </div>
            </div>

            <!-- Services disponibles -->
            <div class="form-group">
                <label>Services :</label>
                <div class="checkbox-group">
                    <label>
                        <input type="checkbox" name="services[]" value="livraison">
                        🚚 Livraison
                    </label>
                    <label>
                        <input type="checkbox" name="services[]" value="parking">
                        🅿️ Parking
                    </label>
                    <label>
                        <input type="checkbox" name="services[]" value="wifi">
                        📶 WiFi gratuit
                    </label>
                    <label>
                        <input type="checkbox" name="services[]" value="accessible">
                        ♿ Accessible PMR
                    </label>
                </div>
            </div>

            <!-- Horaires d'ouverture -->
            <div class="form-group">
                <label>Ouvert maintenant :</label>
                <div class="radio-group">
                    <label>
                        <input type="radio" name="ouverture" value="all" checked>
                        Peu importe
                    </label>
                    <label>
                        <input type="radio" name="ouverture" value="now">
                        Actuellement ouvert
                    </label>
                    <label>
                        <input type="radio" name="ouverture" value="today">
                        Ouvert aujourd'hui
                    </label>
                </div>
            </div>
        </fieldset>

        <!-- Boutons d'action -->
        <div class="form-actions">
            <button type="submit" class="btn-primary">
                🔍 Rechercher
            </button>
            <button type="reset" class="btn-secondary">
                ↺ Réinitialiser
            </button>
        </div>
    </form>
</section>
```

**✅ Checkpoint :** Tester tous les champs du formulaire

---

### Exercice 3 : Page "Ajouter un commerce" (40min)

**Créer un nouveau fichier `ajouter-commerce.html` :**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ajouter un commerce - KaribConnect</title>
</head>
<body>

<header>
    <h1>🌴 KaribConnect</h1>
    <nav>
        <a href="index.html">← Retour à l'accueil</a>
    </nav>
</header>

<main>
    <h2>Ajouter votre commerce</h2>
    <p>Remplissez ce formulaire pour référencer votre établissement sur KaribConnect</p>

    <form action="/api/commerces" method="POST" enctype="multipart/form-data">
        
        <!-- Étape 1 : Informations générales -->
        <section>
            <h3>1️⃣ Informations générales</h3>
            
            <div class="form-group">
                <label for="nom-commerce">Nom du commerce * :</label>
                <input 
                    type="text" 
                    id="nom-commerce" 
                    name="nom" 
                    required
                    minlength="3"
                    maxlength="100"
                    placeholder="Ex: La Savane Gourmande"
                >
            </div>

            <div class="form-group">
                <label for="categorie">Catégorie * :</label>
                <select id="categorie" name="categorie" required>
                    <option value="">Sélectionnez une catégorie</option>
                    <option value="alimentation">Alimentation</option>
                    <option value="restaurant">Restaurant</option>
                    <option value="vetements">Vêtements</option>
                    <option value="electronique">Électronique</option>
                    <option value="beaute">Beauté & Bien-être</option>
                    <option value="services">Services</option>
                </select>
            </div>

            <div class="form-group">
                <label for="description">Description * :</label>
                <textarea 
                    id="description" 
                    name="description" 
                    required
                    minlength="50"
                    maxlength="500"
                    rows="5"
                    placeholder="Décrivez votre commerce, vos produits et services..."
                ></textarea>
                <small>Minimum 50 caractères</small>
            </div>
        </section>

        <!-- Étape 2 : Coordonnées -->
        <section>
            <h3>2️⃣ Coordonnées</h3>
            
            <div class="form-group">
                <label for="adresse">Adresse * :</label>
                <input 
                    type="text" 
                    id="adresse" 
                    name="adresse" 
                    required
                    placeholder="Numéro et nom de rue"
                >
            </div>

            <div class="form-row">
                <div class="form-group">
                    <label for="code-postal">Code postal * :</label>
                    <input 
                        type="text" 
                        id="code-postal" 
                        name="code-postal" 
                        required
                        pattern="972\d{2}"
                        placeholder="97200"
                    >
                </div>

                <div class="form-group">
                    <label for="ville">Ville * :</label>
                    <input 
                        type="text" 
                        id="ville" 
                        name="ville" 
                        required
                        placeholder="Fort-de-France"
                    >
                </div>
            </div>

            <div class="form-row">
                <div class="form-group">
                    <label for="telephone">Téléphone * :</label>
                    <input 
                        type="tel" 
                        id="telephone" 
                        name="telephone" 
                        required
                        pattern="0[5-7][0-9]{8}"
                        placeholder="0596123456"
                    >
                </div>

                <div class="form-group">
                    <label for="email">Email :</label>
                    <input 
                        type="email" 
                        id="email" 
                        name="email"
                        placeholder="contact@exemple.com"
                    >
                </div>
            </div>

            <div class="form-group">
                <label for="site-web">Site web :</label>
                <input 
                    type="url" 
                    id="site-web" 
                    name="site-web"
                    placeholder="https://www.exemple.com"
                >
            </div>
        </section>

        <!-- Étape 3 : Horaires -->
        <section>
            <h3>3️⃣ Horaires d'ouverture</h3>
            
            <fieldset>
                <legend>Jours d'ouverture :</legend>
                
                <div class="horaires-group">
                    <label>
                        <input type="checkbox" name="jours[]" value="lundi" checked>
                        Lundi
                    </label>
                    <input type="time" name="lundi-ouverture" value="08:00">
                    à
                    <input type="time" name="lundi-fermeture" value="18:00">
                </div>

                <div class="horaires-group">
                    <label>
                        <input type="checkbox" name="jours[]" value="mardi" checked>
                        Mardi
                    </label>
                    <input type="time" name="mardi-ouverture" value="08:00">
                    à
                    <input type="time" name="mardi-fermeture" value="18:00">
                </div>

                <!-- Répéter pour les autres jours -->
                
                <div class="horaires-group">
                    <label>
                        <input type="checkbox" name="jours[]" value="dimanche">
                        Dimanche
                    </label>
                    <input type="time" name="dimanche-ouverture">
                    à
                    <input type="time" name="dimanche-fermeture">
                </div>
            </fieldset>
        </section>

        <!-- Étape 4 : Services et options -->
        <section>
            <h3>4️⃣ Services proposés</h3>
            
            <fieldset>
                <legend>Sélectionnez tous les services disponibles :</legend>
                
                <div class="checkbox-grid">
                    <label>
                        <input type="checkbox" name="services[]" value="livraison">
                        🚚 Livraison à domicile
                    </label>
                    <label>
                        <input type="checkbox" name="services[]" value="click-collect">
                        📦 Click & Collect
                    </label>
                    <label>
                        <input type="checkbox" name="services[]" value="parking">
                        🅿️ Parking disponible
                    </label>
                    <label>
                        <input type="checkbox" name="services[]" value="wifi">
                        📶 WiFi gratuit
                    </label>
                    <label>
                        <input type="checkbox" name="services[]" value="cb">
                        💳 Paiement CB
                    </label>
                    <label>
                        <input type="checkbox" name="services[]" value="accessible">
                        ♿ Accessible PMR
                    </label>
                </div>
            </fieldset>

            <div class="form-group">
                <label for="gamme-prix">Gamme de prix :</label>
                <select id="gamme-prix" name="gamme-prix">
                    <option value="economique">€ Économique</option>
                    <option value="moyen" selected>€€ Moyen</option>
                    <option value="premium">€€€ Premium</option>
                </select>
            </div>
        </section>

        <!-- Étape 5 : Photos -->
        <section>
            <h3>5️⃣ Photos de votre commerce</h3>
            
            <div class="form-group">
                <label for="photo-principale">Photo principale * :</label>
                <input 
                    type="file" 
                    id="photo-principale" 
                    name="photo-principale" 
                    accept="image/jpeg,image/png,image/webp"
                    required
                >
                <small>Formats acceptés : JPG, PNG, WebP (max 5 Mo)</small>
            </div>

            <div class="form-group">
                <label for="photos-galerie">Galerie photos (optionnel) :</label>
                <input 
                    type="file" 
                    id="photos-galerie" 
                    name="photos-galerie" 
                    accept="image/jpeg,image/png,image/webp"
                    multiple
                >
                <small>Ajoutez jusqu'à 10 photos supplémentaires</small>
            </div>
        </section>

        <!-- Conditions -->
        <section>
            <div class="form-group">
                <label>
                    <input type="checkbox" name="cgv" required>
                    J'accepte les <a href="cgv.html" target="_blank">conditions générales d'utilisation</a> *
                </label>
            </div>

            <div class="form-group">
                <label>
                    <input type="checkbox" name="newsletter">
                    Je souhaite recevoir les actualités de KaribConnect
                </label>
            </div>
        </section>

        <!-- Actions finales -->
        <div class="form-actions">
            <button type="submit" class="btn-primary">
                ✅ Publier mon commerce
            </button>
            <button type="reset" class="btn-secondary">
                ↺ Réinitialiser le formulaire
            </button>
        </div>

        <p class="form-note">
            * Champs obligatoires<br>
            Votre commerce sera vérifié avant publication (délai 24-48h)
        </p>
    </form>
</main>

<footer>
    <p>&copy; 2026 KaribConnect</p>
</footer>

</body>
</html>
```

---

## 🚀 Exercices bonus

### Bonus 1 : Tableau de données
Créer une page `commerces-liste.html` avec un tableau HTML listant tous les commerces :
- Colonnes : Nom, Catégorie, Ville, Téléphone, Note
- Tri par colonne (attribut `data-sort`)
- Styles alternés pour les lignes (`<tbody>`)

### Bonus 2 : Formulaire multi-étapes
Transformer le formulaire d'ajout en formulaire multi-étapes avec :
- Navigation entre étapes (précédent/suivant)
- Barre de progression
- Sauvegarde automatique dans localStorage

### Bonus 3 : Accessibilité avancée
- Tester avec un lecteur d'écran (NVDA ou JAWS)
- Ajouter des live regions pour les messages dynamiques
- Créer un "skip to content" link

---

## 📚 Ressources

### Validation et accessibilité
- HTML Validator : https://validator.w3.org
- WAVE Accessibility Tool : https://wave.webaim.org
- axe DevTools : extension Chrome

### Documentation
- MDN Forms : https://developer.mozilla.org/fr/docs/Learn/Forms
- ARIA Authoring Practices : https://www.w3.org/WAI/ARIA/apg/
- Schema.org LocalBusiness : https://schema.org/LocalBusiness

---

## 📝 À rendre

1. **3 fichiers HTML :**
   - `index.html` (version sémantique optimisée)
   - `ajouter-commerce.html` (formulaire complet)
   - `commerce-detail.html` (page détail avec tous les attributs sémantiques)

2. **Commit Git :** `"TP2: HTML sémantique et formulaires avancés"`

3. **Rapport d'accessibilité :**
   - Screenshot du rapport WAVE
   - Liste des améliorations apportées


