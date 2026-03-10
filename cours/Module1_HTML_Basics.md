# Module 1 - Séance 1 : Introduction au Web et HTML Basics
## Durée : 2h (20min CI + 1h40 TP)

---

## 📋 COURS THÉORIQUE (CI) - 20 minutes

### 1. Comment fonctionne le Web ? (5min)

**Modèle Client-Serveur**
```
Navigateur (Client) ←──HTTP──→ Serveur Web
      ↓                           ↓
   Affiche                    Stocke
   les pages                  les fichiers
```

**Le trio magique du Web :**
- **HTML** : Structure et contenu (le squelette)
- **CSS** : Présentation et style (la peau)
- **JavaScript** : Comportement et interactivité (les muscles)

**Requête HTTP simplifié :**
1. Vous tapez une URL : `https://karibconnect.com`
2. Le navigateur envoie une requête au serveur
3. Le serveur renvoie les fichiers (HTML, CSS, JS, images)
4. Le navigateur affiche la page

---

### 2. Anatomie d'une page HTML (10min)

**Structure de base :**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ma Première Page</title>
</head>
<body>
    <h1>Bienvenue sur KaribConnect</h1>
    <p>Découvrez les commerces de Martinique</p>
</body>
</html>
```

**Explication de chaque élément :**
- `<!DOCTYPE html>` : Déclare que c'est du HTML5
- `<html lang="fr">` : Élément racine, langue française
- `<head>` : Métadonnées (invisibles à l'écran)
- `<meta charset="UTF-8">` : Encodage des caractères (accents, créole)
- `<meta name="viewport">` : Responsive design (mobile-first)
- `<title>` : Titre dans l'onglet du navigateur
- `<body>` : Contenu visible de la page

---

### 3. Les balises HTML essentielles (5min)

**Balises de structure :**
- `<h1>` à `<h6>` : Titres (hiérarchie)
- `<p>` : Paragraphe
- `<div>` : Conteneur générique
- `<span>` : Conteneur en ligne

**Balises sémantiques :**
- `<header>` : En-tête de page/section
- `<nav>` : Navigation
- `<main>` : Contenu principal
- `<section>` : Section thématique
- `<article>` : Contenu autonome
- `<footer>` : Pied de page

**Balises de contenu :**
- `<a href="">` : Lien hypertexte
- `<img src="" alt="">` : Image
- `<ul>` / `<ol>` / `<li>` : Listes
- `<button>` : Bouton cliquable

**Pourquoi la sémantique ?**
✅ Accessibilité (lecteurs d'écran)
✅ SEO (référencement Google)
✅ Maintenance du code
✅ Standards du Web

---

## 💻 TRAVAUX PRATIQUES (TP1) - 1h40

### Objectif
Créer la page d'accueil de **KaribConnect** avec HTML pur.

---

### Exercice 1 : Configuration de l'environnement (15min)

**1.1 Installation VS Code (si nécessaire)**
- Télécharger depuis https://code.visualstudio.com
- Extensions à installer :
  - Live Server (Ritwick Dey)
  - Prettier (formateur de code)
  - Auto Rename Tag

**1.2 Créer la structure du projet**
```bash
# Créer le dossier du projet
mkdir karibconnect
cd karibconnect

# Créer les fichiers
touch index.html
mkdir css js images

# Structure obtenue :
# karibconnect/
#   ├── index.html
#   ├── css/
#   ├── js/
#   └── images/
```

**1.3 Initialiser Git**
```bash
git init
git add .
git commit -m "Initial commit: project structure"
```

**1.4 Tester Live Server**
- Ouvrir `index.html` dans VS Code
- Clic droit → "Open with Live Server"
- Vérifier que la page s'ouvre dans le navigateur

---

### Exercice 2 : Structure HTML de base (20min)

**Créer le fichier `index.html` avec cette structure :**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Découvrez les meilleurs commerces et services de Martinique">
    <title>KaribConnect - Commerces de Martinique</title>
</head>
<body>
    <!-- En-tête de la page -->
    <header>
        <h1>🌴 KaribConnect</h1>
        <p>Votre guide des commerces martiniquais</p>
    </header>

    <!-- Navigation principale -->
    <nav>
        <ul>
            <li><a href="#accueil">Accueil</a></li>
            <li><a href="#commerces">Commerces</a></li>
            <li><a href="#restaurants">Restaurants</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>

    <!-- Contenu principal -->
    <main>
        <!-- Section hero -->
        <section id="accueil">
            <h2>Découvrez la Martinique autrement</h2>
            <p>Plus de 200 commerces locaux référencés à Fort-de-France, Lamentin et Schoelcher</p>
        </section>

        <!-- Section commerces vedettes -->
        <section id="commerces-vedettes">
            <h2>Commerces à la une</h2>
            <p>Découvrez nos partenaires vedettes</p>
        </section>
    </main>

    <!-- Pied de page -->
    <footer>
        <p>&copy; 2026 KaribConnect - Université des Antilles</p>
    </footer>
</body>
</html>
```

