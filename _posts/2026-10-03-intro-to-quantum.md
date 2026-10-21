---
title: Introduction to Quantum Cryptography
date: 2026-10-03 21:30:00 +0700
categories: [Cryptography, Security]
tags: [Quantum]
math: true
---

## 1. Quantum bits

### 1.1. Quantum bits

- **Hilbert space:** is a vector space (typically defined over the complex numbers), equipped with an inner product. This implies that quantum states are represented as vectors.  

- The elementary Hilbert space used in quantum information is the qubit space, which is a complex Hilbert space of dimension 2. Suppose $|0\rangle$ and $|1\rangle$ form an orthonormal basis for that state space. Then an arbitrary state vector in the state space can be written:

$$|\psi\rangle = \begin{pmatrix} \alpha \\ \beta \end{pmatrix} = \alpha|0\rangle + \beta|1\rangle$$

with $\alpha$ and $\beta$ being complex numbers ($|\alpha|^2 + |\beta|^2 = 1$), where:

$$|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$$

- The states $|0\rangle$ and $|1\rangle$ are analogous to the two values 0 and 1 which a bit may take. The way a qubit differs from a bit is that superpositions of these two states, of the form $\alpha |0\rangle + \beta |1\rangle$, can also exist, in which it is not possible to say that the qubit is definitely in the state $|0\rangle$, or definitely in the state $|1\rangle$.

- A qubit’s state is a unit vector in a two-dimensional complex vector space and is normalized to length 1. 

![Qubit Bases](/assets/img/quantum_bits.jpg)

- **Hadamard basis:**

$$|+\rangle = \begin{pmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{pmatrix} = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$$

$$|-\rangle = \begin{pmatrix} \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} \end{pmatrix} = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$$

- Measuring a qubit we get either the result 0, with probability $|\alpha|^2$, or the result 1, with probability $|\beta|^2$ (Quantum Measurement).

### 1.2 Multiple qubits

#### 1.2.1. Dirac notation

- **Ket (column vector):**

$$|\psi\rangle = \begin{pmatrix} a_1 \\ a_2 \\ \dots \\ a_m \end{pmatrix} \qquad |\varphi\rangle = \begin{pmatrix} b_1 \\ b_2 \\ \dots \\ b_m \end{pmatrix}$$

- **Bra (row vector):**

$$\langle\psi| = (a_1^* \quad a_2^* \quad \dots \quad a_m^*)$$

$$\langle\varphi| = (b_1^* \quad b_2^* \quad \dots \quad b_m^*)$$

- **Bra-ket: inner product (complex number):**

$$\langle\varphi|\psi\rangle = (b_1^* \quad b_2^* \quad \dots \quad b_m^*) \begin{pmatrix} a_1 \\ a_2 \\ \dots \\ a_m \end{pmatrix} = \sum_{i \in [m]} b_i^* a_i \in \mathbb{C}$$

- **Ket-bra: outer product (complex matrix):**

$$|\varphi\rangle\langle\psi| = \begin{pmatrix} b_1 \\ b_2 \\ \dots \\ b_m \end{pmatrix} (a_1^* \quad a_2^* \quad \dots \quad a_m^*) = \begin{pmatrix}  b_1 a_1^* & b_1 a_2^* & \dots & b_1 a_m^* \\  b_2 a_1^* & b_2 a_2^* & \dots & b_2 a_m^* \\  \dots & \dots & \dots & \dots \\  b_m a_1^* & b_m a_2^* & \dots & b_m a_m^*  \end{pmatrix} \in \mathbb{C}^{m \times m}$$

- **Tensor product (Kronecker product):**

$$A \otimes B \equiv \left. \overbrace{\begin{bmatrix} A_{11}B & A_{12}B & \dots & A_{1n}B \\ A_{21}B & A_{22}B & \dots & A_{2n}B \\ \vdots & \vdots & \vdots & \vdots \\ A_{m1}B & A_{m2}B & \dots & A_{mn}B \end{bmatrix}}^{nq} \right\} mp$$

#### 1.2.2. Multiple qubits

- **Postulate:** The state space of a composite physical system is the tensor product of the state spaces of the component physical systems. 

With $n$ qubits:

$$\mathcal{H}_{\text{n-qubits}} = \mathcal{H}_1 \otimes \mathcal{H}_2 \otimes \dots \otimes \mathcal{H}_n$$

$$\implies \text{Dim}(\mathcal{H}_{\text{n-qubits}}) = \text{Dim}(\mathcal{H}_1) \times \text{Dim}(\mathcal{H}_2) \times \dots \times \text{Dim}(\mathcal{H}_n)$$

$$\implies \text{Dim}(\mathcal{H}_{\text{n-qubits}}) = \text{Dim}(\mathbb{C}^2) \times \text{Dim}(\mathbb{C}^2) \times \dots \times \text{Dim}(\mathbb{C}^2)$$

