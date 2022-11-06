# Recommendation system design overview

- The repo including
    - recommendation system introduction
    - application scenario
    - high level system design

<hr>

## Recommendation system (RS) introduction

- RS is composed of users, items, and algorithm.
- Divided into
    - content-based filtering (CB)
    - collaborative-filtering (CF)
        - user-based
        - item-based
    - hybid approach

### 1. content-based filtering (CB)
- recommend items based on users' activity, along with features of items.
- process of CB:
    - building item features
    - building a user interests profile
    - compute similarity between items & users
    - choose top-N items for recommending
- pros:
    - no data from other users is required to start making recommendations
    - recommendations are highly relevant, transparent to the user
    - avoid the cold start issue (compared to CF)
    - easier to create (most of building item features)
- cons:
    - lack of novelty and diversity
    - Scalability (never ending with building features for new item)
    - selected features may be incorrect (so domain  knowledge is important)

### 2. collaborative filtering (CF)
- memory-based
    - process of CF
        - recommend items based on similar users or items
        - (optional) pre-filter users whose rating counts lower than thresholds
        - build similarity table between users (items)
        - KNN (K-nearest neighbor) algorithm for finding K most similar users (items)
        - predict scores of un-purchased (un-recommended) according to K users (items)
        - ranking, top-N recommendation
    - user-based characteristics
        - sparsity (most item ratings is absent)
        - stability (due to sparsity, similarity may change significantly)
        - scalibility (progressive growth of user & item amount, calculation is increased)
    - item-based characteristics
        - stability (more statble than ub CF)
        - scalibility (pre-computing can reduce scalibility than ub CF)
    
    - choices of similarity
        - cosine similarity
        - adjusted cosine similarity
        - pearson correlation similarity
    
    - summary
        - memory-based algorithm utilizes interaction between users & items for recommendation
- model-based
    - singular value decomposition (SVD)
        - decompose user-item table into three factors
        - choose suitable K for reducing calculation
    - matrix factorization
        - decompose user-item table into user latent table & item latent table
        - minimize loss (e.g. MSE) with predictions from latent table
        - latent weights is arbitrary values, not explainable
    - non-negative matrix factorization
        - take all values in latent table in [0, 1] range
        - more explainable than MF
