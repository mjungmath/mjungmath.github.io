---
#
# This file generates an event.
#
layout:      event
title:       Introduction to multi-armed bandits
speaker:     Iuliia Olkhovskaia
dt_start:    29-06-2022 16:00
dt_end:      29-06-2022 17:00
location:    VU Amsterdam, NU-09A46
---

This talk is a brief introduction to the multi-armed bandits. Bandits is a machine learning framework in which an agent sequentially chooses actions to maximize its cumulative reward in the long run. In each round, the agent chooses an action based on the current state of the environment and on the experience gained in previous rounds. At the end of each round, the agent receives a reward associated with the chosen action. The name comes from imagining a gambler, who has to decide which slot machine (“one-armed bandit”) to play.

The plan of the talk is to describe what are the multi-armed bandits, what are the practical applications, and then we get to know what the main algorithms are and which guarantees can be provided for them. I will focus on two main views of the bandits. There’s a stochastic view, where the the world is iid and there is some probability distribution corresponding to each action. The second approach is on completely opposite end of the spectrum - it's a totally adversarial view, where we make no statistical assumptions about the world, and the goal of the learner is to perform as good as the best possible strategy for this environment.