$$= \underbrace{2 \times 2 \times \dots \times 2}_{n \text{ times}} = 2^n$$

---

## 2. Evolution of Quantum States

### 2.1. Theoretical Foundation

- **Schrödinger Equation:** The continuous time evolution of a closed quantum system is governed by:

$$i\hbar \frac{\partial}{\partial t} |\psi\rangle = \hat{H}|\psi\rangle$$

- **Unitary Operator:** In quantum information, state evolution is represented discretely by a unitary operator $U$ (quantum gate).

- **Unitary Condition:**

$$U U^\dagger = U^\dagger U = I \quad \implies \quad U^\dagger = U^{-1}$$

### 2.2. Quantum Unitaries

#### Unitary Operator in Probability Conservation

Consider an $N$-dimensional Hilbert space $\mathcal{H}$ with *Arbitrary orthonormal basis* $\{|e_1\rangle, |e_2\rangle, \dots, |e_N\rangle\}$ satisfying *Completeness relation:* $\sum_{i=1}^{N} |e_i\rangle\langle e_i| = I$.

Representation of an arbitrary state vector $|\psi\rangle \in \mathcal{H}$ with the probability of obtaining outcome $i$ when measuring in the basis $\{|e_i\rangle\}$ is $p(i) = |c_i|^2$.

$$|\psi\rangle = \sum_{i=1}^{N} c_i |e_i\rangle \quad (c_i \in \mathbb{C})$$

*Calculation of the norm squared* $\langle\psi|\psi\rangle$:

$$\langle\psi|\psi\rangle = \left(\sum_{i=1}^{N} c_i^* \langle e_i|\right) \left(\sum_{j=1}^{N} c_j |e_j\rangle\right) = \sum_{i=1}^{N} \sum_{j=1}^{N} c_i^* c_j \underbrace{\langle e_i | e_j \rangle}_{\delta_{ij}}$$

$$\langle\psi|\psi\rangle = \sum_{i=1}^{N} c_i^* c_i = \sum_{i=1}^{N} |c_i|^2 = \sum_{i=1}^{N} p(i) = 1$$

*Consider an $N \times N$ unitary operator $U$ satisfying $U^\dagger U = U U^\dagger = I$.*

When $U$ acts on the state $|\psi\rangle$, the system transitions to a new state $|\psi'\rangle = U|\psi\rangle$.

Expressing $|\psi'\rangle$ in the same basis $\{|e_i\rangle\}$ as $|\psi'\rangle = \sum_{i=1}^{N} c'_i |e_i\rangle$:

$$\langle\psi'|\psi'\rangle = (U|\psi\rangle)^\dagger (U|\psi\rangle) = \langle\psi| U^\dagger U |\psi\rangle = \langle\psi| I |\psi\rangle = \langle\psi|\psi\rangle = 1$$

#### Unitary operator in Reversibility & Information Conservation

For a unitary matrix, we always have $U^{-1} = U^\dagger$. This guarantees that all quantum gates (such as $X$, $Z$, and $H$) are fully reversible without any loss of information:

$$U^\dagger(U|\psi\rangle) = (U^\dagger U)|\psi\rangle = I|\psi\rangle = |\psi\rangle$$

#### 2.2.1. Pauli-X Gate (Bit-Flip)

The $X$ gate acts as the quantum NOT operation in the computational basis, flipping $|0\rangle \leftrightarrow |1\rangle$:

$$X = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$$

Action on basis states:

$$X|0\rangle = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}\begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 0 \\ 1 \end{pmatrix} = |1\rangle \quad \text{and} \quad X|1\rangle = |0\rangle$$

#### 2.2.2 Pauli-Z Gate (Phase-Flip)

The $Z$ gate is the NOT operation in the Hadamard basis. It leaves $|0\rangle$ unchanged and flips the phase of $|1\rangle$:

$$Z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$$

Action on basis states:

$$Z|0\rangle = |0\rangle \quad \text{and} \quad Z|1\rangle = -|1\rangle$$

$$Z|+\rangle = Z \left( \frac{|0\rangle + |1\rangle}{\sqrt{2}} \right) = \frac{Z|0\rangle + Z|1\rangle}{\sqrt{2}} = \frac{|0\rangle - |1\rangle}{\sqrt{2}} = |-\rangle$$

$$Z|-\rangle = Z \left( \frac{|0\rangle - |1\rangle}{\sqrt{2}} \right) = \frac{Z|0\rangle - Z|1\rangle}{\sqrt{2}} = \frac{|0\rangle - (-|1\rangle)}{\sqrt{2}} = \frac{|0\rangle + |1\rangle}{\sqrt{2}} = |+\rangle$$

