---
title: Introduction to Quantum Cryptography
date: 2026-10-21 21:30:00 +0700
categories: [Cryptography, Security]
tags: [Quantum]
math: true
---

## 1. Quantum bits

### 1.1. Quantum bits

* **Hilbert space:** is a vector space (typically defined over the complex numbers), equipped with an inner product. This implies that quantum states are represented as vectors.  

* The elementary Hilbert space used in quantum information is the qubit space, which is a complex Hilbert space of dimension 2. Suppose $\vert{}0\rangle$ and $\vert{}1\rangle$ form an orthonormal basis for that state space. Then an arbitrary state vector in the state space can be written:

$$\vert{}\psi\rangle = \begin{pmatrix} \alpha \\ \beta \end{pmatrix} = \alpha\vert{}0\rangle + \beta\vert{}1\rangle$$

with $\alpha$ and $\beta$ being complex numbers ($\vert{}\alpha\vert{}^2 + \vert{}\beta\vert{}^2 = 1$), where:

$$\vert{}0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad \vert{}1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$$

* The states $\vert{}0\rangle$ and $\vert{}1\rangle$ are analogous to the two values 0 and 1 which a bit may take. The way a qubit differs from a bit is that superpositions of these two states, of the form $\alpha \vert{}0\rangle + \beta \vert{}1\rangle$, can also exist, in which it is not possible to say that the qubit is definitely in the state $\vert{}0\rangle$, or definitely in the state $\vert{}1\rangle$.

* A qubit’s state is a unit vector in a two-dimensional complex vector space and is normalized to length 1. 

![Qubit Bases](/assets/img/quantum_bits.jpg)

* **Hadamard basis:**

$$\vert{}+\rangle = \begin{pmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{pmatrix} = \frac{1}{\sqrt{2}}(\vert{}0\rangle  +  \vert{}1\rangle)$$

$$\vert{}-\rangle = \begin{pmatrix} \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} \end{pmatrix} = \frac{1}{\sqrt{2}}(\vert{}0\rangle  -  \vert{}1\rangle)$$

* Measuring a qubit we get either the result 0, with probability $\vert{}\alpha\vert{}^2$, or the result 1, with probability $\vert{}\beta\vert{}^2$ (Quantum Measurement).

### 1.2 Multiple qubits

#### 1.2.1. Dirac notation

* **Ket (column vector):**

$$\vert{}\psi\rangle = \begin{pmatrix} a_1 \\ a_2 \\ \dots \\ a_m \end{pmatrix} \qquad \vert{}\varphi\rangle = \begin{pmatrix} b_1 \\ b_2 \\ \dots \\ b_m \end{pmatrix}$$

* **Bra (row vector):**

$$\langle\psi\vert{} = (a_1^* \quad a_2^* \quad \dots \quad a_m^*)$$

$$\langle\varphi\vert{} = (b_1^* \quad b_2^* \quad \dots \quad b_m^*)$$

* **Bra-ket: inner product (complex number):**

$$\langle\varphi\vert{}\psi\rangle = (b_1^* \quad b_2^* \quad \dots \quad b_m^*) \begin{pmatrix} a_1 \\ a_2 \\ \dots \\ a_m \end{pmatrix} = \sum_{i \in [m]} b_i^* a_i \in \mathbb{C}$$

* **Ket-bra: outer product (complex matrix):**

$$\vert{}\varphi\rangle\langle\psi\vert{} = \begin{pmatrix} b_1 \\ b_2 \\ \dots \\ b_m \end{pmatrix} (a_1^* \quad a_2^* \quad \dots \quad a_m^*) = \begin{pmatrix}  b_1 a_1^* & b_1 a_2^* & \dots & b_1 a_m^* \\  b_2 a_1^* & b_2 a_2^* & \dots & b_2 a_m^* \\  \dots & \dots & \dots & \dots \\  b_m a_1^* & b_m a_2^* & \dots & b_m a_m^*  \end{pmatrix} \in \mathbb{C}^{m \times m}$$

* **Tensor product (Kronecker product):**

$$A \otimes B \equiv \left. \overbrace{\begin{bmatrix} A_{11}B & A_{12}B & \dots & A_{1n}B \\ A_{21}B & A_{22}B & \dots & A_{2n}B \\ \vdots & \vdots & \vdots & \vdots \\ A_{m1}B & A_{m2}B & \dots & A_{mn}B \end{bmatrix}}^{nq} \right\} mp$$

#### 1.2.2. Multiple qubits

* **Postulate:** The state space of a composite physical system is the tensor product of the state spaces of the component physical systems. 

With $n$ qubits:

$$\mathcal{H}_{\text{n-qubits}} = \mathcal{H}_1 \otimes \mathcal{H}_2 \otimes \dots \otimes \mathcal{H}_n$$

$$\implies \text{Dim}(\mathcal{H}_{\text{n-qubits}}) = \text{Dim}(\mathcal{H}_1) \times \text{Dim}(\mathcal{H}_2) \times \dots \times \text{Dim}(\mathcal{H}_n)$$

$$\implies \text{Dim}(\mathcal{H}_{\text{n-qubits}}) = \text{Dim}(\mathbb{C}^2) \times \text{Dim}(\mathbb{C}^2) \times \dots \times \text{Dim}(\mathbb{C}^2)$$

$$= \underbrace{2 \times 2 \times \dots \times 2}_{n \text{ times}} = 2^n$$

---

