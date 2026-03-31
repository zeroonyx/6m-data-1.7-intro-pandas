# 🎓 Lesson 1.7: Introduction to Pandas — Instructor Guide

## Session Overview

| Item | Detail |
|------|--------|
| **Duration** | 3 hours |
| **Format** | Flipped Classroom + Guided Coding in Jupyter |
| **Prerequisites** | NumPy arrays (Lesson 1.6); Python lists and dictionaries; pre-class setup |
| **Tools** | VS Code + `pds` conda environment; or Google Colab |
| **Notebook** | `notebooks/pandas_lesson.ipynb` |

### Agenda

| Time | Section | Focus |
|------|---------|-------|
| 0:00 – 0:10 | Welcome & Pre-Class Review | Quiz: Series vs. DataFrame; setup check |
| 0:10 – 1:00 | Part 1: DataFrames & Modification | Building and altering Pandas structures |
| 1:00 – 1:05 | Break | — |
| 1:05 – 1:55 | Part 2: Indexing & Selection | `.loc` vs `.iloc`; conditional filtering |
| 1:55 – 2:00 | Break | — |
| 2:00 – 2:55 | Part 3: Functions, Sorting & Ranking | `.apply()`; `.map()`; sort and rank |
| 2:55 – 3:00 | Wrap-Up | Takeaways & post-class assignment briefing |

---

## 🏃 Part 1: DataFrames & Modification (50 min)

### 🎯 Learning Objective
Construct Pandas Series and DataFrames from raw data and modify their structure by adding, renaming, and dropping columns.

### 📖 Theory Recap (10 min)

**Analogy:** A **Series** is a single column in a spreadsheet — it has an index (row labels) and values. A **DataFrame** is the full spreadsheet — multiple Series sharing the same row index.

| Structure | Dimensions | Think of it as |
|-----------|-----------|----------------|
| `Series` | 1D | One column with labels |
| `DataFrame` | 2D | Full spreadsheet / database table |

Key attributes every student should know:
- `.shape` — (rows, columns)
- `.dtypes` — data type per column
- `.columns` — column names
- `.index` — row labels

### 🛠️ Hands-On Activity: "The Inventory System" (35 min)

**Scenario:** You're building a product inventory tracker for a small electronics store.

**In the notebook, work through:**

1. Create a DataFrame from a dictionary:
```python
import pandas as pd

inventory = pd.DataFrame({
    'product': ['Laptop', 'Mouse', 'Monitor', 'Keyboard'],
    'category': ['Computer', 'Accessory', 'Computer', 'Accessory'],
    'units': [10, 50, 15, 30]
})
```

2. Add a `price` column: `inventory['price'] = [1200, 25, 400, 75]`
3. Add a calculated column: `inventory['total_value'] = inventory['units'] * inventory['price']`
4. Rename a column with `.rename()` and drop a column with `.drop()`.
5. Inspect with `.info()` and `.describe()` — note which columns are included.

**Discussion Questions:**
- "What does `.describe()` not include, and why?"
- "If you add a column with a scalar value (e.g., `df['tax_rate'] = 0.09`), what happens to every row?"

### 💬 Q&A & Reflection (10 min)

- **Common Misconception:** "I can modify a DataFrame by assigning to a slice." → Pandas may raise a `SettingWithCopyWarning`. Always use `.loc[]` or `.copy()` when modifying subsets.
- **Business Case:** Pandas is the most-used data tool at companies like Spotify and Zalando — their data teams process millions of rows of user behaviour data daily using exactly these DataFrame operations.

---

## 🏃 Part 2: Indexing & Selection (50 min)

### 🎯 Learning Objective
Apply label-based (`.loc`) and position-based (`.iloc`) indexing to extract specific rows, columns, and subsets of data.

### 📖 Theory Recap (10 min)

**Analogy:** Think of `.loc` as an **address** ("Go to Main Street, House 42") and `.iloc` as **GPS coordinates** ("Go to row 3, column 1"). Both get you to the same place, but through different reference systems.

| Method | Uses | Example |
|--------|------|---------|
| `.loc[rows, cols]` | Labels / conditions | `df.loc[df['price'] > 100, 'product']` |
| `.iloc[rows, cols]` | Integer positions | `df.iloc[0:3, 1:4]` |

**Critical rule:** `.loc` includes the end of a slice; `.iloc` does not. `df.loc[0:3]` returns rows 0, 1, 2, **and 3**. `df.iloc[0:3]` returns rows 0, 1, **and 2**.