Eigenvectors: $\{|0\rangle, |1\rangle\}$ are the eigenvectors of $Z$ corresponding to eigenvalues $+1$ and $-1$, respectively, so the computational basis is also referred to as the **$Z$-basis**.

#### 2.2.3. Hadamard Gate $H$ (Basis Switch)

The $H$ gate transforms states between the computational basis ($Z$-basis) and the Hadamard basis ($X$-basis) in both directions:

$$H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}$$

- Moving from $Z$-basis to $X$-basis:

$$H|0\rangle = |+\rangle \quad \text{and} \quad H|1\rangle = |-\rangle$$

- Moving from $X$-basis back to $Z$-basis:

$$H|+\rangle = |0\rangle \quad \text{and} \quad H|-\rangle = |1\rangle$$

---

## 3. Quantum Circuit

### 3.1. Composing Unitaries

- The circuit is read from left to right. Each line in the circuit represents a wire in the quantum circuit.
- **Multi-Qubit Operator Representation in Quantum Circuits:** Unitary operators $U$ act on the state vector $|\Psi\rangle$ from **right to left** via operator composition:

$$|\Psi_{\text{out}}\rangle = U_3 \cdot U_2 \cdot U_1 |\Psi_{\text{in}}\rangle$$

*(Note: The gate layer executed earliest on the far left appears adjacent to the initial state vector).*

- If a wire does not contain a gate at a given time step, it corresponds to the *Identity operator $I$*—leaving the state of that qubit unchanged.
  - *To be more specific:* If a single-qubit gate $A$ acts on the first qubit while the second qubit remains unacted upon, the global operator acting on the composite system is given by $A \otimes I$.
- When multiple gates act in parallel on distinct wires (qubits) at the same time step, the overall global operator is given by the tensor product of the individual gates.

![Quantum Circuit Operators](/assets/img/image-1.png)

- **The Controlled-NOT Gate (CNOT):** If Qubit 1 is in state $|1\rangle$, flip Qubit 2; if Qubit 1 is in state $|0\rangle$, leave Qubit 2 unchanged.

![CNOT Gate](/assets/img/quantum_NoT.jpg)
![Quantum Circuit](/assets/img/quantum_circuit.jpg)

### 3.2. Application in Circuit Reading Comprehension

![Circuit Reading Example](/assets/img/image-4.png)

- **Initial state:**

$$|\Psi_{\text{in}}\rangle = |\varphi\rangle \otimes |+\rangle \otimes |0\rangle \otimes |0\rangle \otimes |\psi\rangle \equiv |\varphi\rangle |+\rangle |00\rangle |\psi\rangle$$

- **Time step 1:**
  - Wires 1 & 2: Controlled-$G_2$ gate with Wire 1 as control $\rightarrow c(G_2)$
  - Wire 3: Single-qubit gate $G_1$
  - Wires 4 & 5: Idle wires $\rightarrow I_4 \otimes I_5 \equiv I_{45}$

$$U_1 = c(G_2) \otimes G_1 \otimes I_{45}$$

- **Time step 2:**
  - Wires 1, 2 & 3: 3-qubit gate $G_3$
  - Wires 4 & 5: Idle wires $\rightarrow I_{45}$

$$U_2 = G_3 \otimes I_{45}$$

- **Time step 3:**
  - Wire 1: Single-qubit gate $G_2$
  - Wire 2: Idle wire $\rightarrow I$
  - Wires 3 & 4: CNOT gate ($c(X)$) with Wire 3 as control and Wire 4 as target
  - Wire 5: Single-qubit gate $G_1$

$$U_3 = G_2 \otimes I \otimes c(X) \otimes G_1$$

$$\implies U = (G_2 \otimes I \otimes c(X) \otimes G_1)(G_3 \otimes I_{45})(c(G_2) \otimes G_1 \otimes I_{45})|\varphi\rangle|+\rangle|00\rangle|\psi\rangle$$

## 4. Quantum Measurement

Unlike classical physics, quantum mechanics cannot predict the exact outcome of a measurement. Instead, it determines the exact probability distribution of all possible outcomes.

### 4.1. Measure $\hat{A}$ in State $|\psi\rangle$ (No Degeneracy)

Eigenvalues and eigenvectors:

$$\text{Physical quantity } A \longrightarrow \text{Observable } \hat{A}$$

$$\hat{A} |u_n\rangle = \lambda_n |u_n\rangle$$

- **Postulate III:** The result of a measurement of a physical quantity is one of the eigenvalues of the associated observable.
- **Postulate IV:** The measurement of $A$ in a system in normalized state $|\psi\rangle$ gives eigenvalue $\lambda_n$ with probability:

$$P(\lambda_n) = |\langle u_n | \psi \rangle|^2$$

