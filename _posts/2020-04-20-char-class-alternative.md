---
title: "Alternative Algorithm for Characteristic Forms"
categories:
  - SageManifolds
tags:
  - characteristic classes
  - sagemanifolds
  - mathematics
last_modified_at: 2020-04-21 21:14:00 +2
---

**Note:** If you are not familiar with my previous work, take a peek at my [master's thesis]({% link assets/files/masters_thesis.pdf %}). A *very* short review is coming soon.
{: .notice--warning}

Today, I want to introduce a slightly different algorithm, that I currently working on, to implement the computation of characteristic forms. This new approach aims for two purposes:

1. I anticipate to gain a speed-up especially in high dimensions.
2. I want to understand transgression forms even better and hope to lay foundations for them.

## Review and Outline

So far, the algorithm follows the Chern--Weil approach straightforwardly:

1. Compute the curvature matrix.
2. Insert the curvature matrix in an invariant polynomial (e.g. trace, determinant, Pfaffian) composed with an holomorphic function.

However, due to the composition with the holomorphic function, the computation of high powers of matrices over the algebra of mixed differential forms is necessary. Hence, the computational cost swiftly scales with the base space's dimension and vector bundle's rank. To avoid this kind of computation completely, my new approach uses *Chern roots* instead. The idea goes as follows: we compute the *additive/multiplicative sequence* of a given polynomial, then we compute the Chern/Pontryagin form in the usual manner and insert it into the sequence. This approach involves significantly less computations with mixed differential forms.

## Chern/Pontryagin Forms

Let $$E \to M$$ be a vector bundle and $$\nabla$$ a connection on $$E$$. Recall that the *Chern form* of $$\nabla$$ for complex vector bundles is given by

$$c(E,\nabla) = \det\left(1 + \frac{\Omega^\nabla}{2 \pi \mathrm{i}}\right)$$

wheras the *Pontryagin form* of $$\nabla$$ for real vector bundles is obtained by

$$p(E,\nabla) = \det\left(1 + \frac{\Omega^\nabla}{2 \pi}\right).$$

Here, $$\Omega^\nabla$$ denotes the curvature form matrix associated to $$\nabla$$. Obviously, the computation does not involve any kind of powers of $$\Omega^\nabla$$. This is beneficial for the computational intensity.

## Multiplicative Sequences

Let $$f(x)$$ be a polynomial in $$x$$. Consider the invariant polynomial $$P\colon \mathrm{Mat}(n \times n, \mathbb{C}) \to \mathbb{C}$$ with

$$P(X) = \det\left(f(X)\right)$$

for any $$X \in \mathrm{Mat}(n \times n)$$. Now, we want to express $$P$$ in terms of [*elementary symmetric functions*](https://en.wikipedia.org/wiki/Elementary_symmetric_polynomial). Let $$(x_1, \ldots, x_n)$$ be the eigenvalues of $$X$$ including multiplicities. Then we have

$$P(X) = \prod^n_{k=1} f(x_i)$$

and evidently obtain that this is a symmetric polynomial in the $$x_i$$. Due to the fundamental theorem of elementary symmetric functions, we can write $$P$$ as a polynomial in the elementary symmetric functions $$e_i$$:

$$ P = Q(e_1, \ldots e_n).$$

The proof of this theorem comes with an algorithm [1]. However, the computation with symmetric polynomials is already realized in Sage via the [`SymmetricFunctions`](http://doc.sagemath.org/html/en/reference/combinat/sage/combinat/sf/sfa.html) class using the backend [Symmetrica](http://www.algorithm.uni-bayreuth.de/en/research/SYMMETRICA/) written in C. That is perfect for our purposes.

**Note:** For the particular polynomial $$P$$, one can do even better. See [2] for details. However, the computational cost is, in any case, negligible compared to computations with mixed differential forms in high dimensions.
{: .notice--primary}

Notice that the $$i$$-th homogeneous component of the Chern/Pontryagin class represents the $$i$$-th elementary symmetric function by definition.[^1] This connection becomes clear when we take a closer look at the defining equation of the elementary symmetric functions:

$$\det(1+t X) = \sum^n_{i=0} t^i\,e_i(X).$$

Thus, when we insert the homogeneous components of the Chern/Pontryagin class into the polynomial $$Q$$, then we obtain the characteristic class corresponding to $$P\left(\frac{X}{2 \pi \mathrm{i}}\right)$$.

Of course, we can proceed similarly for additive sequences: we simply replace the determinant by the trace and the product by a sum.

## Summary

The concrete proceeding goes as follows now:

1. Compute the additive/multiplicative sequence of the function associated to the class using `SymmetricFunctions`.
2. Compute the Chern/Pontryagin form in the usual manner.
3. Insert the homogeneous components of the Chern/Pontryagin form into the additive/multiplicative sequence.

In a subsequent post, I will show the outlines of my implementation and provide some examples with computation times.

## References

[1] Ben Blum-Smith and Samuel Coskey --- [The Fundamental Theorem on Symmetric Polynomials: History's First Whiff of Galois Theory](https://arxiv.org/pdf/1301.7116.pdf). 2016.

[2] Oleksandr Iena --- [*On Symbolic Computations with Chern Classes*](https://orbilu.uni.lu/bitstream/10993/21949/2/ChernLib.pdf). 2016.

[3] H. Blaine Lawson and Marie-Louise Michelsohn --- *Spin Geometry*. 1989.

[^1]: Notice that the real case needs special care. See [3, 225 ff.] for details.
