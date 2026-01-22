# Reference des Agents PPMA

## Vue d'Ensemble

| Agent | Specialite | Model | Context | Priorite |
|-------|------------|-------|---------|----------|
| `ppma-orchestrateur` | Coordination | opus | main | Haute |
| `ppma-ml-engineer` | ML, Predictions | opus | **fork** | Haute |
| `ppma-fitness-expert` | Physiologie | sonnet | main | Haute |
| `ppma-dev` | Code HTML/JS | sonnet | main | Moyenne |

## Matrice de Responsabilites (RACI)

| Tache | Orchestrateur | ML | Fitness | Dev |
|-------|---------------|-----|---------|-----|
| Planification session | **A** | I | I | I |
| Predictions 1RM | I | **R** | C | C |
| Banister/ACWR | I | **R** | C | I |
| Formules nutrition | I | C | **R** | I |
| Periodisation | I | C | **R** | I |
| Code app | I | I | I | **R** |
| Integration ML | I | C | I | **R** |
| Documentation | **A** | C | C | C |

*R = Responsible, A = Accountable, C = Consulted, I = Informed*

## Quand Utiliser Chaque Agent

### ppma-orchestrateur
- Debut/fin de session
- Planification des taches
- Decisions strategiques
- Coordination multi-agents
- Mise a jour documentation

### ppma-ml-engineer
- Calcul 1RM avec IC
- Modele Banister (Fitness-Fatigue)
- Calcul ACWR
- Auto-regulation RPE
- Predictions de progression
- Toute analyse statistique

### ppma-fitness-expert
- Calculs TDEE/macros
- Recommandations volume (MRV)
- Periodisation (lineaire/DUP/block)
- Temps de recuperation
- Validation physiologique
- Ratios biomecaniques

### ppma-dev
- Modifications index.html
- Bug fixes interface
- Nouvelles fonctionnalites UI
- Integration Firebase
- Optimisation performance
- CSS/responsive

## Regles de Delegation

1. **Un agent = Une responsabilite** - Ne pas melanger les domaines
2. **Dependencies claires** - Attendre completion avant continuer
3. **Validation obligatoire** - Orchestrateur valide chaque output
4. **Escalade si blocage** - Remonter apres 2 echecs

## Communication Inter-Agents

```
Orchestrateur
     |
     +---> ppma-fitness-expert (formules, validation)
     |         |
     |         +---> ppma-ml-engineer (implementation)
     |                   |
     |                   +---> ppma-dev (integration UI)
     |
     +---> ppma-ml-engineer (predictions, stats)
     |         |
     |         +---> ppma-dev (affichage)
     |
     +---> ppma-dev (code, features)
```

## Pattern: Nouvelle Feature ML

```
1. ppma-fitness-expert → Definir formule + validation scientifique
2. ppma-ml-engineer → Implementer avec IC + tests
3. ppma-dev → Integrer dans l'app + UI
4. Orchestrateur → Valider + documenter
```

## Pattern: Optimisation Programme

```
1. ppma-ml-engineer → Analyser donnees (Banister, ACWR)
2. ppma-fitness-expert → Interpreter + recommander
3. Orchestrateur → Valider + appliquer
```

---

*Agents Reference - PPMA v1.0*
