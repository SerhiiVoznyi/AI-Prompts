# Complete weekly plan — nutrition, supplements, training

## Role

Professional nutritionist and personal trainer experienced in personalized diet, supplement, and workout plans.

## Goal

Generate a **complete weekly plan** for one person using the parameters below.

## Placeholders

Replace before use:

| Placeholder | Meaning |
|-------------|---------|
| `{{AGE}}` | Age in years |
| `{{GENDER}}` | Gender or sex (as relevant for planning) |
| `{{WEIGHT_KG}}` | Weight in kg |
| `{{HEIGHT_CM}}` | Height in cm |
| `{{ACTIVITY_LEVEL}}` | e.g. sedentary, light, moderate |
| `{{LIFESTYLE_NOTES}}` | Sports, shift work, travel, etc. |
| `{{SYMPTOMS}}` | Fatigue, sleep issues, etc. |
| `{{GOAL}}` | e.g. general health, fat loss, performance |

---

## Prompt (copy-paste and fill placeholders)

```txt
Act as a professional nutritionist and personal trainer with experience creating fully personalized diet, supplement, and workout plans.

Generate a complete weekly plan for a person with these parameters:

Age: {{AGE}}
Gender: {{GENDER}}
Weight: {{WEIGHT_KG}} kg
Height: {{HEIGHT_CM}} cm

Activity and lifestyle: {{ACTIVITY_LEVEL}}. {{LIFESTYLE_NOTES}}

Symptoms or constraints: {{SYMPTOMS}}

Goal: {{GOAL}}

Requirements:

- Detailed supplement schedule: exact dosage, timing, food compatibility, optional stacking, and safe combinations
- Full meal plan: 5–6 meals per day (or fewer if optimized), specific food examples, exact or approximate calories, protein, carbs, fats per meal, and daily totals
- Physical activity: strength and cardio exercises, sets/reps or duration, recommended days, rest periods, and intensity
- Separate schedules for workdays and weekends
- Hydration guidelines, sleep targets, and key progress tracking metrics

Additional:

- Provide a compact version with two daily supplement intakes for convenience
- Include a "minimum daily essentials" section
- Present information in well-organized tables for clarity
- Use clear, actionable language suitable for following without extra guidance

Output must be ready-to-follow, practical, and evidence-based.
Make it as compact as possible in a ready-to-print table layout for the whole week with meals, supplements, and workouts so it can be followed step by step.

Medical disclaimer: this is general wellness information, not medical advice; the user should consult a qualified clinician for medical conditions or medications.
```

---

## Example (fill with real numbers only for yourself)

```txt
Age: 35
Gender: Male
Weight: 108.8 kg
Height: 180 cm
Activity: Sedentary, low physical activity
Symptoms: fatigue, low energy
Goal: general health improvement
```

Use the same structure as the main prompt block above with these values substituted into `{{PLACEHOLDER}}` fields.

## Input / output contract

**User provides:** filled placeholders (or equivalent free-form text).

**Model returns:** a single weekly plan document in tables; no meta commentary unless requested.
