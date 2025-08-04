Great! Let's now solve the **Activity Selection Problem** using a **Conflict Graph** approach.

---

### 🔍 What is a Conflict Graph?

* Each **activity** is a **node**.
* Draw an **edge** between two activities if they **overlap (conflict)**.
* Our goal is to **select the largest set of activities that are mutually non-conflicting**, i.e., no two of them share an edge.

This is exactly the **Maximum Independent Set (MIS)** problem on the conflict graph.

> **Independent Set:** A set of vertices such that no two are adjacent.

---

### 📌 Example Activities

Let’s take 5 activities as example:

| Activity | Start | End |
| -------- | ----- | --- |
| A0       | 1     | 4   |
| A1       | 3     | 5   |
| A2       | 0     | 6   |
| A3       | 5     | 7   |
| A4       | 8     | 9   |

---

### 🔗 Step 1: Build the Conflict Graph

Check for each pair: do they **overlap**?

Two activities `Ai` and `Aj` **conflict** if:

```
!(Ai.end <= Aj.start || Aj.end <= Ai.start)
```

Let’s build it:

| Pair  | Conflict? |
| ----- | --------- |
| A0–A1 | Yes       |
| A0–A2 | Yes       |
| A0–A3 | No        |
| A0–A4 | No        |
| A1–A2 | Yes       |
| A1–A3 | Yes       |
| A1–A4 | No        |
| A2–A3 | Yes       |
| A2–A4 | No        |
| A3–A4 | No        |

So the graph is:

* A0: A1, A2
* A1: A0, A2, A3
* A2: A0, A1, A3
* A3: A1, A2
* A4: none

---

### 🔗 Conflict Graph (Adjacency List):

```plaintext
A0 — A1, A2
A1 — A0, A2, A3
A2 — A0, A1, A3
A3 — A1, A2
A4 — (no edges)
```

---

### ✅ Step 2: Solve Maximum Independent Set (MIS)

We want the **largest set of activities** such that **no two are connected**.

This is NP-Hard in general graphs, but for small graphs (like n ≤ 20), we can do brute force.

For this example, let's try all combinations manually:

* {A4, A0, A3} → Valid (A4 has no edges, A0 and A3 don’t conflict)
* {A4, A3} → Valid
* {A4, A0} → Valid
* {A4, A2} → Valid
* {A0, A3} → Valid
* {A1, A4} → Valid

Max valid sets of size **3**:

* {A4, A0, A3}

---

### 🎯 Final Answer

✅ **Max non-overlapping set using conflict graph**:
**{A4, A0, A3}** → **Total: 3 activities**

---

### 💡 Code Sketch (Optional)

You can solve this with brute-force subsets in code too:

```cpp
// Pseudocode to solve MIS (n <= 20)
for (each subset of activities) {
   bool valid = true;
   for (each pair in subset) {
       if (graph has edge between them) {
           valid = false; break;
       }
   }
   if (valid) update max_set
}
```

Let me know if you'd like to see full code, or solve for your input image set!