## 2. Evolution of Quantum States

### 2.1. Theoretical Foundation

* **Schrödinger Equation:** The continuous time evolution of a closed quantum system is governed by:

$$i\hbar \frac{\partial}{\partial t} \vert{}\psi\rangle = \hat{H}\vert{}\psi\rangle$$

* **Unitary Operator:** In quantum information, state evolution is represented discretely by a unitary operator $U$ (quantum gate).

* **Unitary Condition:**

$$U U^\dagger = U^\dagger U = I \quad \implies \quad U^\dagger = U^{-1}$$

### 2.2. Quantum Unitaries

#### Unitary Operator in Probability Conservation

Consider an $N$-dimensional Hilbert space $\mathcal{H}$ with *Arbitrary orthonormal basis* $\{\vert{}e_1\rangle, \vert{}e_2\rangle, \dots, \vert{}e_N\rangle\}$ satisfying *Completeness relation:* $\sum_{i=1}^{N} \vert{}e_i\rangle\langle e_i\vert{} = I$.

Representation of an arbitrary state vector $\vert{}\psi\rangle \in \mathcal{H}$ with the probability of obtaining outcome $i$ when measuring in the basis $\{\vert{}e_i\rangle\}$ is $p(i) = \vert{}c_i\vert{}^2$.

$$\vert{}\psi\rangle = \sum_{i=1}^{N} c_i \vert{}e_i\rangle \quad (c_i \in \mathbb{C})$$

Calculation of the norm squared $\langle\psi\vert{}\psi\rangle$:

$$\langle\psi\vert{}\psi\rangle = \left(\sum_{i=1}^{N} c_i^* \langle e_i\vert{}\right) \left(\sum_{j=1}^{N} c_j \vert{}e_j\rangle\right) = \sum_{i=1}^{N} \sum_{j=1}^{N} c_i^* c_j \underbrace{\langle e_i \vert{} e_j \rangle}_{\delta_{ij}}$$

$$\langle\psi\vert{}\psi\rangle = \sum_{i=1}^{N} c_i^* c_i = \sum_{i=1}^{N} \vert{}c_i\vert{}^2 = \sum_{i=1}^{N} p(i) = 1$$

Consider an $N \times N$ unitary operator $U$ satisfying $U^\dagger U = U U^\dagger = I$.

When $U$ acts on the state $\vert{}\psi\rangle$, the system transitions to a new state $\vert{}\psi'\rangle = U\vert{}\psi\rangle$.

Expressing $\vert{}\psi'\rangle$ in the same basis $\{\vert{}e_i\rangle\}$ as $\vert{}\psi'\rangle = \sum_{i=1}^{N} c'_i \vert{}e_i\rangle$:

$$\langle\psi'\vert{}\psi'\rangle = (U\vert{}\psi\rangle)^\dagger (U\vert{}\psi\rangle) = \langle\psi\vert{} U^\dagger U \vert{}\psi\rangle = \langle\psi\vert{} I \vert{}\psi\rangle = \langle\psi\vert{}\psi\rangle = 1$$

#### Unitary operator in Reversibility & Information Conservation

For a unitary matrix, we always have $U^{-1} = U^\dagger$. This guarantees that all quantum gates (such as $X$, $Z$, and $H$) are fully reversible without any loss of information:

$$U^\dagger(U\vert{}\psi\rangle) = (U^\dagger U)\vert{}\psi\rangle = I\vert{}\psi\rangle = \vert{}\psi\rangle$$

#### 2.2.1. Pauli-X Gate (Bit-Flip)

The $X$ gate acts as the quantum NOT operation in the computational basis, flipping $\vert{}0\rangle \leftrightarrow \vert{}1\rangle$:

$$X = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$$

Action on basis states:

$$X\vert{}0\rangle = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}\begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \vert{}1\rangle \quad \text{and} \quad X\vert{}1\rangle = \vert{}0\rangle$$

#### 2.2.2 Pauli-Z Gate (Phase-Flip)

The $Z$ gate is the NOT operation in the Hadamard basis. It leaves $\vert{}0\rangle$ unchanged and flips the phase of $\vert{}1\rangle$:

$$Z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$$

Action on basis states:

$$Z\vert{}0\rangle = \vert{}0\rangle \quad \text{and} \quad Z\vert{}1\rangle = -\vert{}1\rangle$$

$$Z\vert{}+\rangle = Z \left( \frac{\vert{}0\rangle + \vert{}1\rangle}{\sqrt{2}} \right) = \frac{Z\vert{}0\rangle + Z\vert{}1\rangle}{\sqrt{2}} = \frac{\vert{}0\rangle - \vert{}1\rangle}{\sqrt{2}} = \vert{}-\rangle$$

$$Z\vert{}-\rangle = Z \left( \frac{\vert{}0\rangle - \vert{}1\rangle}{\sqrt{2}} \right) = \frac{Z\vert{}0\rangle - Z\vert{}1\rangle}{\sqrt{2}} = \frac{\vert{}0\rangle - (-\vert{}1\rangle)}{\sqrt{2}} = \frac{\vert{}0\rangle + \vert{}1\rangle}{\sqrt{2}} = \vert{}+\rangle$$

Eigenvectors: $\{\vert{}0\rangle, \vert{}1\rangle\}$ are the eigenvectors of $Z$ corresponding to eigenvalues $+1$ and $-1$, respectively, so the computational basis is also referred to as the **$Z$-basis**.

