# PROMPT - Synchronisation Multi-Appareils avec Firebase

## Contexte
Je veux modifier mon application `w2pm_elite_app.html` pour que les données se synchronisent entre mon ordinateur et mon téléphone en temps réel. Actuellement l'app utilise localStorage qui ne fonctionne que localement.

## Objectif
- Données synchronisées entre tous les appareils (PC, téléphone, tablette)
- Sauvegarde automatique dans le cloud
- Fonctionne hors-ligne avec sync automatique au retour de la connexion
- Pas besoin d'ouvrir l'app sur l'ordi pour l'utiliser sur le téléphone

## Solution technique
Utiliser **Firebase Realtime Database** (gratuit).

---

## ÉTAPE 1 : Créer le projet Firebase (à faire manuellement)

1. Aller sur https://console.firebase.google.com/
2. Cliquer "Créer un projet"
3. Nom du projet : `ppma-tracking` (ou autre)
4. Désactiver Google Analytics (pas besoin)
5. Cliquer "Créer le projet"

### Activer Realtime Database :
1. Menu gauche → "Build" → "Realtime Database"
2. Cliquer "Créer une base de données"
3. Choisir "eur3 (europe-west1)" pour la localisation
4. Sélectionner "Démarrer en mode test" (pour commencer simplement)
5. Cliquer "Activer"

### Récupérer la configuration :
1. Cliquer sur l'icône ⚙️ (engrenage) → "Paramètres du projet"
2. Descendre jusqu'à "Vos applications"
3. Cliquer sur l'icône `</>` (Web)
4. Nom de l'app : "PPMA Web"
5. Copier les valeurs de `firebaseConfig`

---

## ÉTAPE 2 : Modifier le fichier HTML

### 2.1 - Ajouter le SDK Firebase dans le `<head>`

Chercher la ligne `<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>` et ajouter APRÈS :

```html
<!-- Firebase SDK -->
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-database-compat.js"></script>
```

### 2.2 - Ajouter la configuration Firebase

Chercher la ligne `const STORAGE_KEY = 'ppma_data';` (environ ligne 5200) et ajouter AVANT :

```javascript
// ==================== FIREBASE CONFIG ==================== //
const firebaseConfig = {
    apiKey: "REMPLACER_PAR_TA_CLE_API",
    authDomain: "REMPLACER.firebaseapp.com",
    databaseURL: "https://REMPLACER-default-rtdb.europe-west1.firebasedatabase.app",
    projectId: "REMPLACER",
    storageBucket: "REMPLACER.appspot.com",
    messagingSenderId: "REMPLACER",
    appId: "REMPLACER"
};

// Initialiser Firebase
firebase.initializeApp(firebaseConfig);
const database = firebase.database();

// ID unique pour cet utilisateur (généré une fois, stocké localement)
let userId = localStorage.getItem('ppma_user_id');
if (!userId) {
    userId = 'user_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
    localStorage.setItem('ppma_user_id', userId);
}
console.log('User ID:', userId);
```

### 2.3 - Remplacer la fonction `loadData()`

Chercher la fonction `function loadData()` et REMPLACER ENTIÈREMENT par :

```javascript
function loadData() {
    return new Promise((resolve) => {
        // D'abord charger depuis localStorage (pour mode offline)
        const localData = localStorage.getItem(STORAGE_KEY);
        if (localData) {
            try {
                state.data = JSON.parse(localData);
                console.log('Données locales chargées');
            } catch (e) {
                console.error('Erreur parsing localStorage:', e);
            }
        }

        // Ensuite synchroniser avec Firebase
        const userRef = database.ref('users/' + userId + '/data');
        
        // Écouter les changements en temps réel
        userRef.on('value', (snapshot) => {
            const cloudData = snapshot.val();
            if (cloudData) {
                // Fusionner intelligemment les données
                const localTimestamp = state.data.lastModified || 0;
                const cloudTimestamp = cloudData.lastModified || 0;
                
                if (cloudTimestamp > localTimestamp) {
                    // Cloud plus récent -> utiliser cloud
                    state.data = cloudData;
                    localStorage.setItem(STORAGE_KEY, JSON.stringify(state.data));
                    console.log('Données synchronisées depuis le cloud');
                    
                    // Mettre à jour l'affichage
                    updateDashboardStats();
                    updatePRsDisplay();
                    updateSessionStats();
                } else if (localTimestamp > cloudTimestamp) {
                    // Local plus récent -> pousser vers cloud
                    saveToCloud();
                }
            } else {
                // Pas de données cloud, pousser les locales
                saveToCloud();
            }
            resolve();
        }, (error) => {
            console.error('Erreur Firebase:', error);
            resolve(); // Continuer avec données locales
        });
    });
}
```

### 2.4 - Remplacer la fonction `saveData()`

Chercher la fonction `function saveData()` et REMPLACER ENTIÈREMENT par :

```javascript
function saveData() {
    try {
        // Ajouter timestamp de modification
        state.data.lastModified = Date.now();
        
        // Sauvegarder localement (pour mode offline)
        localStorage.setItem(STORAGE_KEY, JSON.stringify(state.data));
        
        // Sauvegarder dans Firebase
        saveToCloud();
        
        console.log('Données sauvegardées');
    } catch (error) {
        console.error('Erreur sauvegarde:', error);
    }
}

function saveToCloud() {
    try {
        const userRef = database.ref('users/' + userId + '/data');
        userRef.set(state.data)
            .then(() => console.log('Cloud sync OK'))
            .catch((err) => console.error('Cloud sync failed:', err));
    } catch (error) {
        console.error('Erreur saveToCloud:', error);
    }
}
```