**✅ Checkpoint :** Vérifier que la page s'affiche avec Live Server

---

### Exercice 3 : Ajouter des commerces (30min)

**Créer 3 cartes de commerces dans la section `#commerces-vedettes` :**

```html
<section id="commerces-vedettes">
    <h2>Commerces à la une</h2>
    
    <!-- Commerce 1 : Restaurant -->
    <article>
        <h3>🍽️ La Savane Gourmande</h3>
        <p><strong>Catégorie :</strong> Restaurant créole</p>
        <p><strong>Adresse :</strong> 45 Rue Victor Hugo, Fort-de-France</p>
        <p><strong>Téléphone :</strong> 0596 XX XX XX</p>
        <p>
            Restaurant créole authentique au cœur de Fort-de-France. 
            Spécialités : colombo, court-bouillon, accras.
        </p>
        <button>Voir les détails</button>
    </article>

    <!-- Commerce 2 : Épicerie -->
    <article>
        <h3>🛒 Epice Express</h3>
        <p><strong>Catégorie :</strong> Épicerie locale</p>
        <p><strong>Adresse :</strong> 12 Avenue des Caraïbes, Lamentin</p>
        <p><strong>Horaires :</strong> Lun-Sam 7h-20h</p>
        <p>
            Produits frais et locaux. Fruits, légumes pays, épices créoles.
            Livraison à domicile disponible.
        </p>
        <button>Voir les détails</button>
    </article>

    <!-- Commerce 3 : Service -->
    <article>
        <h3>🔧 TechKarib Réparation</h3>
        <p><strong>Catégorie :</strong> Réparation électronique</p>
        <p><strong>Adresse :</strong> Zone Industrielle, Schoelcher</p>
        <p><strong>Services :</strong> Smartphones, ordinateurs, tablettes</p>
        <p>
            Réparation rapide de vos appareils électroniques. 
            Diagnostic gratuit, garantie 3 mois.
        </p>
        <button>Voir les détails</button>
    </article>
</section>
```

**✅ Checkpoint :** Vous devez voir 3 cartes de commerces

---

### Exercice 4 : Formulaire de recherche (20min)

**Ajouter un formulaire de recherche après la section hero :**

```html
<section id="recherche">
    <h2>Trouvez votre commerce</h2>
    
    <form>
        <!-- Champ de recherche par nom -->
        <div>
            <label for="nom-commerce">Nom du commerce :</label>
            <input 
                type="text" 
                id="nom-commerce" 
                name="nom-commerce" 
                placeholder="Ex: Restaurant, Coiffeur..."
            >
        </div>

        <!-- Sélection de la ville -->
        <div>
            <label for="ville">Ville :</label>
            <select id="ville" name="ville">
                <option value="">Toutes les villes</option>
                <option value="fort-de-france">Fort-de-France</option>
                <option value="lamentin">Lamentin</option>
                <option value="schoelcher">Schoelcher</option>
                <option value="ducos">Ducos</option>
                <option value="riviere-salee">Rivière-Salée</option>
            </select>
        </div>

        <!-- Sélection de la catégorie -->
        <div>
            <label for="categorie">Catégorie :</label>
            <select id="categorie" name="categorie">
                <option value="">Toutes catégories</option>
                <option value="restaurant">Restaurants</option>
                <option value="epicerie">Épiceries</option>
                <option value="vetements">Vêtements</option>
                <option value="electronique">Électronique</option>
                <option value="beaute">Beauté & Bien-être</option>
                <option value="services">Services</option>
            </select>
        </div>

        <!-- Bouton de recherche -->
        <button type="submit">🔍 Rechercher</button>
        <button type="reset">Réinitialiser</button>
    </form>
</section>
```

**✅ Checkpoint :** Le formulaire doit être visible et fonctionnel

---

### Exercice 5 : Enrichissement du contenu (15min)

**5.1 Ajouter une section "Catégories populaires"**

