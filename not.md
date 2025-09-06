---
weight: 1
draft: false
title: not(q, value)
---

Returns a new quadrille by clearing `q` quadrille filled cells, and filling its empty cells with `value` (any data type instance but `undefined`).

{{< callout type="info" >}}
For a **destructive instance version**, call `q.not(value)`.
{{< /callout >}}

## Example

(click on the canvas and press any key)

{{< p5-global-iframe quadrille="true" width="325" height="265" >}}
'use strict';
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
  q = Quadrille.not(q, west ? '🌎' : '🌏');
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
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
  q = Quadrille.not(q, west ? '🌎' : '🌏');
}
```
{{% /details %}}

## Syntax

> `Quadrille.not(quadrille, value)`

## Parameters

| Param   | Description                                                                  |
|---------|------------------------------------------------------------------------------|
| `q`     | Quadrille: the quadrille to negate (clear filled cells and fill empty cells) |
| `value` | Any: the value used to fill empty cells                                      |