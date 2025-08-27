---
layout: page
title: Latent Pattern of Decision Making
description: Applying graph modeling to uncover hidden dependency pattern of various stakeholders in their decision to participate in research
img: 
importance: 1
category: Stats & ML
related_publications: false
---
#### Objective
We aim to uncover and compare patterns of decision making exhibited by various stakeholders in their decision to participate in research.

#### Method
The data is collected from asking different groups (healthy, mentally ill, physically ill) to rate how important various factors are when deciding to participate in research on a 5-point Likert scale. We applied graphical lasso which gives sparse estimate of the inverse of the covariance matrix (precision matrix). The precision matrix can then be converted to a matrix of conditional dependence, with two factors being conditionally independent if the element is equal to zero. This conditional dependence structure can be represented graphically with the factors being nodes and the values of the matrix being edges. We then compared graphical outcomes (modularity, density, betweenness centrality, edge weights) of two stakeholder groups by taking their difference in a given outcome and testing for significance using permutation test.

#### Result
The groups show no significant differences in overall graph structure as shown by density and modularity. The groups show significant differences in betweenness centrality of nodes as well as weights for edges.

#### Discussion
We would like to try alternative approaches that leverage group information (e.g. grouped graphical lasso) and compare different outcome (e.g. degree of a node).

<a href="https://github.com/guswns3396-work/glasso">GitHub</a>