#### 2.2.3. Hadamard Gate $H$ (Basis Switch)

The $H$ gate transforms states between the computational basis ($Z$-basis) and the Hadamard basis ($X$-basis) in both directions:

$$H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$$

* Moving from $Z$-basis to $X$-basis:

$$H\vert{}0\rangle = \vert{}+\rangle \quad \text{and} \quad H\vert{}1\rangle = \vert{}-\rangle$$

* Moving from $X$-basis back to $Z$-basis:

$$H\vert{}+\rangle = \vert{}0\rangle \quad \text{and} \quad H\vert{}-\rangle = \vert{}1\rangle$$

---

## 3. Quantum Circuit

### 3.1. Composing Unitaries

* The circuit is read from left to right. Each line in the circuit represents a wire in the quantum circuit.
* **Multi-Qubit Operator Representation in Quantum Circuits:** Unitary operators $U$ act on the state vector $\vert{}\Psi\rangle$ from **right to left** via operator composition:

$$\vert{}\Psi_{\text{out}}\rangle = U_3 \cdot U_2 \cdot U_1 \vert{}\Psi_{\text{in}}\rangle$$

*(Note: The gate layer executed earliest on the far left appears adjacent to the initial state vector).*

* If a wire does not contain a gate at a given time step, it corresponds to the *Identity operator $I$*—leaving the state of that qubit unchanged.
  * *To be more specific:* If a single-qubit gate $A$ acts on the first qubit while the second qubit remains unacted upon, the global operator acting on the composite system is given by $A \otimes I$.
* When multiple gates act in parallel on distinct wires (qubits) at the same time step, the overall global operator is given by the tensor product of the individual gates.

![Quantum Circuit Operators](/assets/img/image-1.png)

* **The Controlled-NOT Gate (CNOT):** If Qubit 1 is in state $\vert{}1\rangle$, flip Qubit 2; if Qubit 1 is in state $\vert{}0\rangle$, leave Qubit 2 unchanged.

![CNOT Gate](/assets/img/quantum_NoT.jpg)
![Quantum Circuit](/assets/img/quantum_circuit.jpg)

### 3.2. Application in Circuit Reading Comprehension

![Circuit Reading Example](/assets/img/image-4.png)

* **Initial state:**

$$\vert{}\Psi_{\text{in}}\rangle = \vert{}\varphi\rangle \otimes \vert{}+\rangle \otimes \vert{}0\rangle \otimes \vert{}0\rangle \otimes \vert{}\psi\rangle \equiv \vert{}\varphi\rangle \vert{}+\rangle \vert{}00\rangle \vert{}\psi\rangle$$

* **Time step 1:**
  * Wires 1 & 2: Controlled-$G_2$ gate with Wire 1 as control $\rightarrow c(G_2)$
  * Wire 3: Single-qubit gate $G_1$
  * Wires 4 & 5: Idle wires $\rightarrow I_4 \otimes I_5 \equiv I_{45}$

$$U_1 = c(G_2) \otimes G_1 \otimes I_{45}$$

* **Time step 2:**
  * Wires 1, 2 & 3: 3-qubit gate $G_3$
  * Wires 4 & 5: Idle wires $\rightarrow I_{45}$

$$U_2 = G_3 \otimes I_{45}$$

* **Time step 3:**
  * Wire 1: Single-qubit gate $G_2$
  * Wire 2: Idle wire $\rightarrow I$
  * Wires 3 & 4: CNOT gate ($c(X)$) with Wire 3 as control and Wire 4 as target
  * Wire 5: Single-qubit gate $G_1$

$$U_3 = G_2 \otimes I \otimes c(X) \otimes G_1$$

$$\implies U = (G_2 \otimes I \otimes c(X) \otimes G_1)(G_3 \otimes I_{45})(c(G_2) \otimes G_1 \otimes I_{45})\vert{}\varphi\rangle\vert{}+\rangle\vert{}00\rangle\vert{}\psi\rangle$$

---

## 4. Quantum Measurement

Unlike classical physics, quantum mechanics cannot predict the exact outcome of a measurement. Instead, it determines the exact probability distribution of all possible outcomes.

### 4.1. Measure $\hat{A}$ in State $\vert{}\psi\rangle$ (No Degeneracy)

Eigenvalues and eigenvectors:

$$\text{Physical quantity } A \longrightarrow \text{Observable } \hat{A}$$

$$\hat{A} \vert{}u_n\rangle = \lambda_n \vert{}u_n\rangle$$

* **Postulate III:** The result of a measurement of a physical quantity is one of the eigenvalues of the associated observable.
* **Postulate IV:** The measurement of $A$ in a system in normalized state $\vert{}\psi\rangle$ gives eigenvalue $\lambda_n$ with probability:

$$P(\lambda_n) = \vert{}\langle u_n \vert{} \psi \rangle\vert{}^2$$

Having a quantum state prepared in a superposition:

$$\vert{}\psi\rangle = c_1\vert{}u_1\rangle + c_2\vert{}u_2\rangle + \dots + c_n\vert{}u_n\rangle = \sum_{i} c_i\vert{}u_i\rangle \quad \text{where } c_i = \langle u_i \vert{} \psi \rangle$$

Constructing a projection operator $P_n = \vert{}u_n\rangle\langle u_n\vert{}$ to project $\vert{}\psi\rangle$ onto the subspace spanned by $\vert{}u_n\rangle$:

$$P_n \vert{}\psi\rangle = c_n \vert{}u_n\rangle$$

