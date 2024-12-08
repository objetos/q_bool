---
bookCollapseSection: true  
weight: 6  
draft: false  
title: Algebra  
---

The **quadrille algebra** provides a suite of [static methods](https://developer.mozilla.org/en-US/docs/Glossary/Static_method) for applying logical operations to `quadrille` instances. Inspired by [constructive solid geometry](https://en.wikipedia.org/wiki/Constructive_solid_geometry) and [boolean algebra](https://en.wikipedia.org/wiki/Boolean_algebra), these methods combine and manipulate quadrilles, leading to **new quadrilles** as an aggregation of others.  

TODO add sketch showing superimposition concept.

## Method Overview  

- **[neg]({{< relref "neg" >}}):** Performs a logical **NOT** operation, inverting empty and non-empty cells, filling empty cells with a provided value.  
- **[or]({{< relref "or" >}}):** Combines two quadrilles using a logical **OR**, merging their non-empty cells into a new quadrille.  
- **[xor]({{< relref "xor" >}}):** Returns a new quadrille containing all the non-empty cells that appear in either `q1` or `q2` but not in both.  
- **[and]({{< relref "and" >}}):** Returns a new quadrille containing only the cells that are non-empty in both `q1` and `q2`.  
- **[diff]({{< relref "diff" >}}):** Returns a new quadrille containing the non-empty cells from `q1` that do not appear in `q2`.  

These algebraic methods offer powerful tools for composing quadrilles, enabling the construction of intricate patterns, designs, or logical transformations. Whether you're combining shapes, masking cells, or creating dynamic compositions, the quadrille algebra brings structure and precision to your work.