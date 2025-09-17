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
Our objective is to identify and compare the patterns of decision-making among different stakeholders (healthy, mentally ill, and physically ill) in deciding whether to participate in research.

#### Method
We collected data from three stakeholder groups (healthy, mentally ill, and physically ill) who rated the importance of various factors when deciding whether to participate in research on a 5-point Likert scale. To analyze the data, we applied graphical lasso, a method that estimates a sparse inverse of the covariance matrix, also known as the precision matrix. The precision matrix was then used to construct a matrix of conditional dependence, where factors are conditionally independent if the corresponding element is zero. This structure was visualized as a graph, with factors represented as nodes and the relationships between them as edges. We compared the graphical outcomes (modularity, density, betweenness centrality, and edge weights) between the two stakeholder groups by calculating the differences in these outcomes and testing for significance using permutation tests.

#### Result
No significant differences were found in the overall graph structure between the groups, as indicated by the density and modularity measures. However, significant differences were observed in betweenness centrality and edge weights between the groups.

#### Discussion
In future work, we plan to explore alternative approaches, such as grouped graphical lasso, which incorporates group information into the analysis. Additionally, we aim to examine different outcome measures, such as the degree of nodes, to further investigate the decision-making patterns across groups.

<a href="https://github.com/guswns3396-work/glasso">GitHub</a>