The measurement probability $P(\lambda_n)$ is:

$$P(\lambda_n) = \vert{}\langle u_n \vert{} \psi \rangle\vert{}^2 = \vert{}c_n\vert{}^2$$

### 4.2. Measure $\hat{A}$ in State $\vert{}\psi\rangle$ (With Degeneracy)

Degenerate eigenvalues:

$$\hat{A} \vert{}u_n^i\rangle = \lambda_n \vert{}u_n^i\rangle \quad \text{for } i = 1, 2, \dots, g_n$$

The measurement of $A$ in a system in normalized state $\vert{}\psi\rangle$ gives eigenvalue $\lambda_n$ (with degeneracy $g_n$) with probability:

$$P(\lambda_n) = \sum_{i=1}^{g_n} \vert{}\langle u_n^i \vert{} \psi \rangle\vert{}^2$$

Superposition state:

$$\vert{}\psi\rangle = \sum_n \sum_{i=1}^{g_n} c_n^i \vert{}u_n^i\rangle \quad \text{where } c_n^i = \langle u_n^i \vert{} \psi \rangle$$

Projection operator $P_n = \sum_{i=1}^{g_n} \vert{}u_n^i\rangle\langle u_n^i\vert{}$:

$$P_n \vert{}\psi\rangle = \sum_{i=1}^{g_n} c_n^i \vert{}u_n^i\rangle$$

Measurement probability:

$$P(\lambda_n) = \langle\psi\vert{} P_n \vert{}\psi\rangle = \sum_{i=1}^{g_n} \vert{}\langle u_n^i \vert{} \psi \rangle\vert{}^2 = \sum_{i=1}^{g_n} \vert{}c_n^i\vert{}^2$$

### 4.3. Partial Measurement on Composite Systems

In multi-qubit systems, a **partial measurement** involves performing a projective measurement on a specific subset of qubits while leaving the remaining subsystem unmeasured.

#### 4.3.1. Formulation

Consider an $n$-qubit state expressed in the computational basis:

$$\vert{}\psi\rangle = \sum_{i \in \{0,1\}^n} \alpha_i \vert{}i\rangle = \sum_{b \in \{0,1\}} \sum_{j \in \{0,1\}^{n-1}} \alpha_{bj} \vert{}b\rangle \otimes \vert{}j\rangle$$

When measuring only the **first qubit** in the computational basis:

* **Outcome Probability $p_b$:**

$$p_b = \sum_{j \in \{0,1\}^{n-1}} \vert{}\alpha_{bj}\vert{}^2$$

* **State Collapse:**

$$\vert{}\psi'\rangle = \frac{1}{\sqrt{p_b}} \sum_{j \in \{0,1\}^{n-1}} \alpha_{bj} \vert{}bj\rangle$$

#### 4.3.2. Worked Example

Consider a 2-qubit state $\vert{}\psi\rangle = \frac{1}{\sqrt{3}}(\vert{}00\rangle + \vert{}01\rangle + \vert{}10\rangle)$. Measuring the first qubit in the computational basis yields:

* **Outcome $b = 0$:**
  * Probability: $p_0 = \left\vert{}\frac{1}{\sqrt{3}}\right\vert{}^2 + \left\vert{}\frac{1}{\sqrt{3}}\right\vert{}^2 = \frac{2}{3}$
  * Post-Measurement State:

$$\vert{}\psi'\rangle = \frac{1}{\sqrt{2/3}} \left( \frac{1}{\sqrt{3}}\vert{}00\rangle + \frac{1}{\sqrt{3}}\vert{}01\rangle \right) = \frac{1}{\sqrt{2}}(\vert{}00\rangle + \vert{}01\rangle)$$

* **Outcome $b = 1$:**
  * Probability: $p_1 = \left\vert{}\frac{1}{\sqrt{3}}\right\vert{}^2 = \frac{1}{3}$
  * Post-Measurement State:

$$\vert{}\psi'\rangle = \frac{1}{\sqrt{1/3}} \left( \frac{1}{\sqrt{3}}\vert{}10\rangle \right) = \vert{}10\rangle$$

### 4.4. Projective Measurements on Pure States

A projective measurement is defined by a set of Hermitian projection operators $\{\Pi_1, \Pi_2, \dots, \Pi_k\}$ satisfying $\sum_{i=1}^k \Pi_i = I$.

When measuring a pure state $\vert{}\psi\rangle$:

* **Outcome Probability:**

$$P(i) = \Vert{}\Pi_i \vert{}\psi\rangle\Vert{}^2 = \langle\psi\vert{} \Pi_i \vert{}\psi\rangle$$

* **State Collapse:**

$$\vert{}\psi'\rangle = \frac{\Pi_i \vert{}\psi\rangle}{\Vert{}\Pi_i \vert{}\psi\rangle\Vert{}}$$

**State collapse ensure probability normalisation:**

$$\langle\psi'\vert{}\psi'\rangle = \left(\frac{\Pi_i\vert{}\psi\rangle}{\Vert{}\Pi_i\vert{}\psi\rangle\Vert{}}\right)^\dagger \left(\frac{\Pi_i\vert{}\psi\rangle}{\Vert{}\Pi_i\vert{}\psi\rangle\Vert{}}\right) = \frac{\langle\psi\vert{}\Pi_i^\dagger \Pi_i\vert{}\psi\rangle}{\Vert{}\Pi_i\vert{}\psi\rangle\Vert{}^2}$$