Having a quantum state prepared in a superposition:

$$|\psi\rangle = c_1|u_1\rangle + c_2|u_2\rangle + \dots + c_n|u_n\rangle = \sum_{i} c_i|u_i\rangle \quad \text{where } c_i = \langle u_i | \psi \rangle$$

Constructing a projection operator $P_n = |u_n\rangle\langle u_n|$ to project $|\psi\rangle$ onto the subspace spanned by $|u_n\rangle$:

$$P_n |\psi\rangle = c_n |u_n\rangle$$

The measurement probability $P(\lambda_n)$ is:

$$P(\lambda_n) = |\langle u_n | \psi \rangle|^2 = |c_n|^2$$

### 4.2. Measure $\hat{A}$ in State $|\psi\rangle$ (With Degeneracy)

Degenerate eigenvalues:

$$\hat{A} |u_n^i\rangle = \lambda_n |u_n^i\rangle \quad \text{for } i = 1, 2, \dots, g_n$$

The measurement of $A$ in a system in normalized state $|\psi\rangle$ gives eigenvalue $\lambda_n$ (with degeneracy $g_n$) with probability:

$$P(\lambda_n) = \sum_{i=1}^{g_n} |\langle u_n^i | \psi \rangle|^2$$

Superposition state:

$$|\psi\rangle = \sum_n \sum_{i=1}^{g_n} c_n^i |u_n^i\rangle \quad \text{where } c_n^i = \langle u_n^i | \psi \rangle$$

Projection operator $P_n = \sum_{i=1}^{g_n} |u_n^i\rangle\langle u_n^i|$:

$$P_n |\psi\rangle = \sum_{i=1}^{g_n} c_n^i |u_n^i\rangle$$

Measurement probability:

$$P(\lambda_n) = \langle\psi| P_n |\psi\rangle = \sum_{i=1}^{g_n} |\langle u_n^i | \psi \rangle|^2 = \sum_{i=1}^{g_n} |c_n^i|^2$$

### 4.3. Partial Measurement on Composite Systems

In multi-qubit systems, a **partial measurement** involves performing a projective measurement on a specific subset of qubits while leaving the remaining subsystem unmeasured.

#### 4.3.1. Formulation

Consider an $n$-qubit state expressed in the computational basis:

$$|\psi\rangle = \sum_{i \in \{0,1\}^n} \alpha_i |i\rangle = \sum_{b \in \{0,1\}} \sum_{j \in \{0,1\}^{n-1}} \alpha_{bj} |b\rangle \otimes |j\rangle$$

When measuring only the **first qubit** in the computational basis:

- **Outcome Probability $p_b$:**

$$p_b = \sum_{j \in \{0,1\}^{n-1}} |\alpha_{bj}|^2$$

- **State Collapse:**

$$|\psi'\rangle = \frac{1}{\sqrt{p_b}} \sum_{j \in \{0,1\}^{n-1}} \alpha_{bj} |bj\rangle$$

#### 4.3.2. Worked Example

Consider a 2-qubit state $|\psi\rangle = \frac{1}{\sqrt{3}}(|00\rangle + |01\rangle + |10\rangle)$. Measuring the first qubit in the computational basis yields:

- **Outcome $b = 0$:**
  - Probability: $p_0 = \left|\frac{1}{\sqrt{3}}\right|^2 + \left|\frac{1}{\sqrt{3}}\right|^2 = \frac{2}{3}$
  - Post-Measurement State:

$$|\psi'\rangle = \frac{1}{\sqrt{2/3}} \left( \frac{1}{\sqrt{3}}|00\rangle + \frac{1}{\sqrt{3}}|01\rangle \right) = \frac{1}{\sqrt{2}}(|00\rangle + |01\rangle)$$

- **Outcome $b = 1$:**
  - Probability: $p_1 = \left|\frac{1}{\sqrt{3}}\right|^2 = \frac{1}{3}$
  - Post-Measurement State:

$$|\psi'\rangle = \frac{1}{\sqrt{1/3}} \left( \frac{1}{\sqrt{3}}|10\rangle \right) = |10\rangle$$

### 4.4. Projective Measurements on Pure States

A projective measurement is defined by a set of Hermitian projection operators $\{\Pi_1, \Pi_2, \dots, \Pi_k\}$ satisfying $\sum_{i=1}^k \Pi_i = I$.

When measuring a pure state $|\psi\rangle$:

- **Outcome Probability:**

$$P(i) = |\Pi_i |\psi\rangle|^2 = \langle\psi| \Pi_i |\psi\rangle$$

- **State Collapse:**

$$|\psi'\rangle = \frac{\Pi_i |\psi\rangle}{|\Pi_i |\psi\rangle|}$$

**State collapse ensure probability normalisation:**

