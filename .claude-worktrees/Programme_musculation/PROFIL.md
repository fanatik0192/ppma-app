# PROFIL ATHLETE - Antoine

## Informations de Base

| Parametre | Valeur | Notes |
|-----------|--------|-------|
| **Nom** | Antoine | - |
| **Date debut programme** | 30/12/2024 | Semaine 1 |
| **Niveau** | DEBUTANT | < 6 mois experience |
| **Objectif principal** | Prise de masse athletique | +10kg en 40 semaines |

---

## Mesures Corporelles

### Mesures Actuelles (22/01/2025)

| Mesure | Valeur | Date |
|--------|--------|------|
| **Poids** | 70 kg | 22/01/2025 |
| **Taille** | 182 cm | - |
| **Age** | 24 ans | - |
| **Tour de taille** | 76 cm | 22/01/2025 |
| **Tour de cou** | 35 cm | 22/01/2025 |

### Composition Corporelle (Calculee ML)

| Metrique | Valeur | Interpretation |
|----------|--------|----------------|
| **BF% (Navy)** | ~11% | Athlete - Excellent pour prise de masse |
| **Masse maigre (LBM)** | 62.3 kg | Base solide |
| **FFMI** | 18.8 | Moyenne - Potentiel enorme (limite ~25) |
| **Categorie** | Athlete/Fitness | 6-13% BF |

---

## Records Personnels (PRs)

### Lifts Principaux (22/01/2025)

| Exercice | 1RM Actuel | Ratio/BW | Niveau | Objectif 40 sem |
|----------|------------|----------|--------|-----------------|
| **Bench Press** | 75 kg | 1.07× | Intermediaire | 95 kg (+27%) |
| **Squat** | 85 kg | 1.21× | Intermediaire | 110 kg (+29%) |
| **Deadlift** | ? kg | ? | A tester | - |
| **OHP** | ? kg | ? | A tester | - |

### Ratios Biomecaniques

| Ratio | Actuel | Optimal | Status |
|-------|--------|---------|--------|
| **Bench/Squat** | 0.88 | 0.75 | ⚠️ Bench trop fort vs Squat |
| **Squat/DL** | ? | 0.80 | A evaluer |
| **Push/Pull** | ? | 1.00 | A evaluer |

**Analyse:** Ratio Bench/Squat de 0.88 indique que le haut du corps est proportionnellement plus fort. Recommandation: prioriser les jambes.

---

## Niveau Determine par ML

### Methode 1: Temps d'entrainement
- Experience: < 6 mois → **DEBUTANT**

### Methode 2: Ratios de Force
| Exercice | Ratio | Classification |
|----------|-------|----------------|
| Bench | 1.07×BW | Intermediaire (0.75-1.25×) |
| Squat | 1.21×BW | Intermediaire (1.0-1.75×) |

### Conclusion ML
**Niveau: DEBUTANT avec bonnes bases naturelles**
- Progression lineaire recommandee
- Progression attendue: +2.5%/mois minimum
- Deload: toutes les 6 semaines

---

## Nutrition (Calculee ML)

### Metabolisme

| Metrique | Valeur | Formule |
|----------|--------|---------|
| **BMR** | 1722 kcal | Mifflin-St Jeor |
| **TDEE** | 2971 kcal | BMR × 1.725 (actif 6j/sem) |
| **Cible prise de masse** | 3300 kcal | TDEE + 330 |

### Macros Recommandes (Prise de Masse)

| Macro | Quantite | Calories | % |
|-------|----------|----------|---|
| **Proteines** | 140g (2g/kg) | 560 kcal | 17% |
| **Lipides** | 70g (1g/kg) | 630 kcal | 19% |
| **Glucides** | 525g | 2100 kcal | 64% |
| **TOTAL** | - | 3290 kcal | 100% |

---

## Facteurs de Recuperation

### ⚠️ ALERTE CRITIQUE: SOMMEIL

| Parametre | Actuel | Optimal | Status |
|-----------|--------|---------|--------|
| **Duree** | 5-6h | 7-9h | ❌ CRITIQUE |
| **Qualite** | 6/10 | 8+/10 | ⚠️ Insuffisant |
| **Impact ML** | -20% | 0% | Recuperation compromise |

**Consequences du manque de sommeil:**
- Recuperation musculaire reduite de 20-30%
- Testosterone diminuee
- Cortisol augmente (catabolique)
- Performance cognitive reduite
- Risque blessure augmente

**Recommandation #1:** Augmenter le sommeil a 7h minimum est PLUS IMPORTANT que n'importe quelle modification du programme.

### Modificateurs Banister

```javascript
sleepModifier = -0.20  // Poor (5-6h)
// vs 0.00 si 7-8h
// vs +0.05 si 8-9h
```

---

## Objectifs Ajustes (ML)

### Court terme (3 mois)
- [ ] **PRIORITE: Sommeil 7h+/nuit**
- [ ] Tester et etablir PR Deadlift et OHP
- [ ] Maintenir progression lineaire
- [ ] +2-3kg de poids corporel (72-73kg)

### Moyen terme (6 mois)
- [ ] +5kg de poids corporel (75kg)
- [ ] Bench: 85kg (+13%)
- [ ] Squat: 100kg (+18%)
- [ ] Equilibrer ratio Bench/Squat

### Long terme (40 semaines)
- [ ] +10kg de masse (80kg)
- [ ] Bench: 95kg
- [ ] Squat: 110kg
- [ ] BF% maintenu < 15%
- [ ] FFMI: 21+ (au-dessus moyenne)

---

## Parametres ML Calibres

### Banister Model (avec modificateur sommeil)

```javascript
const banisterParams = {
  p0: 100,
  k1: 1.0,
  k2: 2.0,
  tau1: 42,
  tau2: 7,
  sleepModifier: -0.20  // CRITIQUE
};
```

### Progression Attendue (Debutant)

```javascript
const progression = {
  niveau: 'BEGINNER',
  tauxMensuel: 0.025,  // +2.5%/mois
  deloadFrequency: 6,   // semaines
  rpeTarget: 8.0
};
```

---

## Historique des Evaluations

| Date | Poids | BF% | Bench | Squat | DL | OHP | Notes |
|------|-------|-----|-------|-------|-----|-----|-------|
| 22/01/2025 | 70 kg | ~11% | 75 kg | 85 kg | ? | ? | Initial |

---

*Profil calcule par ML - Derniere MAJ: 22/01/2025*