Applying the **Hermiticity** and **Idempotency** properties of the **Projection Operator** $\Pi_i$, we have:

$$\Pi_i^\dagger \Pi_i = \Pi_i \cdot \Pi_i = \Pi_i^2 = \Pi_i$$

Substituting into the numerator:

$$\langle\psi\vert{}\Pi_i^\dagger \Pi_i\vert{}\psi\rangle = \langle\psi\vert{}\Pi_i\vert{}\psi\rangle = \Vert{}\Pi_i\vert{}\psi\rangle\Vert{}^2 = P(i)$$

Thus:

$$\langle\psi'\vert{}\psi'\rangle = \frac{\Vert{}\Pi_i\vert{}\psi\rangle\Vert{}^2}{\Vert{}\Pi_i\vert{}\psi\rangle\Vert{}^2} = \frac{P(i)}{P(i)} = 1$$

#### 4.4.1. Non - Degenerate Measurement

1. **Outcome Probability $P(\lambda_n)$:**
   Substitute $\Pi_n = \vert{}u_n\rangle\langle u_n\vert{}$ into $P(n) = \langle\psi\vert{}\Pi_n\vert{}\psi\rangle$:

   $$P(\lambda_n) = \langle\psi\vert{}(\vert{}u_n\rangle\langle u_n\vert{})\vert{}\psi\rangle = \langle\psi\vert{}u_n\rangle\langle u_n\vert{}\psi\rangle = c_n^* c_n = \vert{}c_n\vert{}^2 = \vert{}\langle u_n\vert{}\psi\rangle\vert{}^2$$

2. **State Collapse $\vert{}\psi'\rangle$:**

   $$\Pi_n\vert{}\psi\rangle = P_n\vert{}\psi\rangle = \vert{}u_n\rangle\langle u_n\vert{}\psi\rangle = c_n\vert{}u_n\rangle$$

   Substitute $P_n\vert{}\psi\rangle$ and $\sqrt{P(\lambda_n)} = \vert{}c_n\vert{}$ into the collapse formula:

   $$\vert{}\psi'\rangle = \frac{P_n\vert{}\psi\rangle}{\sqrt{P(\lambda_n)}} = \frac{c_n\vert{}u_n\rangle}{\vert{}c_n\vert{}} = \left(\frac{c_n}{\vert{}c_n\vert{}}\right)\vert{}u_n\rangle = e^{i\phi}\vert{}u_n\rangle \equiv \vert{}u_n\rangle$$

#### 4.4.2. Degenerate Measurement

1. **Outcome Probability $P(\lambda_n)$:**
   Substitute $\Pi_n = \sum_{i=1}^{g_n} \vert{}u_n^i\rangle\langle u_n^i\vert{}$ into $P(n) = \langle\psi\vert{}\Pi_n\vert{}\psi\rangle$:

   $$P(\lambda_n) = \left\langle\psi\left\vert{}\left(\sum_{i=1}^{g_n} \vert{}u_n^i\rangle\langle u_n^i\vert{}\right)\right\vert{}\psi\right\rangle = \sum_{i=1}^{g_n} \langle\psi\vert{}u_n^i\rangle\langle u_n^i\vert{}\psi\rangle = \sum_{i=1}^{g_n} \vert{}c_n^i\vert{}^2$$

2. **State Collapse $\vert{}\psi'\rangle$:**

   $$\Pi_n\vert{}\psi\rangle = P_n\vert{}\psi\rangle = \sum_{i=1}^{g_n} \vert{}u_n^i\rangle\langle u_n^i\vert{}\psi\rangle = \sum_{i=1}^{g_n} c_n^i \vert{}u_n^i\rangle$$

   Substitute into collapse formula with $\sqrt{P(\lambda_n)} = \sqrt{\sum_{i=1}^{g_n} \vert{}c_n^i\vert{}^2}$:

   $$\vert{}\psi'\rangle = \frac{P_n\vert{}\psi\rangle}{\sqrt{P(\lambda_n)}} = \frac{1}{\sqrt{\sum_{i=1}^{g_n} \vert{}c_n^i\vert{}^2}} \sum_{i=1}^{g_n} c_n^i \vert{}u_n^i\rangle$$

---

## 5. Quantum Entanglement

A bipartite state $\vert{}\psi\rangle_{AB}$ is a **product state** if there exist $\vert{}\psi_1\rangle_A$ and $\vert{}\psi_2\rangle_B$ such that:

$$\vert{}\psi\rangle_{AB} = \vert{}\psi_1\rangle_A \otimes \vert{}\psi_2\rangle_B$$

If a quantum state cannot be written as a product state, it is **entangled**.

Example ($W$-state):

$$W_n = \frac{1}{\sqrt{n}}(\vert{}10\dots0\rangle + \vert{}01\dots0\rangle + \dots + \vert{}00\dots1\rangle)$$

### 5.1. Bell State

Bell states are generated via a quantum circuit consisting of a Hadamard gate ($H$) and a Controlled-NOT gate (CNOT).

![Bell Circuit](/assets/img/image-5.png)

Bell basis states:

