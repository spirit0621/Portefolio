# Architecture détaillée - Portfolio

## Diagramme d'architecture globale

```
┌─────────────────────────────────────────────────────────┐
│                    PORTFOLIO SITE                        │
├─────────────────────────────────────────────────────────┤
│                                                           │
│  ┌──────────────────────────────────────────────────┐   │
│  │           LAYER: PRESENTATION (HTML)             │   │
│  │                                                   │   │
│  │  index.html, presentation.html, projects.html   │   │
│  │  portfolio.html, monitoring.html, bts-sio.html  │   │
│  │  services.html, contact.html, about.html        │   │
│  │                                                   │   │
│  └──────────────────────────────────────────────────┘   │
│                           ↓                              │
│  ┌──────────────────────────────────────────────────┐   │
│  │         LAYER: STYLING (CSS3 + Variables)        │   │
│  │                                                   │   │
│  │           styles.css (15KB)                      │   │
│  │    - Variables CSS pour theming                  │   │
│  │    - Grid/Flexbox layouts                        │   │
│  │    - Media queries responsive                    │   │
│  │    - Animations et transitions                   │   │
│  │                                                   │   │
│  └──────────────────────────────────────────────────┘   │
│                           ↓                              │
│  ┌──────────────────────────────────────────────────┐   │
│  │    LAYER: INTERACTIVITY (JavaScript)             │   │
│  │                                                   │   │
│  │           nav.js (navigation active)             │   │
│  │         Embedded scripts (portfo.js, etc)        │   │
│  │                                                   │   │
│  └──────────────────────────────────────────────────┘   │
│                           ↓                              │
│  ┌──────────────────────────────────────────────────┐   │
│  │      LAYER: STATIC ASSETS (Photo/)               │   │
│  │                                                   │   │
│  │    12 images PNG (captures d'écran)              │   │
│  │                                                   │   │
│  └──────────────────────────────────────────────────┘   │
│                           ↓                              │
│  ┌──────────────────────────────────────────────────┐   │
│  │    DEPLOYMENT: GitHub Pages / HTTP Server        │   │
│  │                                                   │   │
│  │    https://github.com/spirit0621/Portefolio     │   │
│  │                                                   │   │
│  └──────────────────────────────────────────────────┘   │
│                                                           │
└─────────────────────────────────────────────────────────┘
```

---

## Structure de fichiers détaillée

### Racine du projet

```
Portefolio/
│
├── 📄 HTML Pages (8 fichiers)
│   ├── index.html                 # 2.25 KB - Accueil
│   ├── presentation.html          # 3.49 KB - Présentation
│   ├── projects.html              # 4.94 KB - Projets
│   ├── portfolio.html             # 3.45 KB - Portfolio
│   ├── monitoring.html            # 6.14 KB - Veille tech
│   ├── bts-sio.html              # 6.43 KB - BTS SIO
│   ├── services.html              # 4.53 KB - Services
│   ├── contact.html               # 3.72 KB - Contact
│   └── about.html                 # 3.21 KB - À propos
│
├── 🎨 Styling
│   └── styles.css                 # 15.3 KB - Feuille de styles
│
├── 🔧 Scripts
│   ├── nav.js                     # 530 B - Navigation active
│   └── viewer.html                # 1.43 KB - Visualiseur images
│
├── 🖼️  Assets
│   └── Photo/
│       ├── Capture d'écran 2026-01-14 113034.png
│       ├── Capture d'écran 2026-01-14 113058.png
│       ├── [... 10 autres images ...]
│       └── Capture d'écran 2026-01-14 113418.png
│
├── 📚 Documentation
│   ├── README.md                  # Ce fichier
│   └── ARCHITECTURE.md            # Détails architecture
│
├── 📖 Configuration
│   ├── README.md                  # Info repo
│   ├── .gitignore                 # Fichiers ignorés
│   └── .git/                      # Repo Git
│
└── 🔐 CI/CD
    └── (GitHub Actions - implicite)
```

### Taille totale du projet

```
HTML Files:      ~45 KB
CSS:             ~15 KB  
JavaScript:      ~2 KB
Images (12):     ~3-5 MB (selon qualité)
Documentation:   ~50 KB
─────────────────────────
TOTAL:           ~3.1 MB
```

---

## Flux de données

### 1. Chargement initial (User → Browser)

```
1. Utilisateur accède http://localhost:8000
    ↓
2. Browser demande index.html au serveur
    ↓
3. Serveur retourne HTML
    ↓
4. Browser parse HTML et charge :
    - styles.css (via <link>)
    - nav.js (via <script> en fin de body)
    ↓
5. Document Ready (DOMContentLoaded)
    ↓
6. nav.js exécute :
   - Détecte page actuelle
   - Ajoute classe .active aux liens
    ↓
7. Page affichée (rendu complet)
```

