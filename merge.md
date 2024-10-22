---
weight: 1
draft: false
title: merge()
---

Static method that computes a new quadrille by applying a specified logical `operator` to each corresponding cell of two given quadrilles. It serves as a basis for implementing higher-level logical operations. For instance, the [and]({{< relref "and" >}}) operator is implemented using `merge` as:

```js
static and(quadrille1, quadrille2, row, col) {
  return this.merge(quadrille1, quadrille2,
    (q1, q2) => q1 && q2 ? q1 : null,
    row, col);
}
```

# Syntax

> `Quadrille.merge(quadrille1, quadrille2, operator, [row], [col])`

# Parameters

| param      | description                                                                                                   |
|------------|---------------------------------------------------------------------------------------------------------------|
| quadrille1 | Quadrille: first quadrille to merge                                                                           |
| quadrille2 | Quadrille: second quadrille to merge                                                                          |
| operator   | Function: A function that defines the logical operation for merging                                           |
| row        | Number: The vertical displacement of `quadrille2` relative to `quadrille1`[^1]. Negative values are allowed   |
| col        | Number: The horizontal displacement of `quadrille2` relative to `quadrille1`[^2]. Negative values are allowed |

[^1]: Default is `row2 - row1` if both `quadrille1` and `quadrille2` are drawn, or `0` otherwise.
[^2]: Default is `col2 - col1` if both `quadrille1` and `quadrille2` are drawn, or `0` otherwise.