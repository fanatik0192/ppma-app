# Formules Scientifiques PPMA

## 1. ESTIMATION DU 1RM

### Formules Principales

| Nom | Formule | Precision | Plage Reps | Source |
|-----|---------|-----------|------------|--------|
| **Epley** | `1RM = W * (1 + R/30)` | +/-5% | 1-10 | Epley 1985 |
| **Brzycki** | `1RM = W * 36 / (37 - R)` | +/-4% | 1-10 | Brzycki 1993 |
| **Lombardi** | `1RM = W * R^0.1` | +/-6% | 1-10 | Lombardi 1989 |
| **Mayhew** | `1RM = 100*W / (52.2 + 41.9*e^(-0.055R))` | +/-5% | 1-15 | Mayhew 1992 |
| **Wathan** | `1RM = 100*W / (48.8 + 53.8*e^(-0.075R))` | +/-4% | 1-10 | Wathan 1994 |

### Recommandation d'Utilisation

```
Pour R <= 5:    Moyenne(Epley, Brzycki)
Pour 5 < R <= 10: Moyenne(Epley, Brzycki, Wathan)
Pour R > 10:    Mayhew seul (autres peu fiables)
```

### Intervalle de Confiance

**Methode Bootstrap BCa (Bias-Corrected & Accelerated):**
- Plus robuste que percentile simple
- Corrige pour biais et asymetrie
- 10,000 samples recommandes
- IC 95% par defaut

---

## 2. MODELE BANISTER FITNESS-FATIGUE

### Equations (Morton 1997)

```
Performance(t) = p0 + k1 * Fitness(t) - k2 * Fatigue(t)

Fitness(t) = sum[i=1 to t](w(i) * e^(-(t-i)/tau1))
Fatigue(t) = sum[i=1 to t](w(i) * e^(-(t-i)/tau2))

w(i) = Training Load du jour i
```

### Parametres par Defaut (Morton 1997)

| Parametre | Valeur | Description |
|-----------|--------|-------------|
| p0 | 100 | Performance baseline |
| k1 | 1.0 | Coefficient fitness |
| k2 | 2.0 | Coefficient fatigue |
| tau1 | 42 jours | Decay fitness |
| tau2 | 7 jours | Decay fatigue |

### Training Load Calculation

```
Load = Volume * Intensite

Volume = Sets * Reps
Intensite = Charge / 1RM (ou RPE / 10)
```

### Readiness Score (0-100)

```
ratio = Fitness / Fatigue
Readiness = 50 * ratio, clampe [0, 100]

Interpretation:
- 100: Parfaitement repose et en forme
- 50: Equilibre fitness/fatigue
- <30: Fatigue importante -> Deload
```

### Tendances Detectees

| Tendance | Condition | Action |
|----------|-----------|--------|
| Peaking | ratio > 1.5 | Pret pour PR |
| Building | 0.8 <= ratio <= 1.5 | Continuer |
| Fatigued | ratio < 0.8 | Reduire volume |
| Recovering | Pas d'activite recente | Reprendre doucement |

---

## 3. ACWR - ACUTE:CHRONIC WORKLOAD RATIO

### Calcul (Gabbett 2016)

```
Acute Load = sum(charge des 7 derniers jours)
Chronic Load = EWMA sur 28 jours

EWMA: lambda = 2/(N+1) = 2/29 ≈ 0.069

ACWR = Acute / Chronic
```

### Zones de Risque

| Zone | ACWR | Risque | Action |
|------|------|--------|--------|
| Sous-entrainement | < 0.8 | Insuffisant | Augmenter charge |
| **Sweet Spot** | 0.8-1.3 | Minimal | Maintenir |
| Attention | 1.3-1.5 | Modere | Surveiller |
| Danger | 1.5-2.0 | Eleve | Reduire charge |
| Critique | > 2.0 | Tres eleve | Deload immediat |

**Source**: Gabbett, T. (2016). Br J Sports Med. DOI: 10.1136/bjsports-2015-095788

---

## 4. AUTO-REGULATION RPE (Zourdos 2016)

### Echelle RPE

| RPE | RIR | Description |
|-----|-----|-------------|
| 10 | 0 | Echec musculaire |
| 9.5 | 0.5 | Peut-etre 1 rep |
| 9 | 1 | 1 rep en reserve |
| 8.5 | 1-2 | Definitivement 1-2 reps |
| **8** | **2** | **Cible progression** |
| 7.5 | 2-3 | 2-3 reps en reserve |
| 7 | 3 | 3 reps en reserve |
| <7 | 3+ | Effort modere |

### Ajustement de Charge

```
RPE_cible = 8.0

Si RPE_reel >= cible + 1.5 → charge *= 0.97 (-3%)
Si RPE_reel >= cible + 1.0 → charge *= 0.98 (-2%)
Si RPE_reel <= cible - 1.5 → charge *= 1.03 (+3%)
Si RPE_reel <= cible - 1.0 → charge *= 1.025 (+2.5%)
Sinon → maintenir charge
```

**Source**: Zourdos, M.C. et al. (2016). J Strength Cond Res. DOI: 10.1519/JSC.0000000000001515

---

## 5. METABOLISME & NUTRITION

### BMR - Mifflin-St Jeor (Recommande)

```
Hommes: BMR = 10 * Poids(kg) + 6.25 * Taille(cm) - 5 * Age + 5
Femmes: BMR = 10 * Poids(kg) + 6.25 * Taille(cm) - 5 * Age - 161
```

