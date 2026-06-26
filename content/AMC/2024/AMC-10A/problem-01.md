---
title: "Problem 1"
weight: 1
---

## Problem

What is the value of $9901 \cdot 101 - 99 \cdot 10101$?

$\textbf{(A)}~2 \qquad\textbf{(B)}~20 \qquad\textbf{(C)}~200 \qquad\textbf{(D)}~202 \qquad\textbf{(E)}~2020$

## Solution

$$9901 \cdot 101 - 99 \cdot 10101$$
$$= 9901 \cdot 101 - 99 \cdot 101 \cdot 100 - 99 \cdot 101$$

Factor out $101$:

$$= 101(9901 - 9900 - 99) = 101 \cdot (-98)$$

Hmm, let's try directly:

$$9901 \times 101 = 999{,}901 + 9{,}901 = 1{,}000{,}001 - 100 = 1{,}000{,}001 - 100$$

Actually: $9901 \times 101 = 9901 \times 100 + 9901 = 990{,}100 + 9{,}901 = 1{,}000{,}001$

And: $99 \times 10101 = 99 \times 10000 + 99 \times 101 = 990{,}000 + 9{,}999 = 999{,}999$

$$1{,}000{,}001 - 999{,}999 = \boxed{2}$$

Answer: $\textbf{(A)}~2$