$$\langle\psi'|\psi'\rangle = \left(\frac{\Pi_i|\psi\rangle}{|\Pi_i|\psi\rangle|}\right)^\dagger \left(\frac{\Pi_i|\psi\rangle}{|\Pi_i|\psi\rangle|}\right) = \frac{\langle\psi|\Pi_i^\dagger \Pi_i|\psi\rangle}{|\Pi_i|\psi\rangle|^2}$$

Applying the **Hermiticity** and **Idempotency** properties of the **Projection Operator** $\Pi_i$, we have:

$$\Pi_i^\dagger \Pi_i = \Pi_i \cdot \Pi_i = \Pi_i^2 = \Pi_i$$

Substituting into the numerator:

$$\langle\psi|\Pi_i^\dagger \Pi_i|\psi\rangle = \langle\psi|\Pi_i|\psi\rangle = |\Pi_i|\psi\rangle|^2 = P(i)$$

Thus:

$$\langle\psi'|\psi'\rangle = \frac{|\Pi_i|\psi\rangle|^2}{|\Pi_i|\psi\rangle|^2} = \frac{P(i)}{P(i)} = 1$$

#### 4.4.1. Non - Degenerate Measurement

1. **Outcome Probability $P(\lambda_n)$:**
   Substitute $\Pi_n = |u_n\rangle\langle u_n|$ into $P(n) = \langle\psi|\Pi_n|\psi\rangle$:

   $$P(\lambda_n) = \langle\psi|(|u_n\rangle\langle u_n|)|\psi\rangle = \langle\psi|u_n\rangle\langle u_n|\psi\rangle = c_n^* c_n = |c_n|^2 = |\langle u_n|\psi\rangle|^2$$

2. **State Collapse $|\psi'\rangle$:**

   $$\Pi_n|\psi\rangle = P_n|\psi\rangle = |u_n\rangle\langle u_n|\psi\rangle = c_n|u_n\rangle$$

   Substitute $P_n|\psi\rangle$ and $\sqrt{P(\lambda_n)} = |c_n|$ into the collapse formula:

   $$|\psi'\rangle = \frac{P_n|\psi\rangle}{\sqrt{P(\lambda_n)}} = \frac{c_n|u_n\rangle}{|c_n|} = \left(\frac{c_n}{|c_n|}\right)|u_n\rangle = e^{i\phi}|u_n\rangle \equiv |u_n\rangle$$

#### 4.4.2. Degenerate Measurement

1. **Outcome Probability $P(\lambda_n)$:**
   Substitute $\Pi_n = \sum_{i=1}^{g_n} |u_n^i\rangle\langle u_n^i|$ into $P(n) = \langle\psi|\Pi_n|\psi\rangle$:

   $$P(\lambda_n) = \left\langle\psi\left|\left(\sum_{i=1}^{g_n} |u_n^i\rangle\langle u_n^i|\right)\right|\psi\right\rangle = \sum_{i=1}^{g_n} \langle\psi|u_n^i\rangle\langle u_n^i|\psi\rangle = \sum_{i=1}^{g_n} |c_n^i|^2$$

2. **State Collapse $|\psi'\rangle$:**

   $$\Pi_n|\psi\rangle = P_n|\psi\rangle = \sum_{i=1}^{g_n} |u_n^i\rangle\langle u_n^i|\psi\rangle = \sum_{i=1}^{g_n} c_n^i |u_n^i\rangle$$

   Substitute into collapse formula with $\sqrt{P(\lambda_n)} = \sqrt{\sum_{i=1}^{g_n} |c_n^i|^2}$:

   $$|\psi'\rangle = \frac{P_n|\psi\rangle}{\sqrt{P(\lambda_n)}} = \frac{1}{\sqrt{\sum_{i=1}^{g_n} |c_n^i|^2}} \sum_{i=1}^{g_n} c_n^i |u_n^i\rangle$$

---

## 5. Quantum Entanglement

A bipartite state $|\psi\rangle_{AB}$ is a **product state** if there exist $|\psi_1\rangle_A$ and $|\psi_2\rangle_B$ such that:

$$|\psi\rangle_{AB} = |\psi_1\rangle_A \otimes |\psi_2\rangle_B$$

If a quantum state cannot be written as a product state, it is **entangled**.

Example ($W$-state):

$$W_n = \frac{1}{\sqrt{n}}(|10\dots0\rangle + |01\dots0\rangle + \dots + |00\dots1\rangle)$$

### 5.1. Bell State

Bell states are generated via a quantum circuit consisting of a Hadamard gate ($H$) and a Controlled-NOT gate (CNOT).

![Bell Circuit](/assets/img/image-5.png)

Bell basis states:

