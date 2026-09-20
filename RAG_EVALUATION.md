# RAG Evaluation

## Evaluation Objective

Evaluate whether the FinTech Document Intelligence RAG Agent:

1. Retrieves the correct document.
2. Grounds answers in retrieved content.
3. Distinguishes multiple documents.
4. Returns source/version metadata when available.
5. Refuses to answer unsupported questions from outside knowledge.

## Evaluation Set

| # | Test | Expected Source | Result | Status |
|---|---|---|---|---|
| 1 | Purpose of KFS | RBI Digital Lending | Correct RBI retrieval and evidence | PASS |
| 2 | Cooling-off/look-up period | RBI Digital Lending | Correct requirements and evidence | PASS |
| 3 | LSP responsibilities | RBI Digital Lending | Correct document and multiple relevant sections | PASS |
| 4 | DLA data-collection restrictions | RBI Digital Lending | Correct restrictions and evidence | PASS |
| 5 | Present value | Module 2 | Correct document and evidence | PASS |
| 6 | Discrete vs continuous growth | Module 2 | Correct concepts and evidence | PASS |
| 7 | Classical optimization | Module 2 | Correct concept and evidence | PASS |
| 8 | Main subject of each document | Both | Both documents correctly identified | PASS |
| 9 | APR vs present value | Both | Concepts correctly mapped to documents | PASS |
| 10 | Current repo rate | Neither | Correct not-found behavior | PASS |

## Metrics

### Functional pass rate

```text
10 / 10 = 100%
```

### Document-specific retrieval

```text
7 / 7 = 100%
```

### Cross-document retrieval

```text
2 / 2 = 100%
```

### Out-of-scope handling

```text
1 / 1 = 100%
```

## Interpretation

The result shows that the current implementation passed the initial manually designed functional test set.

It should **not** be interpreted as 100% general retrieval accuracy. A larger unseen evaluation set would be required to make stronger claims.

## Important Test Examples

### Grounded retrieval

**Question:**  
According to the RBI Digital Lending document, what is the cooling-off period?

**Expected behavior:**  
Retrieve RBI document, identify the relevant requirement, and report source metadata.

**Observed:**  
Correct RBI document, version `1.0`, topic, and evidence location.

### Cross-document retrieval

**Question:**  
Which document discusses APR and which discusses present value?

**Observed:**  
APR → RBI Digital Lending document.  
Present value → Module 2 quantitative modeling document.

### Out-of-scope behavior

**Question:**  
What is India's current repo rate?

**Observed:**  
The assistant returned that the information could not be found in the uploaded documents and did not provide an unsupported repo-rate value.

## Recommended Future Evaluation

Expand the test set to 30–50 questions and include:

- paraphrased questions
- ambiguous questions
- questions spanning multiple chunks
- questions spanning multiple documents
- questions with similar terminology
- deliberately unsupported questions
- document/version conflict tests
- retrieval failure tests