**Precision**: +/-10%
**Source**: Mifflin et al. (1990), Am J Clin Nutr

### TDEE

```
TDEE = BMR * Facteur_Activite

Facteurs:
- Sedentaire (bureau): 1.2
- Leger (1-3j/sem): 1.375
- Modere (3-5j/sem): 1.55
- Actif (6-7j/sem): 1.725
- Tres actif (athlete): 1.9
```

### Macronutriments

| Nutriment | Prise de masse | Maintenance | Seche |
|-----------|----------------|-------------|-------|
| Proteines | 2.0 g/kg | 1.8 g/kg | 2.2-2.8 g/kg |
| Lipides | 1.0 g/kg | 0.8 g/kg | 0.6 g/kg |
| Glucides | Reste | Reste | Reste |

**Calcul Glucides**:
```
Glucides(g) = (TDEE - Proteines*4 - Lipides*9) / 4
```

**Source**: Morton et al. (2018), Br J Sports Med. DOI: 10.1136/bjsports-2017-097608

---

## 6. COMPOSITION CORPORELLE

### Navy Method (Hodgdon & Beckett 1984)

```
Hommes:
BF% = 495 / (1.0324 - 0.19077*log10(Taille_cm - Cou_cm) + 0.15456*log10(Hauteur_cm)) - 450

Femmes:
BF% = 495 / (1.29579 - 0.35004*log10(Taille_cm + Hanches_cm - Cou_cm) + 0.22100*log10(Hauteur_cm)) - 450
```

**Precision**: +/-3-4%

### FFMI (Fat-Free Mass Index)

```
FFMI = LBM(kg) / Taille(m)^2
FFMI_norm = FFMI + 6.1 * (1.8 - Taille(m))
```

| FFMI | Interpretation |
|------|----------------|
| < 18 | Sous moyenne |
| 18-20 | Moyenne |
| 20-22 | Au-dessus moyenne |
| 22-25 | Excellent |
| 25-27 | Limite naturelle |
| > 27 | Probablement assiste |

**Source**: Kouri et al. (1995), Clin J Sport Med

---

## 7. VOLUME D'ENTRAINEMENT

### MRV par Groupe Musculaire (Renaissance Periodization)

| Groupe | Debutant | Intermediaire | Avance |
|--------|----------|---------------|--------|
| Quadriceps | 12 | 18 | 22-25 |
| Dos | 12 | 18 | 22-25 |
| Pectoraux | 10 | 15 | 18-22 |
| Epaules | 10 | 14 | 16-20 |
| Biceps | 8 | 12 | 15-18 |
| Triceps | 8 | 12 | 15-18 |

### Calcul Volume

```
Volume Relatif = Sets * Reps * (Charge / 1RM)
Volume Absolu = Sets * Reps * Charge
Tonnage = sum(Volume par session)
```

---

## 8. PERIODISATION

### Progression selon Niveau

| Niveau | Type | Progression Hebdo | Deload |
|--------|------|-------------------|--------|
| Debutant | Lineaire | +2.5-5% | Toutes les 6 sem |
| Intermediaire | DUP | +1-2.5% | Toutes les 5 sem |
| Avance | Block | +0.5-1% | Toutes les 4 sem |
| Elite | Block | +0.3% | Toutes les 3 sem |

### Supercompensation

```
Timeline post-entrainement:
0-24h: Fatigue (performance -)
24-48h: Recuperation
48-72h: Supercompensation (performance +)
72h+: Retour baseline
```

---

## 9. RECUPERATION

### Temps de Repos Minimum

```
Base = 48h (petit groupe) ou 72h (grand groupe)

Modificateurs:
- Volume > MRV: +24h
- Intensite > 90%: +12-24h
- Age > 40: +12-24h
- Sommeil < 7h: +12h
- Stress eleve: +12h
```

### Modulateurs Banister

```javascript
sleep_modifier = {
  poor: -0.20,
  fair: -0.10,
  good: 0,
  excellent: +0.05
}

stress_modifier = {
  high: -0.15,
  moderate: -0.05,
  low: 0
}

nutrition_modifier = {
  deficit: -0.10,
  maintenance: 0,
  surplus: +0.05
}
```

---

## 10. RATIOS BIOMECANIQUES (Poliquin/NSCA)

| Ratio | Formule | Optimal | Alerte |
|-------|---------|---------|--------|
| Push/Pull | Bench / Row | 1.0 | >1.2 ou <0.8 |
| Squat/DL | Squat / Deadlift | 0.8 | >0.9 ou <0.7 |
| Upper/Lower | Bench / Squat | 0.75 | >0.9 ou <0.6 |
| Quad/Ham | Leg Ext / Leg Curl | 0.6 | <0.5 |

---

## REFERENCES

1. Banister, E.W. et al. (1975). "A systems model of training"
2. Morton, R.H. (1997). "Modelling training and overtraining"
3. Epley, B. (1985). "Poundage Chart"
4. Brzycki, M. (1993). "Strength testing"
5. Gabbett, T. (2016). "Training-injury prevention paradox"
6. Zourdos, M.C. et al. (2016). "RPE Scale"
7. Mifflin, M.D. et al. (1990). "BMR prediction equations"
8. Morton, R.W. et al. (2018). "Protein meta-analysis"
9. Kouri, E.M. et al. (1995). "FFMI in athletes"
10. Israetel, M. "Renaissance Periodization - MRV guidelines"

---

*Formulas Reference - PPMA v1.0 - Sources Scientifiques Validees*