$$\left\{ \underbrace{\frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)}_{|\Psi_{00}\rangle \text{ (EPR pair)}}, \underbrace{\frac{1}{\sqrt{2}}(|00\rangle - |11\rangle)}_{|\Psi_{01}\rangle}, \underbrace{\frac{1}{\sqrt{2}}(|01\rangle + |10\rangle)}_{|\Psi_{10}\rangle}, \underbrace{\frac{1}{\sqrt{2}}(|01\rangle - |10\rangle)}_{|\Psi_{11}\rangle} \right\}$$

### 5.2. Quantum Teleportation

Alice and Bob share an EPR pair. Alice wishes to transmit an unknown qubit state $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ using only classical communication.

![Quantum Teleportation](/assets/img/image-6.png)

Initial composite state:

$$|\psi_0\rangle = |\psi\rangle|\beta_{00}\rangle = \frac{1}{\sqrt{2}} \left[ \alpha|0\rangle(|00\rangle + |11\rangle) + \beta|1\rangle(|00\rangle + |11\rangle) \right]$$

After Alice applies a CNOT gate:

$$|\psi_1\rangle = \frac{1}{\sqrt{2}} \left[ \alpha|0\rangle(|00\rangle + |11\rangle) + \beta|1\rangle(|10\rangle + |01\rangle) \right]$$

After Alice applies a Hadamard gate to her first qubit:

$$|\psi_2\rangle = \frac{1}{2} \Big[ |00\rangle (\alpha|0\rangle + \beta|1\rangle) + |01\rangle (\alpha|1\rangle + \beta|0\rangle) + |10\rangle (\alpha|0\rangle - \beta|1\rangle) + |11\rangle (\alpha|1\rangle - \beta|0\rangle) \Big]$$

| Alice's Measurement Outcome | Bob's Initial State ($|\psi_3\rangle$) | Applied Pauli Operator | Bob's Final State |
| :---: | :---: | :---: | :---: |
| **`00`** | $\alpha|0\rangle + \beta|1\rangle$ | $I$ (Identity) | $\alpha|0\rangle + \beta|1\rangle = |\psi\rangle$ |
| **`01`** | $\alpha|1\rangle + \beta|0\rangle$ | $X$ (Bit-flip) | $X(\alpha|1\rangle + \beta|0\rangle) = \alpha|0\rangle + \beta|1\rangle = |\psi\rangle$ |
| **`10`** | $\alpha|0\rangle - \beta|1\rangle$ | $Z$ (Phase-flip) | $Z(\alpha|0\rangle - \beta|1\rangle) = \alpha|0\rangle + \beta|1\rangle = |\psi\rangle$ |
| **`11`** | $\alpha|1\rangle - \beta|0\rangle$ | $ZX$ (Bit- & Phase-flip) | $ZX(\alpha|1\rangle - \beta|0\rangle) = \alpha|0\rangle + \beta|1\rangle = |\psi\rangle$ |

### 5.3. Application: Superdense Coding

By transmitting a single qubit, Alice can communicate two classical bits to Bob.

- Initial shared state:

$$|\psi\rangle = \frac{|00\rangle + |11\rangle}{\sqrt{2}}$$

- To send **00** (Apply $I$): $I|\psi\rangle = \frac{|00\rangle + |11\rangle}{\sqrt{2}}$
- To send **01** (Apply $Z$): $Z|\psi\rangle = \frac{|00\rangle - |11\rangle}{\sqrt{2}}$
- To send **10** (Apply $X$): $X|\psi\rangle = \frac{|10\rangle + |01\rangle}{\sqrt{2}}$
- To send **11** (Apply $iY$): $iY|\psi\rangle = \frac{|01\rangle - |10\rangle}{\sqrt{2}}$

---

## 6. Quantum Mixed States

### 6.1. Mixed States

A mixed state represents an ensemble comprising a statistical mixture of pure states $\{ (p_k, |\psi_k\rangle) \}$ with $\sum_k p_k = 1$.

### 6.2. Density Operator

When measuring an observable $\hat{A}$ in mixed states, the outcome can be calculated manually by combining classical statistical probability with quantum mechanics. The total probability of measuring the eigenvalue $\lambda_i$ (corresponding to the eigenstate $|u_i\rangle$) is:

$$P(\lambda_i) = \sum_n p_n P(\lambda_i|\psi_n) = \sum_n p_n |\langle u_i|\psi_n\rangle|^2 = \sum_n p_n |c_i|^2$$

When using the density operator $\hat{\rho} = \sum_n p_n |\psi_n\rangle\langle\psi_n|$, the entire calculation above is simplified into a single operation:

$$P(\lambda_i) = \langle u_i|\hat{\rho}|u_i\rangle$$

#### 6.2.1. Pure Quantum States

- Density Operator:
$$\hat{\rho} = |\psi\rangle \langle\psi|$$

