# `OP()`

Static method that returns the quadrille obtained after applying the given logical operator between the two given quadrilles. This method is useful to implement the other _high-level_ logical operators. For instance the [AND](/docs/boolean_operators/and/) operator is implemented as follows:

```js | p5.quadrille.js
static AND(quadrille1, quadrille2, row, col) {
  return this.OP(quadrille1, quadrille2,
    (q1, q2) => {
      if (q1 && q2) {
        return q1;
      }
    },
    row, col);
}
```

# Syntax

> `Quadrille.OP(quadrille1, quadrille2, operator, [row], [col])`

# Parameters

| param      | description                                                                                   |
|------------|-----------------------------------------------------------------------------------------------|
| quadrille1 | Quadrille: first quadrille                                                                    |
| quadrille2 | Quadrille: second quadrille                                                                   |
| row        | Number: `quadrille2` to `quadrille1` vertical displacement[^1]. Negative values are allowed   |
| col        | Number: `quadrille2` to `quadrille1` horizontal displacement[^1]. Negative values are allowed |

[^1]: Default `quadrille2` displacement respect to `quadrille1` is defined either as `col = col2 - col1` and `row = row2 - row1` if both `quadrille1` and `q2` are drawn, or as `0` otherwise.