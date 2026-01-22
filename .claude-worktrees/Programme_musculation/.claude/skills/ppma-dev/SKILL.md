---
name: ppma-dev
description: Developpeur pour l'application PPMA. HTML, JavaScript, CSS, Firebase Realtime Database. Use when modifying the app code, fixing bugs, adding features to index.html, or working with Firebase.
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - Bash
model: claude-sonnet-4-20250514
user-invocable: true
---

# DEVELOPPEUR PPMA

## Role

Developpeur de l'application PPMA - une single-page app HTML/JS avec Firebase.

## Stack Technique

| Composant | Technologie |
|-----------|-------------|
| Frontend | HTML5 + Vanilla JS |
| Styling | CSS Variables (Gold Premium Theme) |
| Database | Firebase Realtime Database |
| Charts | Chart.js |
| Fonts | Playfair Display + Inter |

## Structure du Code (index.html)

```
index.html (~280K)
├── <head>
│   ├── Meta tags (PWA)
│   ├── Google Fonts
│   ├── Chart.js CDN
│   ├── Firebase SDK
│   └── <style> (CSS complet)
└── <body>
    ├── <header>
    ├── <main>
    │   ├── Navigation
    │   ├── Dashboard
    │   ├── Programme (cycles, semaines)
    │   ├── Statistiques
    │   └── Settings
    └── <script>
        ├── Firebase Config
        ├── State Management
        ├── Data Functions (load/save)
        ├── UI Functions
        └── Event Listeners
```

## Firebase Configuration

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyA-jtvoM8Y7GhryZOz1zRLVD7Z9DFBfBb0",
  databaseURL: "https://ppma-58000-default-rtdb.europe-west1.firebasedatabase.app",
  // ...
};

// Structure donnees
users/
└── [userId]/
    └── data/
        ├── lastModified
        ├── sessions[]
        ├── prs{}
        └── settings{}
```

## Design System

### Variables CSS

```css
:root {
  /* Palette Gold Premium */
  --gold: #C9A962;
  --gold-light: #E8D5A3;
  --gold-dark: #8B7355;

  /* Palette Sombre */
  --black: #1A1A1A;
  --anthracite: #2D2D2D;
  --charcoal: #3D3D3D;

  /* Couleurs Muscles */
  --pecs: #E74C3C;
  --dos: #3498DB;
  --epaules: #9B59B6;
  --bras: #E67E22;
  --jambes: #27AE60;
}
```

## Patterns de Code

### State Management

```javascript
const state = {
  data: {
    sessions: [],
    prs: {},
    settings: {}
  },
  ui: {
    currentView: 'dashboard',
    selectedWeek: 1
  }
};
```

### Sync Firebase

```javascript
// Sauvegarder
function saveData() {
  state.data.lastModified = Date.now();
  localStorage.setItem(STORAGE_KEY, JSON.stringify(state.data));
  saveToCloud();
}

// Charger avec sync temps reel
function loadData() {
  // Local d'abord (offline)
  // Puis listener Firebase pour sync
}
```

## Bonnes Pratiques

1. **Pas de frameworks** - Vanilla JS uniquement
2. **Mobile-first** - Responsive avec media queries
3. **Offline-first** - localStorage + Firebase sync
4. **Performance** - Pas de dependencies lourdes
5. **Accessibilite** - Aria labels, contraste

## Checklist Modification

- [ ] Tester sur mobile
- [ ] Verifier sync Firebase
- [ ] Pas d'erreurs console
- [ ] CSS responsive
- [ ] Backup avant modif majeure

---

*Agent Dev - PPMA v1.0*
