### EX6 Information Retrieval Using Vector Space Model in Python
### DATE: 
### AIM: To implement Information Retrieval Using Vector Space Model in Python.
### Description: 
<div align = "justify">
Implementing Information Retrieval using the Vector Space Model in Python involves several steps, including preprocessing text data, constructing a term-document matrix, 
calculating TF-IDF scores, and performing similarity calculations between queries and documents. Below is a basic example using Python and libraries like nltk and 
sklearn to demonstrate Information Retrieval using the Vector Space Model.

### Procedure:
1. Define sample documents.
2. Preprocess text data by tokenizing, removing stopwords, and punctuation.
3. Construct a TF-IDF matrix using TfidfVectorizer from sklearn.
4. Define a search function that calculates cosine similarity between a query and documents based on the TF-IDF matrix.
5. Execute a sample query and display the search results along with similarity scores.

### Program:
```
import requests
from bs4 import BeautifulSoup
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
from nltk.tokenize import word_tokenize
from nltk.corpus  import stopwords
import string
import nltk
# Download necessary NLTK datasets
nltk.download('punkt')
nltk.download('stopwords')

# Sample documents stored in a dictionary
documents = {
    "doc1": "This is the first document.",
    "doc2": "This document is the second document.",
    "doc3": "And this is the third one.",
    "doc4": "Is this the first document?",
}

# Preprocessing function to tokenize and remove stopwords/punctuation
def preprocess_text(text):
    tokens = word_tokenize(text.lower())
    tokens = [token for token in tokens if token not in stopwords.words("english") and token not in string.punctuation]
    return " ".join(tokens)

# Preprocess documents and store them in a dictionary
preprocessed_docs = {doc_id: preprocess_text(doc) for doc_id, doc in documents.items()}

# Construct TF-IDF matrix
tfidf_vectorizer = TfidfVectorizer()
tfidf_matrix = tfidf_vectorizer.fit_transform(preprocessed_docs.values())

# Calculate cosine similarity between query and documents
def search(query, tfidf_matrix, tfidf_vectorizer):
    query_vec = tfidf_vectorizer.transform([preprocess_text(query)])
    cosine_sim = cosine_similarity(query_vec, tfidf_matrix).flatten()
    results = []
    
    for doc_id, score in zip(documents.keys(), cosine_sim):
        results.append((doc_id, documents[doc_id], score))
    
    results.sort(key=lambda x: x[2], reverse=True)  # Sort by similarity score in descending order
    return results

# Get input from user
query = input("Enter your query: ")

# Perform search
search_results = search(query, tfidf_matrix, tfidf_vectorizer)

# Display search results
print("Query:", query)
for i, result in enumerate(search_results, start=1):
    print(f"\nRank: {i}")
    print("Document ID:", result[0])
    print("Document:", result[1])
    print("Similarity Score:", result[2])
    print("----------------------")

# Get the highest rank cosine score
highest_rank_score = max(result[2] for result in search_results)
print("The highest rank cosine score is:", highest_rank_score)
```

### Output:
![Screenshot 2024-09-28 142336](https://github.com/user-attachments/assets/124a6d2b-5a09-4865-b922-947c088c1a3a)

### Result:
CODE EXECUTED SUCCESSFULLY
