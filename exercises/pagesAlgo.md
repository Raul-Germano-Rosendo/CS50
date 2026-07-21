# Searching Algorithms

One of the first algorithmic ideas introduced in **CS50** is how to efficiently search for information.

Imagine you're looking for the name **"Smith"** in a printed phone book.

---

## Method 1 — Linear Search

The simplest approach is to start at the first page and check every name one by one.

```text
Alice
Bob
Charlie
David
Emma
...
Smith
```

This method always works, but it can be very slow if the phone book is large.

**Time Complexity:** **O(n)**

### "What if I Check Two Pages at a Time?"

A common idea is:

> "Instead of checking one page at a time, why not check **two pages at a time**?"

Example:

```text
Alice   Bob
Charlie David
Emma    Frank
Grace   Henry
...
```

Now you're making roughly **half as many checks**.

This gives a running time of:

**O(n/2)**

At first glance, this seems twice as fast as **O(n)**.

### Why Isn't It Better?

In **Big O notation**, constant factors are ignored.

Although checking two pages at a time reduces the total number of operations, the amount of work still grows **proportionally to the size of the input**.

| Number of Names | O(n) | O(n/2) |
|----------------:|------:|--------:|
| 100 | 100 checks | 50 checks |
| 1,000 | 1,000 checks | 500 checks |
| 1,000,000 | 1,000,000 checks | 500,000 checks |

Mathematically,

```text
O(n/2) = O(n)
```

The algorithm is faster by a **constant factor**, but it still scales linearly as the input grows.

---

## Method 2 — Binary Search

A much faster strategy is possible **only if the phone book is already sorted alphabetically**.

Instead of checking every page:

1. Open the book in the middle.
2. Compare the current page with the name you're looking for.
3. If the name should come **before** the current page, discard the second half.
4. If the name should come **after**, discard the first half.
5. Repeat with the remaining half.

```text
Phone Book

+---------------------------+
|                           |
|           📖              |
|                           |
+---------------------------+

          ↓

        Open Here

        "Miller"

Smith comes after Miller

Discard the left half.

+---------------------------+
|                           |
|       Remaining Half      |
|                           |
+---------------------------+

Repeat...
```

Unlike checking two pages at a time, Binary Search **cuts the entire remaining search space in half after every comparison**.

Example:

```text
1024 pages
↓
512
↓
256
↓
128
↓
64
↓
32
↓
16
↓
8
↓
4
↓
2
↓
1
```

Instead of checking **1,024 pages**, you only need about **10 guesses**.

This gives Binary Search a time complexity of:

**O(log n)**

---

## Comparison

| Algorithm | Requirement | Time Complexity |
|-----------|-------------|-----------------|
| Linear Search | None | **O(n)** |
| Linear Search (2 pages at a time) | None | **O(n/2) = O(n)** |
| Binary Search | Data must be sorted | **O(log n)** |

---

## Key Takeaways

- **Linear Search** checks items one by one.
- Checking **two pages at a time** reduces the number of operations but **does not change the algorithm's growth rate**.
- **Binary Search** repeatedly cuts the remaining search space in half.
- Binary Search is significantly faster for large datasets.
- Binary Search only works when the data is **sorted**.

> **CS50 Insight:** The phone book example teaches one of the most important lessons in computer science: a clever algorithm can make a much bigger difference than simply doing the same work a little faster. Constant improvements (like O(n/2)) are useful, but changing the growth rate (from O(n) to O(log n)) is what truly scales.