---
bookShowToc: true
title: Matemática
description: Anotações sobre matemática
tags:
  - Python
  - tips
  - dicas
  - matemática
  - algebra
  - machine learning
---

# Matemática para Machine Learning

Uma página para agregar todas as pequenas anotações em matemática que eu faço enquanto estou estudando machine learning e suas aplicações.

> Mas Claudio, quanto de matemática eu preciso pra usar machine learning?

Eu comecei com o conhecimento básico de tudo. Apenas as operações comuns da vida cotidiana, com um pouco de embasamento estatístico simples. Porém eu acredito que você precisa de pelo menus um entendimento básico várias áreas para conseguir entender o que os algoritmos estão fazendo, como aplicá-los e saber ler os conceitos que estão sempre presentes nos artigos.

Esta página não foi escrita para criar intuição sobre o assunto, apenas para ser utilizada como material de referência.

## Álgebra Linear

### Unit Vectors:

$$\boldsymbol{\hat{\textbf{i}}} =
\begin{bmatrix}
1 \\\ 0
\end{bmatrix}$$

$$\boldsymbol{\hat{\textbf{j}}} =
\begin{bmatrix}
0 \\\ 1
\end{bmatrix}$$

Portanto se:

$$\vec{v} = \begin{bmatrix}
2 \\\ 3
\end{bmatrix}$$

então: $$\vec{v} = 2\boldsymbol{\hat{\textbf{i}}} + 3\boldsymbol{\hat{\textbf{j}}}$$

Para calcular o vetor de unidade da função acima:

$$ \||\vec{v}\|| = \sqrt{2^2 + 3^2} $$
$$ \||\vec{v}\|| = \sqrt{13} $$

Fazendo com que o unit vector **û**:
$$\boldsymbol{\hat{\textbf{u}}} = \begin{pmatrix} \dfrac{2}{\sqrt{13}} \\ \dfrac{3}{\sqrt{13}}  \end{pmatrix}$$
