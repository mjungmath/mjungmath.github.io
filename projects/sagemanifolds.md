---
title: "SageManifolds"
author_profile: false
layout: single
sidebar:
  nav: "projects"
toc: true
---

## What is SageManifolds?

[SageManifolds](https://sagemanifolds.obspm.fr/) is a sub-project of [SageMath](https://sagemath.org/) and provides a comprehensive symbolic and numeric **tensor calculus** on manifolds. The code is distributed under an **open-source** license and hence freely available. All functionalities are interfaced via the **Python** programming language which makes it a perfect tool for **research and teaching** purposes. The capabilities range from computations with tensor fields, curvatures and Lie derivatives to vector bundles, bundle connections and, most recently, characteristic classes.

## Vector Bundles

In 2019/2020, I contributed *vector bundles* to the SageManifolds project by generalizing the preexisting implementation of tensor fields. All computations are done in local frames. A short introduction is planned in a future post.

## Characteristic Classes

The primary goal of my master's thesis was to implement *characteristic classes* on arbitrary vector bundles. This has been achieved in early 2020. Since version 9.0 of SageMath, it is possible to compute the characteristic form of a given characteristic class and a bundle connection. The implementation bases on the Chern&ndash;Weil homomorphism and includes the computation of multiplicative as well as additive characteristic classes and the Euler class. An introductory post on this topic is coming soon.
## Currently Working on

* Remove code redundancies caused by the new implementation of sections on vector bundles
* Add new vector bundle features such as vector-valued forms, bundle automorphisms, bundle metrics
* Transgression forms of characteristic classes

## Interested?

If you have questions regarding this project, don't hesitate to contact me via [email](mailto:micjung@uni-potsdam.de). You are also invited to [contribute](https://sagemanifolds.obspm.fr/contrib.html).
