---
layout: page
title: sagemanifolds
permalink: /sagemanifolds/
---

## what is sagemanifolds?

[SageManifolds](https://sagemanifolds.obspm.fr/) is a sub-project of [SageMath](https://sagemath.org/) and provides a comprehensive symbolic and numeric ***tensor calculus*** for manifolds.
The code is distributed under an ***open-source*** license and hence freely available.
All functionalities are interfaced via the ***Python*** programming language which makes it a perfect tool for ***research and teaching*** purposes.
The capabilities range from computations with tensor fields, curvatures and Lie derivatives to vector bundles, bundle connections and characteristic classes.

## vector bundles

Between 2019 and 2020, I contributed to the SageManifolds project by implementing the code for vector bundles.
This involved generalizing the existing implementation of tensor fields to support vector bundles.
The documentation for the vector bundle functionality can be accessed [here](https://doc.sagemath.org/html/en/reference/manifolds/sage/manifolds/vector_bundle.html).

## characteristic classes

The primary goal of my [master thesis](https://arxiv.org/abs/2006.13788) was to implement *characteristic classes* on arbitrary vector bundles.
Since version 9.0 of SageMath, it is possible to compute the characteristic form of a given characteristic class and a bundle connection.
The implementation is based on the Chern&ndash;Weil homomorphism and includes the computation of multiplicative as well as additive characteristic classes and the Euler class.

Since then, bugs have been fixed, the code has been restructured, and algorithms have been improved (see [changelog](https://wiki.sagemath.org/ReleaseTours/sage-9.5#De_Rham_cohomology_and_characteristic_classes)).
For instance, if the manifold is given a metric and orientation, the Euler class of the tangent bundle can now be computed automatically.
The most recent complete documentation can be found [here](https://doc.sagemath.org/html/en/reference/manifolds/sage/manifolds/differentiable/characteristic_cohomology_class.html).

## background

Occasionally, if time permits, I post little articles here that give a some insight into the algorithms and provide mathematical background.
Here is a list of existing articles that supplement my master thesis:

<ul>
  {% for post in site.posts %}
    {% if post.categories contains "sagemanifolds" %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endif %}
  {% endfor %}
</ul>

## future projects

*   Implement sections (and vector fields) as sections of sheaves  
    *related tickets: [#31703](https://github.com/sagemath/sage/issues/31703)*
*   Add new vector bundle features such as vector-valued forms, bundle (auto)morphisms, bundle metrics, total spaces, etc.  
    *related tickets: [#34173](https://github.com/sagemath/sage/issues/34173)*
*   Transgression forms for characteristic classes

## interested?

If you have questions regarding this project, don't hesitate to contact me.
You are also invited to [contribute](https://sagemanifolds.obspm.fr/contrib.html).