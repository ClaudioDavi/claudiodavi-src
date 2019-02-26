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

Eu comecei com o conhecimento básico de tudo. Apenas as operações comuns da vida cotidiana, com um pouco de embasamento estatístico simples. Porém eu acredito que você precisa de pelo menos um entendimento básico várias áreas para conseguir entender o que os algoritmos estão fazendo, como aplicá-los e saber ler os conceitos que estão sempre presentes nos artigos.

Esta página não foi escrita para criar intuição sobre o assunto, apenas para ser utilizada como material de referência.

## Álgebra Linear

### Vetor Unidade

$$\boldsymbol{\hat{\textbf{i}}} = \begin{bmatrix}
1 \\\ 0
\end{bmatrix} \hspace{0.5cm} e \hspace{0.5cm} \boldsymbol{\hat{\textbf{j}}} = \begin{bmatrix}
0 \\\ 1
\end{bmatrix} $$

Portanto se:

$$\vec{v} = \begin{bmatrix}
2 \\\ 3
\end{bmatrix} \hspace{0.5cm} então: \hspace{0.5cm} \vec{v} = 2\boldsymbol{\hat{\textbf{i}}} + 3\boldsymbol{\hat{\textbf{j}}}$$

Para calcular o vetor de unidade da função acima:

$$ \||\vec{v}\|| = \sqrt{2^2 + 3^2} $$
$$ \||\vec{v}\|| = \sqrt{13} $$

Fazendo com que o unit vector **û**:
$$\boldsymbol{\hat{\textbf{u}}} = \begin{pmatrix} \dfrac{2}{\sqrt{13}} \\ \dfrac{3}{\sqrt{13}}  \end{pmatrix}$$

### Soma de Vetores
$$\vec{v} = \vec{a} + \vec{b}$$
$$\vec{v} = \begin{bmatrix}
2 \\\ 3
\end{bmatrix} + \begin{bmatrix}
4 \\\ 8
\end{bmatrix} = \begin{bmatrix}
2+4 \\\ 3+8
\end{bmatrix}$$

$$\vec{v} = \begin{bmatrix}
6 \\\ 11
\end{bmatrix}$$

### Multiplicação de vetor por scalar

$$2\vec{v} = \begin{bmatrix}
2 \cdot x \\\ 2 \cdot y
\end{bmatrix} = \begin{bmatrix}
2x \\\ 2y
\end{bmatrix} $$

### Combinação Linear

$$a\vec{v} + b\vec{w}$$

* **span** entre vetores é o grupo de todas as combinações de possíveis vetores entre *a* e *b*
* **Linearmente dependentes**: dois vetores são linearmente dependentes quando um vetor **û**  pode ser removido de uma combinação de vetores e o *span* não é reduzido.
* **Linearmente independentes** Um vetor é linearmente independente quando ao ser adicionado a combinação de vetores adiciona uma nova dimensão ao *span*

### Transformação Linear
Uma transformação linear pode ser representada pelo "movimento" dos vetores de unidade de um vetor.
$$\vec{v} = \begin{bmatrix}
-1 \\\ 2
\end{bmatrix} = $$
$$\vec{v} = -1\boldsymbol{\hat{\textbf{i}}} + 2\boldsymbol{\hat{\textbf{j}}} = $$
$$(Transformado)\vec{v} = -1(\boldsymbol{\hat{\textbf{i}}} Transformado) + 2 (\boldsymbol{\hat{\textbf{j}}} Transformado) = $$
$$ -1 \cdot \begin{bmatrix}
1 \\\ -2
\end{bmatrix} + 2 \cdot \begin{bmatrix}
3 \\\ 0
\end{bmatrix} = $$

$$\begin{bmatrix}
-1 \cdot 1 + 2 \cdot 3 \\\ -1 \cdot -2 + 2 \cdot 0 
\end{bmatrix} = \begin{bmatrix}
5 \\\ 2
\end{bmatrix}$$
</br>
</br>
Em geral, podemos representar os vetores de unidade **î** e **ĵ** como uma matriz de duas dimensões:

$$\begin{bmatrix}
a & b \\\ c & d
\end{bmatrix} = $$

$$\boldsymbol{\hat{\textbf{i}}} = \begin{bmatrix}
a \\\ c
\end{bmatrix} \hspace{0.5cm} e \hspace{0.5cm} \boldsymbol{\hat{\textbf{j}}} = \begin{bmatrix}
b \\\ d
\end{bmatrix} $$

Aplicando essa transformação para qualquer vetor [ *x, y* ] teríamos o seguinte:
$$ \begin{bmatrix}
a & b \\\ c & d
\end{bmatrix} \cdot \begin{bmatrix}
x \\\ y
\end{bmatrix} \hspace{0.5cm} ou \hspace{0.5cm} x \cdot \begin{bmatrix}
a \\\ c
\end{bmatrix} + y \cdot \begin{bmatrix}
b \\\ d
\end{bmatrix}$$

### Multiplicação de Matriz

$$\begin{bmatrix}
a & b \\\ c & d
\end{bmatrix} \cdot \begin{bmatrix}
e & f \\\ g & h
\end{bmatrix} = \begin{bmatrix}
x_1 & x_2 \\\ x_3 & x_4
\end{bmatrix}$$

$$\begin{bmatrix}
a & b \\\ c & d
\end{bmatrix} \cdot \begin{bmatrix}
e \\\ g
\end{bmatrix} = e \cdot  \begin{bmatrix} a \\\ c \end{bmatrix} + g \cdot \begin{bmatrix} b \\\ d \end{bmatrix} = \begin{bmatrix} x_1 \\\ x_3 \end{bmatrix}$$

$$\begin{bmatrix}
a & b \\\ c & d
\end{bmatrix} \cdot \begin{bmatrix}
f \\\ h
\end{bmatrix} = f \cdot  \begin{bmatrix} a \\\ c \end{bmatrix} + h \cdot \begin{bmatrix} b \\\ d \end{bmatrix} = \begin{bmatrix} x_2 \\\ x_4 \end{bmatrix}$$

$$\begin{bmatrix}
a \cdot e + b \cdot g & a \cdot f + b \cdot h \\\ c \cdot e + d \cdot g & c \cdot f + d \cdot h
\end{bmatrix}$$