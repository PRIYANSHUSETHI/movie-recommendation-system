# Movie Recommendation System

This repository contains a **Movie Recommendation System** built using **Content-Based Filtering** with elements of **Popularity-Based Filtering**. The system recommends movies by analyzing their textual features and computing **cosine similarity** to find the best matches.

## Features
- **Content-Based Filtering**: Recommends movies similar to the user-inputted title.
- **TF-IDF Vectorization**: Converts movie descriptions into numerical vectors.
- **Cosine Similarity Algorithm**: Computes similarity scores between movies.
- **Automatic Closest Match Detection**: Uses `difflib` to find the best match for user input.
- **Handles Missing Data**: Replaces missing values with empty strings.
- **Displays Top 30 Recommendations**: Returns a ranked list of similar movies.

## Data Requirements
The system requires a dataset (`movies.csv`) with the following columns:
- `index`: Unique identifier for each movie.
- `title`: Movie title.
- `genres`: Movie genres.
- `keywords`: Relevant keywords.
- `tagline`: Movie tagline.
- `cast`: Main cast members.
- `director`: Movie director.

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/movie-recommendation-system.git
   ```
2. Navigate to the project directory:
   ```bash
   cd movie-recommendation-system
   ```
3. Install required dependencies:
   ```bash
   pip install pandas numpy scikit-learn
   ```

## Usage
1. Ensure that `movies.csv` is in the project directory.
2. Run the script:
   ```bash
   python movie_recommendation_system.py
   ```
3. Enter a movie name when prompted.
4. The script will return a ranked list of the top 30 most similar movies.

## Workflow & Key Functions
1. **Data Loading & Preprocessing**
   - Reads `movies.csv` into a Pandas DataFrame.
   - Fills missing values with empty strings.
   - Combines relevant textual features (`genres`, `keywords`, `tagline`, `cast`, `director`) into a single feature string.
   - Example:
     ```python
     for feature in selected_features:
         movies_data[feature] = movies_data[feature].fillna('')
     combined_features = movies_data['genres'] + movies_data['keywords'] + movies_data['tagline'] + movies_data['cast'] + movies_data['director']
     ```

2. **Feature Extraction & Vectorization**
   - Converts text data into numerical feature vectors using **TF-IDF Vectorization**.
   - Example:
     ```python
     vectorizer = TfidfVectorizer()
     feature_vectors = vectorizer.fit_transform(combined_features)
     ```

3. **Similarity Computation**
   - Uses **cosine similarity** to compute similarity scores between all movies.
   - Example:
     ```python
     similarity = cosine_similarity(feature_vectors)
     ```

4. **User Input Handling & Closest Match Detection**
   - Uses `difflib.get_close_matches()` to find the closest movie title from the dataset.
   - Example:
     ```python
     find_close_match = difflib.get_close_matches(movie_name, list_of_all_titles)
     close_match = find_close_match[0]
     ```

5. **Recommendation Generation**
   - Retrieves the index of the closest match.
   - Finds similar movies based on similarity scores.
   - Sorts movies in descending order of similarity.
   - Prints the top 30 recommended movies.
   - Example:
     ```python
     sorted_similar_movies = sorted(similarity_score, key=lambda x: x[1], reverse=True)
     ```

## Example Output
```
Enter A Movie Name: Inception
Movies Suggested for you:
1. Interstellar
2. The Prestige
3. The Dark Knight
...
```

## Dependencies
- `pandas`
- `numpy`
- `scikit-learn`