The matrix elements $\rho_{ij}$ of the density operator $\hat{\rho}$ in the basis $\{|u_i\rangle\}$:

$$\rho_{ij} = \langle u_i | \hat{\rho} | u_j \rangle = \langle u_i | \Big( |\psi\rangle\langle\psi| \Big) | u_j \rangle = \langle u_i | \psi \rangle \langle \psi | u_j \rangle = c_i c_j^*$$

- Density Matrix Representation:
$$\hat{\rho} = \begin{pmatrix} c_1 c_1^* & c_1 c_2^* & \dots \\ c_2 c_1^* & c_2 c_2^* & \dots \\ \vdots & \vdots & \ddots \end{pmatrix} = |\psi\rangle \langle\psi|$$

- Unit Trace Condition:
$$\rho_{ii} = |c_i|^2$$

$$1 = \sum_i |c_i|^2 = \sum_i \rho_{ii} = \operatorname{Tr}(\hat{\rho})$$

$$1 = \langle\psi|\psi\rangle \iff 1 = \operatorname{Tr}(\hat{\rho})$$

#### 6.2.2. Mixed Quantum States

- Density Operator:
$$\hat{\rho} = \sum_k p_k \hat{\rho}_k = \sum_k p_k |\psi_k\rangle\langle\psi_k| \quad (p_k \ge 0, \, \sum_k p_k = 1)$$

- Matrix Elements: $\rho_{ij} = \sum_k p_k \langle u_i | \psi_k \rangle \langle \psi_k | u_j \rangle$

- Unit Trace Condition:
$$\operatorname{Tr}(\hat{\rho}) = \operatorname{Tr}\left( \sum_k p_k \hat{\rho}_k \right) = \sum_k p_k \underbrace{\operatorname{Tr}(\hat{\rho}_k)}_{= 1} = \sum_k p_k = 1$$

#### 6.2.3. Distinguishing state type:

- **Pure state**: 
$$\hat{\rho}_k^2 = |\psi\rangle \underbrace{\langle\psi|\psi\rangle}_{=1} \langle\psi| = |\psi\rangle\langle\psi| = \hat{\rho}_k$$

$$\operatorname{Tr}(\hat{\rho}_k^2) = 1$$

- **Mixed state**: 

$$\begin{aligned} \hat{\rho}^2 &= \left(\sum_k p_k \hat{\rho}_k\right) \left(\sum_l p_l \hat{\rho}_l\right) = \sum_{k,l} p_k p_l |\psi_k\rangle \underbrace{\langle\psi_k|\psi_l\rangle}_{\delta_{kl}} \langle\psi_l| \\ &= \sum_k p_k^2 |\psi_k\rangle\langle\psi_k| = \sum_k p_k^2 \hat{\rho}_k \neq \hat{\rho} \end{aligned}$$

$$\operatorname{Tr}(\hat{\rho}^2) = \operatorname{Tr}\left(\sum_k p_k^2 \hat{\rho}_k\right) = \sum_k p_k^2 \underbrace{\operatorname{Tr}(\hat{\rho}_k)}_{= 1} = \sum_k p_k^2 < 1$$

Therefore: $\hat{\rho}^2 \neq \hat{\rho}$, $\operatorname{Tr}(\hat{\rho}^2) < 1$.

### 6.3. Partial Trace and Reduced Density Operator

Suppose we have physical systems $A$ and $B$, whose state is described by a density operator $\rho^{AB}$. The reduced density operator for system $A$ is defined by:

$$\rho^A \equiv \operatorname{tr}_B(\rho^{AB})$$

where $\operatorname{tr}_B$ is a map of operators known as the *partial trace* over system $B$. The partial trace is defined by:

$$\operatorname{tr}_B \left( |a_1\rangle\langle a_2| \otimes |b_1\rangle\langle b_2| \right) \equiv |a_1\rangle\langle a_2| \operatorname{tr}\left( |b_1\rangle\langle b_2| \right) \equiv |a_1\rangle\langle a_2| \langle b_2|b_1\rangle$$

where $|a_1\rangle$ and $|a_2\rangle$ are any two vectors in the state space of $A$, and $|b_1\rangle$ and $|b_2\rangle$ are any two vectors in the state space of $B$.

**Remark:**
* $\operatorname{tr}(\rho_A) = \operatorname{tr}_A(\operatorname{tr}_B(\rho_{AB})) = \operatorname{tr}_{AB}(\rho_{AB}) = 1$
* $\rho_A$ contains all information accessible by measurements performed only on $A$.
* Information about correlations with $B$ is generally lost.

**Example:**

A less trivial example is the Bell state $(|00\rangle + |11\rangle)/\sqrt{2}$. This has density operator:

$$\rho = \left( \frac{|00\rangle + |11\rangle}{\sqrt{2}} \right) \left( \frac{\langle 00| + \langle 11|}{\sqrt{2}} \right) = \frac{|00\rangle\langle 00| + |11\rangle\langle 00| + |00\rangle\langle 11| + |11\rangle\langle 11|}{2}$$

Tracing out the second qubit, we find the reduced density operator of the first qubit:

$$\rho^1 = \operatorname{tr}_2(\rho) = \frac{\operatorname{tr}_2(|00\rangle\langle 00|) + \operatorname{tr}_2(|11\rangle\langle 00|) + \operatorname{tr}_2(|00\rangle\langle 11|) + \operatorname{tr}_2(|11\rangle\langle 11|)}{2}$$

$$= \frac{|0\rangle\langle 0|\langle 0|0\rangle + |1\rangle\langle 0|\langle 0|1\rangle + |0\rangle\langle 1|\langle 1|0\rangle + |1\rangle\langle 1|\langle 1|1\rangle}{2} = \frac{|0\rangle\langle 0| + |1\rangle\langle 1|}{2} = \frac{I}{2}$$

Notice that this state $\rho^1$ is a *mixed state*, since $\operatorname{tr}((I/2)^2) = 1/2 < 1$.

### 6.4. Evolution and Measurements of Mixed States

#### 6.4.1. Evolution of Mixed States

The evolution of a closed quantum system is described by the unitary operator $U$. If the system was initially in the state $|\psi_i\rangle$ with probability $p_i$ then after the evolution has occurred the system will be in the state $U|\psi_i\rangle$ with probability $p_i$. Thus, the evolution of the density operator is described by the equation:

$$\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i| \xrightarrow{U} \sum_i p_i U |\psi_i\rangle\langle\psi_i| U^\dagger = U \rho U^\dagger$$

#### 6.4.2. Measurements of Mixed States

**Postulate 3:** Quantum measurements are described by a collection $\{M_m\}$ of *measurement operators*. These are operators acting on the state space of the system being measured. The index $m$ refers to the measurement outcomes that may occur in the experiment. If the state of the quantum system is $\rho$ immediately before the measurement then the probability that result $m$ occurs is given by:

$$p(m) = \operatorname{tr}(M_m^\dagger M_m \rho)$$

and the state of the system after the measurement is:

$$\frac{M_m \rho M_m^\dagger}{\operatorname{tr}(M_m^\dagger M_m \rho)}$$

The measurement operators satisfy the *completeness equation*:

$$\sum_m M_m^\dagger M_m = I$$

##### 6.4.2.1. Projective measurement using density operator

- Properties of projective measurement:

$$P = \sum_{i=1}^{k} |\psi_i\rangle\langle\psi_i| \quad (\text{Degenerate Subspace})$$

$$\hat{P}_\psi = |\psi\rangle\langle\psi| \quad (\text{No Degeneracy})$$

- Idempotent:

$$\hat{P}_\psi^2 = (|\psi\rangle\langle\psi|)(|\psi\rangle\langle\psi|) = |\psi\rangle \underbrace{(\langle\psi|\psi\rangle)}_{= 1} \langle\psi| = |\psi\rangle\langle\psi| = \hat{P}_\psi$$

- Hermitian:

$$\hat{P}_\psi^\dagger = (|\psi\rangle\langle\psi|)^\dagger = |\psi\rangle\langle\psi| = \hat{P}_\psi$$

By substituting $M_m = P_m$ into the composite operator $M_m^\dagger M_m$, applying **Hermiticity** ($P_m^\dagger = P_m$) and **Idempotency** ($P_m^2 = P_m$):

$$M_m^\dagger M_m = P_m^\dagger P_m = P_m \cdot P_m = P_m^2 = P_m$$

Substituting $M_m^\dagger M_m = P_m$ into the **general probability formula** from Postulate 3:

$$p(m) = \operatorname{Tr}\left(M_m^\dagger M_m \rho\right) \xrightarrow{\quad M_m^\dagger M_m = P_m \quad} p(m) = \operatorname{Tr}\left(P_m \rho\right)$$

Substituting $M_m = P_m$ and $M_m^\dagger = P_m$ into the **state collapse formula**:

$$\rho' = \frac{M_m \rho M_m^\dagger}{\operatorname{Tr}\left(M_m^\dagger M_m \rho\right)} = \frac{P_m \rho P_m^\dagger}{\operatorname{Tr}\left(P_m \rho\right)} = \frac{P_m \rho P_m}{\operatorname{Tr}\left(P_m \rho\right)}$$

Substituting $M_m^\dagger M_m = P_m$ into the **general completeness condition**:

$$\sum_m M_m^\dagger M_m = I \xrightarrow{\quad M_m^\dagger M_m = P_m \quad} \sum_m P_m = I$$