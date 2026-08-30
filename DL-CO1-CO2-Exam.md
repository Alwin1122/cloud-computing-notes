# Deep Learning (19I006) — CO1 + CO2 Exam Pack

PSG pattern from past papers. **Only first two COs.** Same split inside each 20-mark question: **(a)(i) 2 + (a)(ii) 2 + (b) 6 + (c) 10**.

If the paper is only CO1+CO2, expect **Q1 = CO1** and **Q2 = CO2** (maybe both 20, or two 20s plus shorts). Prepare **one numerical** for each CO.

---

# CO1 — Machine Learning Concepts

**Outcome:** Realize the importance of ML concepts.

## Must-know short answers (2 marks)

### Supervised vs unsupervised

| | Supervised | Unsupervised |
|---|---|---|
| Labels | Yes (input X, target Y) | No labels |
| Goal | Learn mapping X → Y | Find structure in X |
| Examples | Classification, regression | Clustering, dimensionality reduction, autoencoders |

### Role of a validation set

Training set is used to **fit** weights. Test set is used **once** at the end to report real performance. If you tune hyperparameters on the test set, you **leak** test information and the score becomes optimistic.

**Validation set** = a held-out slice used only to **choose model / hyperparameters** (learning rate, layers, early stopping). You need it **even when train and test exist**, because test must stay untouched.

### Model capacity vs over/underfit

**Capacity** = how flexible the model is (more parameters, deeper nets, higher polynomial degree).

- Capacity **too low** → **underfit** (high bias): train and val both bad.
- Capacity **too high** + little data → **overfit** (high variance): train excellent, val/test poor.

Increasing capacity **reduces underfitting risk** but **increases overfitting risk**.

### VC dimension (1–2 lines)

**VC dimension** of a hypothesis class = the largest number of points the model can **shatter** (classify in all 2^N ways). Higher VC ≈ higher capacity ≈ easier to overfit.

### Least squares and outliers

Ordinary least squares **squares** the residual, so a large error dominates. **Outliers pull the line**. Same estimator does **not** perform better with outliers; use robust loss (Huber), regularization, or remove/winsorize outliers.

### Dropout (also appears in CO2)

Randomly drop neurons during training (set activation to 0 with probability p). Network cannot rely on one neuron → less co-adaptation → **less overfitting**. At test time, use all neurons (scale by keep-prob).

---

## Bias and variance (6 marks — write this fully)

**Bias** = error from wrong assumptions / too-simple model. Model systematically misses the true function. High bias → underfitting.

**Variance** = error from sensitivity to the particular training sample. Model fits noise. High variance → overfitting.

**Total error ≈ bias² + variance + irreducible noise.**

**Trade-off:** make the model more complex → bias falls, variance rises. Goal is a sweet spot that **generalizes**.

**How they affect performance**

- High bias: high train error, high val error, similar to each other.
- High variance: low train error, high val error (gap).

**Past-paper case:** train acc 98%, val acc 68%, complex ensemble, little data → **overfitting (high variance)**. Why: too many parameters for the data size; memorizes train set.

**Three ways to generalize better**

1. More data / data augmentation  
2. Regularization (L1/L2, dropout), simpler model, fewer parameters  
3. Cross-validation + early stopping; tune on validation, not test  

Also: ensemble with care, reduce features, batch-norm sometimes helps.

---

## Cross-validation (6 marks)

**Need:** one train/val split wastes data and the score depends on *which* slice you held out. CV reuses data and gives a more stable estimate.

**Types**

1. **Hold-out** — one split (train/val/test). Fast, unstable on small data.  
2. **k-fold** — split into k folds; each fold is val once, train on the rest; average scores. Typical k = 5 or 10.  
3. **Stratified k-fold** — same class ratio in every fold (use for classification).  
4. **LOOCV** — k = N; almost unbiased, very slow.  
5. **Time-series / walk-forward** — never train on the future.

---

## Challenges in ML + how validation / hyperparameter tuning help (10 marks)

**Challenges:** limited/noisy data; over/underfit; class imbalance; feature choice; vanishing/exploding gradients (deep nets); compute cost; interpretability; distribution shift; choosing architecture and **hyperparameters** (lr, batch size, depth, λ).

**Validation set:** detect overfit (train–val gap); pick early-stopping epoch; compare models fairly.

**Hyperparameter tuning:** grid search, random search, or Bayesian search **on validation** (or inner CV). Example: try lr ∈ {0.1, 0.01, 0.001}; pick the one with best val loss.

Write 2 short examples: (1) high-capacity net + small data → overfit, fix with dropout + val early stop; (2) linear model on nonlinear data → underfit, increase capacity.

---

## Confusion matrix numerical (CO1 10-mark style — Nov 2025)

```
                 Predicted
                 Exc   Avg   Below
Actual Exc       40     5      5
       Avg        6    35      9
       Below      4     8     28
```

