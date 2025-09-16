# 🔍 Advanced RAG Retrievers with LangChain

![LangChain](https://img.shields.io/badge/LangChain-0086CB?style=for-the-badge&logo=langchain) ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai) ![FAISS](https://img.shields.io/badge/FAISS-0080FF?style=for-the-badge) ![PyPDF](https://img.shields.io/badge/PyPDF-F40F0F?style=for-the-badge&logo=adobeacrobatreader) ![Python-Dotenv](https://img.shields.io/badge/Python--Dotenv-EFC538?style=for-the-badge)

Hey there! Welcome to my latest deep dive into the world of Retrieval-Augmented Generation (RAG). After building a basic vector store, I quickly realized that just performing a simple similarity search isn't always enough. The quality of the documents you retrieve is everything—garbage in, garbage out.

This repository, documented in a single Jupyter Notebook, is my journey into exploring more advanced and intelligent **Retrievers** in LangChain. I wanted to see how I could go beyond the basics to fetch more relevant, diverse, and context-rich information to feed to my LLM.

---

### 🤔 The Problem: Naive Search is Not Enough

A basic vector store retriever is great, but it has its limits. It often struggles with:
-   **Ambiguous Queries**: Sometimes a user's question is phrased poorly, and a simple search misses the mark.
-   **Redundant Information**: A simple search might return multiple chunks that all say the same thing.
-   **Lack of Context**: The retriever might miss the "bigger picture" or related concepts that aren't explicitly in the query.

To build a truly smart RAG system, you need smarter retrieval strategies.

---

### ✨ Core Retrieval Strategies I've Explored

This project is a hands-on demonstration of three powerful retrieval techniques:

1.  **Vector Store Retriever (The Baseline)**:
    -   First, I set up a standard `FAISS` vector store and used its basic retriever (`as_retriever`). This is the foundation upon which all other techniques are built.

2.  **Multi-Query Retriever**:
    -   This was a fascinating discovery! The `MultiQueryRetriever` uses an LLM to **rewrite the user's initial query into multiple different versions** from various perspectives. It then performs a search for each of these new queries, collects all the results, and removes duplicates.
    -   **Why it's great**: It's fantastic for tackling ambiguous questions and uncovering documents that a single query might have missed.

3.  **Contextual Compression & Reranking**:
    -   This is probably the most powerful technique I explored. After an initial retrieval, a `ContextualCompressionRetriever` adds a second step:
        -   **Compression**: It passes the retrieved documents through another model (like an `LLMChainExtractor` or a `CohereRerank` model) that either pulls out only the most relevant sentences or completely filters out irrelevant documents.
        -   **Reranking**: More advanced compressors can also re-rank the documents based on their relevance to the original query, ensuring the absolute best context is passed to the final LLM.
    -   **Why it's great**: It drastically reduces noise and ensures that only the highest quality, most relevant information makes it to the final prompt, leading to much better answers.

---

### 🛠️ Tech Stack

-   **Core Framework**: LangChain
-   **LLM & Embedding Provider**: OpenAI
-   **Reranking Provider**: Cohere
-   **Vector Store**: FAISS (CPU version)
-   **Document Loading**: PyPDF
-   **Notebook Environment**: Jupyter

---

### ⚙️ Setup and Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/jsonusuman351/Langchain_Retrivers.git](https://github.com/jsonusuman351/Langchain_Retrivers.git)
    cd Langchain_Retrivers
    ```

2.  **Create and activate a virtual environment:**
    ```bash
    # It is recommended to use Python 3.10 or higher
    python -m venv venv
    .\venv\Scripts\activate
    ```

3.  **Install the required packages:**
    Since I worked directly in a Jupyter Notebook, there isn't a `requirements.txt` file. You can install all the necessary libraries by running this command:
    ```bash
    pip install langchain langchain-core langchain-openai langchain-community openai python-dotenv faiss-cpu pypdf cohere jupyter
    ```

4.  **Set Up Your Environment:**
    -   You will need to **provide your own PDF document** to use as the knowledge base. Place it in the same directory as the notebook.
    -   You also need to **securely provide your API keys**. I recommend setting them as environment variables on your system, but for a quick start, you can also place them directly in the notebook (just remember not to commit them to GitHub!). You'll need keys for OpenAI and Cohere.

---

### 🚀 How to Use This Project

The entire workflow is contained within a single, well-documented Jupyter Notebook.

1.  **Launch Jupyter:**
    Make sure your virtual environment is active, then run:
    ```bash
    jupyter notebook
    ```

2.  **Open the Notebook:**
    In the Jupyter interface that opens in your browser, click on `Langchain_Retrivers.ipynb`.

3.  **Update the PDF Path and Add API Keys:**
    Before running, make sure to update the notebook cell that loads the PDF to point to your own document. Also, ensure your API keys are accessible.

4.  **Run the Cells:**
    You can run each cell in the notebook sequentially to see the entire process, from setting up the base retriever to experimenting with the advanced multi-query and contextual compression techniques.

---

### 🔬 A Tour of My Retrieval Experiments

I've organized this entire project into a single Jupyter Notebook to make it easy to follow my experiments with different retrieval strategies.

<details>
<summary>Click to view the code layout</summary>

```
Langchain_Retrivers/
│
└── Langchain_Retrivers.ipynb    # The complete end-to-end workflow is in this single notebook
```
</details>

---

---
