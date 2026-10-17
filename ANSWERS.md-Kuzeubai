# Midterm 1: answers

GitHub username:'narimankuzeubai-nxz'
Session code:'zebra-28'
Fingerprint:'5d53bca4'

## AI-use declaration

In this study, AI assistants (Gemini) and standard Python libraries were used to automate statistical calculations, determine confidence intervals (using the Wilson score interval method), model candidate-related costs, and format text. The large language model (LLM) served as a discussion partner, helping to structure analytical memos for decision-making and refine the text to ensure it met specified length constraints.

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
A | 0.7000 | 0.7833 | 0.8333 | 0.7461 |
| B | 0.5667 | 0.8000 | 0.8833 | 0.6786 |

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 | 0.7833 | 0.6638 | 0.8688 |
| A, k=5 | 0.8333 | 0.7197 | 0.9069 |
| B, k=3 | 0.8000 | 0.6822 | 0.8817 |
| B, k=5 | 0.8833 | 0.7782 | 0.9423 |
### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 18580.80 |
| A, k=5 | 24132.20 |
| B, k=3 | 12681.47 |
| B, k=5 | 14299.98 |

### 1d. Decision (at most 150 words)

Chosen candidate:B, k=5

Candidate (B, k=5) is recommended. At an annual model cost of $14,299.98, it is the highest-performing candidate that strictly respects the annual budget of $16,400. Candidates (A, k=3) ($18,580.80) and (A, k=5) ($24,132.20) exceed the budget. Candidate (B, k=3) is affordable ($12,681.47), but (B, k=5) yields higher recall (0.8833 vs 0.8000). Their 95% Wilson intervals overlap ([0.7782, 0.9423] vs [0.6822, 0.8817]), making them statistically tied, but (B, k=5) provides higher safety margins for only $1,618.51 additional annual cost.
Per-language recall for (B, k=5) is 100.0% (20/20) for English, 80.0% (16/20) for Russian, and 85.0% (17/20) for Kazakh. Russian users are served worst due to candidate chunk segmentation boundaries in sentence-window retrieval.
### 1e. Next measurement (at most 60 words)
Measure end-to-end downstream LLM accuracy and generation latency using retrieved chunks. Offline retrieval recall@5 does not ensure that 5 sentence-window chunks avoid redundant information or provide coherent context for multi-step reasoning.
## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | 0.8778 | KK, clean | 0.7667 | 0.5907 | 0.8821 | 21910.95 |
| L | 0.8278 | KK, degraded | 0.7333 | 0.5555 | 0.8582 | 9000.00 |

Personal-data pages per year sent abroad under H: 427050

### 2b. Memo (at most 300 words)
To: Head of Operations  
From: AI Engineering Lead  
Subject: Document Pipeline Selection & Risk Evaluation

Pipeline H yields higher overall accuracy (87.78% vs 82.78%), but costs significantly more ($21,910.95 vs $9,000.00). In their weakest cells, Pipeline H (Kazakh clean) drops to 76.67% [0.5907, 0.8821] and Pipeline L (Kazakh degraded) drops to 73.33% [0.5555, 0.8582]. Overlapping Wilson intervals show no statistically significant performance difference in worst-case performance.

However, adopting Pipeline H routes 427,050 pages containing personal data (individual names and ИИН) through foreign cloud infrastructure annually. Applying Law No. 94-V:
1. Where scans go: Pipeline H transmits document images to foreign data centers; Pipeline L processes all files strictly inside Kazakhstan.
2. Who stores data: Foreign API vendors manage cached images; Pipeline L maintains complete local bank custody.
3. Storage duration: Foreign cloud retention policies vary, whereas Pipeline L permits immediate local memory purging post-extraction.

A vendor agreement is not a legal compliance review. Transmitting PII abroad without explicit consent creates severe compliance risks under Kazakh data privacy law.

Safeguards:
- Local PII Anonymization: Implement an on-premise regex and NER filter to redact names and ИИНs before sending page images to foreign API endpoints.
- Compliance Auditing: Run automated validation scripts to hash payload logs and verify zero unmasked personal data leaves local infrastructure.

Recommendation: Select Pipeline L. At $9,000.00/year (1 server), it guarantees 100% data residency compliance and eliminates cross-border legal risk. Extraction errors on degraded scans should be managed via automated confidence scoring and manual fallback review.
## Part 3: Explain your own numbers

### Q1

Number: 1.65
Why (at most 40 words): Kazakh text requires multi-byte UTF-8 encoding (increasing bytes) and suffers from sub-word fragmentation in Model M's tokenizer. The 1.65 ratio indicates that tokenizer vocabulary bias drives the Kazakh token premium beyond pure byte expansion.

### Q2

Number: 13.5%
Why (at most 40 words): English chunks of 576 cl100k tokens expand to 591.8 e5 tokens, exceeding e5-small's 512-token context limit. Only English is truncated (13.5% lost tail); truncated text produces no error but gets omitted from vector embeddings.

### Q3

Number: 63.1%
Why (at most 40 words): Top-p = 0.95 accumulates tokens until cumulative probability reaches 95% (retaining top 4 tokens, excluding "Easter"). Renormalizing over the truncated pool raises the top token's probability to 63.1% without changing ranking or temperature.

### Q4

Number: 15
Why (at most 40 words): Leaderboards without wrong-answer penalties encourage guessing. Scoring with penalties rewards Model Y (+15 points ahead) for outputting "I don't know" on uncertain facts, heavily penalizing Model X for its 34 wrong answers.

### Q5

Number: 10.85
Why (at most 40 words): The model is over-trained (10.85x Chinchilla's compute-optimal ratio). Chinchilla showed most models were undertrained; training beyond optimal tokens per parameter improves inference performance per parameter size.
