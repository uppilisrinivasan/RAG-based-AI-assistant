# 🤖 RAG-style Semantic Search for Customer Support (Colab Setup)

This project provides a simple Colab-based setup to run a **Retrieval-Augmented Generation (RAG)**-like semantic search over a large dataset of customer support tweets using **FAISS** and **Sentence-Transformers**.

## 🔍 Overview

This notebook enables fast semantic search over real customer support interactions using:

- 🤗 `datasets` to load a dataset of customer queries and responses.
- 🔎 `faiss` to create a vector similarity index.
- 🧠 `sentence-transformers` to embed queries.
- 💬 A simple `VectorStore` class to search for top-k relevant support responses.

## 📦 Dependencies

The following libraries are required and installed automatically in the notebook:
- `faiss-cpu`
- `sentence-transformers`
- `datasets`
- `transformers`
- `torch`
- `pandas`
- `tqdm`

## 🔐 Required Accounts & Authentication

To run this notebook seamlessly, you need:

### 🔑 Hugging Face Account
Used for accessing the customer support dataset and pre-trained transformer models.

- Create or log in here: [https://huggingface.co/join](https://huggingface.co/join)
- You may be prompted for an access token if using private models or datasets.
- Token management: [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

### 🌐 ngrok Account (Optional)
If the notebook hosts a local server (e.g., for a demo chatbot), `ngrok` may be used to expose it.

- Sign up here: [https://dashboard.ngrok.com/signup](https://dashboard.ngrok.com/signup)
- Once logged in, find your auth token here: [https://dashboard.ngrok.com/get-started/setup](https://dashboard.ngrok.com/get-started/setup)

## 🛠 How to Use

1. **Open the notebook in Colab**.
2. **Run all cells sequentially**:
    - Installs dependencies.
    - Loads and caches the dataset locally (first time only).
    - Generates or loads sentence embeddings.
    - Builds the FAISS index and enables searching.
3. **Run the sample search**:
    ```python
    vector_store.search("I ordered a laptop, but it arrived with a broken screen. What should I do?")
    ```

This will return a list of the most semantically similar support replies.

## 📁 Dataset

We use the `MohammadOthman/mo-customer-support-tweets-945k` dataset from Hugging Face, which includes:
- `customer_query`: the customer’s tweet or issue.
- `support_reply`: the corresponding company’s support response.

A local CSV cache is created at `cache/customer_support_full.csv` to avoid repeated downloads.

## 💡 Key Features

- ⚡ Fast retrieval using FAISS flat L2 index.
- 📚 Embedding caching to reduce compute time.
- 🧪 Plug-and-play for experimenting with semantic retrieval in customer support.
- ✅ CUDA acceleration (if GPU is available).

## 📌 Example Output

```python
vector_store.search("My phone won’t turn on after charging all night")
# ➜ ['Please try holding the power button for 10 seconds...', 'We’re sorry to hear that! Can you try...', ...]
```

## 📂 Project Structure

```
├── rag_colab_setup.ipynb     # Main notebook
└── cache/
    ├── customer_support_full.csv   # Cached dataset
    └── embeddings_full.npy         # Cached sentence embeddings
```

## 🧠 Notes

- The embedding model used is `all-MiniLM-L6-v2` (384-dimensional vectors).
- FAISS index is rebuilt every time you run the notebook, but embeddings are cached.
- You can extend the search to integrate it with a LLM-based response generation module.

## 🙌 Acknowledgements

- Hugging Face for the dataset and transformer tools.
- Sentence-Transformers team for pre-trained models.
- Facebook AI for FAISS.
- ngrok for easy tunneling.

---

### 🔗 License

This project is licensed under the MIT License.