$$\left\{ \underbrace{\frac{1}{\sqrt{2}}(\vert{}00\rangle + \vert{}11\rangle)}_{\vert{}\Psi_{00}\rangle \text{ (EPR pair)}}, \underbrace{\frac{1}{\sqrt{2}}(\vert{}00\rangle - \vert{}11\rangle)}_{\vert{}\Psi_{01}\rangle}, \underbrace{\frac{1}{\sqrt{2}}(\vert{}01\rangle + \vert{}10\rangle)}_{\vert{}\Psi_{10}\rangle}, \underbrace{\frac{1}{\sqrt{2}}(\vert{}01\rangle - \vert{}10\rangle)}_{\vert{}\Psi_{11}\rangle} \right\}$$

### 5.2. Quantum Teleportation

Alice and Bob share an EPR pair. Alice wishes to transmit an unknown qubit state $\vert{}\psi\rangle = \alpha\vert{}0\rangle + \beta\vert{}1\rangle$ using only classical communication.

![Quantum Teleportation](/assets/img/image-6.png)

Initial composite state:

$$\vert{}\psi_0\rangle = \vert{}\psi\rangle\vert{}\beta_{00}\rangle = \frac{1}{\sqrt{2}} \left[ \alpha\vert{}0\rangle(\vert{}00\rangle + \vert{}11\rangle) + \beta\vert{}1\rangle(\vert{}00\rangle + \vert{}11\rangle) \right]$$

After Alice applies a CNOT gate:

$$\vert{}\psi_1\rangle = \frac{1}{\sqrt{2}} \left[ \alpha\vert{}0\rangle(\vert{}00\rangle + \vert{}11\rangle) + \beta\vert{}1\rangle(\vert{}10\rangle + \vert{}01\rangle) \right]$$

After Alice applies a Hadamard gate to her first qubit:

$$\vert{}\psi_2\rangle = \frac{1}{2} \Big[ \vert{}00\rangle (\alpha\vert{}0\rangle + \beta\vert{}1\rangle) + \vert{}01\rangle (\alpha\vert{}1\rangle + \beta\vert{}0\rangle) + \vert{}10\rangle (\alpha\vert{}0\rangle - \beta\vert{}1\rangle) + \vert{}11\rangle (\alpha\vert{}1\rangle - \beta\vert{}0\rangle) \Big]$$

| Alice's Measurement Outcome | Bob's Initial State ($\vert{}\psi_3\rangle$) | Applied Pauli Operator | Bob's Final State |
| :---: | :---: | :---: | :---: |
| **`00`** | $\alpha\vert{}0\rangle + \beta\vert{}1\rangle$ | $I$ (Identity) | $\alpha\vert{}0\rangle + \beta\vert{}1\rangle = \vert{}\psi\rangle$ |
| **`01`** | $\alpha\vert{}1\rangle + \beta\vert{}0\rangle$ | $X$ (Bit-flip) | $X(\alpha\vert{}1\rangle + \beta\vert{}0\rangle) = \alpha\vert{}0\rangle + \beta\vert{}1\rangle = \vert{}\psi\rangle$ |
| **`10`** | $\alpha\vert{}0\rangle - \beta\vert{}1\rangle$ | $Z$ (Phase-flip) | $Z(\alpha\vert{}0\rangle - \beta\vert{}1\rangle) = \alpha\vert{}0\rangle + \beta\vert{}1\rangle = \vert{}\psi\rangle$ |
| **`11`** | $\alpha\vert{}1\rangle - \beta\vert{}0\rangle$ | $ZX$ (Bit- & Phase-flip) | $ZX(\alpha\vert{}1\rangle - \beta\vert{}0\rangle) = \alpha\vert{}0\rangle + \beta\vert{}1\rangle = \vert{}\psi\rangle$ |

### 5.3. Application: Superdense Coding

By transmitting a single qubit, Alice can communicate two classical bits to Bob.

* Initial shared state:

$$\vert{}\psi\rangle = \frac{\vert{}00\rangle + \vert{}11\rangle}{\sqrt{2}}$$

* To send **00** (Apply $I$): $I\vert{}\psi\rangle = \frac{\vert{}00\rangle + \vert{}11\rangle}{\sqrt{2}}$
* To send **01** (Apply $Z$): $Z\vert{}\psi\rangle = \frac{\vert{}00\rangle - \vert{}11\rangle}{\sqrt{2}}$
* To send **10** (Apply $X$): $X\vert{}\psi\rangle = \frac{\vert{}10\rangle + \vert{}01\rangle}{\sqrt{2}}$
* To send **11** (Apply $iY$): $iY\vert{}\psi\rangle = \frac{\vert{}01\rangle - \vert{}10\rangle}{\sqrt{2}}$

---

## 6. Quantum Mixed States

### 6.1. Mixed States

A mixed state represents an ensemble comprising a statistical mixture of pure states $\{ (p_k, \vert{}\psi_k\rangle) \}$ with $\sum_k p_k = 1$.

### 6.2. Density Operator

When measuring an observable $\hat{A}$ in mixed states, the outcome can be calculated manually by combining classical statistical probability with quantum mechanics. The total probability of measuring the eigenvalue $\lambda_i$ (corresponding to the eigenstate $\vert{}u_i\rangle$) is:

$$P(\lambda_i) = \sum_n p_n P(\lambda_i\vert{}\psi_n) = \sum_n p_n \vert{}\langle u_i\vert{}\psi_n\rangle\vert{}^2 = \sum_n p_n \vert{}c_i\vert{}^2$$

When using the density operator $\hat{\rho} = \sum_n p_n \vert{}\psi_n\rangle\langle\psi_n\vert{}$, the entire calculation above is simplified into a single operation:

