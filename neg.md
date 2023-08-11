---
weight: 2
draft: false
---

# `NEG()`

<!--
Static method that returns the quadrille obtained from clearing the `quadrille` filled cells and filling its empty cells with `pattern`.
-->

Returns a new quadrille by clearing `q` filled cells, and filling `q` empty cells with `pattern` (any data type instance but `undefined` or `null`).

# Example

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

# Syntax

> `Quadrille.NEG(quadrille, pattern)`

# Parameters

| param     | description                                                                                                    |
|-----------|----------------------------------------------------------------------------------------------------------------|
| quadrille | Quadrille: quadrille to be negated                                                                             |
| pattern   | [p5.Image](https://p5js.org/reference/#/p5.Image) \| [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) \| [p5.Color](https://p5js.org/reference/#/p5.Color) \| array \| object \| string \| number |