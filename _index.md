---
bookCollapseSection: true
weight: 6
draft: false
---

# boolean operators

The [static](https://developer.mozilla.org/en-US/docs/Glossary/Static_method) boolean operators `NEG`, `OR`, `XOR`  `AND` and `DIFF` allows a programmer to create a complex quadrille by combining simpler ones.

## Quadrille.NEG(q, pattern)

Returns a new quadrille by clearing `q` filled cells, and filling `q` empty cells with `pattern` (any data type instance but `undefined` or `null`).

(click on the canvas and press any key)

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="325" height="265" >}}
`use strict`;
Quadrille.CELL_LENGTH = 60;
let q;
let west;

function setup() {
  createCanvas(300, 240);
  q = createQuadrille(5, 4, 8, '🌏');
}

function draw() {
  background('purple');
  drawQuadrille(q);
}

function mouseClicked() {
  west = !west;
  q = Quadrille.NEG(q, west ? '🌎' : '🌏');
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.CELL_LENGTH = 60;
let q;
let west;

function setup() {
  createCanvas(300, 240);
  q = createQuadrille(5, 4, 8, '🌏');
}

function draw() {
  background('purple');
  drawQuadrille(q);
}

function keyPressed() {
  west = !west;
  q = Quadrille.NEG(q, west ? '🌎' : '🌏');
}
```
{{< /details >}}

## Quadrille.OR(q1, q2)

Returns a new quadrille `q3` which contains all the filled cells belonging to `q1`, `q2`, or both (`q1` cells take higher precedence).

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
  const q3 = Quadrille.OR(q1, q2);
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
  const q3 = Quadrille.OR(q1, q2);
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

## Quadrille.XOR(q1, q2)

Returns a new quadrille `q3` which contains all the filled cells belonging to `q1` or `q2`, but not both.

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

## Quadrille.AND(q1, q2)

Returns a new quadrille `q3` which contains all the filled cells belonging to `q1` and `q2` (`q1` cells take higher precedence).

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
  const q3 = Quadrille.AND(q1, q2);
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
  const q3 = Quadrille.AND(q1, q2);
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

## Quadrille.DIFF(q1, q2)

Returns a new quadrille `q3` which contains all the filled cells belonging to `q1` but not to `q2`.

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
  const q3 = Quadrille.DIFF(q1, q2);
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
  const q3 = Quadrille.DIFF(q1, q2);
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