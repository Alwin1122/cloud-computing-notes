# Information Security Principles and Practices (23I702) — Unit 5 Notes

Exam-ready notes from **Unit 5.pptx** and **Post-Quantum Cryptography (PQC).pptx**.

**Syllabus line:** Digital Signature — Properties and requirements, ElGamal digital signature scheme, Schnorr digital signature scheme, Digital Signature Standard, Basics of Post-Quantum Cryptography. **(9)**

---

## Table of Contents

1. [Digital signatures — need and capabilities](#1-digital-signatures--need-and-capabilities)
2. [Digital signature model](#2-digital-signature-model)
3. [Attacks and forgeries](#3-attacks-and-forgeries)
4. [Digital signature requirements](#4-digital-signature-requirements)
5. [Direct digital signatures](#5-direct-digital-signatures)
6. [ElGamal digital signature scheme](#6-elgamal-digital-signature-scheme)
7. [Schnorr digital signature scheme](#7-schnorr-digital-signature-scheme)
8. [Digital Signature Standard (DSS) and DSA](#8-digital-signature-standard-dss-and-dsa)
9. [Post-Quantum Cryptography (PQC)](#9-post-quantum-cryptography-pqc)
10. [Quick exam pointers](#10-quick-exam-pointers)

---

## 1. Digital signatures — need and capabilities

**Message authentication** alone does not solve a **lack of trust** between parties (e.g. disputes about who sent what, or denial after the fact).

A **digital signature** adds capabilities beyond simple authentication:

| Capability | Meaning |
|---|---|
| Verify author | Confirms who signed |
| Verify date & time of signature | Supports non-repudiation / audit |
| Authenticate message contents | Detects tampering |
| Third-party verification | A judge/arbitrator can resolve disputes |

Digital signatures therefore include an authentication function **plus** non-repudiation and dispute resolution.

**Exam line (non-repudiation + anti-tampering):**

- **Non-repudiation:** Only the sender knows the **private key**, so a valid signature binds the sender to the message; the sender cannot later deny signing it.
- **Anti-tampering:** The signature is computed over the message (or its hash). Any change to the message makes verification fail.

---

## 2. Digital signature model

Typical flow:

1. Sender computes a **hash** of the message $`M`$: $`m = H(M)`$.
2. Sender **signs** the hash with the **private key** → signature $`S`$.
3. Message $`M`$ and signature $`S`$ are sent to the receiver.
4. Receiver recomputes $`H(M)`$ and **verifies** $`S`$ using the sender’s **public key**.
5. If verification succeeds, the message is authentic and untampered; the signer is accountable.

Signing the **hash** (not the full message) is efficient and is what schemes like ElGamal, Schnorr, and DSA use in practice.

---

## 3. Attacks and forgeries

### 3.1 Types of attacks (what the adversary knows / can ask for)

| Attack | Adversary capability |
|---|---|
| **Key-only attack** | Knows only A’s **public key** |
| **Known message attack** | Given a set of messages and their valid signatures |
| **Generic chosen message attack** | Chooses messages **before** breaking the scheme, independent of A’s public key; then obtains valid signatures for those messages |
| **Directed chosen message attack** | Like generic, but the message list is chosen **after** knowing A’s public key, **before** seeing signatures |
| **Adaptive chosen message attack** | Uses A as an **oracle** — can request signatures that depend on previously obtained message–signature pairs (strongest) |

### 3.2 Types of forgeries (what success means)

| Forgery | Meaning |
|---|---|
| **Total break** | Attacker recovers the **private key** and can sign anything |
| **Selective forgery** | Attacker forges a signature on a **specific** message chosen ahead of time |
| **Existential forgery** | Attacker produces a valid signature on **at least one** message (not necessarily meaningful or chosen in advance) |

A secure signature scheme should resist even existential forgery under adaptive chosen-message attacks (ideal security goal in theory).

---

## 4. Digital signature requirements

A digital signature **must**:

1. **Depend on the message signed** — different messages → different signatures.
2. **Use information unique to the sender** — prevents forgery and denial (private key).
3. Be **relatively easy to produce**.
4. Be **relatively easy to recognize and verify**.
5. Be **computationally infeasible to forge**:
   - create a new message for an existing signature, or
   - create a fraudulent signature for a given message.
6. Be **practical to store** (signature size manageable).

---

## 5. Direct digital signatures

- Involve **only sender and receiver** (no arbitrator).
- Receiver is assumed to have the sender’s **public key**.
- Signature is made by signing the **entire message or its hash** with the sender’s **private key**.
- Optionally encrypt with the receiver’s public key for confidentiality.
- **Important:** **sign first, then encrypt** the message and signature.
- Security depends on protection of the sender’s **private key**.

---

## 6. ElGamal digital signature scheme

### 6.1 Idea

- Signature variant of **ElGamal**, related to **Diffie–Hellman**.
- Uses **exponentiation in a finite field (Galois field)**.
- Security based on the difficulty of computing **discrete logarithms**.
- **Private key** used for signing; **public key** used for verification.

### 6.2 Key generation

Global / public parameters: prime $`q`$, primitive root $`a`$ of $`q`$.

Each user A:

1. Choose secret private key $`x_A`$ with $`1 < x_A < q - 1`$.
2. Compute public key $`y_A = a^{x_A} \bmod q`$.

Public values: $`(q, a, y_A)`$. Private: $`x_A`$.

### 6.3 Signing

Alice signs message $`M`$:

1. Compute hash $`m = H(M)`$ with $`0 \le m \le (q-1)`$.
2. Choose random $`K`$ with $`1 \le K \le (q-1)`$ and $`\gcd(K, q-1) = 1`$.
3. Compute $`S_1 = a^K \bmod q`$.
4. Compute $`K^{-1} \bmod (q-1)`$ (modular inverse of $`K`$).
5. Compute $`S_2 = K^{-1}(m - x_A S_1) \bmod (q-1)`$.
6. Signature is the pair $`(S_1, S_2)`$.

### 6.4 Verification

Any verifier B computes:


```math
V_1 = a^m \bmod q
```



```math
V_2 = (y_A^{S_1} \cdot S_1^{S_2}) \bmod q
```


Signature is **valid** if $`V_1 = V_2`$.

### 6.5 Worked example (from lecture slides)

Field $`\mathrm{GF}(19)`$: $`q = 19`$, $`a = 10`$.

**Key:** $`x_A = 16`$, so


```math
y_A = 10^{16} \bmod 19 = 4
```


**Sign** message with hash $`m = 14`$, choose $`K = 5`$ ($`\gcd(5,18)=1`$):


```math
S_1 = 10^5 \bmod 19 = 3
```



```math
K^{-1} \bmod 18 = 5^{-1} \bmod 18 = 11
```



```math
S_2 = 11(14 - 16 \cdot 3) \bmod 18 = 4
```


Signature = $`(3, 4)`$.

**Verify:**


```math
V_1 = 10^{14} \bmod 19 = 16
```



```math
V_2 = (4^3 \cdot 3^4) \bmod 19 = 16
```


Since $`V_1 = V_2`$, the signature is **valid**.

### 6.6 Exam-style problem (CAT-style)

**Given:** public parameters / key $`\{q, a, y_A\} = \{23, 5, 17\}`$, message $`m = 19`$, $`K = 13`$, private key $`x_A = 14`$. Check whether the signature verifies.

**Step 1 — Consistency of public key**


```math
y_A \stackrel{?}{=} 5^{14} \bmod 23 = 13
```


The correctly computed public key from $`x_A = 14`$ is **$`y_A = 13`$**. (If the paper lists $`17`$, treat that as inconsistent with $`x_A=14`$; verification must use the matching $`y_A`$.)

**Step 2 — Sign**

$`\gcd(13, 22) = 1`$ ✓


```math
S_1 = 5^{13} \bmod 23 = 21
```



```math
K^{-1} = 13^{-1} \bmod 22 = 17
```



```math
S_2 = 17(19 - 14 \cdot 21) \bmod 22 = 11
```


Signature = $`(S_1, S_2) = (21, 11)`$.

**Step 3 — Verify** (with $`y_A = 13`$)


```math
V_1 = 5^{19} \bmod 23 = 7
```



```math
V_2 = (13^{21} \cdot 21^{11}) \bmod 23 = 7
```


$`V_1 = V_2`$ → signature is **verified**.

---

## 7. Schnorr digital signature scheme

### 7.1 Idea

- Also uses exponentiation in a finite field; security from **discrete logs**.
- Designed to **minimize message-dependent computation** (main work can be done in idle time).
- Uses prime modulus $`p`$ where $`p-1`$ has a prime factor $`q`$ of suitable size.
- Typical sizes: $`p`$ ≈ **1024-bit**, $`q`$ ≈ **160-bit**.

### 7.2 Key setup

1. Choose suitable primes $`p, q`$.
2. Choose $`a`$ such that $`a^q \equiv 1 \pmod{p}`$.
3. Global parameters for all users: $`(a, p, q)`$.
4. Each user A chooses secret $`s_A`$ with $`0 < s_A < q`$.
5. Public key: $`v_A = a^{-s_A} \bmod p`$ (as in the lecture form).

### 7.3 Signing

1. Choose random $`r`$ with $`0 < r < q`$; compute $`x = a^r \bmod p`$.
2. Compute $`e = H(M \| x)`$ (hash of message concatenated with $`x`$).
3. Compute $`y = (r + s_A e) \bmod q`$.
4. Signature is the pair $`(e, y)`$.

### 7.4 Verification

1. Compute $`x' = a^y \, v_A^{e} \bmod p`$.
2. Accept if $`e = H(M \| x')`$.

---

## 8. Digital Signature Standard (DSS) and DSA

### 8.1 Background

| Point | Detail |
|---|---|
| Who | US Govt approved scheme; NIST & NSA (early 1990s) |
| Standard | Published as **FIPS 186** (1991); revised 1993, 1996, 2000 |
| Hash | Uses **SHA** |
| Naming | **DSS** = the standard; **DSA** = the algorithm |
| FIPS 186-2 | Also allows RSA and elliptic-curve signature variants |
| Nature | DSA is **signature-only** (unlike RSA, which also encrypts) |
| Security | Discrete logarithms; variant of ElGamal & Schnorr |

### 8.2 DSA properties

- Creates a **320-bit** signature (with classical 512–1024 bit parameter sizes in older DSS).
- Smaller and faster than RSA for signatures.
- Public-key technique; digital signature only.

### 8.3 DSA key generation

**Global public parameters** $`(p, q, g)`$:

1. Choose 160-bit prime $`q`$.
2. Choose large prime $`p`$ with $`2^{L-1} < p < 2^L`$, where $`L = 512`$ to $`1024`$ and multiple of 64, such that $`q`$ divides $`(p-1)`$.
3. Choose $`g = h^{(p-1)/q} \bmod p`$, where $`1 < h < p-1`$ and $`g > 1`$.

**Per-user keys:**

- Private: random $`x < q`$.
- Public: $`y = g^x \bmod p`$.

### 8.4 DSA signature creation

Sender signs $`M`$:

1. Choose random per-message key $`k`$ with $`k < q`$.
   - $`k`$ must be random, destroyed after use, and **never reused**.
2. Compute


```math
r = (g^k \bmod p) \bmod q
```



```math
s = \bigl[k^{-1}\bigl(H(M) + x r\bigr)\bigr] \bmod q
```


3. Send message $`M`$ with signature $`(r, s)`$.

### 8.5 DSA signature verification

Receiver has $`M`$ and $`(r, s)`$:


```math
w = s^{-1} \bmod q
```



```math
u_1 = \bigl[H(M)\, w\bigr] \bmod q
```



```math
u_2 = (r w) \bmod q
```



```math
v = \bigl[\bigl(g^{u_1} y^{u_2} \bmod p\bigr)\bigr] \bmod q
```


If $`v = r`$, the signature is **verified**.

### 8.6 Worked DSS example (CAT-style)

**Given:** $`p = 47`$, $`q = 23`$, $`h = 31`$, $`x = 19`$, $`k = 17`$, $`H(M) = 21`$.

**Manny (signer) — generate keys and signature**


```math
g = h^{(p-1)/q} \bmod p = 31^{2} \bmod 47 = 21
```



```math
y = g^x \bmod p = 21^{19} \bmod 47 = 28
```



```math
r = (g^k \bmod p) \bmod q = (21^{17} \bmod 47) \bmod 23 = 12
```



```math
k^{-1} \bmod 23 = 17^{-1} \bmod 23 = 19
```



```math
s = \bigl[17^{-1}(21 + 19 \cdot 12)\bigr] \bmod 23 = 16
```


**Signature generated:** $`(r, s) = (12, 16)`$.

**Oscar (verifier) — verify**


```math
w = s^{-1} \bmod 23 = 16^{-1} \bmod 23 = 13
```



```math
u_1 = (21 \cdot 13) \bmod 23 = 20
```



```math
u_2 = (12 \cdot 13) \bmod 23 = 18
```



```math
v = \bigl[(21^{20} \cdot 28^{18}) \bmod 47\bigr] \bmod 23 = 12
```


Since $`v = r = 12`$, the signature is **verified**.

---

## 9. Post-Quantum Cryptography (PQC)

### 9.1 What PQC is

**Post-Quantum Cryptography** = cryptographic algorithms designed to stay secure even against attacks by **powerful quantum computers**.

- Traditional public-key systems (**RSA**, **ECC**) rely on problems that classical computers cannot solve efficiently, but **quantum algorithms** could break them.
- Quantum computers use **qubits**, which can represent and process many states in ways classical bits cannot; they are not limited to trying combinations strictly one-by-one in the classical sense.

Today’s public-key crypto is based on:

- **Integer factorization** → RSA
- **Discrete log problems** → DSA, Diffie–Hellman, ECC

A sufficiently large quantum computer could break these or weaken symmetric keys/hashes far faster than classical machines. PQC uses a new set of **quantum-resistant algorithms**, developed by researchers and evaluated by bodies such as **NIST** and **ANSSI**.

### 9.2 Why PQC is needed

- Quantum computers can solve some problems **exponentially faster** than classical computers.
- **Shor’s algorithm** efficiently factors large integers and computes discrete logarithms.
- Therefore **RSA** and **ECC**, which secure much of today’s internet traffic, could be broken by a powerful quantum computer.
- Data encrypted today can be stored and decrypted later (“harvest now, decrypt later”) — so long-term confidentiality already motivates migration.

### 9.3 Characteristics of PQC

| Characteristic | Meaning |
|---|---|
| **Quantum-resistant** | Based on math problems not efficiently solved by known quantum algorithms |
| **Classical deployability** | Runs on today’s classical hardware/networks (unlike QKD, which needs special devices) |
| **Public-key algorithms** | Focus on key exchange, digital signatures, and encryption |
| **Long-term security** | Protects data that must stay confidential for decades |

### 9.4 Main families of PQC algorithms

**1. Lattice-based cryptography**

- Hard problems such as **Learning With Errors (LWE)**.
- Strong security and good performance.
- Examples: **Kyber** (encryption / KEM), **Dilithium** (digital signature).

**2. Code-based cryptography**

- Based on decoding random linear codes (hard even for quantum computers).
- Example: **Classic McEliece**.

**3. Hash-based signatures**

- Rely on security of cryptographic **hash functions**.
- Well-studied; mainly for signatures.
- Example: **SPHINCS+**.

**4. Multivariate cryptography**

- Solving systems of multivariate polynomial equations over finite fields.
- Efficient for signatures; some schemes vulnerable to algebraic attacks.

**5. Isogeny-based cryptography** (less common now)

- Mathematics of elliptic-curve isogenies; compact keys but complex.
- Example: **SIKE** (largely broken; still of research interest historically).

### 9.5 Standardization (NIST)

NIST’s **Post-Quantum Cryptography Standardization Project** selects algorithms for global use.

Announced direction (2022 draft standards):

| Role | Algorithms |
|---|---|
| Encryption / key encapsulation | **Kyber** |
| Digital signatures | **Dilithium**, **Falcon**, **SPHINCS+** |

These will **replace or complement** RSA and ECC in future protocols.

### 9.6 Applications and migration

PQC will be integrated into:

- **TLS/SSL** (secure web)
- **VPNs** and secure communication protocols
- **Digital signatures**, identity systems, blockchain
- Secure storage; government/defense communications

Organizations should build **crypto-agility** — the ability to switch algorithms easily — for a smooth migration to PQC.

### 9.7 Challenges

- Larger **key sizes** and **signatures** for some PQC schemes
- Integration into existing standards and infrastructure
- **Side-channel** resistance and implementation security
- Global coordination for deployment

### 9.8 Short 6-mark style answer (company / quantum threat)

**Need:** Quantum computers (via Shor’s algorithm) threaten RSA/ECC discrete-log and factoring assumptions; confidential business data encrypted today may be decrypted later.

**Two algorithms (examples):** Kyber (KEM/encryption), Dilithium (signatures) — or Falcon / SPHINCS+.

**How PQC helps:** Replaces vulnerable public-key primitives with quantum-resistant math (lattices, hashes, codes, etc.), deployable on classical systems, preserving confidentiality and authentication against future quantum attacks when migrated with crypto-agility.

---

## 10. Quick exam pointers

| Topic | Remember |
|---|---|
| Why signatures? | Trust, non-repudiation, third-party dispute resolution |
| Sign then encrypt | Order matters for direct signatures |
| ElGamal / Schnorr / DSA security | Discrete logarithm problem |
| ElGamal verify | $`V_1 = a^m \bmod q`$, $`V_2 = y^{S_1} S_1^{S_2} \bmod q`$ |
| DSA verify | Compute $`w, u_1, u_2, v`$; accept if $`v = r`$ |
| Never reuse $`k`$ in DSA | Reusing $`k`$ can leak the private key |
| DSS vs DSA | DSS = standard; DSA = algorithm |
| PQC threat | Shor → RSA/ECC break |
| PQC examples | Kyber, Dilithium, Falcon, SPHINCS+, Classic McEliece |
| PQC ≠ QKD | PQC is software/classical; QKD needs quantum channels/devices |

---

*Sources: Unit 5.pptx (Digital Signatures); Post-Quantum Cryptography (PQC).pptx.*
