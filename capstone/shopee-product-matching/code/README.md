## Code

01: Exploratory Data Analysis
    - Explore label groups, image phash, images and titles
    
02: Image Embedding
    - Create image embeddings using default and retrained EfficientNetB4
    
03: Image Nearest Neighbours cuML
    - Use Rapids cuML NearestNeighbors algorithm to predict product matches from image embeddings
    
04: Text Embedding
    - Use TF-IDF vectorizer on processed title tokens to generate text embeddings
    - Use sklearn NearestNeighbors algorithm to predict product matches from text embeddings
    
04a: Semantic Text Embedding LaBSE
    - Use Google LaBSE model to generate semantic text embeddings
    
05: Combined Predictions
    - Combine image and text predictions using different heuristics