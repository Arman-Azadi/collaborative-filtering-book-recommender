# Collaborative Filtering Book Recommender
**Author:** Arman Azadi
**Institution:** Iran University of Science and Technology (IUST)

## 📌 Project Overview
This project implements a **Memory-Based Collaborative Filtering** system to recommend books to users. It builds the system from scratch using linear algebra (numpy/pandas) without relying on high-level recommendation libraries.

The project explores two primary approaches:
1.  **User-Based CF:** Finds users with similar reading histories and suggests books they liked.
2.  **Item-Based CF:** Finds books that are frequently rated similarly by the same users.

## 🔬 Methodology

### 1. Similarity Computation
* **Metric:** Cosine Similarity.
* **Implementation:** Efficient matrix multiplication is used to compute the similarity matrix for users ($U \times U$) and items ($I \times I$).
* **Sparsity Handling:** The system addresses the challenge of sparse data (where most users have rated very few books) by focusing on shared non-zero ratings.

### 2. Prediction Strategy
The predicted rating $\hat{r}_{u,i}$ is calculated as the weighted average of ratings from the top-k similar neighbors:
$$\hat{r}_{u,i} = \frac{\sum_{v \in N} sim(u,v) \cdot r_{v,i}}{\sum_{v \in N} |sim(u,v)|}$$

### 3. Evaluation
The recommendations are evaluated against a "Gold Standard" dataset (`gold_interactions.csv`) containing hidden interactions for test users.
* **Metrics:**
    * **Precision@K (P@5, P@10):** Measures how many recommended items were actually relevant.
    * **NDCG@10:** Measures ranking quality (position of relevant items).
    * **Spearman Correlation:** Measures the monotonic relationship between predicted and actual rankings.

## 📊 Results Summary
As detailed in `Performance_Analysis.pdf`, the **User-Based** approach significantly outperformed Item-Based CF on this dataset. This is attributed to the high sparsity of the book data (users cluster better than items).

| Method | Mean P@5 | Mean P@10 | Mean NDCG |
| :--- | :--- | :--- | :--- |
| **User-Based CF** | **0.0384** | **0.0298** | **0.0384** |
| **Item-Based CF** | 0.0056 | 0.0060 | 0.0055 |

## 🛠️ Tech Stack
* **Language:** Python 3.x
* **Data Manipulation:** `Pandas`, `NumPy`
* **Math:** Linear Algebra (Matrix Operations)

## 🚀 Usage

### Prerequisites
1.  Clone the repository.
2.  **Unzip the dataset:** Extract `dataset.zip` into the root directory.
    * *Note:* Ensure the CSV files (like `interactions.csv`) are accessible to the notebooks.

### Running the System
1.  **Generate Recommendations:**
    Run `recommender_engine.ipynb`. This will process the data and save two files: `user_based_results.csv` and `item_based_results.csv`.
2.  **Evaluate Performance:**
    Run `evaluation_metrics.ipynb`. This will read the generated result files and print the final P@5 and NDCG scores.
