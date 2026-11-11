# The Paper That Started the AI Trade — Thematic Briefing (Draft)

**Working title:** "The paper that started the AI trade"
**Purpose:** Factual spine for research meeting; pair of anchors: the Transformer paper (arXiv 1706.03762) and NVIDIA (NVDA).
**Status:** Draft for circulation. Company and paper facts below are verified against primary sources (Yahoo Finance data service for NVDA; arXiv LaTeX source of 1706.03762). Commentary to be added separately.

---

## 1. Company Snapshot — NVIDIA (NVDA)

- **Ticker / exchange:** NVDA, listed on NasdaqGS (NMS); market state: REGULAR; last price 176.74 USD.
- **Sector / industry:** Technology / Semiconductors.
- **Market cap:** 4267740758016 USD (non-diluted market cap: 4078186830000 USD). Currency: USD.
- **Headquarters:** Santa Clara, CA, United States. Full-time employees: 42,000. Incorporated 1993.
- **Business description (as returned):** NVIDIA Corporation operates as a data center scale AI infrastructure company in the US, Taiwan, China, Hong Kong, Europe, and internationally, through Compute & Networking and Graphics segments. Compute & Networking provides data center accelerated computing and networking platforms and AI solutions; Graphics offers GeForce GPUs for gaming and Quadro/NVIDIA RTX for enterprise workstation graphics.
- **Trailing P/E:** 22.34387; **forward P/E:** 11.109554. **Trailing annual revenue:** 302970011648 USD. **Net income to common:** 192880001024 USD. **Profit margin:** 0.63663. **Dividend rate:** 1.0 (yield 0.59%). **Analyst consensus:** strong_buy (recommendation mean 1.32258, 57 analyst opinions; mean target 319.98773, median 315.0, high 515.0, low 180.0).
- **Valuation / balance sheet context:** enterpriseValue 4046640119808 USD; total cash 62469001216 USD; total debt 38860001280 USD; EBITDA 201266003968 USD; return on equity 1.17211; gross margins 0.74674004.
- **Key officer:** Jen-Hsun (Jensen) Huang, Co-Founder, CEO & Director.

---

## 2. Institutional Ownership Table — NVDA

- **Institutions % held:** 0.71384 (i.e., 71.384% of shares outstanding held by institutions). Insiders % held: 0.04006 (4.006%). Institutions as % of float: 0.74364. Number of institutions: 7753.
- **Top three institutional holders by most recently reported share count** (all reported as of 2026-06-30 per the data service):

| # | Holder (as reported) | Shares | % Held | Value (USD) | Δ vs. prior Reports |
|---|----------------------|--------|--------|-------------|---------------------|
| 1 | Blackrock Inc. | 1941918386 | 0.0806 | 343234074725 | +0.85% |
| 2 | Vanguard Capital Management LLC | 1540816358 | 0.0639 | 272339291276 | +0.15% |
| 3 | State Street Corporation | 1009783437 | 0.0419 | 178479222489 | +1.60% |

- **Notable next in line (for context):** FMR, LLC — 932807820 shares (0.0387); Geode Capital Management, LLC — 613740577 shares (0.0255).
- Shares outstanding: 24147000000; float shares: 23133590000; shares short: 279579505 (1.16% of float).

---

## 3. Paper Facts — "Attention Is All You Need" (arXiv 1706.03762)

**Headline machine-translation results (from the abstract):**
- **28.4 BLEU** on the **WMT 2014 English-to-German** translation task — improving over the existing best results (including ensembles) by over 2 BLEU.
- **41.8 BLEU** on the **WMT 2014 English-to-French** translation task — a new single-model state-of-the-art, achieved after training for 3.5 days on eight GPUs (a small fraction of the training cost of the best models in the literature).
- The abstract also notes the model "generalizes well to other tasks," applied successfully to English constituency parsing with both large and limited training data.

**Stack depth (Model Architecture, Section 3):**
- **Encoder:** a stack of **N = 6 identical layers**, each with two sub-layers (multi-head self-attention; position-wise fully connected feed-forward network), residual connections + layer normalization, d_model = 512.
- **Decoder:** also a stack of **N = 6 identical layers**, with a third sub-layer performing multi-head attention over the output of the encoder stack; masking prevents attending to subsequent positions to preserve the autoregressive property.

**Scaled dot-product attention (Section 3.2.1):**
- Formulation: **Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) V**.
- Queries and keys have dimension d_k; values have dimension d_v. Dot products of the query with all keys are computed, **divided by sqrt(d_k)**, and a softmax yields the weights on the values.
- Scaling rationale (as stated in the paper): for large d_k, dot products grow large in magnitude, pushing the softmax into regions with extremely small gradients; to counteract this, dot products are **scaled by 1/sqrt(d_k)** (a dot product of q and k with independent mean-0, variance-1 components has mean 0 and variance d_k).
- Dot-product attention is chosen over additive attention because it is much faster and more space-efficient in practice (EMS-optimized matrix multiplication), and for small d_k the two perform similarly.

**Multi-head attention (Section 3.2.2):**
- Instead of a single attention function with d_model-dimensional keys/values/queries, queries, keys and values are **linearly projected h times with different, learned linear projections** to d_k, d_k and d_v dimensions; attention is run in parallel on each projected version, yielding d_v-dimensional outputs that are **concatenated and projected again** with W^O.
- Multi-head attention lets the model jointly attend to information from different representation subspaces at different positions; with a single head, averaging inhibits this.
- **The base model employs h = 8 parallel attention layers (heads)**, with d_k = d_v = d_model/h = 64. Due to the reduced per-head dimension, total computational cost is similar to single-head attention with full dimensionality.
- The Transformer uses multi-head attention in three ways: encoder-decoder attention (queries from previous decoder layer, keys/values from encoder output); encoder self-attention (keys, values and queries from the same place); and decoder self-attention (masked to preserve auto-regression).
- Supporting facts: inner feed-forward dimension d_ff = 2048; sinusoidal positional encodings added to input embeddings since there is no recurrence or convolution.

---

## 4. Sources

- arXiv identifier: **1706.03762** — "Attention Is All You Need" (Vaswani et al.). Full text verified via arXiv LaTeX source (abstract + Model Architecture section).
- Market and institutional ownership data: Yahoo Finance data service (stock info for NVDA; institutional holders and major holders for NVDA). Figures reported exactly as returned by the service, unrounded.

---

## 5. open questions / commentary TODO (to be added by research team)

- connective tissue between the 2017 paper's 28.4/41.8 BLEU results and today's data-center AI build-out;
- inputs, lags, and risks in reading institutional ownership (Blackrock/Vanguard/State Street) as a signal of conviction in NVDA;
- any gaps in the primary-source verification above.
