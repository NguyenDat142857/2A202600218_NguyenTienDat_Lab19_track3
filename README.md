# 2A202600218_NguyenTienDat_Lab19_track3
---

# 🚀 GraphRAG System – Tech Company Corpus

## 📌 Tổng quan

Dự án này xây dựng hệ thống **GraphRAG (Graph-based Retrieval Augmented Generation)** nhằm cải thiện khả năng trả lời câu hỏi từ dữ liệu về các công ty công nghệ.

So sánh 2 phương pháp:

* **Flat RAG**: truy xuất dựa trên vector (TF-IDF / embedding)
* **GraphRAG**: sử dụng đồ thị tri thức + suy luận đa bước (multi-hop)

---

## ⚙️ Pipeline hệ thống

### 1. Trích xuất thực thể & quan hệ

Sử dụng LLM để chuyển văn bản thành các bộ ba (triples):

```text
(OpenAI, FOUNDED_BY, Sam Altman)
(OpenAI, FOUNDED_BY, Elon Musk)
(OpenAI, FOUNDED_IN, 2015)
```

---

### 2. Xây dựng đồ thị tri thức

* Sử dụng **NetworkX**
* Node: thực thể (công ty, con người…)
* Edge: quan hệ (FOUNDED_BY, ACQUIRED_BY…)

---

### 3. Truy vấn GraphRAG

* Trích xuất entity từ câu hỏi
* Duyệt đồ thị bằng **BFS 2-hop**
* Tổng hợp thông tin → gửi vào LLM

---

### 4. Flat RAG (baseline)

* Truy xuất văn bản bằng TF-IDF / vector search
* Không có cấu trúc quan hệ

---

## 📊 Kết quả đánh giá (20 câu hỏi)

| Phương pháp | Accuracy |
| ----------- | -------- |
| Flat RAG    | 55%      |
| GraphRAG    | 100%     |

👉 GraphRAG vượt trội rõ rệt trong các câu hỏi cần **multi-hop reasoning**

---

## 🧠 Nhận xét

### ❌ Flat RAG

* Không hiểu quan hệ giữa các thực thể
* Dễ retrieve sai context
* Không xử lý được multi-hop

### ✅ GraphRAG

* Dựa trên đồ thị tri thức
* Suy luận nhiều bước
* Trả lời chính xác hơn, ít hallucination

---

## 💰 Phân tích chi phí

* **Flat RAG**:

  * Nhanh, ít token
* **GraphRAG**:

  * Tốn token hơn (do extraction + graph context)
  * Chậm hơn ở bước build graph

👉 Trade-off: **GraphRAG tốn chi phí hơn nhưng accuracy cao hơn đáng kể**

---

## 🖼️ Kết quả trực quan

### 📌 Knowledge Graph
![Đồ thị tri thức](./image/Đồ%20thị%20tri%20thức.png)
![Đồ thị tri thức](./image/Đồ%20thị%20tri%20thức1.png)

---

### 📌 Bảng kết quả benchmark

![Biểu đồ so](./image/Đồ%20thị%20tri%20thức1.png)

---

### 📌 Biểu đồ so sánh

![Biểu đồ so sánh](./image/so20%sánh20%Benhmark.png)

---


## 🏁 Kết luận

GraphRAG là một hướng tiếp cận mạnh mẽ cho bài toán QA, đặc biệt khi:

* Dữ liệu có nhiều quan hệ
* Cần suy luận nhiều bước

👉 Hiệu quả hơn Flat RAG trong các bài toán thực tế phức tạp.