### 2. Navigation inter-pages

```
User clique lien (ex: projects.html)
    ↓
Browser charge projects.html
    ↓
Même processus : CSS → JS → Active link
    ↓
Page affichée
```

### 3. Chargement images

```
HTML référence Photo/image.png
    ↓
Browser demande image
    ↓
Serveur retourne image PNG
    ↓
CSS applique (object-fit: cover)
    ↓
Image affichée responsive
```

---

## Composants réutilisables

### 1. Navigation Bar

```html
<nav class="navbar">
  <div class="nav-container">
    <a href="index.html" class="nav-logo">Alves Fernandes</a>
    <ul class="nav-menu">
      <li><a href="index.html" class="nav-link active">Accueil</a></li>
      <li><a href="presentation.html" class="nav-link">Présentation</a></li>
      <!-- ... autres liens ... -->
    </ul>
  </div>
</nav>
```

**CSS associé :**
```css
.navbar { position: sticky; top: 0; z-index: 100; }
.nav-link.active { border-bottom: 2px solid var(--secondary); }
```

### 2. Page Hero

```html
<section class="page-hero">
  <div class="container">
    <h1>Titre de page</h1>
    <p>Sous-titre descriptif</p>
  </div>
</section>
```

**CSS :**
```css
.page-hero {
  background: linear-gradient(135deg, var(--primary) 0%, var(--secondary) 100%);
  color: white;
  padding: 80px 20px;
  text-align: center;
}
```

### 3. Card composant

**Variant: Service Card**
```html
<div class="service-card">
  <h3>Titre</h3>
  <p>Description</p>
</div>
```

**Variant: Project Card**
```html
<div class="project-card">
  <div class="project-image">
    <img src="Photo/image.png" alt="Projet">
  </div>
  <div class="project-info">
    <h3>Titre</h3>
    <p class="project-category">Catégorie</p>
  </div>
</div>
```

### 4. Grid système

```css
/* 1. Auto-fit responsive grid */
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

/* 2. Fixed columns grid */
.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

/* 3. 2-column layout */
.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
}
```

---

## Variables CSS

### Palette de couleurs

```css
:root {
  /* Primaire : Bleu-gris foncé */
  --primary: #2c3e50;
  
  /* Secondaire : Bleu clair */
  --secondary: #3498db;
  
  /* Accent : Rouge */
  --accent: #e74c3c;
  
  /* Neutres */
  --light: #ecf0f1;      /* Fond clair */
  --dark: #1a1a1a;       /* Texte foncé */
  --text: #333;          /* Texte normal */
  --border: #ddd;        /* Bordures */
}
```

### Utilisation des variables

```css
/* Avant (hardcoded) */
.button { color: #2c3e50; background: #3498db; }
.button:hover { background: #2980b9; }

/* Après (variables) */
.button { color: var(--primary); background: var(--secondary); }
.button:hover { background: darken(var(--secondary), 10%); }

/* Avantage : Changer 1 variable = mise à jour partout */
```

---

## Responsive breakpoints

```css
/* Mobile First Approach */

/* Défaut : Mobile (0px - 480px) */
.nav-menu { gap: 0.5rem; font-size: 0.8rem; }

/* Tablet (481px - 768px) */
@media (max-width: 768px) {
  .nav-menu { gap: 1rem; font-size: 0.9rem; }
  .about-grid { grid-template-columns: 1fr; }
  .contact-grid { grid-template-columns: 1fr; }
}

/* Desktop (769px+) */
@media (min-width: 769px) {
  .nav-menu { gap: 2rem; font-size: 1rem; }
  .about-grid { grid-template-columns: 1fr 1fr; }
}

/* Breakpoints utilisés */
480px  - Mobile petit
768px  - Tablet/Mobile grand
1000px - Desktop standard
```

---

## Système d'animation

### Transitions

```css
/* Navigation link */
.nav-link {
  transition: color 0.3s ease, border-bottom 0.3s ease;
}

/* Gallery item hover */
.gallery-item {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
```

### Transforms

```css
/* Subtle lift effect */
.project-card:hover {
  transform: translateY(-5px);        /* Déplace vers le haut */
}

/* CTA button */
.cta-button:hover {
  transform: translateY(-2px);         /* Petit déplacement */
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
}
```

### Shadow system

