# Friend Recommendation in Social Networks: A Comparative Study of Feature Extraction and Learning Techniques

This repository contains the code and methodology for our final project in the *Machine Learning in Network Science* course at CentraleSupélec. We investigate the **link prediction** problem in social networks using a variety of techniques, including handcrafted graph features, graph embeddings, and Graph Neural Networks (GNNs).

📌 **Dataset:** [Facebook Social Circles](https://snap.stanford.edu/data/ego-Facebook.html)

---

## 🔍 Project Overview

We aim to recommend friends by predicting the likelihood of a link between two users in a social graph. We compare four different modeling strategies:

1. **Local & Global Structural Features + ML Classifiers**
2. **Node2Vec Embeddings + ML Classifiers**
3. **SVD-Based Feature Construction + ML Classifiers**
4. **Node2Vec + GNN (GraphSAGE)**

All models are trained and evaluated on a balanced dataset split from the Facebook combined network (4039 nodes, 88234 edges), with performance assessed using AUC, F1, Precision, and Recall.


---

## 🧪 Models and Techniques

### 1. Local & Global Graph Features + Classifiers
- Features: Common Neighbors, Density Metrics, Inverse Degree Similarity.
- Classifiers: Random Forest, XGBoost
- Additional: Circle-aware features extracted from `.circles` files.

### 2. Node2Vec Embeddings
- Generates 64-dimensional embeddings for each node.
- Edge features created via Hadamard product.
- Hyperparameter tuning on (p, q) to explore different walk strategies.

### 3. SVD-based Features
- Dimensionality reduction on the adjacency matrix (TruncatedSVD).
- Combined with circle features and trained using XGBoost and RF.

### 4. GNN (Node2Vec + GraphSAGE)
- Node2Vec embeddings used as initial features.
- GraphSAGE layers aggregate neighbor info.
- Final prediction via MLP with sigmoid.

---

## 📊 Results Summary

| Model                                | F1 Score | ROC-AUC |
|-------------------------------------|----------|---------|
| Graph Features + XGBoost            | **0.9758** | **0.9957** |
| SVD + XGBoost                       | 0.9713   | 0.9946  |
| Node2Vec + XGBoost (p=1, q=4)       | 0.7937   | 0.8715  |
| Node2Vec + GNN                      | 0.9014   | 0.9475  |
