# Summary on paper: **Random Oracles are Practical: A Paradigm for Designing Efficient Protocols**[^1]

## Introduction and Background:

### Disparity between Theoretical Practical views:
This paper present a bridge between cryptographic theory and practice by introducing a paradigm based on the use of random oracles. 

In the field of cryptography, the gap between theoretical models and practical implementations. Theorists takes certain primitives for granted and  builds schemes on top of these primitives. For example, a one-way function is considered a basic building block and more complex primitives like pseudorandom functions are built on top of it. However, in practice, powerful primitives like the Data Encryption Standard (DES) are already available and used directly as pseudorandom functions. If one needs a one-way function, it is often constructed from DES, thereby transforming a theoretically "simple" primitive into a "complex" one. This disparity results in inefficiencies and a mismatch between theoretical constructs and practical applications. 

Practical primitives, not only possess desirable properties, but also have strengths which have not been defined or formalized. For instance, the MD5 hash function, denoted as $h_2$, with restricted input length $\leq 400$, exhibits the properties that it is hard to find an $x$ such that $h_2(x) = x$; that it is hard to find an $x$ such that $h_2(x)$ has Hamming weight exceeding $120$; also $f_a(x) = h_2(xa)$ is a pseudorandom function family; etc [^2]. These properties, although not fully formalized in theoretical terms, are valuable in practice.

### This Paper's Contribution

This paper aims to bridge the gap between cryptographic theory and practice by introducing a paradigm based on the use of random oracles. The contributions are fourfold:

1. **The paper raises the implicit philosophy behind the use of a random oracle to an explicitly articulated paradigm**, demonstrating its significant benefits to practical cryptography.
2. **It systematically applies this paradigm** to various cryptographic problems, resulting in efficient solutions.
3. **The paper provides definitions** and proofs to justify the previously "unjustified" uses of hash functions within the random oracle model.
4. **It suggests constructions of hash functions** deemed appropriate to instantiate the random oracle, further discussed in [Section 6](#instantiation).

### The Random Oracle Paradigm

The proposed paradigm for designing efficient cryptographic protocols involves the following steps:

1. **Formal Definition:** Find a formal definition for a protocol problem $\Pi$ within a model where all parties have access to a public random oracle $R$.
2. **Protocol Design:** Design a protocol $P$ for $\Pi$ in the random oracle model.
3. **Proof of Correctness:** Prove that $P$ satisfies the definition for $\Pi$.
4. **Oracle Replacement:** Replace accesses to the random oracle $R$ with the computation of an appropriately chosen function $h$.

### Thesis

The central thesis of this paper is that when the above method is properly carried out, the resulting protocol will be both secure and efficient. This approach provides a practical pathway to leverage the theoretical strengths of the random oracle model while addressing the efficiency needs of real-world applications. By carefully choosing and using practical primitives, cryptographic protocols can achieve the desired security properties without sacrificing performance.

## Preliminaries

### Some Definitions Outside of Class

Given that we have been taking this cryptography class, we have a solid understanding of the basic notions. However, to fully comprehend the concepts presented in this paper, we need to define some additional terms. 

**PPT (Probabilistic Polynomial Time):** A probabilistic polynomial time algorithm is one that, given an input of size $n$, runs in time that is polynomial in $n$, with the added element of randomness. This means the algorithm can make decisions based on random choices, and its running time is polynomial relative to the input size.

**Negligible Function:** A function $\epsilon(k)$ is considered negligible if, for every positive integer $c$, there exists an integer $k_c$ such that for all $k > k_c$, $\epsilon(k) \leq \frac{1}{k^c}$. In other words, as $k$ grows, $\epsilon(k)$ becomes exceedingly small.

**Non-negligible Function:** A function is non-negligible if it is not negligible. This implies that the function does not decay to zero faster than the inverse of any polynomial as $k$ increases.

### Most Things Follow the Convention from Class
The following definitions have been discussed in class, albeit with minor variations. For the sake of clarity, they will be explicitly redefined here.
<!-- albeit = even tho -->

$A \rightarrow a$, this $A$ is a probabilistic algorithm and $a$ is its output. $[A(x, y, z, \dots)]$ denotes the set of all possible outputs of $A$ when run with inputs $x, y, z, \ldots$.

$\{0, 1\}^*$ denotes the set of all finite binary strings. $\{0, 1\}^\infty$ represents the set of all infinite binary strings. Concatenation of strings $a$ and $b$ is denoted by $a||b$ or simply $ab$. The empty string is denoted by $\Lambda$.

**Random Oracles:**
A random oracle $R$ is a map from $\{0, 1\}^*$ to $\{0, 1\}^\infty$, chosen uniformly at random from the set of all such maps. The notation $2^\infty$ denotes the set of all random oracles. $R$ represents a "generic" random oracle.

$G: \{0, 1\}^* \rightarrow \{0, 1\}^\infty$ denotes a random generator, which produces an infinite sequence of random bits.

$H: \{0, 1\}^* \rightarrow \{0, 1\}^k$ is a random hash function that maps a binary string of any length to a fixed-size output of $k$ bits.

When multiple random oracles are used, they are assumed to be independently chosen to ensure their outputs are not correlated.

**Trapdoor Permutations:**
$\mathcal{G}$ denotes a PPT algorithm that generates trapdoor permutations. On input $1^k$, $\mathcal{G}$ outputs a triple of algorithms $(f, f^{-1}, d)$, where:
  - $f$ is a permutation function,
  - $f^{-1}$ is its inverse, denoted by $g$ in class,
  - $d$ is a probabilistic algorithm whose output is a subset of $\{0, 1\}^k$.

This $d$ corresponds to the modulus $N$ in the RSA encryption scheme seen in class. The functions $f$ and $f^{-1}$ must be computable in polynomial time.

For an adversary $A$, the probability $\epsilon(k) = Pr[(f, f^{-1}, d) \leftarrow \mathcal{G}(1^k); y \leftarrow f(x): A(f, y, d) \Rightarrow 1]$ is negligible. This indicates that the adversary's chance of inverting $f$ without the trapdoor information $f^{-1}$ is negligible, ensuring the security of the permutation.

## Instantiation


[^1]: BELLARE, M., AND ROGAWAY, P. "Random Oracles are Practical: A Paradigm for Designing Efficient Protocols." In Proceedings of the 1st ACM conference on Computer and communications security (CCS '93). https://doi.org/10.1145/168588.168596

[^2]: M.RABIN, "Digitalized Signatures and Public-Key Functions as Intractable as Factorization," MIT Laboratory for Computer Science TR-212, 1979.