N = 140. Accuracy = (40+35+28)/140 = **103/140 = 0.736 (73.6%)**.

For a class: Precision = TP/(TP+FP), Recall = TP/(TP+FN), F1 = 2PR/(P+R).

**Excellent:** TP=40, FP=6+4=10, FN=5+5=10  
P=40/50=0.80, R=40/50=0.80, F1=0.80

**Average:** TP=35, FP=5+8=13, FN=6+9=15  
P=35/48=0.729, R=35/50=0.70, F1=0.714

**Below Average:** TP=28, FP=5+9=14, FN=4+8=12  
P=28/42=0.667, R=28/40=0.70, F1=0.683

**Weighted precision** = (50·0.80 + 50·0.729 + 40·0.667) / 140 = (40+36.45+26.68)/140 ≈ **0.737**

**Average class:** precision ≈ how many predicted-Avg are truly Avg; recall ≈ how many true-Avg were found. Model is decent but misses 15 of 50 Avg students.

**Why accuracy misleads:** classes are slightly uneven; accuracy hides that Below Average has the weakest precision. A model can look “73% good” while one class is systematically worse.

**Weakest class:** Below Average (lowest P and F1). Improve: more samples of that class, class weights, better features, threshold tuning, or a model that does not ignore the minority.

---

# CO2 — Deep Feedforward Networks + Learning

**Outcome:** Architecture of deep feedforward nets and how they learn.

## Architecture (write once, reuse)

**MLP / feedforward:** input layer → one or more **hidden** layers → output layer. Signal goes **only forward** (no loops). Each neuron:  
`z = w·x + b`, `a = f(z)` where f is an **activation**.

**Why activation:** without a nonlinearity, stacked layers collapse to one linear map. Activations let the net learn curves.

| Activation | Formula | Use |
|---|---|---|
| Sigmoid | 1/(1+e^(−z)) | Output for binary class; saturates (vanishing grad) |
| Tanh | (e^z − e^(−z))/(e^z + e^(−z)) | Hidden (zero-centered); still saturates |
| ReLU | max(0,z) | Hidden default; cheap, sparse; dead ReLU if z always < 0 |

**Tanh numerical (2–3 marks):**  
tanh(1) ≈ 0.761, tanh(3) ≈ 0.995. Small z → slope steep (good gradient). Large z → **saturates near ±1**, gradient ≈ 0 → **slow learning**.

---

## Regularization, dropout, loss (2–6 marks)

**Regularization** = extra penalty so weights stay small → less overfit.

- **L2 (weight decay):** add λ Σ w². Shrinks all weights smoothly.  
- **L1:** add λ Σ |w|. Drives many weights to **exactly 0** (sparse features).

**Loss** = how wrong the prediction is; training **minimizes** it.

| Task | Common loss |
|---|---|
| Regression | MSE / squared: (y − ŷ)² |
| Binary class | Binary cross-entropy |
| Multi-class | Categorical / softmax CE |

---

## Hebb vs perceptron (6 marks)

**Hebb (unsupervised):** “neurons that fire together wire together.” Δw ∝ x · y (or x · activation). No error signal, no target. Used for associative memory / simple feature learning.

**Perceptron (supervised):** needs a **target** t ∈ {0,1} or {−1,+1}.  
Predict ŷ = 1 if w·x + b ≥ 0 else 0.  
**Update only if wrong:**  
`w ← w + η (t − ŷ) x`  
`b ← b + η (t − ŷ)`

Difference: Hebb has **no teacher**; perceptron **corrects error** using labels. Perceptron only works for **linearly separable** data.

---

## Optimization + weight updates (6 marks)

Gradient descent: `θ ← θ − η ∇_θ L`

| Method | Gradient from | Speed | Stability | Best for |
|---|---|---|---|---|
| **BGD** | whole dataset | slow/epoch, smooth | most stable | small data |
| **SGD** | one sample | fast updates, noisy | high variance | online / huge data |
| **Mini-batch** | a batch (32–256) | good compromise | stable enough | **deep nets with millions of params** |

**Why mini-batch for deep nets:** GPU-friendly, noise helps escape sharp minima, more stable than pure SGD, much faster than full batch.

**Adagrad:** η_t,i = η / √(G_t,i + ε) where G accumulates **squared past gradients** per parameter. Rare features get a **larger effective lr**; frequent ones get smaller. Converges better on sparse data than fixed-η GD. Weakness: G grows → lr → 0 (RMSProp/Adam fix this).

---

## Perceptron numerical (practice this)

Given W = [0.4, 0.3], assume b = 0 if not given, η = 1 unless given. For each sample:

1. z = W·X + b  
2. ŷ = 1 if z ≥ 0 else 0  
3. If ŷ ≠ Y: W ← W + η(Y − ŷ)X, b ← b + η(Y − ŷ)  
4. Show W after each sample. One full pass = one epoch.

Dataset from Mar 2025:

| Sample | X1 | X2 | Y |
|---|---|---|---|
| S1 | 4 | 5 | 0 |
| S2 | 9 | 2 | 1 |
| S3 | 5 | 7 | 0 |
| S4 | 7 | 1 | 1 |

Start W = [0.4, 0.3]. Write every step; do not skip samples even if already correct.

---

## Backprop / MLP numerical (the 10-mark they love)

**Network:** 2 inputs → 2 hidden (ReLU) → 1 output (sigmoid). Squared loss. SGD. η = 0.001. Target y = 1.

Inputs: x1=1.0, x2=2  
Weights: w1=0.4, w2=0.3, w3=0.2, w4=0.3, w5=0.9, w6=0.2  
Biases: b1=0.2, b2=0.2, b3=0.1  

Typical wiring (write this diagram):

```
x1 --w1--> h1 --w5--> ŷ
x2 --w2--> h1
x1 --w3--> h2 --w6--> ŷ
x2 --w4--> h2
```

h1, h2 use ReLU; ŷ uses sigmoid.

**Forward**

- z1 = w1 x1 + w2 x2 + b1 = 0.4(1)+0.3(2)+0.2 = **1.2** → a1 = ReLU(1.2) = **1.2**
- z2 = w3 x1 + w4 x2 + b2 = 0.2(1)+0.3(2)+0.2 = **1.0** → a2 = ReLU(1.0) = **1.0**
- z3 = w5 a1 + w6 a2 + b3 = 0.9(1.2)+0.2(1.0)+0.1 = **1.38**  
- ŷ = σ(1.38) = 1/(1+e^(−1.38)) ≈ **0.799**

**Loss** L = ½(y − ŷ)² or (y − ŷ)² — **state which you use** (paper said “squared loss”; ½ is nicer for derivatives).  
If L = ½(y−ŷ)²: dL/dŷ = ŷ − y = 0.799 − 1 = **−0.201**

**Backward (chain rule)**

σ'(z) = σ(z)(1−σ(z)) ≈ 0.799×0.201 ≈ **0.161**  
δ_out = (dL/dŷ) · σ' ≈ −0.201 × 0.161 ≈ **−0.0324**

dL/dw6 = δ_out · a2 ≈ −0.0324 × 1.0 = **−0.0324**  
dL/dw5 = δ_out · a1 ≈ −0.0324 × 1.2 = **−0.0389**

ReLU'(z) = 1 if z>0 else 0. Both hidden z > 0.

δ_h2 = δ_out · w6 · 1 ≈ −0.0324 × 0.2 = **−0.00648**  
δ_h1 = δ_out · w5 · 1 ≈ −0.0324 × 0.9 = **−0.0292**

dL/dw1 = δ_h1 · x1 ≈ −0.0292 × 1 = **−0.0292**

**SGD update:** w ← w − η (dL/dw)

w1_new = 0.4 − 0.001(−0.0292) ≈ **0.400029**  
w6_new = 0.2 − 0.001(−0.0324) ≈ **0.200032**

(Tiny because η=0.001 — that is expected. Show the formula; they mark the method.)

**If they use L = (y−ŷ)² without ½:** dL/dŷ = 2(ŷ−y); just scale δ by 2; still show steps.

**Sigmoid-only backprop paper (Nov 2024 style):** same idea — forward all layers, δ = (ŷ−t) σ'(z) at output, then δ_h = (W_out δ) ⊙ σ'(z_h), then Δw = −η δ a_prev.

---

## One-page CO2 theory dump

**Learning process:** init weights → forward → compute loss → backprop gradients → update with GD/SGD → repeat epochs.

**Why deep feedforward works:** each layer builds a more abstract feature; nonlinearity + enough width/depth can approximate complex functions (universal approximation with one wide hidden layer; depth is more parameter-efficient).

**Problems:** vanishing/exploding gradients (sigmoid stacks), overfit (use L2/dropout), slow train (use ReLU, Adam/mini-batch, good init).

---

# Likely paper (CO1 + CO2 only)

**Q1 CO1**  
(a) validation set + capacity/overfit **or** supervised vs unsupervised + VC  
(b) bias–variance **or** cross-validation types  
(c) over/underfit case **or** confusion-matrix metrics  

**Q2 CO2**  
(a) activation / dropout **or** L1 vs L2 + loss list **or** tanh(1), tanh(3)  
(b) Hebb vs perceptron **or** BGD/SGD/MBGD + Adagrad  
(c) **perceptron table** or **one backprop pass** (they will give numbers)

---

# 15-minute drill (night before)

1. Draw bias–variance vs complexity; recite 3 fixes for overfit.  
2. Write k-fold in 6 lines.  
3. Compute Excellent/Avg/Below P, R, F1 from the matrix above without looking.  
4. Write perceptron update rule from memory; run S1 and S2.  
5. Write backprop for 2-2-1: forward z,a then δ then Δw.  
6. Table: BGD vs SGD vs MBGD — pick MBGD for deep nets and say why.  
)