### 🛠️ Hands-On Activity: "The Data Detective" (35 min)

**Scenario:** You're a data analyst at an e-commerce company. The operations manager has sent you 4 specific requests — extract exactly what they need.

**In the notebook, complete these extraction tasks:**

1. Select only the `product` and `total_value` columns using `.loc`.
2. Select the first 2 rows and first 3 columns using `.iloc`.
3. Filter rows where `total_value > 5000` using a boolean condition.
4. Filter rows where `category == 'Computer'` AND `units < 20`.

```python
# Challenge: How many high-value computer products do we have?
high_value_computers = inventory.loc[
    (inventory['category'] == 'Computer') & (inventory['total_value'] > 5000)
]
```

5. Use `.at[]` to retrieve a single cell by label, and `.iat[]` by position.

**Discussion Questions:**
- "What does `df.loc[:, 'price']` return vs. `df['price']`? Are they the same?"
- "When would you use `.iloc` instead of `.loc`?"

### 💬 Q&A & Reflection (10 min)

- **Common Misconception:** "`loc` and `iloc` are interchangeable." → Only when the index is the default integer range (0, 1, 2…). With custom string indices or after filtering, they diverge significantly.
- **Business Case:** At Amazon, analysts use conditional `.loc` filters daily to isolate specific product categories, date ranges, or customer segments from billion-row datasets.

---

## 🏃 Part 3: Functions, Sorting & Ranking (50 min)

### 🎯 Learning Objective
Transform data using `.apply()` and `.map()`, and surface meaningful patterns through sorting and ranking.

### 📖 Theory Recap (10 min)

**Analogy:** `.apply()` is like a factory assembly line — every row (or column) passes through the same machine and comes out transformed. `.map()` is like a translation dictionary — each value gets swapped for its mapped equivalent.

| Method | Applied to | Use case |
|--------|-----------|----------|
| `.apply(func)` | Rows or columns | Custom calculations, multi-column logic |
| `.map(dict_or_func)` | A single Series | Value replacement or encoding |
| `.sort_values()` | DataFrame | Order rows by one or more columns |
| `.rank()` | Series | Assign rank positions (handles ties) |

### 🛠️ Hands-On Activity: "The Leaderboard" (35 min)

**Scenario:** The store manager wants a ranked report: products categorised by value tier, sorted by total value, with ranking.

**In the notebook, work through:**

1. Categorise products using `.apply()`:
```python
def value_tier(row):
    if row['total_value'] >= 10000:
        return 'Premium'
    elif row['total_value'] >= 3000:
        return 'Mid-Range'
    else:
        return 'Budget'

inventory['tier'] = inventory.apply(value_tier, axis=1)
```

2. Use `.map()` to encode categories as numbers: `{'Computer': 1, 'Accessory': 0}`
3. Sort by `total_value` descending: `.sort_values('total_value', ascending=False)`
4. Add a rank column: `inventory['rank'] = inventory['total_value'].rank(ascending=False)`
5. Sort by multiple columns: `['tier', 'total_value']` with mixed ascending order.

**Discussion Questions:**
- "What's the difference between `.rank(method='min')` and `.rank(method='dense')` when there are ties?"
- "Why is `.apply()` generally slower than vectorised operations like `df['col'] * 2`?"

### 💬 Q&A & Reflection (10 min)

- **Common Misconception:** "`.apply()` is always the best way to transform data." → `.apply()` is row-by-row and slow on large datasets. Vectorised operations (NumPy/Pandas built-ins) are 10–100× faster. Use `.apply()` only when vectorisation isn't possible.
- **Business Case:** Retail companies use `.apply()` with complex pricing rules (discounts, loyalty tiers, regional adjustments) to transform millions of product records — but always benchmark against vectorised alternatives first.

---

## 🎯 Wrap-Up (5 min)

### Key Takeaways
1. **DataFrame = multiple Series sharing an index.** Master `.shape`, `.dtypes`, `.info()` — these are your first three calls on any new dataset.
2. **`.loc` for labels, `.iloc` for positions.** When in doubt, use `.loc` — it's more explicit and less error-prone.
3. **`.apply()` is powerful but slow** — use built-in vectorised operations where possible.

### Next Steps
- **Post-Class:** Complete the [post-class.md](./post-class.md) Pandas exercises — 5 challenges covering selection, aggregation, and manipulation (45–60 min).
- **Next Lesson:** Lesson 1.8 applies everything learned so far to real-world Exploratory Data Analysis (EDA).
