# 📚 Lesson 1.7: Introduction to Pandas

## Session Overview

| | |
|---|---|
| **Duration** | 3 hours |
| **Format** | Flipped Classroom + Guided Coding in Jupyter |
| **Tools** | Google Colab (recommended) or VS Code + `pds` conda environment |
| **Notebook** | `notebooks/pandas_lesson.ipynb` |

## Agenda

| Time | Part | Topic |
|------|------|-------|
| 0:00 – 1:00 | Part 1 | Structures & Modification — DataFrames, Series, attributes |
| 1:00 – 2:00 | Part 2 | The Art of Selection — loc, iloc, Boolean filtering |
| 2:00 – 3:00 | Part 3 | Analysis & Operations — apply, sort, rank |

## 🎯 Learning Objectives

By the end of this session, you will be able to:

1. Create and modify Pandas data structures (Series and DataFrames).
2. Apply Pandas indexing and selection using `.loc`, `.iloc`, and Boolean filters.
3. Apply functions and mapping in Pandas using `.apply()` and `.map()`.
4. Sort and rank data in Pandas.

---

## 🏃 Part 1: Structures & Modification (60 min)

### 🎯 Focus
LO1 — Create and modify Pandas data structures.

### Concept Overview

Open the notebook `notebooks/pandas_lesson.ipynb` and follow along.

**Key topics in this section:**
- Creating DataFrames from dictionaries vs. lists
- DataFrame attributes: `.shape`, `.dtypes`, `.columns`
- Accessing columns
- Adding a new column (scalar vs. array assignment)

### 🛠️ Activity: "The Inventory System"

Create a DataFrame representing a store inventory, add columns for `Price` and `Stock`, and calculate `Total Value`.

> **Discussion:** How does vectorization (operating on entire columns at once) replace the need for loops?

---

## 🏃 Part 2: The Art of Selection (60 min)

### 🎯 Focus
LO2 — Indexing and Selection (`.loc`, `.iloc`, `[]`).

### Concept Overview

**Analogy:** Think of `.loc` as using a street address (label-based), and `.iloc` as using GPS coordinates (position-based).

**Key topics in this section:**
- Slicing rows with `.loc` and `.iloc`
- Selecting specific columns
- Boolean filtering: `df[df['Value'] > 100]`
- Common pitfall: `[]` slicing behavior

### 🛠️ Activity: "Data Detective"

Given a dataset with specific targets, extract:

1. Rows 5–10.
2. The `Email` column for users in `Texas`.
3. Update values for specific rows using `.loc`.

> **Question:** "Which method would you use to select the last row of a DataFrame — `.loc` or `.iloc`? Why?"

---

## 🏃 Part 3: Analysis & Operations (60 min)

### 🎯 Focus
LO3 (Functions) & LO4 (Sort/Rank).

### Concept Overview

**Key topics in this section:**
- Introduction to `.apply()` vs. loops
- Sorting by index vs. values
- Ranking data (handling ties)
- Using `.apply()` for custom text formatting

### 🛠️ Activity: "Leaderboard Logic"

Given a dataset of game scores:

1. Create a function to categorize scores (e.g., `'High'` / `'Low'`).
2. Apply it to create a `Category` column.
3. Sort the data to find the winner.
4. Rank the players.

### 💬 Reflection

- What are the optional topics for further self-study? (Reindexing, Dropping Entries, Multi-indexing)
- What is the difference between sorting by index and sorting by values?

---

## 🎯 Wrap-Up

**Key Takeaways:**
1. DataFrames are the central data structure in Pandas — understanding how to create and modify them is foundational.
2. `.loc` (label-based) and `.iloc` (position-based) are the primary tools for row and column selection.
3. `.apply()` lets you transform DataFrame values with custom logic — cleaner and faster than writing loops.

**Next Steps:**
- Complete the [Assignment](./assignment.md) — Pandas practice covering selection, aggregation, and manipulation.
- Next lesson: Lesson 1.8 introduces EDA Basic — inspecting, cleaning, and understanding your data.
