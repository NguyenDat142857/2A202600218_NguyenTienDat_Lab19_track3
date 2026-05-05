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

| # | Question | Entity | Flat RAG | GraphRAG | Flat ✓ | Graph ✓ |
|---|----------|--------|----------|----------|--------|---------|
| 1 | Ai thành lập OpenAI? | OpenAI | Sam Altman, Elon Musk | Sam Altman, Elon Musk | 1 | 1 |
| 2 | OpenAI được đầu tư bởi ai? | OpenAI | Microsoft (2019) | Microsoft | 1 | 1 |
| 3 | Elon Musk liên quan công ty nào? | Elon Musk | Tesla | Tesla | 1 | 1 |
| 4 | Google mua công ty nào? | Google | DeepMind (2014) | DeepMind | 1 | 1 |
| 5 | DeepMind làm gì? | DeepMind | Nghiên cứu AI | Phát triển AlphaGo | 0 | 1 |
| 6 | Sam Altman là ai? | Sam Altman | CEO OpenAI | CEO OpenAI | 1 | 1 |
| 7 | Tesla được thành lập khi nào? | Tesla | 2003 | 2003 | 1 | 1 |
| 8 | Microsoft đầu tư vào ai? | Microsoft | OpenAI | OpenAI | 1 | 1 |
| 9 | AlphaGo được tạo bởi ai? | AlphaGo | DeepMind | DeepMind | 1 | 1 |
|10 | DeepMind thuộc công ty nào? | DeepMind | Google | Google | 1 | 1 |
|11 | Ai sáng lập công ty Microsoft đầu tư? | Microsoft | Không rõ | Sam Altman, Elon Musk | 0 | 1 |
|12 | Công ty phát triển AlphaGo? | AlphaGo | Không rõ | DeepMind (Google) | 0 | 1 |
|13 | Founder Tesla liên quan công ty nào? | Elon Musk | Tesla | Tesla, OpenAI | 0 | 1 |
|14 | Google mua công ty tạo AlphaGo? | Google | DeepMind | DeepMind | 1 | 1 |
|15 | Vai trò Sam Altman? | Sam Altman | Không rõ | CEO OpenAI | 0 | 1 |
|16 | Công ty thành lập 2015? | 2015 | Không rõ | OpenAI - Altman, Musk | 0 | 1 |
|17 | Công ty liên quan Musk & Altman? | Elon Musk | Không rõ | OpenAI | 0 | 1 |
|18 | DeepMind & Google? | DeepMind | Có liên quan | Công ty con | 0 | 1 |
|19 | Microsoft đầu tư + năm thành lập? | Microsoft | OpenAI | OpenAI - 2015 | 0 | 1 |
|20 | Ai đứng sau AlphaGo? | AlphaGo | DeepMind | DeepMind | 1 | 1 |

---

### 📌 Biểu đồ so sánh

![Biểu đồ so sánh](./image/so%20sánh%20Benhmark.png)

---

## 🏁 Kết luận

GraphRAG là một hướng tiếp cận mạnh mẽ cho bài toán QA, đặc biệt khi:

* Dữ liệu có nhiều quan hệ
* Cần suy luận nhiều bước

👉 Hiệu quả hơn Flat RAG trong các bài toán thực tế phức tạp.

