# Random Oracles are Practical: A Paradigm for Designing Efficient Protocols

## Section 1:
* (problem with current theoretical and practical gap)
    * cost of efficiency
    disparity between theoreticians' and practioners' views on primitives, for example:  
        * Theorists view a one-way function as a basic object (and build pseudo-random functions from it)

        * In practice, DES is used as a pseudo-random function, and if one needs a one-way function, one would construct it from DES.

        * reducing "simple" to "complex" !
    * properties that practical primitives seems to posses
        * MD5 which denotes by $h_2$ with restricted input length  
        It is hard to find an $x$ such that $h_2(x) = x$;

* This paper's contribution
    1. First: "we raise the implicit philosophy behind the use of a random oracle to an explicitly articulated paradigm which we maintain brings significant benefits to practice."
    2. Second: "Second, we systematically apply the paradigm to diverse cryptographic problems to obtain efficient solutions. "
    3. Third: "we provide definitions and proofs to show that some of the  reviously "unjustified" uses of hash functions can find justification in the random oracle model."
    4. Last: "Finally, we suggest constructions of hash functions which we believe are appropriate to instantiate the random oracle." [Section 6](#section-6)

### The Random Oracle Paradigm
1. Find a formal definition for a protocol problem $\Pi$ in the model which all parties have access to a random oracle $R$.
2. Design a protocol $P$ for $\Pi$ in the random oracle model.
3. Prove that $P$ satisfies the definition for $\Pi$.
4. Replace the random oracle access to $R$ by computation of $h$.

#### Thesis
When above method is properly carriedout, the resulting protocol is secure and efficient.

### Result
#### Efficient encryption
[Section 3](#section-3)
#### Justification Of Know Heuristic/Theoretical Results
[Section 4](#section-4)

### ~~Background and Related Work~~ Dan's paper that uses random oracles
[Dan Boneh's paper](./Functional%20Encryption.pdf)


## Section 2 Preliminaries

### Some definitions outside of class
"PPT" stands for "probabilistic polynomial time."  
A function $\epsilon (k)$ is _negligible_ if for every $c$ there exists a $k_c$ such that for all $k > k_c$, $\epsilon(k) \leq \frac{1}{k^c}$.  
A function is _non-negligible_ if it is not negligible.

### most things follow the convension from class  
$A \rightarrow a$ means $A$ is a probabilistic algorithm and $a$ is its output  
$[A(x, y, z, \dots)]$ denotes the set of all possible outputs of $A$ when run on input $x, y, z, \dots$  
$\{0, 1$^*$ denotes the space of finite binary strings  
$\{0, 1$^\infty $ denotes the space of infinite binary strings  
$a||b$ or $ab$ denotes the concatenation of strings $a$ and $b$  
$\Lambda$ denotes empty string

#### Oracles
a random oracle $R$ is a map from $\{0, 1$^*$ to $\{0, 1$^\infty$ that is chosen uniformly at random from the set of all such maps. $2^\infty$ denotes the set of all randome oracles.  
$R$ denotes a "generic" random oracle.  
$G: \{0, 1$^* \rightarrow \{0, 1$^\infty $ denotes a random generator.  
$H: \{0, 1$^* \rightarrow \{0, 1$^k$ denotes a random hash function.  
Whenever, multiple random oracles are used, they are assumed to be independently choosen.

#### Trapdoor permutations
$\mathcal{G}$ denotes a PPT algorithm and a generator for a trapdoor permutation.  
$\mathcal{G}$ on input $1^k$ outputs a triple of algorithms $(f, f^{-1}, d)$ where $f$ is the same $f$ as seen in class and $f^{-1}$ is denoted by $g$ in class.  
$d$ is a probabilistic output such that $[d(1^k)]$ is a subset of $\{0, 1$^k$ and $f$, $f^{-1}$ be permutations on $[d(1^k)]$. This $d$ correspond to the $mod$ $N$ in the RSA encryption scheme as seen as an example in class.  
Also, $(f, f^{-1}, d)$ is computable in polynomial time.  
For adversary $A$, $$\epsilon(k) = Pr[(f, f^{-1}, d) \leftarrow \mathcal{G}(1^k); y \leftarrow f(x): A(f, y, d) => 1]$$ is negligible.



## Section 6
Section 6 of the paper on "Random Oracles" focuses on the instantiation of random oracles with concrete cryptographic primitives such as hash functions. Here's a breakdown of the key points:

### Instantiation

1. **General Guidelines:**
   - The specific details of the target protocol whose random oracles are being instantiated are not important. 
   - What matters is the number of oracles used and their input/output length requirements.

2. **Careful Choice of Functions:**
   - It is crucial to carefully choose a concrete function $h$ to instantiate an oracle. 
   - Some functions do not work well as replacements for random oracles, such as MD5 and its compression function, due to their inherent structure and susceptibility to attacks.

### Examples of Poor Instantiations

- **MD5 as an Oracle:**
  - MD5 is not suitable as a random oracle because specific structures in MD5 allow for easy computation of certain values given an input and its MD5 hash.

- **Compression Function of MD5:**
  - The compression function of MD5 also fails as a good replacement for a random oracle due to the possibility of efficiently finding collisions.

### Suitable Candidates

1. **Truncated Hash Functions:**
   - Example: Using the first 64 bits of MD5 as $ h_1(x) $.

2. **Hash Functions with Restricted Input Lengths:**
   - Example: Using MD5 with input lengths restricted to less than 400 bits as $ h_2(x) $.

3. **Nonstandard Uses of Hash Functions:**
   - Example: Defining $ h_3(x) = \text{MD5}(a \| x) $ where $ a $ is a fixed string.

4. **First Block Compression Functions:**
   - Example: Using the compression of the first 512-bit block of MD5 as $ h_4 $.

### How to extend the domain and range for a instantiated hash function
The last paragraph of Section 6 in the paper discusses a specific example of instantiating a random oracle with a concrete function. Let's go through this example in detail:

### Example Instantiation of a Random Oracle

1. **Choosing a Base Function:**
   - The authors suggest a heuristic choice of a map $ h': \{0, 1$^{256} \rightarrow \{0, 1$^{64} $ defined by:
     $$
     h'(x) = \text{first 64 bits of } h_4((x) \oplus C)
     $$
     - Here, $ h_4 $ is a function derived from a cryptographic hash function's first block compression function.
     - $ C $ is a randomly chosen 512-bit constant.

2. **Extending Domain and Range:**
   - To handle inputs of arbitrary length, the authors extend the domain and range as needed for the given application. They propose the following steps:
   
   3. **Encoding Input:**
      - Encode each input $ x $ by $ x' $, which consists of $ x $, the bit "1", and enough "0"s to make $ |x'| $ a multiple of 128 bits.

   4. **Defining Extended Function $h$:**
      - Define $ h''(x) $ as the concatenation of the outputs of $ h' $ applied to each 64-bit block of the encoded input $ x' $:
        $$
        h''(x) = h'(x_0) \| h'(x_1) \| h'(x_2) \| \ldots
        $$
        where $ x_0, x_1, x_2, \ldots $ are 64-bit blocks derived from $ x' $.

   5. **Combining Blocks:**
      - Finally, define $ h(x) $ by combining the outputs of $ h'' $ using bitwise XOR:
        $$
        h(x) = h''(x_0) \oplus h''(x_1) \oplus \ldots \oplus h''(x_n)
        $$
        This construction effectively yields a map $ h: \{0, 1$^* \rightarrow \{0, 1$^\infty $ that behaves similarly to a random oracle for practical purposes.
