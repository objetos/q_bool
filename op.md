# `OP()`

Static method that returns the quadrille obtained after applying the given logical operator between the two given quadrilles. This method is useful to implement the other _high-level_ logical operators. For instance the [AND]({{< relref "and" >}}) operator is [implemented](https://github.com/objetos/p5.quadrille.js/blob/main/p5.quadrille.js#L41) as follows:

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
| col        | Number: `quadrille2` to `quadrille1` horizontal displacement[^2]. Negative values are allowed |

[^1]: Default is `row2 - row1` if both `quadrille1` and `quadrille2` are drawn, or `0` otherwise.
[^2]: Default is `col2 - col1` if both `quadrille1` and `quadrille2` are drawn, or `0` otherwise.