$$P(\lambda_i) = \langle u_i\vert{}\hat{\rho}\vert{}u_i\rangle$$

#### 6.2.1. Pure Quantum States

* Density Operator:

$$\hat{\rho} = \vert{}\psi\rangle \langle\psi\vert{}$$

The matrix elements $\rho_{ij}$ of the density operator $\hat{\rho}$ in the basis $\{\vert{}u_i\rangle\}$:

$$\rho_{ij} = \langle u_i \vert{} \hat{\rho} \vert{} u_j \rangle = \langle u_i \vert{} \Big( \vert{}\psi\rangle\langle\psi\vert{} \Big) \vert{} u_j \rangle = \langle u_i \vert{} \psi \rangle \langle \psi \vert{} u_j \rangle = c_i c_j^*$$

* Density Matrix Representation:

$$\hat{\rho} = \begin{pmatrix} c_1 c_1^* & c_1 c_2^* & \dots \\ c_2 c_1^* & c_2 c_2^* & \dots \\ \vdots & \vdots & \ddots \end{pmatrix} = \vert{}\psi\rangle \langle\psi\vert{}$$

* Unit Trace Condition:

$$\rho_{ii} = \vert{}c_i\vert{}^2$$

$$1 = \sum_i \vert{}c_i\vert{}^2 = \sum_i \rho_{ii} = \operatorname{Tr}(\hat{\rho})$$

$$1 = \langle\psi\vert{}\psi\rangle \iff 1 = \operatorname{Tr}(\hat{\rho})$$

#### 6.2.2. Mixed Quantum States

* Density Operator:

$$\hat{\rho} = \sum_k p_k \hat{\rho}_k = \sum_k p_k \vert{}\psi_k\rangle\langle\psi_k\vert{} \quad (p_k \ge 0, \, \sum_k p_k = 1)$$

* Matrix Elements: $\rho_{ij} = \sum_k p_k \langle u_i \vert{} \psi_k \rangle \langle \psi_k \vert{} u_j \rangle$

* Unit Trace Condition:

$$\operatorname{Tr}(\hat{\rho}) = \operatorname{Tr}\left( \sum_k p_k \hat{\rho}_k \right) = \sum_k p_k \underbrace{\operatorname{Tr}(\hat{\rho}_k)}_{= 1} = \sum_k p_k = 1$$

#### 6.2.3. Distinguishing state type

* **Pure state**:

$$\hat{\rho}_k^2 = \vert{}\psi\rangle \underbrace{\langle\psi\vert{}\psi\rangle}_{=1} \langle\psi\vert{} = \vert{}\psi\rangle\langle\psi\vert{} = \hat{\rho}_k$$

$$\operatorname{Tr}(\hat{\rho}_k^2) = 1$$

* **Mixed state**:

$$\begin{aligned} \hat{\rho}^2 &= \left(\sum_k p_k \hat{\rho}_k\right) \left(\sum_l p_l \hat{\rho}_l\right) = \sum_{k,l} p_k p_l \vert{}\psi_k\rangle \underbrace{\langle\psi_k\vert{}\psi_l\rangle}_{\delta_{kl}} \langle\psi_l\vert{} \\ &= \sum_k p_k^2 \vert{}\psi_k\rangle\langle\psi_k\vert{} = \sum_k p_k^2 \hat{\rho}_k \neq \hat{\rho} \end{aligned}$$

$$\operatorname{Tr}(\hat{\rho}^2) = \operatorname{Tr}\left(\sum_k p_k^2 \hat{\rho}_k\right) = \sum_k p_k^2 \underbrace{\operatorname{Tr}(\hat{\rho}_k)}_{= 1} = \sum_k p_k^2 < 1$$

Therefore: $\hat{\rho}^2 \neq \hat{\rho}$, $\operatorname{Tr}(\hat{\rho}^2) < 1$.

### 6.3. Partial Trace and Reduced Density Operator

Suppose we have physical systems $A$ and $B$, whose state is described by a density operator $\rho^{AB}$. The reduced density operator for system $A$ is defined by:

$$\rho^A \equiv \operatorname{tr}_B(\rho^{AB})$$

where $\operatorname{tr}_B$ is a map of operators known as the *partial trace* over system $B$. The partial trace is defined by:

$$\operatorname{tr}_B \left( \vert{}a_1\rangle\langle a_2\vert{} \otimes \vert{}b_1\rangle\langle b_2\vert{} \right) \equiv \vert{}a_1\rangle\langle a_2\vert{} \operatorname{tr}\left( \vert{}b_1\rangle\langle b_2\vert{} \right) \equiv \vert{}a_1\rangle\langle a_2\vert{} \langle b_2\vert{}b_1\rangle$$

where $\vert{}a_1\rangle$ and $\vert{}a_2\rangle$ are any two vectors in the state space of $A$, and $\vert{}b_1\rangle$ and $\vert{}b_2\rangle$ are any two vectors in the state space of $B$.

**Remark:**

$$\operatorname{tr}(\rho_A) = \operatorname{tr}_A(\operatorname{tr}_B(\rho_{AB})) = \operatorname{tr}_{AB}(\rho_{AB}) = 1$$

* $\rho_A$ contains all information accessible by measurements performed only on $A$.
* Information about correlations with $B$ is generally lost.

**Example:**

A less trivial example is the Bell state $(\vert{}00\rangle + \vert{}11\rangle)/\sqrt{2}$. This has density operator:

