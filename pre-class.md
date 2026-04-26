# 📚 Pre-Class: Introduction to Pandas

⏱️ **Estimated Time:** 45–60 minutes
**Prerequisites:** Lesson 1.6 — NumPy

> In Lesson 1.6 you worked with NumPy arrays — fast numerical grids. NumPy is powerful but low-level: it doesn't know about column names, dates, or mixed data types. **Pandas** is built on top of NumPy and adds all of that — it's the tool you'll use to load, explore, and clean real-world datasets for the rest of this course.

## **🎯 What You'll Learn Before Class**

By completing this pre-class work, you will:

* **Understand** the difference between a list, a dictionary, and a Pandas DataFrame.  
* **Identify** the two core Pandas structures: Series and DataFrame.  
* **Recognize** how to import Pandas and Numpy.

## 🎬 Brief intro of Pandas

* **Watch this video:** [Pandas: Your Data Toolbox](https://youtu.be/QnMPKycUW64?si=7JiFGkIo9Tl9pF6k)

## **💻 Part 1: Environment Setup (15-20 min)**

### **Prerequisites**

### For Google Colab User

**If you use Google Colab to run the Jupyter notebook, no installation is required.**

### For VS Code User

**Please follow the Installation Instructions below**

Ensure you have Python 3.8+ and Jupyter Notebook/Lab installed.
Open your terminal or command prompt and run:

Install the prescribed conda environment before you begin.

```bash
conda env create -f environment.yml
```

To start Jupyter Notebook, open your terminal (or anaconda prompt), then activate the conda environment:

```bash
conda activate pds
```


```
pip install pandas numpy
# Or using conda:
conda install pandas numpy
```

#### **Verification**

Create a new Jupyter Notebook and run this cell:

```python
import pandas as pd
import numpy as np

print(f"Pandas version: {pd.__version__}")
print("✅ Environment is ready!")
```

## **📚 Part 2: Course Introduction (10-15 min)**

### **What Is Pandas?**

Pandas is the Excel of Python. It takes data that might look like a messy pile of lists or dictionaries and organizes it into a clean, tabular format called a **DataFrame**.

Real-World Example:

Imagine you have sales data. In standard Python, calculating the "Average Sales per Region" requires loops and complex logic. In Pandas, it's often a single line of code.

### **Why This Matters**

* **Efficiency:** Handle millions of rows in seconds.  
* **Integration:** Works perfectly with visualization tools and machine learning libraries.  
* **Standard:** It is the industry standard for data manipulation in Python.

## **🧠 Part 3: Basic Concepts (20-25 min)**

### **Concept 1: The Series**

Definition: A Series is a one-dimensional labeled array.

Analogy: Think of a Series like a single column in an Excel sheet. It has values, and it has row labels (the index).

**Try It Yourself:**

```python
import pandas as pd
# A simple list of data
data = [10, 20, 30, 40]
# Converting it to a Pandas Series
s = pd.Series(data, index=['a', 'b', 'c', 'd'])
print(s)
```

### **Concept 2: The DataFrame**

Definition: A DataFrame is a 2-dimensional labeled data structure with columns of potentially different types.

Analogy: Think of a DataFrame like the whole Spreadsheet. It is essentially a collection of Series (columns) that share the same index (rows).

**Try It Yourself:**

```
# A dictionary where keys are column names
data = {
    'Apples': [3, 2, 0, 1],
    'Oranges': [0, 3, 7, 2]
}
df = pd.DataFrame(data)
print(df)
```

## **✅ Pre-Class Self-Check**

Before class, make sure you can:

* \[ \] Import pandas as pd.
* \[ \] Create a simple Series from a list.
* \[ \] Explain the difference between a Series and a DataFrame.

## **❓ Pre-Class Questions to Consider**

Try to answer these yourself first, then check below.

1. Why might we want to label our data (using an Index) instead of just using numbered positions (0, 1, 2)?
2. If a DataFrame is a collection of Series, what happens if we extract just one column from a DataFrame?

<details>
<summary>Suggested answers</summary>

**Q1:** Labels make data self-documenting and robust. If you use positional indexing (`df[0]`) and someone reorders the DataFrame, your index now points to the wrong row. A named index like `df['Alice']` or a date index like `df['2024-01-15']` is meaningful and stable — it doesn't break if rows are added or reordered.

**Q2:** Extracting a single column from a DataFrame returns a **Series** — a 1D labelled array. You can verify this with `type(df['column_name'])`. The Series shares the same row index as the original DataFrame, which is why you can combine or compare columns easily.

</details>
