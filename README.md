# Algorithms Practicals: Implementation & Time Analysis

A collection of **12 Jupyter notebooks** that implement classic algorithms in Python and analyze them empirically and theoretically. Every notebook follows the same structure:

- A from-scratch Python implementation of each algorithm
- **Interactive user input** (enter your own data)
- **Runtime measurement** using Python's `time` module
- **Time and space complexity** analysis (best / average / worst case where it applies)
- A **runtime comparison** with a chart, and a summary table
- **Saved outputs**, so each notebook can be read on GitHub without running anything

## Contents

| #  | Notebook | Topic | Technique | Headline Complexity |
|----|----------|-------|-----------|---------------------|
| 1  | [Practical-1.ipynb](Practical-1.ipynb)   | [Sorting Algorithms](#practical-1-sorting-algorithms) | Comparison sorts | O(n²) to O(n log n) |
| 2  | [Practical-2.ipynb](Practical-2.ipynb)   | [Linear and Binary Search](#practical-2-linear-and-binary-search) | Searching | O(n) vs O(log n) |
| 3  | [Practical-3.ipynb](Practical-3.ipynb)   | [Heap Sort (Max-Heap)](#practical-3-heap-sort-max-heap) | Heap data structure | O(n log n), O(1) space |
| 4  | [Practical-4.ipynb](Practical-4.ipynb)   | [Factorial (Iterative vs Recursive)](#practical-4-factorial-iterative-vs-recursive) | Iteration vs recursion | O(n) time |
| 5  | [Practical-5.ipynb](Practical-5.ipynb)   | [Knapsack Problem](#practical-5-knapsack-problem-dynamic-programming) | Dynamic programming | O(n·W) |
| 6  | [Practical-6.ipynb](Practical-6.ipynb)   | [Matrix Chain Multiplication](#practical-6-matrix-chain-multiplication-dynamic-programming) | Dynamic programming | O(n³) |
| 7  | [Practical-7.ipynb](Practical-7.ipynb)   | [Coin Change](#practical-7-coin-change-dynamic-programming) | Dynamic programming | O(amount · k) |
| 8  | [Practical-8.ipynb](Practical-8.ipynb)   | [Graph Traversal (DFS and BFS)](#practical-8-graph-traversal-dfs-and-bfs) | Graph search | O(V + E) |
| 9  | [Practical-9.ipynb](Practical-9.ipynb)   | [Prim's Algorithm (MST)](#practical-9-prims-algorithm-mst) | Greedy | O(E log V) |
| 10 | [Practical-10.ipynb](Practical-10.ipynb) | [Kruskal's Algorithm (MST)](#practical-10-kruskals-algorithm-mst) | Greedy + Union-Find | O(E log E) |
| 11 | [Practical-11.ipynb](Practical-11.ipynb) | [Floyd-Warshall (All-Pairs Shortest Paths)](#practical-11-floyd-warshall-all-pairs-shortest-paths) | Dynamic programming | O(V³) |
| 12 | [Practical-12.ipynb](Practical-12.ipynb) | [Travelling Salesman Problem (TSP)](#practical-12-travelling-salesman-problem-tsp) | Brute force, DP, heuristics | O(n!) / O(n²·2ⁿ) / O(n²) |

## Getting Started

1. Clone the repository
2. Install the dependencies:
   ```bash
   pip install jupyter matplotlib networkx numpy
   ```
   | Notebooks | Extra libraries needed |
   |-----------|------------------------|
   | 1 – 7 and 12 | `matplotlib` only (everything else is the Python standard library) |
   | 8 – 10       | `matplotlib`, `networkx` |
   | 11           | `matplotlib`, `networkx`, `numpy` |
3. Open any notebook in **Jupyter Notebook**, **JupyterLab**, or **Google Colab**
4. Run the cells from top to bottom

### Using your own input

The demo cells run on sample data so each notebook executes end-to-end without prompting. Every notebook has small helper functions that take an optional sample string. **Call the helper with no arguments** and it will prompt you with `input()` instead:

```python
user_arr = get_user_list("64,34,25,12,22,11,90")   # uses the sample data
user_arr = get_user_list()                         # prompts you to type your own
```

| #  | Helper function(s) | Input format |
|----|--------------------|--------------|
| 1, 3 | `get_user_list()` | numbers separated by commas, e.g. `5,3,8,1,9` |
| 2    | `get_user_list()`, `get_user_target()` | a list as above, then the number to find |
| 4    | `get_user_number()` | a non-negative integer `n` |
| 5    | `get_user_items()`, `get_user_capacity()` | weights `2,3,4,5`, values `3,4,5,6`, then the capacity |
| 6    | `get_user_dimensions()` | matrix dimensions `p`, e.g. `10,20,30,40,30` for 4 matrices |
| 7    | `get_user_coins()`, `get_user_amount()` | coins `1,2,5`, then the target amount |
| 8    | `get_user_edges()`, `get_user_start_node()` | edges `A,B;A,C;B,D`, then the start node |
| 9    | `get_user_edges()`, `get_user_start_node()` | weighted edges `A,B,4;A,C,3;B,C,1`, then the start node |
| 10   | `get_user_edges()` | weighted edges `A,B,4;A,C,3;B,C,1` |
| 11   | `get_user_edges()` | **directed** weighted edges `A,B,3;B,C,2;C,A,5` |
| 12   | `get_user_matrix()` | distance matrix, rows split by `;`, e.g. `0,10,15,20;10,0,35,25;15,35,0,30;20,25,30,0` |

Invalid input never crashes a notebook; each helper falls back to a sensible default and says so.

---

## Practical 1: Sorting Algorithms

**Notebook:** [Practical-1.ipynb](Practical-1.ipynb)

Implements **Bubble, Selection, Insertion, Merge, and Quick Sort**, each with a user-input demo, then compares all five on the same 1,000-element random list with a bar chart.

| Algorithm      | Best       | Average    | Worst      | Space     | Stable | In-Place |
|----------------|------------|------------|------------|-----------|--------|----------|
| Bubble Sort    | O(n)       | O(n²)      | O(n²)      | O(1)      | Yes    | Yes      |
| Selection Sort | O(n²)      | O(n²)      | O(n²)      | O(1)      | No     | Yes      |
| Insertion Sort | O(n)       | O(n²)      | O(n²)      | O(1)      | Yes    | Yes      |
| Merge Sort     | O(n log n) | O(n log n) | O(n log n) | O(n)      | Yes    | No       |
| Quick Sort     | O(n log n) | O(n log n) | O(n²)      | O(log n)  | No     | Yes      |

**Sample result:** `[64, 34, 25, 12, 22, 11, 90]` sorts to `[11, 12, 22, 25, 34, 64, 90]`. On 1,000 random elements, Merge and Quick Sort finish in about 1-2 ms while Bubble Sort takes tens of milliseconds.

## Practical 2: Linear and Binary Search

**Notebook:** [Practical-2.ipynb](Practical-2.ipynb)

Implements **Linear Search** and **Binary Search** (iterative and recursive). The comparison searches for a missing value (the worst case) in sorted lists from 1,000 to 1,000,000 elements and plots runtime on a log-scale chart.

| Algorithm     | Best | Average  | Worst    | Space                              | Needs Sorted Data |
|---------------|------|----------|----------|-------------------------------------|-------------------|
| Linear Search | O(1) | O(n)     | O(n)     | O(1)                                | No                |
| Binary Search | O(1) | O(log n) | O(log n) | O(1) iterative / O(log n) recursive | Yes               |

**Sample result:** searching `[64, 34, 25, 12, 22, 11, 90]` for `22` finds it at index 4; binary search on the sorted list finds `25` at index 3. Linear search time grows with the list, while binary search stays almost flat.

## Practical 3: Heap Sort (Max-Heap)

**Notebook:** [Practical-3.ipynb](Practical-3.ipynb)

Implements `heapify`, bottom-up `build_max_heap`, and in-place `heap_sort`. Includes a **binary-tree visualization** of the array before and after heapify, and a comparison against Python's built-in `sorted()` (Timsort).

| Aspect        | Heap Sort      |
|---------------|----------------|
| Best / Average / Worst | O(n log n) |
| Build-heap cost | O(n)         |
| Space         | O(1) (in-place) |
| Stable        | No             |

**Sample result:** building a max-heap from `[4, 10, 3, 5, 1, 8, 9]` gives `[10, 5, 9, 4, 1, 8, 3]` (root is the maximum); `[12, 11, 13, 5, 6, 7]` sorts to `[5, 6, 7, 11, 12, 13]`.

## Practical 4: Factorial (Iterative vs Recursive)

**Notebook:** [Practical-4.ipynb](Practical-4.ipynb)

Computes `n!` with a loop and with recursion, checks that both agree for several values of `n`, and times them for `n` from 100 to 3,000.

| Method    | Time | Space | Stack-overflow risk | Speed                  |
|-----------|------|-------|---------------------|------------------------|
| Iterative | O(n) | O(1)  | No                  | Faster                 |
| Recursive | O(n) | O(n)  | Yes (large n)       | Slower (call overhead) |

**Sample result:** `10! = 3628800` from both methods. Both do the same `n` multiplications, but the recursive version is consistently slower because of function-call overhead.

## Practical 5: Knapsack Problem (Dynamic Programming)

**Notebook:** [Practical-5.ipynb](Practical-5.ipynb)

Solves the **0/1 Knapsack** problem three ways: naive recursion, 2D dynamic programming, and a space-optimized 1D DP. The 2D table is traced back to report **which items** were chosen.

| Approach               | Time   | Space  | Can recover chosen items? |
|------------------------|--------|--------|---------------------------|
| Naive recursion        | O(2ⁿ)  | O(n)   | With extra bookkeeping    |
| DP (2D table)          | O(n·W) | O(n·W) | Yes                       |
| DP (1D, optimized)     | O(n·W) | O(W)   | No (max value only)       |

**Sample result:** weights `[2, 3, 4, 5]`, values `[3, 4, 5, 6]`, capacity `5` gives a maximum value of **7**, taking items 0 and 1.

## Practical 6: Matrix Chain Multiplication (Dynamic Programming)

**Notebook:** [Practical-6.ipynb](Practical-6.ipynb)

Finds the order of multiplying a chain of matrices that minimizes scalar multiplications. Compares naive recursion with bottom-up DP, prints the DP cost table, and **reconstructs the optimal parenthesization**.

| Approach        | Time                       | Space |
|-----------------|----------------------------|-------|
| Naive recursion | O(4ⁿ / n^1.5), exponential | O(n)  |
| DP              | O(n³)                      | O(n²) |

**Sample result:** dimensions `[10, 20, 30, 40, 30]` (4 matrices) give a minimum cost of **30000** with the order `(((A1A2)A3)A4)`.

## Practical 7: Coin Change (Dynamic Programming)

**Notebook:** [Practical-7.ipynb](Practical-7.ipynb)

Solves both classic variants: the **minimum number of coins** and the **number of distinct ways** to make an amount. Each has a naive recursive and a DP version, and a log-scale chart shows the exponential vs polynomial gap.

| Approach  | Min Coins    | Counting Ways | Space     |
|-----------|--------------|---------------|-----------|
| Naive     | O(k^amount)  | O(2^amount)   | O(amount) |
| DP        | O(amount·k)  | O(amount·k)   | O(amount) |

**Sample result:** coins `[1, 2, 5]`, amount `11` need a minimum of **3 coins** and can be made in **11 distinct ways**. At amount 22 the naive version takes tens of milliseconds while DP stays in microseconds.

## Practical 8: Graph Traversal (DFS and BFS)

**Notebook:** [Practical-8.ipynb](Practical-8.ipynb)

A `Graph` class (adjacency list) with **DFS** (recursive and iterative) and **BFS**. Includes `networkx` visualizations of the traversal order, a **BFS shortest path** (fewest edges) bonus, and a runtime comparison on random graphs up to 20,000 nodes.

| Algorithm | Time     | Space | Data structure       | Shortest path (unweighted)? |
|-----------|----------|-------|----------------------|-----------------------------|
| DFS       | O(V + E) | O(V)  | Stack / recursion    | No                          |
| BFS       | O(V + E) | O(V)  | Queue                | Yes                         |

**Sample result:** on edges `A-B, A-C, B-D, C-D, D-E, E-F` from `A`, DFS visits `A, B, D, C, E, F` and BFS visits `A, B, C, D, E, F`. The shortest path from `A` to `F` is `A, B, D, E, F`.

## Practical 9: Prim's Algorithm (MST)

**Notebook:** [Practical-9.ipynb](Practical-9.ipynb)

Builds a **Minimum Spanning Tree** with Prim's algorithm, using both a **min-heap** and a simple **array scan**. Results are drawn with the MST highlighted, verified against `networkx`, and timed on sparse and dense random graphs.

| Implementation | Time       | Space    | Best for      |
|----------------|------------|----------|---------------|
| Min-heap       | O(E log V) | O(V + E) | Sparse graphs |
| Array scan     | O(V²)      | O(V)     | Dense graphs  |

**Sample result:** on the 5-vertex sample graph, Prim's from `A` picks `A-C, C-B, B-D, D-E` for a total MST weight of **8**. In the experiment, the heap version won on sparse graphs and the array version won on dense ones.

## Practical 10: Kruskal's Algorithm (MST)

**Notebook:** [Practical-10.ipynb](Practical-10.ipynb)

Finds the MST by sorting edges and adding each one that doesn't form a cycle, using a **Union-Find** (path compression + union by rank). Prints an accept/reject log for every edge, demonstrates a **minimum spanning forest** on a disconnected graph, and compares against heap-based Prim's.

| Algorithm | Time                    | Space    | Key structure                | Disconnected graphs?              |
|-----------|-------------------------|----------|------------------------------|-----------------------------------|
| Kruskal's | O(E log E) = O(E log V) | O(V + E) | Sorted edges + Union-Find    | Yes (minimum spanning forest)     |

**Sample result:** the same sample graph gives edges `B-C, B-D, D-E, A-C` with total weight **8**, matching Practical 9 and `networkx`. In this pure-Python experiment Kruskal's was faster than heap-based Prim's on both sparse and dense graphs; the textbook "Prim's for dense graphs" advice applies to the array-based version.

## Practical 11: Floyd-Warshall (All-Pairs Shortest Paths)

**Notebook:** [Practical-11.ipynb](Practical-11.ipynb)

Computes the shortest distance between **every pair of vertices** in a directed weighted graph. Uses a next-hop matrix to **reconstruct actual paths**, shows the matrix after each intermediate vertex, handles **negative edges**, and **detects negative cycles**. Includes a graph plus distance-matrix heatmap, verification against `networkx`, and a comparison with running Dijkstra from every vertex.

| Approach                   | Time          | Space  | Negative edges | Negative-cycle detection |
|----------------------------|---------------|--------|----------------|--------------------------|
| Floyd-Warshall             | O(V³)         | O(V²)  | Yes            | Yes                      |
| Dijkstra from every vertex | O(V·E log V)  | O(V²)  | No             | No                       |

**Sample result:** on the 4-vertex sample, the shortest `A` to `C` distance is **5** via `A → B → C`, and `A` to `D` is **6** via `A → B → C → D`. In the experiment, repeated Dijkstra was faster than Floyd-Warshall on both sparse and dense random graphs; Floyd-Warshall's advantages are its short implementation and support for negative edges.

## Practical 12: Travelling Salesman Problem (TSP)

**Notebook:** [Practical-12.ipynb](Practical-12.ipynb)

Finds the shortest tour that visits every city once and returns to the start (an **NP-hard** problem). Implements **brute force**, **Held-Karp dynamic programming**, the **Nearest Neighbor** heuristic, and **2-opt** improvement. Includes a map visualization of the tours and a study of how close the heuristics get to the optimum.

| Algorithm                | Time            | Space      | Optimal? | Practical limit (pure Python) |
|--------------------------|-----------------|------------|----------|-------------------------------|
| Brute force              | O(n!)           | O(n)       | Yes      | about 10 cities               |
| Held-Karp (DP)           | O(n²·2ⁿ)        | O(n·2ⁿ)    | Yes      | about 15-20 cities            |
| Nearest Neighbor         | O(n²)           | O(n)       | No       | thousands of cities           |
| Nearest Neighbor + 2-opt | O(n²) per pass  | O(n)       | No       | hundreds to thousands         |

**Sample result:** the classic 4-city matrix has an optimal tour of length **80** (`A → B → D → C → A`). Over 30 random 10-city instances, Nearest Neighbor averaged about **12%** above optimal, and adding 2-opt cut that to under **1%**.

---

## Complexity Cheat Sheet

| Problem | Naive / Basic | Better approach |
|---------|---------------|-----------------|
| Sorting | Bubble / Selection / Insertion: O(n²) | Merge / Heap: O(n log n); Quick: O(n log n) average |
| Searching | Linear: O(n) | Binary: O(log n) on sorted data |
| Factorial | Recursive: O(n) time, O(n) space | Iterative: O(n) time, O(1) space |
| Knapsack | Recursion: O(2ⁿ) | DP: O(n·W) |
| Matrix chain | Recursion: exponential | DP: O(n³) |
| Coin change | Recursion: exponential | DP: O(amount · k) |
| Graph traversal | | DFS / BFS: O(V + E) |
| Minimum spanning tree | | Prim: O(E log V); Kruskal: O(E log E) |
| All-pairs shortest paths | | Floyd-Warshall: O(V³) |
| TSP | Brute force: O(n!) | Held-Karp: O(n²·2ⁿ); heuristics: O(n²) |

## Notes on the Measurements

- Runtimes depend on the machine, so the saved timings are illustrative. The **trends** (for example, exponential vs polynomial growth) are what each notebook is designed to show.
- Several notebooks compare two methods on the same random data and assert that both return the same answer, so a speed difference never hides a correctness bug.
- Results that went against textbook expectations are reported as measured rather than smoothed over (for example, Kruskal's vs Prim's in Practical 10 and Floyd-Warshall vs Dijkstra in Practical 11).

## Repository Structure

```
.
├── README.md
├── Practical-1.ipynb    # Sorting algorithms
├── Practical-2.ipynb    # Linear and binary search
├── Practical-3.ipynb    # Heap sort (max-heap)
├── Practical-4.ipynb    # Factorial: iterative vs recursive
├── Practical-5.ipynb    # 0/1 knapsack (DP)
├── Practical-6.ipynb    # Matrix chain multiplication (DP)
├── Practical-7.ipynb    # Coin change (DP)
├── Practical-8.ipynb    # Graph traversal: DFS and BFS
├── Practical-9.ipynb    # Prim's algorithm
├── Practical-10.ipynb   # Kruskal's algorithm
├── Practical-11.ipynb   # Floyd-Warshall
└── Practical-12.ipynb   # Travelling salesman problem
```

## License

MIT
