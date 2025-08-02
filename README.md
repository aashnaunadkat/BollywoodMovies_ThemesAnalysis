# Step-by-Step Project Workflow

## Step 1: Dataset Preparation
Source: Downloaded the dataset from Kaggle.
Filtering: Cleaned the release_year column to ensure correct datatypes.
Sampling: Wrote a Python script to randomly sample 100 movies released after 2010.

## Step 2: Gathering Movie Data
### 2a. Posters
Used the poster_path from the dataset to download posters.
Logged failed poster downloads (due to missing path or link errors) into a .txt file.
Attempted to scrape posters for failed entries from their corresponding Wikipedia pages.
Only 1 movie poster remained missing, which was manually downloaded.

### 2b. Subtitles
Created an account on opensubtitles.org and generated an API key.
Authenticated using a token and used it to download subtitles.
Due to network instability, ran the script multiple times to retrieve as many subtitles as possible.
Successfully retrieved subtitles for 80 movies; 20 had no subtitles available, even after a manual search.

### 2c. Descriptions
Used the Python Cinemagoer library (formerly known as IMDbpy) to scrape the movie synopsis of each movie using its imdb_id.
Extended the descriptions by scraping longer plot summaries or synopses from the movie's Wikipedia page, since some IMDb synposes were only 1 line. 
- First resolved the final permalink of the Wikipedia page (handling any redirects), and then scanned the page for any section headings that included keywords like "plot", "plot summary", or "synopsis".
- Appended the available synposes to the descriptions from IMDb


## Step 3: Getting Metadata
### 3a. Getting Director Gender
Used the OMDB API to retrieve director names for each movie by imdb_id, stored as director_1_name and director_2_name.
Inferred gender for each director using:
Step 1: Scraped the director’s Wikipedia page and analyzed the first paragraph for gendered pronouns.
Step 2: For directors without a clear Wikipedia result, used a Kaggle dataset of Indian names (https://www.kaggle.com/datasets/shubhamuttam/indian-names-by-gender) to infer gender from the first token of the name (assumed to be the first name).
Avoided using full names to mitigate cultural naming ambiguities (e.g., daughters using father’s name or sons using mother’s name as middle name).
Only 13 director genders remained unidentified after this, and they were manually classified.

### 3b. Getting Box Office Information
Initially used the OMDB API, but it only provided US/Canada box office data for ~25 movies, which was not useful for this project.
Attempted to scrape boxofficeindia.com by:
Searching for each movie’s movie_id via title + release year.
Using the movie_id to access and scrape its box office page.
This approach failed due to the site timing out on every request.
Final approach: Used Wikipedia for box office numbers.
Found usable data for ~60 movies.
Cleaned and standardized the values using a Python script to convert all amounts into INR crores.
This cleaned box office value was appended to the final movie dataset.

## Step 4: Thematic Analysis Using Claude
Created an account on Anthropic and loaded 10$ on it. 
Generated an API key that I could use to analyse my movies.
Cleaned .srt subtitles files and converted them to .txt files, and then appended this to the movie synposes as a combined .txt file.
Used these combined files to run my Anthropic prompt on.

### Justification of added measure for thematic analysis
As an additional analytical measure, I introduced an "Escapist vs. Confrontational" axis to assess the tone and directness with which a film engages with its themes. This measure captures whether a movie acts as a tool for escapism, offering comfort and entertainment, or as a confrontational work that challenges viewers and provokes thought. Unlike many thematic metrics, this dimension is genre-agnostic, making it applicable across a wide range of films and offering deeper insight into how Hindi cinema navigates sociopolitical commentary.
Incorporating this axis alongside the other three (Exclusionary–Secular, Positive–Negative, Progressive–Conservative) adds significant analytical depth. For instance, a film may appear "Progressive" in content, but the Escapist-Confrontational measure reveals how that progressivism is conveyed—whether through a direct, assertive narrative or through a subtle, feel-good story that normalizes the idea without overt confrontation. This added layer enriches time-series analyses by clarifying not just what themes are present, but how they are being presented to audiences, offering a more nuanced understanding of Bollywood’s evolving cinematic language.

## Step 5: Create plots
Used ggplot2 to create time-series plots of each theme / sentiment combination.
