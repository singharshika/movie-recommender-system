Movie Recommender System
This project implements a content-based movie recommendation system using machine learning techniques. It provides personalized movie recommendations based on the similarity of movie features such as genres, keywords, tagline, cast, and director. The system also fetches movie posters using The Movie Database (TMDb) API to make the recommendations more visually appealing.

Table of Contents
Overview
Features
Requirements
Installation
Usage
Data
Model
API
Gradio Interface
Contributing
License
Overview
The Movie Recommender System is built using the following components:

Pandas: For data manipulation and analysis.
Scikit-learn: For vectorizing movie features and calculating cosine similarity.
Difflib: To find close matches for user-inputted movie names.
Gradio: For creating an interactive web interface.
Requests: For fetching movie posters from TMDb API.
Features
Content-Based Filtering: Recommends movies based on the content of the movies the user likes.
Poster Fetching: Uses TMDb API to fetch and display movie posters.
Interactive Interface: Gradio is used to build a simple, user-friendly web interface for the system.

Requirements
To run this project, you'll need to install the following Python packages:
pip install pandas scikit-learn gradio requests
Installation
Clone this repository:
git clone https://github.com/yourusername/movies-recommender.git
cd movies-recommender
Install the required Python packages:
pip install -r requirements.txt

Add your TMDb API key to the fetch_poster function in the app.py file:
url = f"https://api.themoviedb.org/3/movie/{movie_id}?api_key=YOUR_API_KEY&language=en-US"
Place your movies.csv file in the project directory. Ensure that the CSV file contains the following columns: index, id, title, genres, keywords, tagline, cast, and director.
Usage
To run the recommender system, execute the following command:
python app.py
This will launch a Gradio interface in your browser where you can interact with the movie recommender system.

Data
The dataset used in this project is a CSV file (movies.csv) that contains information about various movies. The essential columns are:

index: A unique identifier for each movie.
id: The movie ID corresponding to TMDb.
title: The title of the movie.
genres: The genres associated with the movie.
keywords: Keywords or tags related to the movie.
tagline: The tagline of the movie.
cast: Main cast members.
director: The director of the movie.
Model
Feature Extraction
The selected features (genres, keywords, tagline, cast, director) are combined into a single string for each movie. These combined strings are then transformed into numerical feature vectors using TF-IDF vectorization.

Cosine Similarity
Cosine similarity is used to calculate the similarity between the feature vectors of different movies. The movies with the highest similarity to the selected movie are recommended.

API
Fetch Poster
The fetch_poster function uses the TMDb API to fetch movie posters. If no poster is available, a placeholder image is returned.
def fetch_poster(movie_id):
    url = f"https://api.themoviedb.org/3/movie/{movie_id}?api_key=YOUR_API_KEY&language=en-US"
    data = requests.get(url).json()
    poster_path = data.get('poster_path')
    if poster_path:
        full_path = f"https://image.tmdb.org/t/p/w500/{poster_path}"
        return full_path
    else:
        return "https://via.placeholder.com/500x750?text=No+Image"
Gradio Interface
Gradio is used to create a simple interface where users can select a movie from a dropdown list and receive up to 10 recommended movies along with their posters.

Layout
The layout is divided into rows and columns, with each column displaying the name and poster of a recommended movie.

Functionality
Dropdown: Allows the user to select a movie title.
Show Recommend Button: Triggers the recommendation function and displays the recommended movies.

with gr.Blocks() as demo:
    gr.Markdown("# Movie Recommender System")
    with gr.Row():
        selectvalue = gr.Dropdown(label="Select movie from dropdown", choices=movies_data['title'].tolist(), value=movies_data['title'].tolist()[0])
    show_button = gr.Button("Show Recommend")

    with gr.Row():
        col1 = gr.Column(scale=1)
        # ... other columns and inputs ...

    show_button.click(
        update_recommendations,
        inputs=selectvalue,
        outputs=[rec1_name, rec1_img, rec2_name, rec2_img, ...]
    )

demo.launch()
Contributing
Contributions are welcome! Please feel free to submit a Pull Request or open an Issue on GitHub.





