---
weight: 1
draft: false
title: merge(q1, q2, operator, row, col)
---

Static method that computes a new quadrille by applying a specified logical `operator` to each corresponding cell of two given quadrilles. This method serves as the foundation for higher-level logical operations, such as [or]({{< ref "or" >}}), [xor]({{< ref "xor" >}}), [and]({{< ref "and" >}}), and [diff]({{< ref "diff" >}}).

## Example 1: `and` operator

The `merge` method can be used to create higher-level logical operations. For instance, the [and(q1, q2, row, col)]({{< ref "and" >}}) operation between two quadrilles can be implemented using `merge` to return a cell value only when both corresponding cells in `q1` and `q2` are non-empty.

```js
static and(q1, q2, row, col) {
  return this.merge(q1, q2,
    (cell1, cell2) => cell1 && cell2 ? cell1 : null, row, col);
}
```

In this example, the `and` function checks each cell of `q1` and `q2`. If both cells are non-empty (i.e., non `null`), the result will contain the cell value from `q1`. If either cell is empty (i.e., `null`), the merged cell will also be empty.

## Example 1: `null` operator

This example implements the `null` operator (`() => null`), which produces a new quadrille with all empty cells. It demonstrates that the dimensions of the resulting quadrille span the minimum area required to cover both `q1` and `q2`.

(to move `q2` drag mouse or press **a**, **s**, **w**, **z** keys)

{{< p5-global-iframe quadrille="true" width="475" height="325" >}}
'use strict';

const COLS = 15, ROWS = 10;
// q0 is defined as reference quadrille
let q0, q1, q2;
const col1 = 3, row1 = 4;
let col2 = 9, row2 = 3;
Quadrille.outlineWeight = 3;
Quadrille.cellLength = 30;

function setup() {
  createCanvas(COLS * Quadrille.cellLength, ROWS * Quadrille.cellLength);
  q0 = createQuadrille(COLS, ROWS, COLS * ROWS, color('darkkhaki'));
  q1 = createQuadrille(2, 3, 4, '👻');
  q2 = createQuadrille(3, 2, 4, '✈️');
}

function draw() {
  drawQuadrille(q0, { outlineWeight: 0.5 });
  drawQuadrille(q1, { col: col1, row: row1, outline: 'yellow' });
  drawQuadrille(q2, { col: col2, row: row2, outline: 'magenta' });
  const q3 = Quadrille.merge(q1, q2, () => null);
  q3.fill(color(255, 0, 255, 35)); // Fill q3 with semi-transparent magenta
  drawQuadrille(q3, { col: min(col1, col2), row: min(row1, row2),
                      outline: 'green', outlineWeight: 1 });
  text('(row2: ' + row2 + ', col2: ' + col2 + ')', 10, 25);
}

function mouseDragged() {
  row2 = q0.mouseRow;
  col2 = q0.mouseCol;
  return false; // Prevent scrolling
}

function keyPressed() {
  row2 = key === 'w' ? row2 - 1 : key === 'z' ? row2 + 1 : row2;
  col2 = key === 'a' ? col2 - 1 : key === 's' ? col2 + 1 : col2;
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
const COLS = 15, ROWS = 10;
// q0 is defined as reference quadrille
let q0, q1, q2;
const col1 = 3, row1 = 4;
let col2 = 9, row2 = 3;
Quadrille.outlineWeight = 3;
Quadrille.cellLength = 30;

function setup() {
  createCanvas(COLS * Quadrille.cellLength, ROWS * Quadrille.cellLength);
  q0 = createQuadrille(COLS, ROWS, COLS * ROWS, color('darkkhaki'));
  q1 = createQuadrille(2, 3, 4, '👻');
  q2 = createQuadrille(3, 2, 4, '✈️');
}

function draw() {
  drawQuadrille(q0, { outlineWeight: 0.5 });
  drawQuadrille(q1, { col: col1, row: row1, outline: 'yellow' });
  drawQuadrille(q2, { col: col2, row: row2, outline: 'magenta' });
  const q3 = Quadrille.merge(q1, q2, () => null);
  q3.fill(color(255, 0, 255, 35)); // Fill q3 with semi-transparent magenta
  drawQuadrille(q3, { col: min(col1, col2), row: min(row1, row2),
                      outline: 'green', outlineWeight: 1 });
  text('(row2: ' + row2 + ', col2: ' + col2 + ')', 10, 25);
}

function mouseDragged() {
  row2 = q0.mouseRow;
  col2 = q0.mouseCol;
  return false; // Prevent scrolling
}

function keyPressed() {
  row2 = key === 'w' ? row2 - 1 : key === 'z' ? row2 + 1 : row2;
  col2 = key === 'a' ? col2 - 1 : key === 's' ? col2 + 1 : col2;
}
```
{{< /details >}}

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