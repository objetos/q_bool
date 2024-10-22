---
weight: 2
draft: false
title: neg()
---

Returns a new quadrille by clearing `q` filled cells, and filling `q` empty cells with `value` (any data type instance but `undefined`).

# Example

(click on the canvas and press any key)

{{< p5-global-iframe quadrille="true" width="325" height="265" >}}
`use strict`;
Quadrille.cellLength = 60;
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
Quadrille.cellLength = 60;
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

| param      | description                                                                                                   |
|------------|---------------------------------------------------------------------------------------------------------------|
| quadrille1 | Quadrille: first quadrille to merge                                                                           |
| quadrille2 | Quadrille: second quadrille to merge                                                                          |
| row        | Number: The vertical displacement of `quadrille2` relative to `quadrille1`[^1]. Negative values are allowed   |
| col        | Number: The horizontal displacement of `quadrille2` relative to `quadrille1`[^2]. Negative values are allowed |

[^1]: Default is `row2 - row1` if both `quadrille1` and `quadrille2` are drawn, or `0` otherwise.
[^2]: Default is `col2 - col1` if both `quadrille1` and `quadrille2` are drawn, or `0` otherwise.