# Workflow Orchestrateur PPMA

## Protocole de Session

### Phase 1: Initialisation (Automatique)

```powershell
# 1. BACKUP SYSTEMATIQUE
$timestamp = Get-Date -Format 'yyyyMMdd_HHmmss'
Copy-Item index.html "backups/index_$timestamp.html"

# 2. VERIFICATION ETAT
git status
```

**Checklist Demarrage:**
- [ ] Backup effectue
- [ ] Git status propre
- [ ] Phase actuelle confirmee (lire CLAUDE.md)
- [ ] Objectifs de session definis

### Phase 2: Analyse de Demande

```
1. RECEPTION
   - Comprendre la demande d'Antoine
   - Identifier le scope (feature, bug, analyse, etc.)

2. DECOMPOSITION
   - Taches atomiques
   - Dependencies entre taches
   - Agents necessaires

3. PRIORISATION
   - MoSCoW: Must/Should/Could/Won't
   - Critical path
```

### Phase 3: Planification

**Template Plan:**
```markdown
## PLAN SESSION - [DATE]

### Objectif Principal
[Description claire]

### Taches

| # | Tache | Agent | Dependance | Priorite |
|---|-------|-------|------------|----------|
| 1 | ...   | ...   | -          | Must     |
| 2 | ...   | ...   | #1         | Must     |

### Criteres de Succes
1. [Critere mesurable 1]
2. [Critere mesurable 2]
```

### Phase 4: Execution

**Boucle d'Execution:**
```
POUR CHAQUE tache:
    1. Briefer l'agent avec contexte complet
    2. Superviser l'execution
    3. Valider l'output
    4. SI echec:
       - Analyser la cause
       - Ajuster et re-executer (max 2 fois)
       - SI toujours echec: escalader
    5. Mettre a jour TodoWrite
    6. Documenter les decisions
```

**Regles d'Execution:**
- Maximum 2 agents en parallele
- Zones de code differentes si parallele
- Tests apres chaque modification
- Backup avant modif majeure

### Phase 5: Validation

**Quality Gates:**
```
- App fonctionne (ouvrir index.html)
- Pas d'erreurs console
- Sync Firebase OK
- Mobile responsive
```

**Checklist Validation:**
- [ ] App fonctionne sans erreur
- [ ] Donnees persistent (localStorage + Firebase)
- [ ] Interface responsive

### Phase 6: Cloture

**Actions Fin de Session:**
```
1. VERIFICATION
   - Tester l'app
   - Verifier console

2. DOCUMENTATION
   - Mettre a jour CLAUDE.md si necessaire
   - Prochaines etapes definies

3. GIT (si demande)
   - Stage fichiers modifies
   - Commit descriptif

4. BILAN
   - Afficher tableau recapitulatif
```

**Format Bilan Obligatoire:**
```markdown
## BILAN SESSION #X - [DATE]

### Taches Completees
| Tache | Status | Agent | Fichiers |
|-------|--------|-------|----------|
| ...   | OK     | ...   | ...      |

### Pour Reprendre
Commande: `claude`
Contexte: [resume 1 ligne]
Prochaine tache: [tache prioritaire]
```

## Patterns de Coordination

### Pattern: Implementation ML

```
Orchestrateur
    |
    +---> ppma-fitness-expert (formule, validation scientifique)
    |         |
    |         +---> ppma-ml-engineer (implementation + IC)
    |                   |
    |                   +---> ppma-dev (integration UI)
```

### Pattern: Bug Fix

```
Orchestrateur
    |
    +---> ppma-dev (identifier + corriger)
    |         |
    |         +---> Test manuel
```

### Pattern: Analyse Programme

```
Orchestrateur
    |
    +---> ppma-ml-engineer (Banister, ACWR, predictions)
    |         |
    |         +---> ppma-fitness-expert (interpreter + recommander)
```

## Gestion des Erreurs

| Situation | Action |
|-----------|--------|
| App ne charge pas | Verifier console, rollback si necessaire |
| Firebase sync fail | Verifier config, tester connexion |
| Agent bloque | Max 2 retries, puis escalader |
| Regression | Rollback depuis backup |

## Anti-Patterns a Eviter

| Anti-Pattern | Consequence | Alternative |
|--------------|-------------|-------------|
| Pas de backup | Perte de travail | Backup systematique |
| Skip validation | Bugs | Toujours tester |
| 3+ agents paralleles | Conflits | Max 2 paralleles |
| Magic numbers | Non-reproductible | Constantes documentees |
| Pas de TodoWrite | Oubli | Tracking systematique |

---

*Workflow Orchestrateur - PPMA v1.0*