```css
/* Ombre douce */
box-shadow: 0 2px 8px rgba(0,0,0,0.1);

/* Ombre moyenne */
box-shadow: 0 4px 10px rgba(0,0,0,0.1);

/* Ombre prononcée (hover) */
box-shadow: 0 8px 20px rgba(0,0,0,0.2);
```

---

## JavaScript architectural

### Module pattern

```javascript
// nav.js - Gestion de la navigation
(function() {
  document.addEventListener('DOMContentLoaded', function() {
    // 1. Déterminer page active
    const currentPage = window.location.pathname.split('/').pop() || 'index.html';
    
    // 2. Sélectionner tous les liens
    const navLinks = document.querySelectorAll('.nav-link');
    
    // 3. Itérer et marquer l'actif
    navLinks.forEach(link => {
      const href = link.getAttribute('href');
      if (href === currentPage || (currentPage === '' && href === 'index.html')) {
        link.classList.add('active');
      } else {
        link.classList.remove('active');
      }
    });
  });
})();
```

### DOM Manipulation (portfolio.html)

```javascript
// Créer éléments dynamiquement
const gallery = document.getElementById('gallery');

photos.forEach(name => {
  // 1. Créer container
  const item = document.createElement('div');
  item.className = 'gallery-item';
  
  // 2. Créer image
  const img = document.createElement('img');
  img.alt = name;
  img.src = encodeURI('Photo/' + name);  // Encode pour caractères spéciaux
  
  // 3. Assembler
  item.appendChild(img);
  gallery.appendChild(item);
});
```

### Event Handling (contact.html)

```javascript
// Gestion du formulaire
document.getElementById('contactForm').addEventListener('submit', function(e) {
  e.preventDefault();                    // Empêcher envoi par défaut
  
  const formData = new FormData(this);
  
  // Simuler envoi (en prod : requête POST)
  alert('Merci pour votre message !');
  this.reset();                          // Réinitialiser form
});
```

---

## Performance optimizations

### Téchniques appliquées

```css
/* 1. CSS Variables au lieu de duplication */
:root { --color: #3498db; }
.element { color: var(--color); }  /* Réutilisable */

/* 2. Shorthand properties */
margin: 1rem;              /* Au lieu de margin-top, bottom, etc */

/* 3. Minimal selectors */
.gallery-item img {}       /* Spécifique, pas .gallery > div > img */

/* 4. Hardware acceleration */
.gallery-item {
  transform: translateZ(0); /* GPU acceleration */
}

/* 5. Lazy loading conceptuel */
<img src="..." loading="lazy" />
```

### Bundling pour production

```bash
# Minifier CSS (optionnel)
cssnano styles.css > styles.min.css

# Compresser images
imagemin Photo/*.png --out-dir=Photo

# Résultat : site encore plus rapide
```

---

## Extensibilité

### Ajouter une nouvelle page

```
1. Créer new-page.html
   ├── Copier structure HTML de base
   ├── Ajouter class="active" au bon lien nav
   └── Ajouter contenu dans section principale

2. Ajouter CSS pour cette page
   └── Ajouter dans styles.css ou <style> en head

3. Ajouter JavaScript si besoin
   └── Créer new-page.js et importer

4. Mettre à jour toutes les navigations
   ├── index.html
   ├── presentation.html
   ├── ... tous les fichiers ...
```

### Ajouter un nouveau style de card

```css
/* Nouveau composant */
.testimonial-card {
  background: var(--light);
  padding: 1.5rem;
  border-left: 4px solid var(--secondary);
  border-radius: 8px;
}

.testimonial-card:hover {
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  transform: translateY(-2px);
}

/* Utiliser partout avec une classe */
<div class="testimonial-card">
  <p>"Citation ..."</p>
</div>
```

---

## Versioning et maintenance

### Historique versioning

```
v1.0 (44ede1b) - Portfolio single page
v1.1 (134261f) - Multi-pages restructuration
v2.0 (22470e9) - Ajout pages: Présentation, Projets, Veille, BTS SIO
v2.1 (CURRENT) - Documentation technique
```

### Branches futures

```
main          - Production
dev           - Développement
feature/...   - Nouvelles fonctionnalités
```

---

## Checklist de deployment

- [ ] Tous les liens fonctionnent
- [ ] Navigation active correcte
- [ ] Images responsive sur tous les écrans
- [ ] Pas de console errors (F12)
- [ ] CSS appliqué correctement
- [ ] JavaScript fonctionne
- [ ] Forms testés
- [ ] Lighthouse score > 90
- [ ] Push vers main
- [ ] GitHub Pages à jour

---

**Architecture version:** 2.0
**Last updated:** 15 janvier 2026
