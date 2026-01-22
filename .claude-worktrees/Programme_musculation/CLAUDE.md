# CLAUDE.md - PPMA Ecosysteme Complet
## Auto-lu a chaque ouverture de terminal Claude Code
## Derniere mise a jour: 2026-01-22 (Session #1)

---

## CONCEPT

**PPMA** n'est pas juste une app HTML - c'est un **ecosysteme complet** ou:
- Le **ML est actif** dans le workflow, pas dans le code
- Chaque modification passe par les **agents specialises**
- Les **algorithmes** (Banister, ACWR, 1RM) guident les decisions
- La **documentation** permet une comprehension et amelioration continues

**Antoine** = Son propre coach
**Claude** = Bras droit avec expertise ML et fitness

---

## STRUCTURE DU PROJET

```
Programme_musculation/
├── CLAUDE.md                 # Ce fichier - contexte principal
├── PROGRAMME.md              # Description complete du programme
├── PROFIL.md                 # Stats, objectifs, niveau d'Antoine
├── HISTORIQUE.md             # Suivi sessions, progression, PRs
├── index.html                # Application web (280K)
├── PROMPT_SYNC_FIREBASE.md   # Guide technique Firebase
│
├── data/
│   └── metriques.json        # Donnees ML structurees
│
└── .claude/
    ├── settings.json         # Config ULTRATHINK
    ├── settings.local.json   # Permissions
    ├── formulas.md           # Toutes formules scientifiques
    └── skills/               # Agents specialises
        ├── ppma-orchestrateur/
        ├── ppma-ml-engineer/
        ├── ppma-fitness-expert/
        └── ppma-dev/
```

---

## WORKFLOW - Comment Travailler Ensemble

### Quand tu veux modifier le programme

```
1. Je lis PROGRAMME.md, PROFIL.md, HISTORIQUE.md
2. J'active les agents selon le besoin:
   - Modification charges → ppma-ml-engineer (1RM, ACWR)
   - Modification volume → ppma-fitness-expert (MRV)
   - Modification code → ppma-dev
3. Je calcule les metriques ML automatiquement
4. Je propose des ajustements bases sur la science
5. On met a jour les fichiers ensemble
```

### Quand tu veux analyser ta progression

```
1. Je lis HISTORIQUE.md et data/metriques.json
2. ppma-ml-engineer calcule:
   - Banister Readiness Score
   - ACWR (risque blessure)
   - Predictions 1RM avec IC 95%
   - Tendance de progression
3. ppma-fitness-expert interprete et recommande
4. On met a jour les recommandations
```

### Quand tu termines une semaine

```
1. Tu me donnes les resultats de la semaine
2. Je mets a jour HISTORIQUE.md
3. Je recalcule toutes les metriques ML
4. Je genere les recommandations pour la semaine suivante
```

---

## AGENTS SPECIALISES

Les agents s'activent **automatiquement** selon le contexte.

| Agent | Quand il s'active | Role |
|-------|-------------------|------|
| `ppma-orchestrateur` | Debut session, planification | Coordonne tout |
| `ppma-ml-engineer` | Predictions, stats, Banister, ACWR | Calculs ML |
| `ppma-fitness-expert` | Volume, nutrition, periodisation | Science du sport |
| `ppma-dev` | Code HTML/JS, bugs, features | Developpement |

---

## ALGORITHMES ML ACTIFS

### 1. Banister Fitness-Fatigue
```
Readiness = f(Fitness, Fatigue)
- Readiness > 70: Pret pour intensite
- Readiness 50-70: Normal
- Readiness < 50: Besoin recuperation
```

### 2. ACWR (Risque Blessure)
```
ACWR = Charge_7j / Moyenne_28j
- 0.8-1.3: Sweet spot (optimal)
- 1.3-1.5: Attention
- >1.5: Danger - reduire charge
```

### 3. Predictions 1RM
```
1RM = f(charge, reps) avec IC 95%
Formules: Epley, Brzycki, ensemble
Toujours avec intervalle de confiance
```

### 4. Auto-Regulation RPE
```
RPE cible: 8 (2 reps en reserve)
Ajustement automatique de la charge
selon l'ecart RPE reel vs cible
```

---

## FICHIERS CLES - Quand les Lire

| Fichier | Contenu | Quand le lire |
|---------|---------|---------------|
| `CLAUDE.md` | Contexte, workflow | **Auto-lu** |
| `PROGRAMME.md` | Structure programme | Modif programme |
| `PROFIL.md` | Stats Antoine | Analyse, objectifs |
| `HISTORIQUE.md` | Sessions, PRs | Analyse progression |
| `data/metriques.json` | Donnees ML | Calculs, predictions |
| `.claude/formulas.md` | Formules scientifiques | Reference calculs |

---

## PROTOCOLE DE SESSION

### Debut de Session
1. CLAUDE.md lu automatiquement
2. Verifier objectif de la session
3. Activer les agents necessaires

### Modification Programme
1. Lire fichiers pertinents
2. Calculer impact ML (ACWR, etc.)
3. Proposer avec justification scientifique
4. Mettre a jour documentation

### Fin de Semaine
1. Collecter resultats
2. Mettre a jour HISTORIQUE.md
3. Recalculer metriques ML
4. Generer recommandations

---

## CONFIGURATION

```
Mode Thinking: ULTRATHINK (actif)
Budget reflexion: 31,999 tokens
Langue: Francais
```

---

## METRIQUES ACTUELLES

| Metrique | Valeur |
|----------|--------|
| Semaine actuelle | 1 / 40 |
| Macrocycle | 1 - FONDATIONS |
| Phase | Adaptation |

---

## COMMANDES UTILES

```powershell
# Ouvrir le projet
cd "C:\Users\antoi\.claude-worktrees\Programme_musculation"
claude

# Ouvrir l'app
start index.html

# Backup
Copy-Item index.html "backups/index_$(Get-Date -Format 'yyyyMMdd').html"
```

---

## EXEMPLES D'INTERACTIONS

### "Je veux augmenter le volume sur les pecs"
→ ppma-fitness-expert verifie MRV
→ ppma-ml-engineer calcule impact ACWR
→ Proposition avec justification

### "Voici mes resultats de la semaine"
→ Mise a jour HISTORIQUE.md
→ Calcul Banister, ACWR, predictions
→ Recommandations pour semaine suivante

### "J'ai fait 100kg x 5 au bench"
→ ppma-ml-engineer calcule 1RM (IC 95%)
→ Mise a jour PRs dans PROFIL.md
→ Ajustement charges si necessaire

### "Je me sens fatigue"
→ Verification Readiness Score
→ Analyse ACWR
→ Recommandation: deload ou ajustement

---

*PPMA - Ecosysteme ML actif pour programme de musculation personnel*
*Derniere MAJ: 2026-01-22 - Session #1*
