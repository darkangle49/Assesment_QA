# Medical Question-Answering Pipeline (RAG)

## Overview
This project implements a **Retrieval-Augmented Generation (RAG)** pipeline for answering medical questions using a Q&A dataset. The system combines:

1. **Sentence-BERT embeddings** for retrieving relevant context from the dataset.
2. **Text generation (LLaMA)** to produce concise, readable answers based on retrieved passages.

The goal is to provide accurate answers to medical questions, even if phrased differently from the training data.

---

## Dataset
- **Source:** `mle_screening_dataset.csv`  
- **Content:** ~16,000 question-answer pairs about medical diseases.  
- **Format:**  

| question                       | answer |
|--------------------------------|--------|
| What is (are) Glaucoma ?       | Open-angle glaucoma is the most common form… |
| How to prevent Glaucoma ?      | Early detection and treatment… |

---

## Pipeline

### 1. Data Preprocessing
- Load the CSV file.  
- Clean and structure the Q&A pairs.  
- Optional: use a subset (e.g., 10%) for evaluation.

### 2. Embedding & Retrieval
- Load **Sentence-BERT (`all-MiniLM-L6-v2`)**.  
- Encode all questions and answers to generate embeddings.  
- Use **cosine similarity** to retrieve Top-K relevant answers for a query.

### 3. Optional Generation
- Load a **LLaMA-based text generation model**.  
- Concatenate retrieved passages as context and generate concise answers.  

### 4. Evaluation
- **Retrieval metrics:** Mean Reciprocal Rank (MRR), Top-K Accuracy.  
- **Generation metrics:** ROUGE (1, 2, L) to evaluate answer similarity to reference.  

**Example retrieval metrics on subset:**  
- Retrieval MRR: 0.751  
- Top-3 Accuracy: 0.876  

---

## Example Interactions

**User Query:** What is glaucoma?  
**Answer:** Open-angle glaucoma is the most common form of glaucoma. Early treatment can protect your eyes from serious vision loss.

**User Query:** How can glaucoma be prevented?  
**Answer:** Early detection and treatment of glaucoma is the best way to control the disease.

**User Query:** Who is at risk for glaucoma?  
**Answer:** People over 40 (especially African-Americans), everyone over 60, and those with a family history of glaucoma.

---

## Improvements & Notes
- **Model choice:** Using a larger LLaMA or domain-specific medical LLM can improve answer quality.  
- **Fine-tuning:** Optional fine-tuning on Q&A data can increase accuracy but requires more resources.  
- **Prompt engineering:** Clear instructions to the generator improve conciseness and relevance.  
- **Resource efficiency:** Current 1B LLaMA model is chosen to run on low-resource setups.  

---

## Installation & Usage

```bash
# Clone repo
git clone https://github.com/<USERNAME>/<REPO_NAME>.git
cd <REPO_NAME>

# Install dependencies
pip install -r requirements.txt

# Run pipeline in Colab or local environment
