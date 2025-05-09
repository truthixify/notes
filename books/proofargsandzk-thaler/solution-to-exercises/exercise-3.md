# Exercise 3 Solutions

## 3.1

Here we have $x = (r_1, r_2,..., r_n)$ \
Let $p_{C_{i}} = \sum_{j=1}^{n}{C_{i}r_j}$ and $`p_{(AB)_{i}} = \sum_{j=1}^{n}{(AB)_{i}r_j}`$

- Completeness: If $`C_{ij} = (AB)_{ij}`$ for all $i = 1,...,n, j = 1,...,n$ then it is obvious that $V$ will output EQUAL for every possible choice of $x$ since $p_{C_{ij}}(x) = p_{(AB)_{ij}}(x)$.
- Soundness: If there is at least one $`(i, j) \in [n] \times [n]`$ such that $`C_{ij} \ne (AB)_{ij}`$  \
  Suppose that $C \ne AB$ and let $C_i$ and $`(AB)_i`$ denote the ith row of $C_i$ and $`(AB)_i`$ respectively, since $`C \ne (AB)`$, then there is some row $i$ such that $`C_i \ne (AB)_i`$. But we have $x = (r_1, r_2,..., r_n)$,
  so $`(Cx)_i`$ and $`(ABx)_i`$ are multilinear polynomials, call them $p_{C_{i}}(x)$ and $`p_{(AB)_{i}}(x)`$ respectively.
  Now by Schwartz-Zippel lemma, $p_{C_{i}}(x)$ = $`p_{(AB)_{i}}(x)`$ with probability $\frac{1}{|\mathbb{F}|}$, since d = 1.
  which implies that the probability that $`(Cx)_i \ne (ABx)_i`$ is at least 1 - $\frac{1}{|\mathbb{F}|}$

## 3.2

The communication protocol here will be the same as in exercise 3.1, here we have $x = (r_0, r_2,..., r_{n-1})$, also let $p_a(r) = \sum_{i=0}^{n-1}{a_{i}r_{i}}$ \
In this protocol, Alice send $n+1$ elements of $\mathbb{F}$ to Bob namely $v, r_0, ..., r_{n}$ where $v = p_a(r)$. \
Now by Schwartz-Zippel lemma, $Pr[p_a(r) = p_b(r)] \le \frac{1}{n}$, since d = 1.
Since we want this probability Bob outputs the wrong answer is at most $\frac{1}{n}$, then we have: \
$\frac{1}{\mathbb{F}} \le \frac{1}{n}$ $\implies$ $\mathbb{F} \ge n$. \
For the communication cost, Alice send $n+1$ elements of $\mathbb{F}$ to Bob namely so the total communication cost is $(n+1) \cdot log{\mathbb{F}}$ and since $\mathbb{F} \ge n$, total communication cost is $(n+1)logn$ which is $O(nlogn)$

## 3.4

```Python
p = 11

def get_w(input_len):
    result = []
    v = input_len.bit_length() - 1
    for i, _ in enumerate(data):
        w = tuple((i >> j) & 1 for j in reversed(range(v)))
        result.append(w)
    return result

def basis(w, eval):
    result = 1
    for i in range(len(eval)):
        result = (result * (eval[i] * w[i] + (1 - eval[i]) * (1 - w[i]))) % p
    return result
        

def eval(hypercube_eval_result, eval_point):
    f = 0
    w = get_w(len(hypercube_eval_result))
    for i in range(len(hypercube_eval_result)):
        f = f + hypercube_eval_result[i] * (basis(w[i], eval_point))
    return f % p
```