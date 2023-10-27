---
weight: 2
draft: false
---

# `neg()`

Returns a new quadrille by clearing `q` filled cells, and filling `q` empty cells with `value` (any data type instance but `undefined`).

# Example

(click on the canvas and press any key)

{{< p5-global-iframe lib1="/p5.quadrille.js/docs/libs/p5.quadrille.js" width="325" height="265" >}}
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
  q = Quadrille.neg(q, west ? '🌎' : '🌏');
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
  q = Quadrille.neg(q, west ? '🌎' : '🌏');
}
```
{{< /details >}}

# Syntax

> `Quadrille.neg(quadrille, value)`

# Parameters

| param     | description                                                                                                    |
|-----------|----------------------------------------------------------------------------------------------------------------|
| quadrille | Quadrille: quadrille to be negated                                                                             |
| value     | [p5.Image](https://p5js.org/reference/#/p5.Image) \| [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) \| [p5.Color](https://p5js.org/reference/#/p5.Color) \| array \| object \| string \| number \| `null`: empty cells |