### 2.5 - Ajouter un indicateur de sync (optionnel mais utile)

Chercher dans le CSS la section `/* ==================== FOOTER ==================== */` et ajouter AVANT :

```css
/* ==================== SYNC INDICATOR ==================== */
.sync-indicator {
    position: fixed;
    bottom: 20px;
    left: 20px;
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 8px 16px;
    background: var(--anthracite);
    border-radius: var(--radius-full);
    font-size: var(--text-sm);
    color: var(--gray-light);
    z-index: 1000;
    opacity: 0;
    transition: opacity 0.3s;
}

.sync-indicator.visible {
    opacity: 1;
}

.sync-indicator.synced {
    color: var(--success);
}

.sync-indicator.syncing {
    color: var(--warning);
}

.sync-indicator.offline {
    color: var(--danger);
}

.sync-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: currentColor;
}

.sync-indicator.syncing .sync-dot {
    animation: pulse 1s infinite;
}

@keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.3; }
}
```

### 2.6 - Ajouter le HTML de l'indicateur

Chercher `</body>` à la fin du fichier et ajouter JUSTE AVANT :

```html
<!-- Sync Indicator -->
<div id="sync-indicator" class="sync-indicator">
    <span class="sync-dot"></span>
    <span class="sync-text">Synchronisé</span>
</div>
```

### 2.7 - Ajouter la logique de l'indicateur

Ajouter dans la section JavaScript, après la fonction `saveToCloud()` :

```javascript
// ==================== SYNC INDICATOR ==================== //
function updateSyncIndicator(status) {
    const indicator = document.getElementById('sync-indicator');
    if (!indicator) return;
    
    indicator.classList.remove('synced', 'syncing', 'offline');
    indicator.classList.add('visible', status);
    
    const text = indicator.querySelector('.sync-text');
    switch(status) {
        case 'synced':
            text.textContent = 'Synchronisé ✓';
            setTimeout(() => indicator.classList.remove('visible'), 2000);
            break;
        case 'syncing':
            text.textContent = 'Synchronisation...';
            break;
        case 'offline':
            text.textContent = 'Mode hors-ligne';
            break;
    }
}

// Détecter connexion/déconnexion
window.addEventListener('online', () => {
    updateSyncIndicator('syncing');
    saveToCloud();
});

window.addEventListener('offline', () => {
    updateSyncIndicator('offline');
});
```

### 2.8 - Mettre à jour la fonction saveToCloud avec l'indicateur

Modifier la fonction `saveToCloud()` pour inclure l'indicateur :

```javascript
function saveToCloud() {
    if (!navigator.onLine) {
        updateSyncIndicator('offline');
        return;
    }
    
    updateSyncIndicator('syncing');
    
    try {
        const userRef = database.ref('users/' + userId + '/data');
        userRef.set(state.data)
            .then(() => {
                console.log('Cloud sync OK');
                updateSyncIndicator('synced');
            })
            .catch((err) => {
                console.error('Cloud sync failed:', err);
                updateSyncIndicator('offline');
            });
    } catch (error) {
        console.error('Erreur saveToCloud:', error);
        updateSyncIndicator('offline');
    }
}
```

---

## ÉTAPE 3 : Héberger l'application

Pour accéder à l'app depuis ton téléphone, tu as plusieurs options :

### Option A : GitHub Pages (Gratuit, recommandé)

1. Créer un compte GitHub si pas déjà fait
2. Créer un nouveau repository : `ppma-app`
3. Uploader le fichier `w2pm_elite_app.html` renommé en `index.html`
4. Aller dans Settings → Pages → Source: "Deploy from a branch" → main → Save
5. URL sera : `https://TON_USERNAME.github.io/ppma-app/`

### Option B : Firebase Hosting (Gratuit aussi)

1. Dans la console Firebase, aller dans "Hosting"
2. Suivre les instructions d'installation
3. Déployer avec `firebase deploy`

### Option C : Netlify (Super simple)

1. Aller sur https://app.netlify.com/drop
2. Glisser-déposer ton fichier HTML
3. URL générée automatiquement

---

## ÉTAPE 4 : Installer sur téléphone comme une app

### iPhone (Safari) :
1. Ouvrir l'URL dans Safari
2. Appuyer sur le bouton partage (carré avec flèche)
3. "Sur l'écran d'accueil"
4. Nommer "PPMA" → Ajouter

### Android (Chrome) :
1. Ouvrir l'URL dans Chrome
2. Menu ⋮ → "Ajouter à l'écran d'accueil"
3. Ou si PWA détectée : "Installer l'application"

---

## Résumé des modifications

| Ligne ~    | Modification |
|------------|--------------|
| `<head>`   | Ajouter 2 scripts Firebase |
| ~5200      | Ajouter config Firebase + userId |
| ~5209      | Remplacer `loadData()` |
| ~5225      | Remplacer `saveData()` + ajouter `saveToCloud()` |
| CSS        | Ajouter styles `.sync-indicator` |
| Avant `</body>` | Ajouter HTML sync indicator |
| JS         | Ajouter `updateSyncIndicator()` + event listeners |

---

## Test de validation

Après les modifications :
1. Ouvrir l'app sur l'ordinateur
2. Ajouter une donnée (ex: enregistrer un poids)
3. Ouvrir l'app sur le téléphone
4. Vérifier que la donnée apparaît
5. Modifier sur le téléphone
6. Vérifier que ça se met à jour sur l'ordinateur

C'est parti ! 🚀
