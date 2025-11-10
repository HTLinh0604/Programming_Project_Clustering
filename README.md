#  Programming Project Clustering Based on README.md Text Analysis  
*(Phân cụm Dự án Lập trình Dựa trên Phân tích Văn bản README.md)*

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python)
![ScikitLearn](https://img.shields.io/badge/Scikit--Learn-Machine_Learning-F7931E?style=flat&logo=scikit-learn)
![NLP](https://img.shields.io/badge/NLP-Preprocessing-6AC045?style=flat&logo=nltk)
![BERT](https://img.shields.io/badge/BERT-Embeddings-7933FF?style=flat&logo=transformers)
![UMAP](https://img.shields.io/badge/UMAP-Dimensionality_Reduction-00BFFF?style=flat)
![HDBSCAN](https://img.shields.io/badge/HDBSCAN-Clustering-FF4500?style=flat)

---

##  Overview *(Tổng quan và Mục tiêu)*

Project is a research project focusing on the **analysis and clustering of GitHub repositories** — an increasingly important problem due to the exponential growth of open-source ecosystems.  
*(Dự án là một nghiên cứu tập trung vào việc phân tích và phân loại các dự án GitHub — điều này rất cần thiết do sự phát triển nhanh chóng của các hệ sinh thái mã nguồn mở.)*

###  Importance of README.md *(Tầm quan trọng của README.md)*
The **README.md** file plays a central role in open-source projects, providing essential information such as purpose, functionality, setup instructions, and usage.  
Hence, it serves as a **rich textual source** for semantic understanding and classification of software projects.  
*(README.md là tệp cốt lõi chứa mô tả mục đích, chức năng, hướng dẫn cài đặt và sử dụng, nên được coi là nguồn dữ liệu văn bản phong phú và đáng tin cậy để hiểu và mô tả dự án phần mềm.)*

###  Research Objective *(Mục tiêu Nghiên cứu)*
To propose a **comprehensive framework** for clustering programming projects based on the **semantic information embedded in README.md** files — enabling topic discovery, trend analysis, and intelligent organization of software ecosystems.  
*(Đề xuất một khuôn khổ toàn diện cho việc phân cụm các dự án lập trình dựa trên thông tin ngữ nghĩa được trích xuất từ các tệp README.md — nhằm khai phá chủ đề, phân tích xu hướng và tổ chức thông minh hệ sinh thái phần mềm.)*

**Keywords:** GitHub, README.md, Text Clustering, TF-IDF, BERT Embeddings, K-Means, DBSCAN, HDBSCAN, UMAP, Unsupervised Learning.

---

## ⚙️ Methodology *(Phương pháp luận)*

The study follows a **five-stage clustering pipeline**:  
*(Nghiên cứu áp dụng quy trình phân cụm gồm năm giai đoạn chính)*  
1. Data Collection *(Thu thập dữ liệu)*  
2. Text Representation *(Biểu diễn văn bản)*  
3. Dimensionality Reduction *(Giảm chiều dữ liệu)*  
4. Clustering Algorithms *(Thuật toán phân cụm)*  
5. Evaluation Metrics *(Đánh giá kết quả)*  

---

### 1️ Data Collection *(Thu thập Dữ liệu)*

| **Hạng mục** | **Mô tả chi tiết** |
|---------------|--------------------|
| **Dataset size** | 57,383 README.md files |
| **Source** | GitHub GraphQL API (from 50+ distinct topics) |
| **Sampling strategy** | Collected across multiple ranking types: *Most Starred, Most Forked, Recently Updated, and Best Match* |
| **Deduplication** | Up to 1,000 unique repositories per topic were retained |

*(Tổng cộng 57.383 README.md được thu thập từ hơn 50 chủ đề GitHub riêng biệt, sử dụng 4 loại xếp hạng. Quá trình khử trùng lặp đảm bảo tính đa dạng và đại diện.)*

---

### 2️ Text Representation *(Biểu diễn Văn bản)*

Two approaches were compared to capture **lexical and semantic information**:

| **Phương pháp** | **Mô tả chi tiết** |
|------------------|--------------------|
| **TF-IDF (Term Frequency–Inverse Document Frequency)** | Captures statistical word importance. Includes lowercase conversion, URL/code/Markdown removal, enhanced stopword list, and lemmatization. |
| **Sentence-BERT (all-MiniLM-L6-v2)** | Transformer-based model producing 384-dimensional sentence embeddings. Minimal preprocessing to preserve contextual meaning. |

*(Nghiên cứu so sánh giữa TF-IDF truyền thống và Sentence-BERT hiện đại để nắm bắt đặc trưng ngữ nghĩa sâu.)*

---

### 3️ Dimensionality Reduction *(Giảm Chiều Dữ liệu)*

- **Truncated SVD (Singular Value Decomposition):**  
  Applied to TF-IDF features → reduced to 100 dimensions (≈18.9% variance retained).  
- **UMAP (Uniform Manifold Approximation and Projection):**  
  Applied to BERT embeddings → preserves local & global semantic structure for visualization.  

*(Giảm chiều giúp tăng hiệu quả tính toán và phục vụ trực quan hóa không gian ngữ nghĩa.)*

---

### 4️ Clustering Algorithms *(Thuật toán Phân cụm)*

The study evaluates multiple algorithms for unsupervised learning:

| **Thuật toán** | **Mô tả ngắn gọn** |
|----------------|--------------------|
| **K-Means** | Divides data into *K* clusters minimizing intra-cluster variance. |
| **DBSCAN** | Density-based clustering detecting noise and arbitrary shapes. |
| **Spectral Clustering** | Uses eigenvectors of Laplacian matrix for graph-based clustering. |
| **HDBSCAN** | Hierarchical version of DBSCAN that adapts to varying densities and auto-detects cluster count. |

---

### 5️ Evaluation Metrics *(Chỉ số Đánh giá)*

As the task is **unsupervised**, internal clustering metrics were used:

| **Metric** | **Ý nghĩa** |
|-------------|-------------|
| **Silhouette Score** | Measures cohesion vs. separation (−1 → 1). Higher = better-defined clusters. |
| **Davies–Bouldin Index (DB)** | Average similarity between each cluster and its most similar one. Lower = better. |
| **Calinski–Harabasz Score** | Ratio of between-cluster dispersion to within-cluster dispersion. Higher = better. |

---

##  Experimental Results *(Kết quả Thực nghiệm)*

###  Performance Comparison

| **Representation** | **Algorithm** | **Silhouette** | **Observations** |
|---------------------|----------------|-----------------|------------------|
| TF-IDF + SVD | K-Means (k=79) | 0.0625 | Moderately compact clusters; weak separation based on surface keywords. |
| TF-IDF + SVD | Spectral Clustering | — | Captures more interpretable topic structures (e.g., server/API/Docker group 48.25%). |
| TF-IDF + SVD | DBSCAN | —- | Formed one dense cluster → poor differentiation. |
| BERT Embeddings | K-Means (k=40) | 0.0269 | Overlapping semantic clusters; BERT space too continuous. |
| BERT Embeddings | HDBSCAN | **0.3057 (non-noise points)** | 17 clusters detected; 97.4% noise; semantically coherent “core topics.” |

---

###  Key Insights *(Phân tích Chính)*

- **Trade-off between Quantitative and Semantic Performance:**  
  TF-IDF models perform better numerically but rely on surface-level tokens.  
  *(TF-IDF đạt điểm định lượng cao hơn nhưng thiếu chiều sâu ngữ nghĩa.)*

- **Semantic Strength of BERT:**  
  BERT embeddings produce **conceptually cohesive** clusters despite lower numerical scores.  
  *(BERT thể hiện cụm ngữ nghĩa sâu sắc và sát nghĩa, thể hiện rõ trên đồ thị UMAP.)*

- **Algorithm Sensitivity:**  
  Distance-based methods (K-Means, DBSCAN) struggle in high-dimensional semantic space.  
  *(Các thuật toán dựa khoảng cách gặp khó với không gian ngữ nghĩa phức tạp.)*

- **Optimal Combination:**  
  **BERT + HDBSCAN** yields the most **semantically meaningful** results — forming dense “topic cores” while filtering general/noisy repositories.  
  *(Kết hợp BERT với HDBSCAN được chứng minh là tối ưu nhất — phát hiện các lõi chủ đề rõ ràng, đồng thời xử lý nhiễu hiệu quả.)*


---

##  Conclusion *(Kết luận Tổng thể)*

This research demonstrates that **semantic embeddings (BERT)** combined with **density-based clustering (HDBSCAN)** produce **highly meaningful and conceptually coherent clusters** of programming projects.  
Capturing **contextual and semantic relationships** is crucial for effectively categorizing complex software ecosystems.

*(Phương pháp BERT + HDBSCAN mang lại các cụm ngữ nghĩa sâu sắc và có ý nghĩa nhất. Việc nắm bắt mối quan hệ ngữ cảnh và ngữ nghĩa là yếu tố then chốt trong phân loại dự án phần mềm phức tạp.)*



---

##  Authors *(Nhóm Thực hiện)*

**Students:** *(Sinh viên thực hiện)*  
- Hồ Gia Thành  
- Huỳnh Thái Linh  
- Trương Minh Khoa  

**Supervisor:** *(Giảng viên hướng dẫn)* *ThS. Lê Nhật Tùng*  
**University:** *(Trường)* Trường Đại học Công nghệ TP. Hồ Chí Minh — *Khoa học Dữ liệu*  
**Year:** *(Năm thực hiện)* 2025

---

> © 2025 — Project: *Programming Project Clustering Based on README.md Text Analysis*  
> *Developed for academic research and educational purposes.*
