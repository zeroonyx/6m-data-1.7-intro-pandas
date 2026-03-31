# 📚 Lesson 1.7: Introduction to Pandas

**Theme:** The Data Workbench — manipulating tabular data with Python's most powerful library

---

## 📅 Lesson Overview

| Section | Duration | Topic / Activity |
|---------|----------|-----------------|
| **Part 1: DataFrames & Modification** | 55 min | Series vs. DataFrame; creating & modifying data structures |
| **Part 2: Indexing & Selection** | 55 min | `.loc` vs. `.iloc`; conditional filtering; data extraction |
| **Part 3: Functions, Sorting & Ranking** | 55 min | `.apply()`; `.map()`; sorting; ranking |

---

## 🎯 Learning Outcomes

By the end of this lesson, you will be able to:

1. **Construct** Pandas Series and DataFrames from dictionaries and lists, and modify their structure.
2. **Apply** label-based (`.loc`) and position-based (`.iloc`) indexing to extract specific rows and columns.
3. **Use** `.apply()` and `.map()` to transform DataFrame values with custom functions.
4. **Sort** and **rank** DataFrames by one or more columns to surface meaningful patterns.

---

## 📂 Course Materials

| Material | Description | Est. Time |
|----------|-------------|-----------|
| [Pre-Class](./pre-class.md) | Series vs. DataFrame; Pandas vs. lists; environment setup | 30–45 min |
| [Lesson Plan](./lesson.md) | Instructor guide for the 3-hour coding session | 3 hours |
| [Post-Class](./post-class.md) | Pandas practice — selection, aggregation, and manipulation | 45–60 min |
| [Reference](./reference.md) | Pandas cheat sheet, indexing reference, common operations | As needed |

---

## 🛠️ Tools & Setup

- **[Google Colab](https://colab.research.google.com)** *(recommended)*: No installation needed.
- **[VS Code](https://code.visualstudio.com)** + Python + Jupyter extensions *(alternative)*.
- **Notebook:** `notebooks/pandas_lesson.ipynb` — open in Colab or VS Code with the `pds` kernel.
- **Environment:** `conda env create -f environment.yml` then `conda activate pds` (VS Code users only).
