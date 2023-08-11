---
weight: 4   
draft: false
---

# `XOR()`

<!--
Static method that returns the quadrille obtained from the *intersection* minus the *union* of the two given quadrilles.
-->

Returns a new quadrille `q3` which contains all the filled cells belonging to `q1` or `q2`, but not both.

# Example

(to move `q2` drag mouse or press **a**, **s**, **w**, **z** keys)

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="355" height="505" >}}
`use strict`;
const COLS = 11, ROWS = 16;
// q0 is defined as reference quadrille
let q0, q1, q2;
const col1 = 2, row1 = 3;
let col2 = 6, row2 = 3;
const col3 = 2, row3 = 10;

function setup() {
  Quadrille.CELL_LENGTH = 30;
  createCanvas(COLS * Quadrille.CELL_LENGTH, ROWS * Quadrille.CELL_LENGTH);
  q0 = createQuadrille(COLS, ROWS, COLS * ROWS, color('darkkhaki'));
  q1 = createQuadrille(2, 3, 4, '👻');
  q2 = createQuadrille(3, 2, 4, '✈️');
}

function draw() {
  drawQuadrille(q0, { outlineWeight: 0.5 });
  drawQuadrille(q1, { col: col1, row: row1, outline: 'yellow' });
  drawQuadrille(q2, { col: col2, row: row2, outline: 'magenta' });
  const q3 = Quadrille.XOR(q1, q2);
  drawQuadrille(q3, { col: col3, row: row3, outline: 'green' });
  text('(row2: ' + row2 + ', col2: ' + col2 + ')', 10, 25);
}

function mouseDragged() {
  row2 = q0.mouseRow;
  col2 = q0.mouseCol;
  return false; // prevent scrolling
}

function keyPressed() {
  row2 = key === 'w' ? row2 - 1 : key === 'z' ? row2 + 1 : row2;
  col2 = key === 'a' ? col2 - 1 : key === 's' ? col2 + 1 : col2;
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
const COLS = 11, ROWS = 16;
// q0 is defined as reference quadrille
let q0, q1, q2;
const col1 = 2, row1 = 3;
let col2 = 6, row2 = 3;
const col3 = 2, row3 = 10;

function setup() {
  Quadrille.CELL_LENGTH = 30;
  createCanvas(COLS * Quadrille.CELL_LENGTH, ROWS * Quadrille.CELL_LENGTH);
  q0 = createQuadrille(COLS, ROWS, COLS * ROWS, color('darkkhaki'));
  q1 = createQuadrille(2, 3, 4, '👻');
  q2 = createQuadrille(3, 2, 4, '✈️');
}

function draw() {
  drawQuadrille(q0, { outlineWeight: 0.5 });
  drawQuadrille(q1, { col: col1, row: row1, outline: 'yellow' });
  drawQuadrille(q2, { col: col2, row: row2, outline: 'magenta' });
  const q3 = Quadrille.XOR(q1, q2);
  drawQuadrille(q3, { col: col3, row: row3, outline: 'green' });
  text('(row2: ' + row2 + ', col2: ' + col2 + ')', 10, 25);
}

function mouseDragged() {
  row2 = q0.mouseRow;
  col2 = q0.mouseCol;
  return false; // prevent scrolling
}

function keyPressed() {
  row2 = key === 'w' ? row2 - 1 : key === 'z' ? row2 + 1 : row2;
  col2 = key === 'a' ? col2 - 1 : key === 's' ? col2 + 1 : col2;
}
```
{{< /details >}}

# Syntax

> `Quadrille.XOR(quadrille1, quadrille2, [row], [col])`

# Parameters

| param      | description                                                                                   |
|------------|-----------------------------------------------------------------------------------------------|
| quadrille1 | Quadrille: first quadrille                                                                    |
| quadrille2 | Quadrille: second quadrille                                                                   |
| row        | Number: `quadrille2` to `quadrille1` vertical displacement[^1]. Negative values are allowed   |
| col        | Number: `quadrille2` to `quadrille1` horizontal displacement[^1]. Negative values are allowed |

[^1]: Default `quadrille2` displacement respect to `quadrille1` is defined either as `col = col2 - col1` and `row = row2 - row1` if both `quadrille1` and `q2` are drawn, or as `0` otherwise.