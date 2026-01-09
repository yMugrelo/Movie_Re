# Movie Recommendation System

## Overview

This project implements a hybrid movie recommendation system that combines multiple Machine Learning techniques to deliver accurate and diverse recommendations. The system follows a microservices-oriented architecture, featuring a FastAPI backend for model inference and data integration, and a Streamlit frontend for interactive user exploration.

The primary objective is to demonstrate the full lifecycle of an ML-powered product, including data preprocessing, model training, API deployment, and real-time inference.

---

## Key Features

### Hybrid Recommendation Engine
- Content-based filtering using TF-IDF vectorization on movie plot descriptions  
- Genre-based recommendations leveraging TMDB metadata  
- Weighted combination of multiple recommendation signals to balance relevance and diversity  

### Production-Oriented Backend
- RESTful API built with FastAPI  
- Asynchronous request handling  
- Response caching to reduce latency and external API usage  
- CORS-enabled for frontend-backend separation  

### Interactive Frontend
- Real-time movie search with autocomplete  
- Dynamic recommendation generation  
- Responsive grid-based layout  
- Detailed movie views with posters and metadata  

### Real-Time Data Integration
- Integration with TMDB API (300k+ movies)  
- Up-to-date movie metadata  
- High-resolution posters and backdrops  

---

## System Architecture

┌─────────────────┐
│ Streamlit UI │
│ (Frontend) │
└────────┬────────┘
│ HTTP / REST
┌────────▼────────┐ ┌──────────────┐
│ FastAPI │◄─────┤ TMDB API │
│ (Backend) │ │ (External) │
└────────┬────────┘ └──────────────┘
│
┌────▼─────┐
│ ML Model │
│ (TF-IDF) │
└──────────┘


---

## Machine Learning Methodology

### Content-Based Filtering (TF-IDF)

The system applies TF-IDF (Term Frequency–Inverse Document Frequency) vectorization to movie plot descriptions to compute semantic similarity between titles.

**Pipeline**
1. Text preprocessing (lowercasing, stop-word removal)  
2. TF-IDF vectorization with unigrams and bigrams  
3. Cosine similarity computation  
4. Retrieval of top-N most similar movies  

TF-IDF was selected for its computational efficiency, explainability, and suitability for real-time recommendation workloads.

---

### Genre-Based Recommendations

Genre-based filtering complements textual similarity by leveraging TMDB’s genre taxonomy:

1. Extraction of the primary genre for the selected movie  
2. Querying TMDB’s discovery endpoint  
3. Filtering results by popularity and rating thresholds  
4. Excluding the input movie from the result set  

This approach supports discovery while maintaining contextual relevance.

---

### Hybrid Strategy

Final recommendations combine both methods:
- TF-IDF-based results emphasize narrative and semantic similarity  
- Genre-based results promote diversity and popularity-aware discovery  

This hybrid strategy reduces over-specialization and improves recommendation coverage.

---

## Dataset

**Source:** The Movies Dataset (Kaggle)

**Statistics**
- Over 45,000 movies from the MovieLens dataset  
- Metadata including budget, revenue, release date, language, and production companies  
- Categorical features such as genres, keywords, cast, and crew  
- Popularity scores and user ratings  

**Preprocessing Steps**
- Handling missing values in critical fields (title, overview)  
- Parsing JSON-encoded columns  
- Feature engineering by combining plot, genre, and keyword information  
- Text normalization and cleaning  

---

## Getting Started

### Prerequisites
- Python 3.9+  
- pip or conda  
- TMDB API key  

## Model Performance

### TF-IDF Similarity Metrics

- Vocabulary size: ~15,000 terms  
- Matrix sparsity: ~99.7%  
- Average query latency: ~45 ms  
- Top-10 relevance accuracy: ~73% (user study, N=50)  

Evaluation prioritized real-time usability and qualitative relevance.

---

## Development Notes

Model training is performed offline using Jupyter notebooks. Trained artifacts are serialized and loaded by the FastAPI service at startup to ensure fast inference and reproducibility.

The system is structured to allow extension with additional recommendation signals without significant architectural changes.

---

## License

MIT License

---

## Contact

**Author:** Murilo Rosa  
**GitHub:** https://github.com/yMugrelo/Movie_Re
**Live Demo:** https://movie-rec.streamlit.app