```html
<section id="categories">
    <h2>Explorer par catégorie</h2>
    
    <ul>
        <li>
            <a href="#restaurants">
                <span>🍽️</span>
                <strong>Restaurants</strong>
                <p>42 établissements</p>
            </a>
        </li>
        <li>
            <a href="#epiceries">
                <span>🛒</span>
                <strong>Épiceries</strong>
                <p>28 établissements</p>
            </a>
        </li>
        <li>
            <a href="#beaute">
                <span>💇</span>
                <strong>Beauté</strong>
                <p>35 établissements</p>
            </a>
        </li>
        <li>
            <a href="#services">
                <span>🔧</span>
                <strong>Services</strong>
                <p>51 établissements</p>
            </a>
        </li>
    </ul>
</section>
```

**5.2 Enrichir le footer**

```html
<footer>
    <section>
        <h3>À propos</h3>
        <p>
            KaribConnect est un projet étudiant de l'Université des Antilles 
            visant à promouvoir les commerces locaux de Martinique.
        </p>
    </section>
    
    <section>
        <h3>Contact</h3>
        <p>Email : contact@karibconnect.fr</p>
        <p>Téléphone : 0596 XX XX XX</p>
    </section>
    
    <section>
        <h3>Suivez-nous</h3>
        <ul>
            <li><a href="#">Facebook</a></li>
            <li><a href="#">Instagram</a></li>
            <li><a href="#">Twitter</a></li>
        </ul>
    </section>
    
    <p>&copy; 2026 KaribConnect - Université des Antilles - L1 Informatique</p>
</footer>
```

---

## ✅ Critères de validation TP1

### HTML valide (obligatoire)
- [ ] DOCTYPE HTML5 présent
- [ ] Encodage UTF-8 déclaré
- [ ] Balises sémantiques utilisées (header, nav, main, section, article, footer)
- [ ] Tous les attributs obligatoires présents (alt pour img, href pour a, etc.)

### Contenu minimal
- [ ] Header avec titre et description
- [ ] Navigation avec au moins 4 liens
- [ ] Section hero avec présentation
- [ ] Formulaire de recherche fonctionnel
- [ ] 3 cartes de commerces minimum
- [ ] Section catégories
- [ ] Footer complet

### Bonnes pratiques
- [ ] Indentation correcte (2 ou 4 espaces)
- [ ] Commentaires HTML pertinents
- [ ] Attributs `id` et `name` cohérents
- [ ] Structure hiérarchique des titres (h1 > h2 > h3)

---

## 🚀 Exercices bonus (pour aller plus loin)

### Bonus 1 : Page détail commerce
Créer un fichier `commerce-detail.html` avec :
- Informations complètes d'un commerce
- Galerie d'images (min 3 images)
- Horaires d'ouverture sous forme de tableau
- Formulaire de contact du commerce
- Fil d'Ariane (breadcrumb) pour la navigation

### Bonus 2 : Accessibilité
- Ajouter des attributs `aria-label` pertinents
- Tester la navigation au clavier (Tab)
- Valider le HTML sur https://validator.w3.org

### Bonus 3 : SEO
- Ajouter des balises meta Open Graph (Facebook)
- Structurer les données avec schema.org (LocalBusiness)
- Créer un fichier `robots.txt`

---

## 📚 Ressources complémentaires

### Documentation
- MDN HTML : https://developer.mozilla.org/fr/docs/Web/HTML
- HTML5 Semantic Elements : https://www.w3schools.com/html/html5_semantic_elements.asp
- Forms Guide : https://developer.mozilla.org/fr/docs/Learn/Forms

### Validation
- HTML Validator : https://validator.w3.org
- Accessibility Checker : https://wave.webaim.org

### Inspiration locale
- bizouk.com (structure de catalogue)
- kiprix.com (recherche et filtres)
- madiana.com (pages produits)

---

## 📝 À rendre pour la prochaine séance

1. **Fichier `index.html` complet** avec tous les exercices
2. **Commit Git** avec message explicite : `"TP1: Structure HTML KaribConnect"`
3. **Screenshot** de votre page dans le navigateur
4. **Questions** : noter les difficultés rencontrées

**Format de livraison :** 
- Créer un repository GitHub privé
- Inviter l'enseignant (@ roor-killa)
- Ajouter un README.md avec screenshots

---

##  Prochaine séance

**HTML Sémantique & Formulaires avancés**
- Optimisation sémantique de KaribConnect
- Formulaires multi-étapes
- Intégration de médias (images, vidéos)
- Tableaux de données

**Préparation recommandée :**
- Lire : MDN Forms Guide
- Regarder : vidéo "HTML5 Semantic HTML" (20min)
- Réfléchir : quelles améliorations pour votre page actuelle ?
