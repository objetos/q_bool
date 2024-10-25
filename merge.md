---
weight: 1
draft: false
title: merge(...args)
---

Static method that computes a new quadrille by applying a specified logical `operator` to each corresponding cell of two given quadrilles. It serves as a basis for implementing higher-level logical operations.

## Example

The `merge` method can be used to create higher-level logical operations. For instance, the [and(q1, q2, row, col)]({{< ref "and" >}}) operation between two quadrilles can be implemented using `merge` to return a cell value only when both corresponding cells in `q1` and `q2` are non-empty.

```js
static and(q1, q2, row, col) {
  return this.merge(q1, q2,
    (cell1, cell2) => cell1 && cell2 ? cell1 : null,
    row, col);
}
```

In this example, the `and` function checks each cell of `q1` and `q2`. If both cells are non-empty (i.e., non `null`), the result will contain the cell value from `q1`. If either cell is empty (i.e., `null`), the merged cell will also be empty.

## Syntax

> `Quadrille.merge(q1, q2, operator, [row], [col])`

## Parameters

| param    | description                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| q1       | Quadrille: The first quadrille to merge                                                       |
| q2       | Quadrille: The second quadrille to merge                                                      |
| operator | Function: A function defining the logical operation for merging                               |
| row      | Number: The vertical displacement of `q2` relative to `q1`. Negative values are allowed[^1].  |
| col      | Number: The horizontal displacement of `q2` relative to `q1`. Negative values are allowed[^2].|

[^1]: Default is `row2 - row1` if both `q1` and `q2` are drawn, or `0` otherwise.
[^2]: Default is `col2 - col1` if both `q1` and `q2` are drawn, or `0` otherwise.
```