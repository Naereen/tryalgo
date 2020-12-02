---
layout: en
title: "SymPy vs. SageMath: symbolic computation and automatic differentiation in Python"
category: arithmetics
author: Jill-Jênn Vie
---

## Get Started

    python3 -m venv venv
    . venv/bin/activate  # Load a virtualenv (optional)

But if you don't need a virtualenv, you can directly do:

    pip install sympy
    python
    >>> from sympy import Symbol, log, exp, pprint
    >>> u = sympy.Symbol('u')
    >>> v = sympy.Symbol('v')
    >>> x = sympy.Symbol('x')
    >>> f = x * v * u - log(1 + exp(v * u))
    >>> f.diff(u)  # df/du
    v*x - v*exp(u*v)/(exp(u*v) + 1)
    >>> pprint(f.diff(u))
              u⋅v 
           v⋅ℯ    
    v⋅x - ────────
           u⋅v    
          ℯ    + 1
    >>> pprint(f.diff(u).diff(u))  # d2f/du2
       2  u⋅v      2  2⋅u⋅v 
      v ⋅ℯ        v ⋅ℯ      
    - ──────── + ───────────
       u⋅v                 2
      ℯ    + 1   ⎛ u⋅v    ⎞ 
                 ⎝ℯ    + 1⎠ 

So if $f = xv^T u - \log(1 + \exp(v^T u))$,

$$ \frac{\partial^2 f}{ {\partial u}^2 } = \left[\frac{\exp u^T v}{1 + \exp u^T v} + \frac{\exp 2 u^T v}{ {(1 + \exp u^T v)}^2}\right] v v^T. $$

(Yes. We cheated.)

## Automatic differentiation

- [What automatic differentiation looks like](https://en.wikipedia.org/wiki/Automatic_differentiation).
- [TensorFlow does it](https://stackoverflow.com/a/36373220/827989) for computing gradients automatically.

## Symbolic computation

![SymPy vs. SageMath](/static/sympy-sagemath.png)

[Differences between SymPy and SageMath on sympy's wiki](https://github.com/sympy/sympy/wiki/SymPy-vs.-Sage)

## SymPy

[Try SymPy in your browser](http://docs.sympy.org/latest/tutorial/intro.html#a-more-interesting-example) (live shell on every page, wow!).

    pip install sympy

- [Someone doing approximate matrix differentiation with SymPy](https://zulko.wordpress.com/2012/04/15/symbolic-matrix-differentiation-with-sympy/) (by propagating his own rules recursively on the expression tree)
- [Derivatives by array](http://docs.sympy.org/latest/modules/tensor/array.html#derivatives-by-array): it can derivate by vector, do a symbolic differentiation (as long as you name the parameters).
- [Common Subexpression Detection and Collection](http://docs.sympy.org/latest/modules/rewriting.html#module-sympy.simplify.cse_main), it's actually [a nice problem](https://en.wikipedia.org/wiki/Common_subexpression_elimination)
- [Output into TensorFlow format](http://docs.sympy.org/latest/modules/utilities/lambdify.html#sympy.utilities.lambdify.lambdify)
- [Tests for differentiation with tensors](https://github.com/sympy/sympy/blob/49649c2bd0488840fe1cb47184e35b0fb42c7098/sympy/tensor/tests/test_indexed.py) (GitHub)

See [this interesting Jupyter notebook](https://github.com/jilljenn/tryalgo.org/blob/master/_notebooks/SymPy%20Demo.ipynb)!

### SymPy vs. SageMath

SymPy can do better symbolic differentiation than SageMath (ex. [derivatives by array](http://docs.sympy.org/latest/modules/tensor/array.html#derivatives-by-array)). It has [**symbolic matrices**](http://docs.sympy.org/latest/modules/matrices/expressions.html), unlike SageMath. But SageMath has [many more libraries](http://doc.sagemath.org/html/en/reference/combinat/module_list.html), and may be better at factoring expressions, I guess.

### The Matrix Cookbook

What none of these libraries cannot do though, is **symbolic matrix differentiation**. But it is an [ongoing issue on their GitHub](https://github.com/sympy/sympy/issues/5858).

It made me learn the existence of [The Matrix Cookbook](http://www2.imm.dtu.dk/pubdb/views/edoc_download.php/3274/pdf/imm3274.pdf), which is a great reference!!

## SageMath

[Try it on CoCalc](https://cocalc.com) (formerly SageMathCloud).

You can [download this SageMath worksheet (logreg.sagews)](https://github.com/jilljenn/tryalgo.org/tree/master/_notebooks) to load it there.

- [Many tools](http://doc.sagemath.org/html/en/reference/combinat/module_list.html) about block design in combinatorics, Galois fields, etc.
- Really used by cryptographers.
- See the [extensive documentation](http://doc.sagemath.org/html/en/reference/index.html)

Also: [Suffix trees and arrays?!](http://doc.sagemath.org/html/en/reference/combinat/sage/combinat/words/suffix_trees.html)

## But…

But unlike Wolfram Alpha, they cannot output a [Pikachu curve](https://www.wolframalpha.com/input/?i=pikachu+curve) :/

<blockquote class="twitter-tweet" data-lang="fr"><p lang="de" dir="ltr">Type pikachu curve in Wolfram Alpha: <a href="https://t.co/axW9M3b9nv">https://t.co/axW9M3b9nv</a> <a href="https://twitter.com/hashtag/Pok%C3%A9mon?src=hash">#Pokémon</a> <a href="https://t.co/BJrG4U5qx4">pic.twitter.com/BJrG4U5qx4</a></p>&mdash; Jill-Jênn Vie (@jjvie) <a href="https://twitter.com/jjvie/status/885408471998320640">13 juillet 2017</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
