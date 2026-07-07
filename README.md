# MyAnimeList Data Collector & Manga Recommendation System

Scrape and collect anime/manga data using MAL API / Jikan API.
This project is strictly for educational purposes, and does not use direct web browser automation for illegal data scraping.
**Not for commercial or any other illegal purposes.**

---

## Course Project: Introduction to Data Science (Group 03)
An integrated system featuring two recommendation models: Content-based Filtering and a RAG Chatbot.

### Project Structure

The project is divided into two main directories corresponding to the two subsystems:

1. **`content_based_filtering/`**: A Manga recommendation system using TF-IDF & Weighted Soup.
2. **`semantic_analysis/`**: A Manga recommendation system using RAG, ChromaDB & a Multilingual Model.

---

## Installation & Setup

Before running the project, please install the required libraries:

```bash
pip install streamlit pandas numpy scikit-learn chromadb sentence-transformers
```

## User Guide

### 1. Content-Based Filtering Model

**Functionality**: Recommends similar Manga based on the user's history and ratings.

**Step 1:** Navigate to the directory:
```bash
cd content_based_filtering
```

**Step 2:** Train the model (generates the `.pkl` file):
```bash
python train.py
```
*(The system will process the data and save the model into the `models/` directory)*

**Step 3:** Launch the application:
```bash
streamlit run app.py
```

---

### 2. RAG Chatbot Model

**Functionality**: Search for Manga using natural language (with excellent Vietnamese support) via a Chatbot.

**Step 1:** Navigate to the directory:
```bash
cd semantic_analysis
```

**Step 2:** Data Preparation (Only required on the first run or if data files are lost):
- Run `eda_analysis.ipynb` (Run All) to clean the data and create the `processed_manga.pkl` file.
- Run `model_vn.ipynb` (Run All) to create the Vector Database with Vietnamese support (`manga_chroma_db_vn`).

**Step 3:** Launch the Chatbot:
```bash
streamlit run app.py
```

---

## Technical Pipeline & Methodologies

**For Content-based Filtering:**
- **Feature Engineering:** Uses the "Weighted Soup" technique—combining Genres (x3), Themes (x2), Demographics (x2), Score, and Synopsis.
- **Vectorization:** Uses TF-IDF (n-gram=(1,2); max_features=10,000).
- **Similarity:** Calculates Cosine Similarity to find related manga.

**For Semantic Analysis & RAG Data Collection:**
- **Scraping:** `scrape_and_clean_new.ipynb` (Collects data from Jikan API v4).
- **Cleaning & EDA:** `eda_analysis.ipynb` (Handles noisy data, removes sensitive content, plots distribution charts and Knowledge Graph).
- **Embedding Models:**
  - Recommended (Vietnamese): `model_vn.ipynb` using the `paraphrase-multilingual-mpnet-base-v2` model.
  - Lightweight version (English): `model_eng.ipynb` using the `all-MiniLM-L6-v2` model.
- **Retrieval:** Uses ChromaDB for vector querying and a Hybrid Ranking algorithm (combining semantic score and popularity).

---

## Team Members (Group 03)

1. Sần Dịch Anh - 21120411: Crawl Data, Data Cleaning, questioning.
2. Nguyễn Văn Hậu - 21120449: EDA, built Content-based Filtering model.
3. Nguyễn Trung Dũng - 21120228: EDA, built RAG Model + Semantic Search, ChromaDB.
4. Ngô Gia Long - 20120525: Streamlit UI Code, Presentation Slides.
