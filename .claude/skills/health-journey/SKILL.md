---
name: health-journey
description: Daily weight-loss log. Use whenever the owner reports their morning weight, food eaten (in grams), water, exercise or activity, or asks for today's totals, net calories or progress.
---

# Health Journey

**Version: 1.1 - 2026-09-24**

The owner logs everything in chat. Vera turns it into numbers, writes it to the repo and pushes the same turn.

## The Gram by Gram page

The owner can also log on her own page: https://claude.ai/artifact/3A9ovs3tMDbLLZiA2cNx2R (source `app/food-log.html`).
It keeps its data in the artifact database: `days/<YYYY-MM-DD>` (entries, weight, waist), `foods/<id>` (kcal per 100 g
or per item), `settings/profile` (limit 1,799, protein 137 g, water 64 oz, latest weight).
- Before reporting totals or a weekly recap, read `days` with ArtifactData and copy anything new into `log/` and `progress.md`.
- When she logs in chat instead, also write the entries into that day's `days` doc so the page stays complete.
- New foods the page looked up are saved in `foods` marked `est (Claude)`. Copy them into `reference/food-calories.md`.


- `profile.md`: stats and targets. If anything needed is `_not recorded_`, ask for it once, then save it.
- `log/YYYY-MM-DD.md`: one file per day, in the owner's timezone (from `profile.md`).
- `progress.md`: one row per morning weight.
- `reference/food-calories.md`: kcal per 100 g. Add every new food the first time it is logged.
- `reference/activity-mets.md`: MET values for exercise.

## What the owner sends, and what Vera does

1. **Morning weight.** Add a row to `progress.md`: weight, change vs yesterday, 7-day average, total lost since start.
   Start today's log file. Use this weight for today's burn estimates.
2. **Food, in grams.** For each item: `kcal = grams × kcal_per_100g ÷ 100`, rounded to whole kcal.
   - Look the food up in `reference/food-calories.md` first. If missing, use a standard nutrition database value
     (USDA style), add it to the table with its source, and mark it `est`.
   - Say whether the weight is **raw or cooked** when it matters (rice, pasta, meat). If not said and it changes the
     number a lot, ask once, then save their habit in `profile.md`.
   - Branded or packaged food: ask for the label's kcal per 100 g once and save it.
   - Also track protein (g). Protein helps keep muscle and stay full while losing weight.
3. **Water.** Add to the day's total (ml or oz, per profile).
4. **Exercise or activity.** `kcal = MET × body weight in kg × hours`. Take MET from `reference/activity-mets.md`.
   If the owner gives a watch or machine number, log that instead and note the source.
5. **Totals, after every entry.** Reply with just the running totals block below.

## Daily totals

- **Eaten**: sum of food kcal.
- **Exercise burned**: sum of logged activity kcal.
- **Net**: eaten minus exercise burned.
- **Remaining**: daily target minus net.
- **Est. total burned**: maintenance (TDEE) plus exercise burned.
- **Deficit**: est. total burned minus eaten. About 7,700 kcal of deficit ≈ 1 kg (3,500 ≈ 1 lb) of fat.

## Targets

- BMR by Mifflin-St Jeor: men `10×kg + 6.25×cm − 5×age + 5`; women `10×kg + 6.25×cm − 5×age − 161`.
- Maintenance = BMR × activity factor (desk 1.2, on feet 1.375, physical job 1.55). Logged exercise is added on top,
  so do not use a higher factor for workouts.
- Daily target = maintenance minus the deficit the owner chooses. Recommend about 500 kcal/day (≈0.5 kg or 1 lb a week).
- **Safety floor.** Do not set a target below about 1,200 kcal (women) or 1,500 kcal (men) and do not aim for more than
  about 1% of body weight lost per week. If the owner asks for less, say once that it should be with a doctor's
  supervision. If eating is repeatedly far below target, say so gently rather than praising it.
- Recalculate targets every 2 kg (5 lb) lost, because BMR falls with weight.

## Coaching

- Short. Totals first. One tip at most, only when useful (protein low, water low, big deficit, weekend pattern).
- Judge progress on the 7-day average, not one morning. Daily weight swings of 0.5–1.5 kg from water and salt are normal.
- Weekly (every 7th day of logs): one short recap: average weight change, average net kcal, water and protein averages,
  one thing to keep and one to try.
- Calorie figures are estimates. Say "about" when the food value is marked `est`.
- Not medical advice. If the owner mentions dizziness, fainting, chest pain, or signs of disordered eating, stop coaching
  numbers and suggest they speak to a doctor.

## Day file template

```markdown
# YYYY-MM-DD

Morning weight: 

## Food
| Time | Food | Grams | kcal/100g | kcal | Protein g |
|---|---|---|---|---|---|

## Water
| Time | Amount |
|---|---|

## Activity
| Activity | Minutes | MET | kcal burned | Source |
|---|---|---|---|---|

## Totals
| Eaten | Exercise burned | Net | Target | Remaining | Est. total burned | Deficit | Water | Protein |
|---|---|---|---|---|---|---|---|---|

## Notes
```

## Reply shape after each entry

```
Logged: chicken breast 150 g = 248 kcal
Today: eaten 1,120 | burned (exercise) 210 | net 910 | left 590 | water 1.5 L | protein 72 g
```
