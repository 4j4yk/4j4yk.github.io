---
title: "The Growth Hierarchy: The Most Important Big-O Table You Should Memorize"
date: 2026-01-22
draft: false
tags: ["algorithms", "big-o", "performance", "computer-science"]
summary: "A simple growth hierarchy of time complexities every engineer should memorize, and why anything worse than O(n²) is often dangerous."
---

When analyzing algorithms, one idea matters more than any other:

> **How fast does this grow as input size increases?**

This is what **Big-O notation** answers.[^big-o]

And there is one table that every engineer should **memorize** because it explains a large share of performance problems you’ll ever face.

---

## The Growth Hierarchy (Fastest → Slowest)

| Order | Complexity | Typical Example |
|------|------------|-----------------|
| 1 | **O(1)** | Array index access, hash lookup (amortized)[^hash-table] |
| 2 | **O(log n)** | Binary search[^binary-search] |
| 3 | **O(n)** | Single loop, linear scan |
| 4 | **O(n log n)** | Efficient sorting (merge sort, heap sort)[^merge-sort][^heapsort] |
| 5 | **O(n²)** | Nested loops, simple bubble sort[^bubble-sort] |
| 6 | **O(2ⁿ)** | Subset generation, brute-force recursion[^big-o-orders] |
| 7 | **O(n!)** | Permutations, traveling salesman brute force[^big-o-orders] |

---

## How to Read This Table

Think of it as **how quickly your runtime explodes** as `n` grows.

- O(1) and O(log n) barely grow  
- O(n) grows steadily  
- O(n log n) is typically practical  
- O(n²) becomes slow fast  
- O(2ⁿ) and O(n!) become impossible very quickly  

---

## The Golden Rule

> **If your solution is worse than O(n²), you are often in danger.**

Why?

Because:

- n = 100  
- n² = 10,000 (still fine)  
- 2ⁿ = 1,267,650,600,228,229,401,496,703,205,376 (base‑2 exponential)  

Exponential growth destroys performance long before memory or CPU limits appear.

![Exponential blow-up comparison (illustrative, log-scaled)](/images/big-o/exponential-blowup.svg)

---

## What This Means in Practice

{{< rawhtml >}}
<h3 style="color: #1B8A3A;">Safe Zone (Preferred)</h3>
{{< /rawhtml >}}

- O(1)  
- O(log n)  
- O(n)  
- O(n log n)  

These scale well and survive production traffic. (See the table above.)

---

{{< rawhtml >}}
<h3 style="color: #E67E22;">Danger Zone (Use With Caution)</h3>
{{< /rawhtml >}}

Acceptable only when:
- input size is small  
- data is bounded  
- the algorithm runs rarely  

---

{{< rawhtml >}}
<h3 style="color: #C0392B;">Red Zone (Avoid in Production)</h3>
{{< /rawhtml >}}

These are typically:
- brute-force solutions  
- backtracking without pruning  
- interview solutions before optimization  

They explode with even moderate input sizes.

---

## Mental Shortcut

When reading code, use quick cues:

- Loop + binary search? → O(n log m) (where `m` is the search space)  
- Loop inside loop? → O(n²)  
- Recursive branching without pruning? → often exponential  

This lets you estimate performance in seconds without re-deriving everything.

![Linear scan vs binary search steps](/images/big-o/linear-vs-binary.svg)

---

## Final Thought

Big-O is not about math.[^big-o]  
It’s about **survival at scale**.

If you memorize only one thing from algorithms, memorize this:

> **Once you cross O(n²), performance stops being a tuning problem and becomes an architectural problem.**

---

## Comic (xkcd)

![xkcd 2939: Complexity Analysis](https://imgs.xkcd.com/comics/complexity_analysis.png)

Attribution: xkcd 2939 “Complexity Analysis” by Randall Munroe (CC BY-NC 2.5).  
Source: https://xkcd.com/2939/  
License: https://xkcd.com/license.html

---

## References

[^big-o]: NIST Dictionary of Algorithms and Data Structures — “big-O notation”. https://www.nist.gov/dads/HTML/bigOnotation.html
[^hash-table]: NIST Dictionary of Algorithms and Data Structures — “hash table” (complexity may be constant if the table is big enough or grows). https://www.nist.gov/dads/HTML/hashtab.html
[^binary-search]: NIST Dictionary of Algorithms and Data Structures — “binary search” (run time O(ln n)). https://www.nist.gov/dads/HTML/binarySearch.html
[^merge-sort]: NIST Dictionary of Algorithms and Data Structures — “merge sort” (run time Θ(n log n)). https://www.nist.gov/dads/HTML/mergesort.html
[^heapsort]: NIST Dictionary of Algorithms and Data Structures — “heapsort” (run time O(n log n)). https://www.nist.gov/dads/HTML/heapSort.html
[^bubble-sort]: NIST Dictionary of Algorithms and Data Structures — “bubble sort” (O(n^2) for arbitrary data). https://www.nist.gov/dads/HTML/bubblesort.html
[^big-o-orders]: Wikipedia — “Big O notation”, “Orders of common functions” (O(c^n) exponential, O(n!) factorial) with typical examples. https://en.wikipedia.org/wiki/Big_O_notation
