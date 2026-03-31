# 📝 Post-Class: Introduction to Pandas

> ⏱️ **Estimated Time:** 45–60 minutes | Complete this **after** your class session.

---

## 🎯 Learning Objectives Revisited

This assignment reinforces what you practised in class:
- Constructing and modifying Pandas DataFrames
- Applying `.loc` and `.iloc` for precise data extraction
- Transforming data with `.apply()`, `.map()`, sorting, and ranking

---

## Part 1: Conceptual Check (15 min)

Test your understanding before diving into the code.

**Question 1:** What is the key difference between a Pandas `Series` and a `DataFrame`?

**Question 2:** You run `df.loc[0:3]`. How many rows do you get? What about `df.iloc[0:3]`?

**Question 3:** You have a DataFrame with a `price` column stored as `object` type (strings like "£45.99"). What problem does this cause, and how do you fix it?

**Question 4:** When would you use `.apply()` instead of a direct vectorised operation like `df['col'] * 2`?

**Question 5:** How do you select all numeric columns from a DataFrame, excluding float types?

<details>
<summary>💡 Check Your Answers</summary>

**Q1:** A `Series` is 1-dimensional (a single column with an index). A `DataFrame` is 2-dimensional — it's a collection of Series sharing the same index, like a full spreadsheet.

**Q2:** `.loc[0:3]` returns **4 rows** (0, 1, 2, and 3 — end is inclusive). `.iloc[0:3]` returns **3 rows** (0, 1, 2 — end is exclusive).

**Q3:** You can't compute statistics (mean, sum) on string columns. Fix with: `df['price'] = df['price'].str.extract(r'(\d+\.?\d*)').astype(float)`

**Q4:** Use `.apply()` when you need row-level logic involving multiple columns, or when no vectorised equivalent exists. For simple column-wise maths, always prefer vectorised operations — they're 10–100× faster.

**Q5:** `df.select_dtypes(include=['number'], exclude=['float'])`

</details>

---

## Part 2: Practical Challenge (30–45 min)

### Scenario: "The Bookshop Analyst"

You're a data analyst for an online bookshop. The operations team has exported their inventory to a CSV and they need your help making sense of it.

---

### Challenge 1: Build and Inspect the Dataset

Create the following DataFrame and perform a health check:

```python
import pandas as pd

books = pd.DataFrame({
    'title': ['The Pragmatic Programmer', 'Clean Code', 'Python Crash Course',
              'Data Science from Scratch', 'Designing Data-Intensive Apps'],
    'author': ['Hunt & Thomas', 'Robert Martin', 'Eric Matthes',
               'Joel Grus', 'Martin Kleppmann'],
    'genre': ['Tech', 'Tech', 'Tech', 'Data', 'Data'],
    'price': [45.99, 38.50, 29.99, 42.00, 55.00],
    'units_sold': [120, 95, 200, 80, 60],
    'in_stock': [True, True, False, True, False]
})
```

**Tasks:**
1. Use `.info()` — how many non-null values does each column have?
2. Use `.describe()` — what's the average price and maximum units sold?
3. Add a `revenue` column: `price × units_sold`.
4. What is the total revenue across all books?

<details>
<summary>💡 Hint</summary>

For total revenue: `books['revenue'].sum()`. For the new column: `books['revenue'] = books['price'] * books['units_sold']`.

</details>

<details>
<summary>✅ Solution</summary>

```python
books['revenue'] = books['price'] * books['units_sold']
print(books.info())
print(books.describe())
print(f"Total revenue: £{books['revenue'].sum():,.2f}")
```

</details>

---

### Challenge 2: Indexing & Filtering

**Tasks:**
1. Use `.loc` to select only `title` and `revenue` for Data genre books.
2. Use `.iloc` to retrieve the last 3 rows and first 3 columns.
3. Filter books that are **in stock** AND have a **price above £40**.
4. Find the book with the **highest revenue** using `.loc` with `.idxmax()`.

<details>
<summary>💡 Hint</summary>

For `.idxmax()`: `books.loc[books['revenue'].idxmax()]` returns the full row of the highest-revenue book.

</details>

<details>
<summary>✅ Solution</summary>

```python
# 1. Data genre books, title and revenue only
data_books = books.loc[books['genre'] == 'Data', ['title', 'revenue']]

# 2. Last 3 rows, first 3 columns
subset = books.iloc[-3:, :3]

# 3. In-stock books priced above £40
premium_stock = books.loc[(books['in_stock'] == True) & (books['price'] > 40)]

# 4. Highest revenue book
top_book = books.loc[books['revenue'].idxmax()]
print(f"Top earner: {top_book['title']} — £{top_book['revenue']:,.2f}")
```

</details>

---

### Challenge 3: Transform, Sort & Rank

**Tasks:**
1. Use `.apply()` to add a `price_tier` column: `'Budget'` (< £35), `'Standard'` (£35–£50), `'Premium'` (> £50).
2. Sort the DataFrame by `revenue` descending.
3. Add a `sales_rank` column using `.rank(ascending=False)`.
4. Use `.map()` to encode `genre` as a number: `{'Tech': 0, 'Data': 1}`.

<details>
<summary>✅ Solution</summary>

```python
# 1. Price tier
def get_tier(price):
    if price < 35:
        return 'Budget'
    elif price <= 50:
        return 'Standard'
    else:
        return 'Premium'

books['price_tier'] = books['price'].apply(get_tier)

# 2. Sort by revenue
books_sorted = books.sort_values('revenue', ascending=False)

# 3. Sales rank
books['sales_rank'] = books['units_sold'].rank(ascending=False).astype(int)

# 4. Encode genre
books['genre_encoded'] = books['genre'].map({'Tech': 0, 'Data': 1})

print(books[['title', 'price_tier', 'sales_rank', 'genre_encoded']])
```

</details>

---

### 🏆 Stretch Challenge (Optional)

The manager wants a report comparing average price and total revenue by `price_tier`. Use `groupby()` to generate this summary. Which tier contributes the most total revenue despite having the lowest average price?

---

## 💬 Reflection (5 min)

In 2–3 sentences, answer:

> *Think of a dataset you might work with in your field. Which Pandas operation from today (indexing, `.apply()`, sorting, or ranking) would be most immediately useful? Why?*

---

## 📤 Share Your Work

Post your Challenge 3 output and reflection in **Discord** under `#assignments`. React to at least one classmate's post.
