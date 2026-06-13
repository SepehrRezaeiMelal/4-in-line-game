# 4-in-line-game
# Artificial Intelligence — Final Project

**Instructor:** Dr. Barshban
**University of Guilan** — Academic year 1400, Semester 1 (Fall 2021)

---

## Project Description

In class, you have already become familiar with the **minimax** algorithm for board games. In short, this algorithm takes the **minimum** of the child-node values at one level, and at the next level takes the **maximum** of those values as the parent node's value. You also learned about **alpha** and **beta** pruning for this tree.

The **4-in-line** game is similar to tic-tac-toe. In this game (shown below), a board is placed vertically, and at each turn you can drop your piece into one of the **eight columns**. The piece falls down that column until it lands on another piece. The first player to line up **four pieces in a row wins** the game — just like tic-tac-toe, the four pieces can be aligned **horizontally, vertically, or diagonally**.

*(See the game board image in the original document.)*

---

## Why Negamax Instead of Minimax

The minimax algorithm is a teaching tool for understanding the underlying concept, but it comes with difficulties in practical implementation. For example, at every level you have to check whether the current step is a **maximizing** step or a **minimizing** step. Likewise, applying alpha-beta pruning to this tree is awkward. For these reasons, you are asked to work with the alternative algorithm, **negamax**.

### 1. The core idea

In this algorithm, at each level the values of all child nodes are **multiplied by −1**, and then their **maximum** is taken as the parent node's value. Note that taking the maximum over negated values is equivalent to taking the minimum, and at the next level, negating numbers that were already negated once results in a maximization again.

### 2. Alpha-beta pruning in negamax

Alpha-beta pruning is implemented as follows:

**a)** For each node we consider two numbers `(a, b)`. Whenever a node's value drops **below `a`** or rises **above `b`**, all of its siblings are pruned and are not evaluated; the value of the node that fell outside this range is multiplied by −1 and set as the parent node's value.

**b)** For the main node — the **root** — these two numbers are initialized to `(−∞, +∞)`.

**c)** If a parent node has bounds `(a, b)`, its **first child** will have bounds `(−b, −a)`. In effect, the allowed range is multiplied by −1.

**d)** For every child **other than the first**, the value of its **left sibling** is computed first. If that value is `d`, then this child's bounds become `(−b, d)`.

### Negamax pseudocode

```
function negamax(node, depth, α, β, color) is
    if depth = 0 or node is a terminal node then
        return color × the heuristic value of node

    childNodes := generateMoves(node)
    childNodes := orderMoves(childNodes)
    value := −∞
    foreach child in childNodes do
        value := max(value, −negamax(child, depth − 1, −β, −α, −color))
        α := max(α, value)
        if α ≥ β then
            break    (* cut-off *)
    return value
```

---

## Running the Game

For more background on this game, see: **4-in-line**.

When the program runs, the game board is displayed, and the user and the program take turns playing. The board must clearly indicate **whose turn it is**. The user must be able to **select one of the columns** so that their piece drops into that column. When one of the players wins, the **result must be shown**, and there must be an option to **restart the game**.

---

## Additional Requirements

- Using **alpha-beta pruning** in the implementation is **mandatory**.
- Supplementary use of other algorithms taught in the course earns **bonus marks**.
- The user interface may be **console-based or graphical**. Implementing the project with a **graphical user interface earns bonus marks**.
- The project may be implemented in **Java or Python**.
- **Any copying is considered cheating.** The project will also include a **delivery/defense session**, and **all group members must fully understand the project**.
- Project groups may consist of **at most three people**.

---

*AI Course Teaching Assistants:*
*Seyyedeh Fatemeh Ahmadi, Gita Shojaei, Shakiba Ehteshami*
