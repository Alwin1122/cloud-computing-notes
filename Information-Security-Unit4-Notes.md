# Information Security Principles and Practices (23I702) — Unit 4 Notes

Exam-ready notes from **UNIT 4.pptx**, **UNIT 4_1.pptx**, and **MAC_nemo.ppt**.

**Syllabus line:** Requirements and applications of hash functions, Message Digest, Secure Hash Algorithm, Authentication requirements, Authentication functions, Message Authentication Codes, Hash-based MAC, Block-cipher-based MAC: Data Authentication Algorithm and Cipher-based Message Authentication Code, Hashing case study: Bitcoin, MAC/HMAC case study: authenticating data sent by external applications. **(9+3)**

**Course outcome 4:** Analyze the principles and applications of hash functions and message authentication techniques in ensuring data integrity and authenticity.

The **9-mark** portion is the hash, SHA, and MAC material. The **3-mark** portion is one of the two case studies at the end.

---

## Table of Contents

1. [Cryptographic hash function](#1-cryptographic-hash-function)
2. [Requirements of a hash function](#2-requirements-of-a-hash-function)
3. [Applications of a hash function](#3-applications-of-a-hash-function)
4. [Message authentication with a hash](#4-message-authentication-with-a-hash)
5. [Hash functions and digital signatures](#5-hash-functions-and-digital-signatures)
6. [Secure Hash Algorithm — the SHA family](#6-secure-hash-algorithm--the-sha-family)
7. [SHA-512: padding and block processing](#7-sha-512-padding-and-block-processing)
8. [SHA-512 round function](#8-sha-512-round-function)
9. [Authentication requirements](#9-authentication-requirements)
10. [Authentication functions](#10-authentication-functions)
11. [Message Authentication Code (MAC)](#11-message-authentication-code-mac)
12. [Requirements and security of MACs](#12-requirements-and-security-of-macs)
13. [HMAC — hash-based MAC](#13-hmac--hash-based-mac)
14. [Data Authentication Algorithm (DAA)](#14-data-authentication-algorithm-daa)
15. [CMAC — cipher-based MAC](#15-cmac--cipher-based-mac)
16. [Case study: Bitcoin hashing](#16-case-study-bitcoin-hashing)
17. [Case study: HMAC for external applications](#17-case-study-hmac-for-external-applications)
18. [Quick exam pointers](#18-quick-exam-pointers)

---

## 1. Cryptographic hash function

A **cryptographic hash function** $`H`$ maps a message of any length to a short, fixed-length value called the **hash value**, **hash code**, or **message digest**.

```text
M  (variable length, L bits)  →  H  →  h = H(M)  (fixed length)
```

The lecture diagram labels the purpose as **data integrity**: the digest is a fingerprint of $`M`$. Two properties are marked on that figure:

- **One-way property** — computing $`H(M)`$ from $`M`$ is easy; recovering $`M`$ from $`H(M)`$ is computationally infeasible.
- **Collision-free property** — it is infeasible to find two different inputs with the same digest.

A hash is **not** encryption. There is no key, and there is no inverse operation that restores $`M`$.

---

## 2. Requirements of a hash function

Seven requirements are named in the deck. A 9-mark answer should list them with one line each.

| Requirement | Meaning | What it stops |
|---|---|---|
| **Deterministic** | The same input always produces the same digest | Verification would be useless if $`H(M)`$ changed between sender and receiver |
| **Fast computation** | $`H(M)`$ is practical even for large inputs and real-time use | A slow hash cannot protect bulk data or a busy protocol |
| **Fixed length** | The output length does not depend on the length of $`M`$ | Digests can be stored, compared, and signed as a short block |
| **Pre-image resistance** (one-way) | Given $`h`$, it is infeasible to find any $`M`$ such that $`H(M) = h`$ | Stops recovery of a secret or a password from its digest |
| **Second pre-image resistance** | Given $`M`$ and $`H(M)`$, it is infeasible to find $`M' \ne M`$ with $`H(M') = H(M)`$ | Stops forgery of a different message that still matches an existing digest |
| **Collision resistance** | It is infeasible to find any pair $`M \ne M'`$ with $`H(M) = H(M')`$ | Two inputs must not share a fingerprint. This is stronger than second pre-image resistance, because the attacker may choose **both** inputs |
| **Avalanche effect** | Flipping one input bit changes the digest in a large, unpredictable way | A small edit cannot leave the fingerprint almost unchanged |

**Exam distinction.** Pre-image: you are given only the digest. Second pre-image: you are given a specific message. Collision: you may hunt for any pair. Collision resistance implies second pre-image resistance. The birthday attack against collision resistance costs about $`2^{n/2}`$ hash evaluations for an $`n`$-bit digest, which is why the MAC slides say a 128-bit hash looks vulnerable and 160 bits is better.

---

## 3. Applications of a hash function

The applications slide names three uses.

1. **Message authentication** — detect that the received data is exactly the data that was sent.
2. **Digital signatures** — sign the short digest with a private key instead of signing the whole message.
3. **Other applications (Internet protocols)** — integrity checks inside protocols. The two case studies (Bitcoin, and HMAC on data from an external application) are the syllabus examples of this idea.

**What “message authentication” checks** (from the message-authentication slide):

- no **modification** of the contents
- no **insertion**
- no **deletion**
- no **replay**

A bare hash detects modification, insertion, and deletion only if the digest travels by a channel the attacker cannot change. Replay protection needs extra data bound into the authenticated input, such as a sequence number or a timestamp. Origin authentication needs a secret (a MAC key, or a private signature key).

---

## 4. Message authentication with a hash

Message authentication is a service that assures the data received are exactly the data sent. Stallings’ four arrangements (the two figure slides, with the lecture notes) are the ones to draw.

Notation: $`M`$ message, $`H`$ hash, $`E`$ / $`D`$ symmetric encrypt / decrypt, $`K`$ shared secret key, $`S`$ shared secret value that is **not** sent, $`\|`$ concatenation.

| | What is sent | What it provides |
|---|---|---|
| **(a)** | $`E(K,\, M \mathbin{\|} H(M))`$ | Confidentiality **and** authentication. Only A and B know $`K`$, so the message came from A and was not altered. The hash supplies the redundancy that lets B detect a change |
| **(b)** | $`M \mathbin{\|} E(K,\, H(M))`$ | Authentication only. The message is readable. Only the short digest is encrypted, so this is cheaper when confidentiality is not required |
| **(c)** | $`M \mathbin{\|} H(M \mathbin{\|} S)`$ | Authentication with **no encryption**. B recomputes the hash because B also knows $`S`$. An interceptor does not have $`S`$, so cannot forge a new message or alter $`M`$ and recompute a valid tag |
| **(d)** | $`E(K,\, M \mathbin{\|} H(M \mathbin{\|} S))`$ | Same idea as (c), plus confidentiality of the whole string |

**Exam line.** When confidentiality is not required, **(b)** costs less than **(a)** and **(d)**, because those two encrypt the entire message. Method **(c)** needs no cipher at all, but the secret $`S`$ must stay off the wire.

Receiver check, same in every case: recompute the hash from the received message (and from $`S`$ or from the decrypted digest) and **compare**. Accept only on a match.

---

## 5. Hash functions and digital signatures

A digital signature here works like a MAC, except the hash is encrypted with the sender’s **private key**. Anyone who has the sender’s **public key** can check integrity. An attacker who wants to alter the message needs that private key.

| | What is sent | What it provides |
|---|---|---|
| **(a)** | $`M \mathbin{\|} E(PR_a,\, H(M))`$ | Authentication and a **digital signature**. Only A could have produced the encrypted hash. B verifies with $`PU_a`$ |
| **(b)** | $`E(K,\, M \mathbin{\|} E(PR_a,\, H(M)))`$ | The signature of (a), plus **confidentiality** under a shared symmetric key $`K`$. This is the common pattern: sign the hash, then encrypt the message and the signature |

Signing the hash, not the whole message, is what makes the signature short and fast. The signature also goes beyond authentication between A and B: a third party can check it, because verification uses a public key. A MAC cannot do that (section 11).

---

## 6. Secure Hash Algorithm — the SHA family

**SHA** is the Secure Hash Algorithm family. The digest is the **message digest**: the fixed-length output. Parameters from the comparison slide (sizes in bits):

| | SHA-1 | SHA-256 | SHA-384 | SHA-512 |
|---|---:|---:|---:|---:|
| Message digest size | 160 | 256 | 384 | 512 |
| Message size | $`< 2^{64}`$ | $`< 2^{64}`$ | $`< 2^{128}`$ | $`< 2^{128}`$ |
| Block size | 512 | 512 | 1024 | 1024 |
| Word size | 32 | 32 | 64 | 64 |
| Number of steps | 80 | 64 | 80 | 80 |
| Security | 80 | 128 | 192 | 256 |

**How to read the security row.** It is the birthday-attack strength, about half the digest length: $`2^{80}`$, $`2^{128}`$, $`2^{192}`$, $`2^{256}`$. The MAC slides use the same idea: a 128-bit hash looks vulnerable to a birthday collision; 160 bits is better; a MAC tag should be at least 128 bits.

SHA-256 and SHA-512 are the ones to describe in detail if the question says “explain SHA”. The worked figures in the deck are **SHA-512**.

---

## 7. SHA-512: padding and block processing

SHA-512 takes a message shorter than $`2^{128}`$ bits and produces a **512-bit** digest. The processing figure has three stages.

**1. Pad the message** so its length is a multiple of **1024** bits.

- Append a 1 bit, then zeros (`100…0` on the figure).
- Place the original length $`L`$ in the last **128** bits.
- The padded message is $`N \times 1024`$ bits, split into blocks $`M_1, M_2, \ldots, M_N`$.

**2. Set the initial value.** $`H_0`$ is a 512-bit **IV**, eight 64-bit words:

| Word | Hex value |
|---|---|
| $`a`$ | `6A09E667F3BCC908` |
| $`b`$ | `BB67AE8584CAA73B` |
| $`c`$ | `3C6EF372FE94F82B` |
| $`d`$ | `A54FF53A5F1D36F1` |
| $`e`$ | `510E527FADE682D1` |
| $`f`$ | `9B05688C2B3E6C1F` |
| $`g`$ | `1F83D9ABFB41BD6B` |
| $`h`$ | `5BE0CD19137E2179` |

**3. Process each block**, then add back into the chaining value.

- Each block enters a compression function $`F`$ together with the previous chaining value ($`H_{i-1}`$, 512 bits).
- $`F`$ runs **80 rounds**.
- The round output is added to $`H_{i-1}`$ **word by word, modulo** $`2^{64}`$:

```text
H_i = H_{i-1} + F(M_i, H_{i-1})     (eight 64-bit additions, mod 2^64)
```

- After block $`N`$, $`H_N`$ is the 512-bit hash code.

The addition modulo $`2^{64}`$ is why a later block cannot be glued on without changing the digest: every block is mixed into the chaining value.

---

## 8. SHA-512 round function

One 1024-bit block is handled in **80 rounds** (rounds 0 through 79). The round figure shows:

- The **message schedule** expands block $`M_i`$ into 80 words $`W_0, W_t, \ldots, W_{79}`$.
- Each round also takes a round constant $`K_t`$.
- Eight working variables $`a, b, c, d, e, f, g, h`$ are loaded from $`H_{i-1}`$ (64 bits each).
- After round 79, each working variable is added (mod $`2^{64}`$) to the corresponding word of $`H_{i-1}`$ to produce $`H_i`$.

**One round**, as written on the slide. The right-hand sides use the values at the start of the round, so the registers are updated from $`h`$ back to $`a`$:

```text
T1 = h + Ch(e, f, g) + Σ1(e) + W_t + K_t
T2 = Σ0(a) + Maj(a, b, c)
h = g
g = f
f = e
e = d + T1
d = c
c = b
b = a
a = T1 + T2
```

All additions are modulo $`2^{64}`$.

**Symbols used in those equations**

| Symbol | Meaning |
|---|---|
| $`\mathrm{Ch}(e,f,g)`$ | Choose: $`(e \land f) \oplus (\lnot e \land g)`$ |
| $`\mathrm{Maj}(a,b,c)`$ | Majority: $`(a \land b) \oplus (a \land c) \oplus (b \land c)`$ |
| $`\Sigma_0(a)`$ | $`\mathrm{ROTR}^{28}(a) \oplus \mathrm{ROTR}^{34}(a) \oplus \mathrm{ROTR}^{39}(a)`$ |
| $`\Sigma_1(e)`$ | $`\mathrm{ROTR}^{14}(e) \oplus \mathrm{ROTR}^{18}(e) \oplus \mathrm{ROTR}^{41}(e)`$ |

$`\mathrm{ROTR}^{k}`$ is a rotate right by $`k`$ bits inside a 64-bit word. $`W_t`$ is the scheduled message word. $`K_t`$ is the round constant.

**What to say if asked “why 80 rounds and an add-back?”** Each round mixes one message word into all eight registers, and the final addition folds that result into $`H_{i-1}`$. A one-bit change in $`M_i`$ changes $`W_t`$ and then, by the avalanche effect, the whole digest.

---

## 9. Authentication requirements

Message authentication is concerned with three things:

- **integrity** of the message
- **identity of the originator**
- **non-repudiation of origin** (a dispute about who sent it can be resolved)

The requirements slide lists eight message-security threats. The ones it highlights as authentication problems are:

| Threat | What the attacker does |
|---|---|
| **Masquerade** | Pretends to be a legitimate source |
| **Content modification** | Inserts, deletes, or changes bits of the message |
| **Sequence modification** | Reorders messages, or inserts and deletes whole messages in a stream |
| **Timing modification** | Delays or replays messages |
| **Source repudiation** | The sender later denies sending the message |

**Disclosure** and **traffic analysis** are confidentiality problems. Encryption, not a bare hash, is what hides contents and patterns. **Destination repudiation** (the receiver denies receiving the message) is also on the list; a signature scheme aimed only at the sender does not by itself prove that the receiver got the message.

The three functions the deck then uses to meet these requirements are a **hash function**, **message encryption**, and a **message authentication code (MAC)**.

---

## 10. Authentication functions

### 10.1 Symmetric encryption

Encrypting $`M`$ under a shared key $`K`$ can provide **both confidentiality and authentication**:

```text
A:  M  →  E(K, M)  →  B:  D(K, M) = M
```

- B knows the sender must have been A, because only A and B know $`K`$.
- The contents cannot have been altered **if** the plaintext has structure, redundancy, or a checksum. Random-looking garbage after decryption is then rejected.
- Without that redundancy, an attacker can flip ciphertext bits and B may accept the result.

### 10.2 Public-key encryption

Encrypting with the **receiver’s public key** gives secrecy and **no** confidence about the sender. Anyone can know $`PU_b`$ and can create $`E(PU_b, M)`$.

Both secrecy and authentication need two public-key operations:

1. A **signs** with A’s private key: $`E(PR_a, M)`$.
2. A **encrypts** that result with B’s public key: $`E(PU_b,\, E(PR_a, M))`$.

B decrypts with $`PR_b`$, then with $`PU_a`$. The figure labels this pattern **confidentiality, authentication, and signature**. The cost is two public-key operations on the message, which is why real systems sign a **hash** (section 5) instead of the whole message. Altered messages still have to be recognizable, so redundancy or a hash is still required.

---

## 11. Message Authentication Code (MAC)

A **MAC** is a small fixed-size block produced from the **message and a secret key**.

```text
MAC = C(K, M) = C_K(M)
```

- It depends on $`M`$ and $`K`$.
- It need not be reversible. It is a cryptographic checksum, not ciphertext.
- The sender appends it to $`M`$.
- The receiver computes $`C(K, M)`$ again and compares.

```text
A:  M  and  C(K, M)   →   B:  recompute C(K, M) and compare
```

A match assures B that the message was **not altered** and that it comes from a party who knows $`K`$.

**Properties**

- $`C_K`$ condenses a variable-length $`M`$ to a fixed-size authenticator.
- It is a **many-to-one** function: many messages can share one MAC value. Finding such a pair must be very difficult (that is the second-pre-image style requirement, now keyed).

**Why use a MAC when encryption exists**

- Sometimes only authentication is needed, and the message may stay in the clear.
- Sometimes the authentication check must **outlive** the encryption, for example when a file is stored in an archive after the encryption key has changed.
- Encryption can still be added for secrecy. Use a **separate key** for the cipher and for the MAC. The MAC may be computed before or after encryption; the lecture treats **MAC first, then encrypt** as the better order.

**A MAC is not a digital signature.** Both parties who know $`K`$ can compute the same MAC. A third party cannot tell which of them produced it, so a MAC does not give non-repudiation against the other key holder. A signature uses a private key that only the signer has, and anyone can verify it with the public key.

---

## 12. Requirements and security of MACs

### 12.1 Three requirements

Taking the attacks in section 9 into account, a MAC should satisfy:

1. Given a message and its MAC, it is **infeasible to find another message with the same MAC**.
2. MAC values should be **uniformly distributed**: for two messages chosen by the attacker, the chance they share a MAC is about $`2^{-n}`$ for an $`n`$-bit MAC.
3. The MAC should **depend equally on all bits** of the message. Flipping any bit, anywhere, should change the MAC in an unpredictable way (avalanche, now under a key).

### 12.2 Attacks

**Brute force**

- Against a hash, a strong collision search costs about $`2^{m/2}`$ for an $`m`$-bit digest. A 128-bit hash looks vulnerable; 160 bits is better.
- Against a MAC, the attacker who has seen message–MAC pairs can search the **key space**, or search for a colliding **MAC value**.
- A MAC of **at least 128 bits** is the size the slide requires for security.

**Cryptanalysis**

- These attacks use the internal structure, as with a block cipher.
- The design goal is that brute force remains the best attack.
- MACs differ a lot internally, so one cryptanalytic trick rarely covers every MAC. That is why the deck then shows two families: HMAC (built on a hash) and DAA/CMAC (built on a block cipher).

---

## 13. HMAC — hash-based MAC

**HMAC** is the hash-based MAC in **RFC 2104**. Any hash can be plugged in. The slide’s examples are **MD5, SHA-1, RIPEMD-160, and Whirlpool**. In this unit the hash to name first is SHA-256 or SHA-512.

**Formula**

```text
HMAC_K(M) = H[ (K+ XOR opad) || H[ (K+ XOR ipad) || M ] ]
```

| Symbol | Meaning |
|---|---|
| $`K^+`$ | The key padded out to the hash **block size** $`b`$ bits |
| $`\mathrm{ipad}`$ | Inner padding constant, the byte `0x36` repeated to $`b`$ bits |
| $`\mathrm{opad}`$ | Outer padding constant, the byte `0x5c` repeated to $`b`$ bits |
| $`H`$ | The hash, with its usual IV |

**Steps matching the overview figure**

1. $`S_i = K^+ \oplus \mathrm{ipad}`$ ($`b`$ bits).
2. Inner hash: $`H(S_i \mathbin{\|} M)`$, which is an $`n`$-bit digest. The figure writes the message blocks as $`Y_0, Y_1, \ldots, Y_{L-1}`$.
3. Pad that inner digest out to $`b`$ bits.
4. $`S_o = K^+ \oplus \mathrm{opad}`$.
5. Outer hash: $`H(S_o \mathbin{\|} \text{inner digest})`$.
6. The $`n`$-bit result is $`\mathrm{HMAC}(K, M)`$.

**Cost.** The extra work is **three** hash-block calculations beyond hashing the message alone: the inner prefix block $`S_i`$, the outer prefix block $`S_o`$, and the outer hash of the inner digest.

**Why the nested construction.** A raw $`H(M \mathbin{\|} S)`$ or $`H(S \mathbin{\|} M)`$ is the idea of figure (c) in section 4. HMAC is that idea made safe for hashes such as SHA-256: the key is mixed with two different pads, and the inner digest is hashed again. An attacker who does not know $`K`$ cannot finish either hash.

**Security (HMAC security slide)**

- The proved security of HMAC is tied to the security of the underlying hash.
- An attack is either a **brute-force search of the key**, or a **birthday attack**. Because the construction is keyed, a birthday attack needs a very large number of observed messages.
- Choose the hash for the **speed versus security** trade-off the application can accept. A faster hash (and a shorter digest) is cheaper and gives a weaker tag.

---

## 14. Data Authentication Algorithm (DAA)

**DAA** is a block-cipher MAC: **DES in CBC mode**, also called **CBC-MAC**.

Rules from the slide:

- Block size is **64 bits** (DES). The key is the **56-bit** DES key.
- **IV = 0**.
- Zero-pad the final block so the message fills whole blocks $`D_1, D_2, \ldots, D_N`$.
- Encrypt in CBC mode and keep **only the final block** as the MAC.
- The tag actually sent may be the **leftmost** $`M`$ bits of that block, with $`16 \le M \le 64`$. The figure labels this **DAC** (data authentication code), 16 to 64 bits.

**Recurrence** (the “+” on the figure is XOR):

```text
O1 = E_K(D1)                         IV = 0, so the first block is encrypted alone
Oi = E_K(Di XOR O_{i-1})             for i = 2 … N
DAC = leftmost M bits of O_N
```

Each ciphertext block is chained into the next plaintext block. The last block $`O_N`$ therefore depends on every earlier block and on $`K`$.

**Limit the slide states.** A tag of at most 64 bits is **too small** for the 128-bit MAC size required in section 12. The same slide notes that message blocks can be used in reverse order as a variation; the next slides treat the real limitation as **message length**. Plain CBC-MAC was acceptable for a fixed, agreed length. With messages of many lengths it can be abused, which is why CMAC adds two extra keys and a padding rule.

---

## 15. CMAC — cipher-based MAC

**CMAC** (Cipher-based Message Authentication Code) is the block-cipher MAC adopted in **NIST SP 800-38B**.

The deck’s points:

- It starts from DAA (CBC-MAC), which was widely used in government and industry.
- DAA has a **message-size limitation**.
- The limitation is removed with **two keys and a padding rule**.
- Any approved block cipher can play the role of “Encrypt” on the figure. $`K`$ is that cipher’s key, of length $`k`$ bits. The block size is $`b`$ bits.

Two subkeys $`K_1`$ and $`K_2`$ are derived from $`K`$. They are used only on the **last** block. $`T`$ is the tag: the **most significant** $`Tlen`$ bits of the final ciphertext, written $`\mathrm{MSB}(Tlen)`$.

**Case (a) — length is an exact multiple of the block size**

- CBC-encrypt every block under $`K`$.
- Before the last encryption, XOR the last message block with **$`K_1`$**.
- $`T = \mathrm{MSB}(Tlen)`$ of that final ciphertext.

**Case (b) — length is not a multiple of the block size**

- Pad the last partial block with **`10…0`** (a 1 bit, then zeros) until it is $`b`$ bits.
- XOR that padded block with **$`K_2`$**, not $`K_1`$.
- CBC-encrypt, and again take $`\mathrm{MSB}(Tlen)`$ as $`T`$.

Using $`K_1`$ for a full last block and $`K_2`$ for a padded last block means a padded message cannot be rearranged into a different valid message of another length. That is the fix for DAA’s message-size limitation.

**DAA and CMAC side by side**

| | DAA | CMAC |
|---|---|---|
| Cipher | DES-CBC | A block cipher in a CBC-style chain |
| IV | 0 | Previous ciphertext (first block encrypted alone) |
| Last-block secret | The cipher key only | Extra subkey $`K_1`$ or $`K_2`$ |
| Partial final block | Zero-pad | Pad `10…0`, then XOR $`K_2`$ |
| Tag length | 16 to 64 bits | $`Tlen`$ bits, taken from the final block |
| Variable-length messages | The weak point | The case the two subkeys are there to handle |
| Standard on the slide | DES-based DAA | NIST SP 800-38B |

---

## 16. Case study: Bitcoin hashing

This is the **hashing case study** named on the unit syllabus slide. It is an application of the hash requirements in section 2, not a new hash algorithm.

Bitcoin binds every transaction and every block to a digest:

- Each transaction is hashed. Those digests are paired and hashed again, forming a **Merkle tree**. The **Merkle root** is one field of the block header. Change any transaction and, by the avalanche effect and collision resistance, the root changes.
- The block header (including the Merkle root and a **nonce**) is hashed with **SHA-256 applied twice**. The result is the block’s identity and the link to the next block.
- **Proof of work:** miners change the nonce until the double SHA-256 digest is numerically below a target (in practice, a digest with enough leading zeros). Pre-image resistance is why they cannot solve for the nonce; they can only try values. The fixed-length, deterministic digest is why every node can recompute the same hash and accept the block.

**Integrity argument to write in the exam.** Altering a past transaction changes its hash, the Merkle root, and the block hash. Every later block stores the previous block hash, so the change breaks the chain. Checking the chain is a hash recomputation. No secret key is involved; this is integrity of a public ledger, which is why it is a hash case study and not a MAC case study.

---

## 17. Case study: HMAC for external applications

This is the **MAC/HMAC case study** on the syllabus slide: authenticating data that an outside application sends in.

**Setting.** An external application (a payment service, a webhook, a partner system) sends records to your server. The payload need not be secret. It must be intact, and it must come from that partner.

**What the two sides share.** A secret MAC key $`K`$, distributed beforehand. The key is not sent with the data.

**What is sent.** The message $`M`$ (the body, often with a timestamp or a request id) and the tag $`\mathrm{HMAC}_K(M)`$.

**What the server does.**

1. Recompute $`\mathrm{HMAC}_K(M)`$ with the stored key.
2. Compare it with the tag that arrived.
3. Accept the record only if the tags match. Reject it if the body was edited, if a different sender forged it, or if the key is wrong.

**Why HMAC, not a bare hash.** $`H(M)`$ alone can be recomputed by anyone who edits $`M`$. $`H(M \mathbin{\|} S)`$ is figure (c) in section 4. HMAC is the RFC 2104 form of that idea: the key is mixed with `ipad` and `opad`, and the inner digest is hashed again, so the partner’s identity and the integrity of the body stand or fall together.

**Why this is not a signature.** Both sides know $`K`$, so either could have produced the tag. That is enough for the server to trust a partner it enrolled. It is not enough to prove the partner’s identity to an outside judge. If the exam asks for non-repudiation, the answer is a digital signature (section 5), not this HMAC.

**Replay.** Include a timestamp or a unique request id **inside** $`M`$ before the HMAC is computed. A copied old request then fails as a timing-modification attack (section 9), because the fresh check rejects a repeated id.

---

## 18. Quick exam pointers

### If the question is the 9-mark portion

Write in this order. One sentence of definition, then the list or the small diagram.

1. Hash: variable-length $`M`$ to fixed-length $`H(M)`$, for integrity.
2. Seven requirements. Be precise on pre-image, second pre-image, and collision.
3. Three applications: authentication, digital signature, protocols.
4. Four hash arrangements (a)–(d), and the two signature arrangements. Say what is encrypted and whether the result is secret.
5. SHA table: digest, block, word, steps, security. Then SHA-512 in four lines: pad to a multiple of 1024 with a 128-bit length, 512-bit IV, 80 rounds, add modulo $`2^{64}`$.
6. Authentication threats: masquerade, content, sequence, timing, source repudiation.
7. Three functions: hash, encryption, MAC. Symmetric encryption authenticates only when the plaintext has redundancy. Public-key encryption alone does not identify the sender.
8. MAC = $`C(K, M)`$. Not a signature. Three MAC requirements. 128-bit tag. HMAC formula. DAA as DES-CBC with IV 0. CMAC as DAA plus $`K_1`$ / $`K_2`$ and `10…0` padding (NIST SP 800-38B).

### If the question is the 3-mark case study

- **Bitcoin:** double SHA-256 of the block header, Merkle root over transactions, nonce searched until the digest is below the target. One-way and avalanche explain why the chain detects a change. No shared key.
- **External application:** shared key, send $`M`$ and $`\mathrm{HMAC}_K(M)`$, server recomputes and compares. Put a timestamp or request id inside $`M`$ to stop replay. Say why a bare hash is not enough, and why this is still not a digital signature.

### One comparison worth memorising

| | Hash | MAC (HMAC, DAA, CMAC) | Digital signature |
|---|---|---|---|
| Key | None | Shared secret $`K`$ | Sender’s private key |
| Who can check | Anyone who has $`M`$ and the digest | Only a party who knows $`K`$ | Anyone who has the public key |
| Confidentiality | No | No, unless the message is also encrypted | No, unless the message is also encrypted |
| Non-repudiation | No | No — either key holder could have created the tag | Yes — only the private-key holder could have signed |
| Main slide examples | SHA-512 | HMAC (RFC 2104), DAA, CMAC (SP 800-38B) | $`E(PR_a, H(M))`$ |

### Short key-term list

**Hash:** message digest, pre-image, second pre-image, collision resistance, avalanche, birthday attack $`2^{n/2}`$, SHA-1, SHA-256, SHA-384, SHA-512, IV, padding, Merkle–Damgård-style chaining, round function, $`\mathrm{Ch}`$, $`\mathrm{Maj}`$.

**Authentication:** masquerade, content modification, sequence modification, timing modification, source repudiation, symmetric encryption, public-key encryption, sign then encrypt.

**MAC:** $`C(K, M)`$, many-to-one, HMAC, $`K^+`$, ipad `0x36`, opad `0x5c`, RFC 2104, DAA, CBC-MAC, DES, DAC, CMAC, $`K_1`$, $`K_2`$, NIST SP 800-38B.
