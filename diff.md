---
weight: 6
draft: false
---

# `diff()`

Returns a new quadrille which contains all the filled cells belonging to `quadrille1` but not to `quadrille2`.

# Example

(to move `quadrille2` drag mouse or press **a**, **s**, **w**, **z** keys)

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="355" height="505" >}}
`use strict`;
const COLS = 11, ROWS = 16;
// quadrille0 is defined as reference quadrille
let quadrille0, quadrille1, quadrille2;
const col1 = 2, row1 = 3;
let col2 = 6, row2 = 3;
const col3 = 2, row3 = 10;

function setup() {
  Quadrille.cellLength = 30;
  createCanvas(COLS * Quadrille.cellLength, ROWS * Quadrille.cellLength);
  quadrille0 = createQuadrille(COLS, ROWS, COLS * ROWS, color('darkkhaki'));
  quadrille1 = createQuadrille(2, 3, 4, '👻');
  quadrille2 = createQuadrille(3, 2, 4, '✈️');
}

function draw() {
  drawQuadrille(quadrille0, { outlineWeight: 0.5 });
  drawQuadrille(quadrille1, { col: col1, row: row1, outline: 'yellow' });
  drawQuadrille(quadrille2, { col: col2, row: row2, outline: 'magenta' });
  const quadrille3 = Quadrille.diff(quadrille1, quadrille2);
  drawQuadrille(quadrille3, { col: col3, row: row3, outline: 'green' });
  text('(row2: ' + row2 + ', col2: ' + col2 + ')', 10, 25);
}

function mouseDragged() {
  row2 = quadrille0.mouseRow;
  col2 = quadrille0.mouseCol;
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
// quadrille0 is defined as reference quadrille
let quadrille0, quadrille1, quadrille2;
const col1 = 2, row1 = 3;
let col2 = 6, row2 = 3;
const col3 = 2, row3 = 10;

function setup() {
  Quadrille.cellLength = 30;
  createCanvas(COLS * Quadrille.cellLength, ROWS * Quadrille.cellLength);
  quadrille0 = createQuadrille(COLS, ROWS, COLS * ROWS, color('darkkhaki'));
  quadrille1 = createQuadrille(2, 3, 4, '👻');
  quadrille2 = createQuadrille(3, 2, 4, '✈️');
}

function draw() {
  drawQuadrille(quadrille0, { outlineWeight: 0.5 });
  drawQuadrille(quadrille1, { col: col1, row: row1, outline: 'yellow' });
  drawQuadrille(quadrille2, { col: col2, row: row2, outline: 'magenta' });
  const quadrille3 = Quadrille.diff(quadrille1, quadrille2);
  drawQuadrille(quadrille3, { col: col3, row: row3, outline: 'green' });
  text('(row2: ' + row2 + ', col2: ' + col2 + ')', 10, 25);
}

function mouseDragged() {
  row2 = quadrille0.mouseRow;
  col2 = quadrille0.mouseCol;
  return false; // prevent scrolling
}

function keyPressed() {
  row2 = key === 'w' ? row2 - 1 : key === 'z' ? row2 + 1 : row2;
  col2 = key === 'a' ? col2 - 1 : key === 's' ? col2 + 1 : col2;
}
```
{{< /details >}}

# Syntax

> `Quadrille.diff(quadrille1, quadrille2, [row], [col])`

# Parameters

| param      | description                                                                                   |
|------------|-----------------------------------------------------------------------------------------------|
| quadrille1 | Quadrille: first quadrille                                                                    |
| quadrille2 | Quadrille: second quadrille                                                                   |
| row        | Number: `quadrille2` to `quadrille1` vertical displacement[^1]. Negative values are allowed   |
| col        | Number: `quadrille2` to `quadrille1` horizontal displacement[^2]. Negative values are allowed |

[^1]: Default is `row2 - row1` if both `quadrille1` and `quadrille2` are drawn, or `0` otherwise.
[^2]: Default is `col2 - col1` if both `quadrille1` and `quadrille2` are drawn, or `0` otherwise.