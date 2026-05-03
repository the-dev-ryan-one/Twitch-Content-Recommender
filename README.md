# Twitch Content Recommendation Engine
### Python | Dask | NumPy | Collaborative Filtering | DATA301 — University of Canterbury

**Grade: 100%**

---

## Overview
A user-based collaborative filtering recommendation system built on 15.5 million records 
of Twitch watch history. Given a target user, the system identifies similar users via cosine 
similarity and recommends streamers they haven't watched yet.

**Research question:** How well does user similarity predict the accuracy of Twitch-streamer 
recommendations, as measured by Recall@K?

**Conclusion:** Yes — there is a strong positive correlation between the cosine similarity of 
a user's nearest neighbours and recommendation accuracy (Recall@K).

---

## How It Works
1. Downloads and preprocesses Twitch watch history CSV data using Dask
2. Calculates watch time per user per streamer, normalised to a percentage of total watch time
3. Computes cosine similarity between the target user and all other users
4. Selects the top 5 nearest neighbours and weights their watch preferences by similarity
5. Recommends the top predicted streamers the target user hasn't watched
6. Evaluates accuracy using Recall@K against held-out ground truth data

---

## Results
- Recall@K significantly outperformed random recommendations across all test users
- Larger dataset size correlated with higher Recall@K — more data means closer neighbours
  and more accurate recommendations
- Key limitation: the lookup dictionary creation is sequential and doesn't parallelise well,
  limiting scalability

---

## Tech Stack
**Language:** Python  
**Big Data Processing:** Dask (distributed computing, local cluster)  
**Numerical Computing:** NumPy, SciPy  
**Dataset:** 15.5M records — UCSD McAuley Lab Twitch Dataset  

---

## Running the Model
```python
run_model(UserIDofInterest, problemSize, numberOfWorkers, k)
```
- `problemSize` — number of records to process
- `numberOfWorkers` — number of Dask workers (CPUs)
- `k` — number of recommendations to generate
