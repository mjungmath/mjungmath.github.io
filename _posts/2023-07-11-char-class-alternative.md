---
layout: post
title: "Alternative Algorithm for Characteristic Forms"
categories:
  - sagemanifolds
tags:
  - characteristic classes
  - sagemanifolds
  - mathematics
---

In this little article, I want to introduce a new approach that improves the implementation from my [master thesis](https://arxiv.org/abs/2006.13788).
The new approach has the following main advantages:

1. A tremendous speed-up especially in high dimensions.
2. More flexibility and robustness in terms of code maintanance.
3. The option to implement transgression forms.

## review and outline

Before, the algorithm has followed the Chern--Weil approach straightforwardly:

1. Compute the curvature matrix.
2. Insert the curvature matrix in an invariant polynomial (e.g. trace, determinant, Pfaffian) composed with an holomorphic function.

However, due to the composition with a holomorphic function, the computation of high powers of matrices over the algebra of mixed differential forms is necessary.
Hence, the computational cost swiftly scales with the base space's dimension and vector bundle's rank.
To avoid this kind of computation, the new approach uses *Chern roots* instead.
The idea goes as follows: we compute the *additive/multiplicative sequence* of a given polynomial, then we compute the Chern/Pontryagin form and insert it into the sequence.
This approach involves significantly less computations with mixed differential forms.

## Chern and Pontryagin forms

Let $$E \to M$$ be a vector bundle and $$\nabla$$ a connection on $$E$$.
Recall that the *Chern form* of $$\nabla$$ for complex vector bundles is given by

  $$c(E,\nabla) = \det\left(1 + \frac{\Omega^\nabla}{2 \pi \mathrm{i}}\right)$$

wheras the *Pontryagin form* of $$\nabla$$ for real vector bundles is obtained by

  $$p(E,\nabla) = \det\left(1 + \frac{\Omega^\nabla}{2 \pi}\right).$$

The *Euler form* on the other hand, is given by

  $$e(E,\nabla) = \mathrm{Pf}\left(\frac{\Omega^\nabla}{2 \pi}\right).$$

In all three cases, $$\Omega^\nabla$$ denotes the curvature form matrix associated to $$\nabla$$.
The computation does not involve powers of $$\Omega^\nabla$$.
This is beneficial for the computational intensity.

To compute these forms, we use the [Faddeev-LeVerrier algorithm](https://en.wikipedia.org/wiki/Faddeev–LeVerrier_algorithm).
The advantage of this algorithm is that it can be used for differential forms as it only invovles division by integers, and it is comparibly fast.
For the Euler form, we use a variation that has been developed by Baer [1].

## multiplicative sequences

Let $$f(x)$$ be a polynomial in $$x$$.
Consider the invariant polynomial $$P\colon \mathrm{Mat}(n \times n, \mathbb{C}) \to \mathbb{C}$$ with

  $$P(X) = \det\left(f(X)\right)$$

for any $$X \in \mathrm{Mat}(n \times n)$$.
Now, we want to express $$P$$ in terms of [*elementary symmetric functions*](https://en.wikipedia.org/wiki/Elementary_symmetric_polynomial).
Let $$(x_1, \ldots, x_n)$$ be the eigenvalues of $$X$$ including multiplicities.
Then we have

  $$P(X) = \prod^n_{k=1} f(x_i)$$

and evidently obtain that this is a symmetric polynomial in the $$x_i$$.
Due to the fundamental theorem of elementary symmetric functions, we can write $$P$$ as a polynomial in the elementary symmetric functions $$e_i$$:

  $$P = Q(e_1, \ldots e_n).$$

The proof of this theorem comes with an algorithm; see [2].
Fortunately, the computation with symmetric polynomials is already realized in Sage via the [`SymmetricFunctions`](http://doc.sagemath.org/html/en/reference/combinat/sage/combinat/sf/sfa.html) class using the backend [Symmetrica](http://www.algorithm.uni-bayreuth.de/en/research/SYMMETRICA/) written in C.
That is perfect for our purposes.

**Note:** For the particular polynomial $$P$$, one can do even better. See [3] for details.
However, the computational cost is, in any case, negligible compared to computations with mixed differential forms in high dimensions.

Notice that the $$i$$-th homogeneous component of the Chern/Pontryagin class represents the $$i$$-th elementary symmetric function by definition.[^1]
This link becomes clear when we take a closer look at the defining equation of the elementary symmetric functions:

  $$\det(1+t X) = \sum^n_{i=0} t^i\,e_i(X).$$

Thus, when we insert the homogeneous components of the Chern/Pontryagin class into the polynomial $$Q$$, then we obtain the multiplicative characteristic class associated to $$f(x)$$.

Of course, we can proceed similarly for additive classes: we simply replace the determinant by the trace and the product by a sum.

## summary

The concrete proceeding goes as follows now:

1. Compute the additive/multiplicative sequence of the function associated to the class using `SymmetricFunctions`.
2. Compute the Chern or Pontryagin form with Faddeev-LeVerrier.
3. Insert the homogeneous components of the Chern/Pontryagin form into the additive/multiplicative sequence.

The new algorithm is available since SageMath 9.5 and comes with more features:

* Rudimentary de Rham cohomology.
* Decoupling of characteristic forms and characteristic cohomology classes.
* Characteristic cohomology classes as subring of de Rham cohomology ring.
* Euler form of manifold with metric and orientation is computed automatically.

See [Sage 9.5 Release Tour](https://wiki.sagemath.org/ReleaseTours/sage-9.5#De_Rham_cohomology_and_characteristic_classes) for details.

## references

[1] Christian Baer --- [*The Faddeev-LeVerrier algorithm and the Pfaffian*](https://doi.org/10.1016/j.laa.2021.07.023). In: Linear Algebra and its Applications 630 (2021), 39-55.

[2] Ben Blum-Smith and Samuel Coskey --- [*The Fundamental Theorem on Symmetric Polynomials: History's First Whiff of Galois Theory*](https://doi.org/10.4169/college.math.j.48.1.18). In: College mathematics journal 48(1):18-29, 2017.

[3] Oleksandr Iena --- [*On Symbolic Computations with Chern Classes*](https://orbilu.uni.lu/bitstream/10993/21949/2/ChernLib.pdf). 2016.

[4] H. Blaine Lawson and Marie-Louise Michelsohn --- *Spin Geometry*. 1989.

[^1]: Notice that the real case needs special care. See [4, 225 ff.] for details.
