# Step Calculator

A single-file walking calculator that converts steps to distance, distance to calories, and calories to weight change — and runs the same math backwards to answer "how many steps to burn this?"

No build step, no dependencies, no network calls. Open `index.html` in a browser.

```
open index.html
```

## Why this exists

Most step calculators ask for your age. Age does not appear anywhere in the physics of walking. They ask for your pace, which cancels out of the equation entirely on flat ground. And they present a "personalized step target" that is usually a calorie figure divided by a step cost, dressed up as a formula.

This page runs that same division. It just shows you the formula.

The "10,000 steps" figure has no clinical origin either. A 1965 Japanese pedometer was marketed as the *manpo-kei* — "10,000-step meter." The name stuck for sixty years and got retrofitted with the authority of a guideline.

## The math

Calorie cost comes from the American College of Sports Medicine walking equation:

```
VO₂ = 0.1·v + 1.8·v·g + 3.5    (ml/kg/min)
```

where `v` is speed in m/min and `g` is the grade as a decimal.

Drop the resting `3.5` term to get **net** cost — energy above what you would burn sitting still. Convert from time to distance and the speed term cancels, leaving:

```
net kcal = (0.5 + 9g) × weight_kg × km
```

On flat ground this collapses to the familiar `0.5 × kg × km`.

Distance comes from `km = steps × stride_m / 1000`, with stride estimated as `height × 0.414` unless you enter a measured value.

Weight change uses `7,700 kcal ≈ 1 kg` of fat (the "3,500 calories per pound" rule).

### Three things that fall out of this

**Pace does not change calories per step.** Walking briskly burns the same energy per kilometer as strolling — you just finish sooner. Speed only matters for time-bounded targets, or once you cross into running (~1 kcal/kg/km).

**Incline is the real multiplier.** A 5% grade nearly doubles the cost per meter. The page has a grade selector where other calculators put a pace dropdown.

**Age does nothing.** Moving mass over distance is mechanics. Age affects how a walk *feels* — heart rate, recovery, joint tolerance — not the work performed.

## Net vs. gross

This page reports net calories throughout. Gross figures are larger and make better marketing, but they include the calories you would have burned anyway. Subtracting a gross figure from your daily intake double-counts your resting metabolism.

## The 3,500-calorie rule decays

The linear `7,700 kcal/kg` conversion holds for a few weeks, then degrades. A lighter body burns less doing the identical walk, and appetite compensates for part of the deficit. Real loss bends away from the straight line.

The projection table shows both: the naive linear figure, and a decayed figure approximating Hall's dynamic model. At one year the decayed value lands near half the naive one. If a calculator shows you only the first column, it is overstating your results by roughly 2× on a twelve-month horizon.

## Features

- **Steps → calories** — distance, net burn, walking time, kcal per 1,000 steps
- **Calories → steps** — enter a calorie target, or pick from 14 food items with portion sizes
- **Projection table** — deficit and weight change at 1 week through 1 year, naive and decayed
- **Rate → steps** — target loss per week, converted to a daily step requirement
- **Metric / imperial toggle** — converts every entered value on switch
- **Stride override** — for anyone who has actually measured theirs

## Assumptions and limits

| | |
|---|---|
| Valid range | Walking, roughly 3–6 km/h on measured ground |
| Running | Not modeled; costs more per meter (~1 kcal/kg/km) |
| Stride estimate | `height × 0.414`, a population mean — individual variation is significant |
| Food calories | Typical published figures; real items vary by brand and preparation |
| Body composition | Not modeled; the 7,700 kcal/kg figure assumes loss is entirely fat |

Stride error propagates linearly into every number on the page. If the outputs matter to you, measure your stride over a known distance and enter it.

This is an estimator, not medical advice.

## License

MIT