$$\rho = \left( \frac{\vert{}00\rangle + \vert{}11\rangle}{\sqrt{2}} \right) \left( \frac{\langle 00\vert{} + \langle 11\vert{}}{\sqrt{2}} \right) = \frac{\vert{}00\rangle\langle 00\vert{} + \vert{}11\rangle\langle 00\vert{} + \vert{}00\rangle\langle 11\vert{} + \vert{}11\rangle\langle 11\vert{}}{2}$$

Tracing out the second qubit, we find the reduced density operator of the first qubit:

$$\rho^1 = \operatorname{tr}_2(\rho) = \frac{\operatorname{tr}_2(\vert{}00\rangle\langle 00\vert{}) + \operatorname{tr}_2(\vert{}11\rangle\langle 00\vert{}) + \operatorname{tr}_2(\vert{}00\rangle\langle 11\vert{}) + \operatorname{tr}_2(\vert{}11\rangle\langle 11\vert{})}{2}$$

$$= \frac{\vert{}0\rangle\langle 0\vert{}\langle 0\vert{}0\rangle + \vert{}1\rangle\langle 0\vert{}\langle 0\vert{}1\rangle + \vert{}0\rangle\langle 1\vert{}\langle 1\vert{}0\rangle + \vert{}1\rangle\langle 1\vert{}\langle 1\vert{}1\rangle}{2} = \frac{\vert{}0\rangle\langle 0\vert{} + \vert{}1\rangle\langle 1\vert{}}{2} = \frac{I}{2}$$

Notice that this state $\rho^1$ is a *mixed state*, since $\operatorname{tr}((I/2)^2) = 1/2 < 1$.

### 6.4. Evolution and Measurements of Mixed States

#### 6.4.1. Evolution of Mixed States

The evolution of a closed quantum system is described by the unitary operator $U$. If the system was initially in the state $\vert{}\psi_i\rangle$ with probability $p_i$ then after the evolution has occurred the system will be in the state $U\vert{}\psi_i\rangle$ with probability $p_i$. Thus, the evolution of the density operator is described by the equation:

$$\rho = \sum_i p_i \vert{}\psi_i\rangle\langle\psi_i\vert{} \xrightarrow{U} \sum_i p_i U \vert{}\psi_i\rangle\langle\psi_i\vert{} U^\dagger = U \rho U^\dagger$$

#### 6.4.2. Measurements of Mixed States

**Postulate 3:** Quantum measurements are described by a collection $\{M_m\}$ of *measurement operators*. These are operators acting on the state space of the system being measured. The index $m$ refers to the measurement outcomes that may occur in the experiment. If the state of the quantum system is $\rho$ immediately before the measurement then the probability that result $m$ occurs is given by:

$$p(m) = \operatorname{tr}(M_m^\dagger M_m \rho)$$

and the state of the system after the measurement is:

$$\frac{M_m \rho M_m^\dagger}{\operatorname{tr}(M_m^\dagger M_m \rho)}$$

The measurement operators satisfy the *completeness equation*:

$$\sum_m M_m^\dagger M_m = I$$

##### 6.4.2.1. Projective measurement using density operator

* Properties of projective measurement:

$$P = \sum_{i=1}^{k} \vert{}\psi_i\rangle\langle\psi_i\vert{} \quad (\text{Degenerate Subspace})$$

$$\hat{P}_\psi = \vert{}\psi\rangle\langle\psi\vert{} \quad (\text{No Degeneracy})$$

* Idempotent:

$$\hat{P}_\psi^2 = (\vert{}\psi\rangle\langle\psi\vert{})(\vert{}\psi\rangle\langle\psi\vert{}) = \vert{}\psi\rangle \underbrace{(\langle\psi\vert{}\psi\rangle)}_{= 1} \langle\psi\vert{} = \vert{}\psi\rangle\langle\psi\vert{} = \hat{P}_\psi$$

* Hermitian:

$$\hat{P}_\psi^\dagger = (\vert{}\psi\rangle\langle\psi\vert{})^\dagger = \vert{}\psi\rangle\langle\psi\vert{} = \hat{P}_\psi$$

By substituting $M_m = P_m$ into the composite operator $M_m^\dagger M_m$, applying **Hermiticity** ($P_m^\dagger = P_m$) and **Idempotency** ($P_m^2 = P_m$):

$$M_m^\dagger M_m = P_m^\dagger P_m = P_m \cdot P_m = P_m^2 = P_m$$

Substituting $M_m^\dagger M_m = P_m$ into the **general probability formula** from Postulate 3:

$$p(m) = \operatorname{Tr}\left(M_m^\dagger M_m \rho\right) \xrightarrow{\quad M_m^\dagger M_m = P_m \quad} p(m) = \operatorname{Tr}\left(P_m \rho\right)$$

Substituting $M_m = P_m$ and $M_m^\dagger = P_m$ into the **state collapse formula**:

$$\rho' = \frac{M_m \rho M_m^\dagger}{\operatorname{Tr}\left(M_m^\dagger M_m \rho\right)} = \frac{P_m \rho P_m^\dagger}{\operatorname{Tr}\left(P_m \rho\right)} = \frac{P_m \rho P_m}{\operatorname{Tr}\left(P_m \rho\right)}$$

Substituting $M_m^\dagger M_m = P_m$ into the **general completeness condition**:

$$\sum_m M_m^\dagger M_m = I \xrightarrow{\quad M_m^\dagger M_m = P_m \quad} \sum_m P_m = I$$