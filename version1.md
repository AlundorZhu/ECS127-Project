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
4. **It suggests constructions of hash functions** deemed appropriate to instantiate the random oracle, further discussed in [Section 6](# Instantiation).

### The Random Oracle Paradigm

The proposed paradigm for designing efficient cryptographic protocols involves the following steps:

1. **Formal Definition:** Find a formal definition for a protocol problem $\Pi$ within a model where all parties have access to a public random oracle $R$.
2. **Protocol Design:** Design a protocol $P$ for $\Pi$ in the random oracle model.
3. **Proof of Correctness:** Prove that $P$ satisfies the definition for $\Pi$.
4. **Oracle Replacement:** Replace accesses to the random oracle $R$ with the computation of an appropriately chosen function $h$.

### Thesis

The central thesis of this paper is that when the above method is properly carried out, the resulting protocol will be both secure and efficient. This approach provides a practical pathway to leverage the theoretical strengths of the random oracle model while addressing the efficiency needs of real-world applications. By carefully choosing and using practical primitives, cryptographic protocols can achieve the desired security properties without sacrificing performance.

## Instantiation


[^1]: BELLARE, M., AND ROGAWAY, P. "Random Oracles are Practical: A Paradigm for Designing Efficient Protocols." In Proceedings of the 1st ACM conference on Computer and communications security (CCS '93). https://doi.org/10.1145/168588.168596

[^2]: M.RABIN, "Digitalized Signatures and Public-Key Functions as Intractable as Factorization," MIT Laboratory for Computer Science TR-212, 1979.