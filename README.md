# Data Mining & Music Recommendation System

## Repository Contents

### MovieLens Dataset Analysis
1. **Data Preparation Analysis**: Initial data cleaning, basic statistics, and visualization of the MovieLens dataset.
2. **Structure Analysis**: Investigation of data patterns using probability distributions and clustering methods.

### Music Genre Classification and Recommendation Systems

Implementation of a music genre classification and recommendation system using Spotify data.

## 1. Music Genre Classification

### 1.1 Data Processing

We will classify songs into 6 of the most popular genres on Spotify:
- Rap
- Pop
- Rock
- Latin
- EDM
- Classical

The genres were selected based on popularity data from Every Noise (https://everynoise.com/everynoise1d.cgi?scope=all).

Initial genre characteristics hypothesis:
- Classical: High instrumentalness and acousticness
- Rap: High speechiness
- Rock: Low danceability
- EDM: High tempo and energy
- Latin: High danceability
- Pop: Mixed characteristics

#### Data Collection
Used Spotify's API through the Spotipy library to collect:
- 200 artists per genre (1,200 total)
- 10 albums per artist (12,000 total)
- 10 songs per album (120,000 total)
- After removing duplicates: 83,698 unique tracks

<img src="resources/genre/num_tracks.png" width="400"/>

<img src="resources/genre/duration_outliers.png" width="800"/>
<img src="resources/genre/outliers_minMax.png" width="500"/>
<img src="resources/genre/outliersRemoved_minMax.png" width="500"/>

#### Feature Analysis

<img src="resources/genre/audioF_14.png" width="900"/>
<img src="resources/genre/audioF_58.png" width="900"/>
<img src="resources/genre/audioF_912.png" width="900"/>

<img src="resources/genre/audioF_boxplot_16.png" width="900"/>

Key findings from audio feature analysis:
- Rap shows significantly higher speechiness
- Classical and Rock have distinct danceability patterns
- Energy levels are lowest in Classical, highest in Rock and EDM
- Instrumentalness and acousticness are dominant in Classical
- Rock shows higher liveness scores

<img src="resources/genre/audioF_boxplot_712.png" width="900"/>

- Classical tends toward more somber valence, while Latin shows higher positive valence
- Classical has lower loudness and more varied duration
- EDM shows the most consistent tempo patterns
- Key and mode showed no significant patterns for genre classification

<img src="resources/genre/audio_features_correlation.png" width="900"/>

Notable correlation: Energy and loudness show strong positive correlation

### 1.2 Genre Classification

#### Models Used
1. Decision Tree
2. K-Nearest Neighbors (KNN)
3. Random Forests
4. Gradient Boosting Classifier

Baseline accuracy threshold: 17% (random chance with 6 genres)

<img src="resources/genre/matrix_4.png" width="900"/>
<img src="resources/genre/classifiersAccuracy.png" width="500"/>

#### Results
Classification accuracy by genre:
- Classical: 93% (highest)
- Rock: 70%
- Rap: 67%
- EDM: 60%
- Latin: 57%
- Pop: 33% (lowest)

Model Performance:
- KNN performed 3% better than Decision Trees
- Random Forests showed significant improvement over KNN, especially for Rock and Rap
- Gradient Boosting achieved similar accuracy to Random Forests but with higher computational cost

## 2. Song Recommendation System

### 2.1 Playlist Similarity Analysis

Analyzed 24 playlists across genres:
- Classical (4 playlists)
- Rap (4 playlists)
- EDM (2 playlists)
- Techno (1 playlist)
- House (1 playlist)
- Rock (4 playlists)
- Latin (4 playlists)
- Pop (4 playlists)

<img src="resources/vector/playlist_vector.png" width="700"/>

Methodology:
1. Created feature vectors using mean/sum of track attributes
2. Added genre distribution vectors
3. Calculated similarity using cosine similarity

<img src="resources/vector/delez_zanrov.png" width="700"/>
<img src="resources/vector/podobnost_playlistov_vector.png" width="300"/>

### 2.2 KNN-Based Song Recommendations

Process:
1. Select n random songs from playlists
2. Find 100 nearest neighbors for each song
3. Calculate playlist distribution of neighbors

<img src="resources/knn/knn_10pesmi.png" width="700"/>

Results showed strong genre clustering, particularly for Classical and Rap genres.

<img src="resources/knn/delez_sosedov1.png" width="400"/>

### 2.3 Playlist Recommendation System

Final implementation:
1. Find 3 most similar playlists using KNN mean
2. Select 2 most similar songs from each playlist
3. Recommend 6 songs total (2 songs × 3 playlists)

Results by genre:

Classical:
<img src="resources/knn/reccomended_songs_klasika.png" width="900"/>

Rap:
<img src="resources/knn/reccomended_songs_rap.png" width="700"/>

Latin:
<img src="resources/knn/reccomended_songs_latino.png" width="600"/>

Key Findings:
- System shows strong performance in maintaining genre consistency
- Classical and Rap recommendations show highest accuracy
- System successfully identifies user preferences based on playlist history
- Limitation: Musical preference remains subjective and depends on factors beyond audio features

Note: The system performs well within the test set of 24 playlists but would need further validation on larger datasets.