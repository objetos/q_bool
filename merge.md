---
weight: 1
draft: false
title: merge(...args)
---

Static method that computes a new quadrille by applying a specified logical `operator` to each corresponding cell of two given quadrilles. It serves as a basis for implementing higher-level logical operations. For instance, the [and]({{< relref "and" >}}) operator is implemented using `merge` as:

```js
static and(q1, q2, row, col) {
  return this.merge(q1, q2,
    (cell1, cell2) => cell1 && cell2 ? cell1 : null,
    row, col);
}
```

# Syntax

> `Quadrille.merge(q1, q2, operator, [row], [col])`

# Parameters

| param    | description                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| q1       | Quadrille: first quadrille to merge                                                           |
| q2       | Quadrille: second quadrille to merge                                                          |
| operator | Function: A function that defines the logical operation for merging                           |
| row      | Number: The vertical displacement of `q2` relative to `q1`[^1]. Negative values are allowed   |
| col      | Number: The horizontal displacement of `q2` relative to `q1`[^2]. Negative values are allowed |

[^1]: Default is `row2 - row1` if both `q1` and `q2` are drawn, or `0` otherwise.
[^2]: Default is `col2 - col1` if both `q1` and `q2` are drawn, or `0` otherwise.