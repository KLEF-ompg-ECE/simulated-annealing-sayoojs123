# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** Sayooj S
**Student ID    :** 2310040095
**Date Submitted:** 11-03-2026

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
count_clashes() counts the total number of scheduling conflicts across all students.
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
generate_neighbor() creates a new timetable by copying the current one and then
randomly picking one exam and moving it to a different time slot. 
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This line decides whether to accept the neighbour solution. 
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of iterations completed | 1379 |
| Clashes at iteration 1 | 12 |
| Final best clashes | 3 |
| Did SA reach 0 clashes? (Yes / No) | No |

**Copy the printed timetable output here:**
```
  Final Timetable
------------------------------------------
  Slot 1:  Geography
  Slot 2:  Chemistry, English
  Slot 3:  History, Computer Science, Economics
  Slot 4:  Biology, Statistics
  Slot 5:  Mathematics, Physics
------------------------------------------
  Total clashes : 3
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
Clashes drop quickly in the first ~100 iterations from 12 to about 3–4, then the curve flattens at 3, meaning SA couldn’t remove the last clashes before the temperature became too low.

```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
|-------------|---------------|----------------------|--------------------|
| 0.80        | 8             | 31                   | No                 |
| 0.95        | 3             | 135                  | No                 |
| 0.995       | 3             | 1379                 | No                 |

**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
Fast cooling (0.80) runs 31 iterations and stops at 8 clashes. Medium cooling (0.95) runs 135 iterations and reaches 3 clashes. Slow cooling (0.995) runs 1379 iterations but still ends at 3 clashes.

```

**Which cooling_rate gave the best result? Why do you think that is?**
```
Both 0.95 and 0.995 gave the best result of 3 clashes. The slower cooling rates give
SA more iterations to explore the solution space, allowing it to find better solutions.
0.80 cools too fast and stops before finding a good solution.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 | 3 | Baseline SA reduces clashes from 12 to 3 in 1379 iterations but does not reach 0 |
| 2 — Cooling rate | cooling_rate = 0.95 / 0.995 | 3 | Slower cooling gives SA more time to explore, producing better results than fast cooling |

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
The cooling rate strongly affects SA’s performance. Fast cooling (0.80) limits exploration and traps the algorithm in a poor local minimum. Slower cooling (0.95 or 0.995) allows more exploration and finds better solutions, though it still may not reach the global optimum (3 clashes, not 0).

```

---

## Submission Checklist

- [x] Student name and ID filled in
- [x] Q1, Q2, Q3 answered
- [x] Experiment 1: table filled, timetable pasted, plot observation written
- [x] Experiment 2: results table filled (3 rows), observation and answer written
- [x] Summary table completed and reflection written
- [x] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
