# Supplementary Attributes to Enrich the Movie Dataset

To provide deeper insight into each film's critical reception, regulatory treatment, and audience engagement, we propose the following three supplementary attributes:

---

### 1. **Censorship Cuts Data**
- **Attributes**:  
  - `cut_description`: Description of each cut/modification  
  - `cut_type`: Type of change (e.g., deletion, replacement, insertion)  
  - `cut_duration`: Number of seconds removed or altered  
  - `cut_guideline_code`: CBFC rule or guideline cited for the cut  
- **Source**:  
  - [Dataful Dataset #21452](https://dataful.in/datasets/21452/) – *“Movie Cuts by CBFC”*  
- **Collection Method**:  
  - Download the dataset in CSV or Parquet format  
  - Join with movie records based on title, year, and language  
  - Clean text fields and summarize per film if multiple cuts exist  
- **Purpose**:  
  - Analyze how regulatory decisions vary by genre, language, or theme  
  - Explore trends in censorship over time

---

### 2. **Awards and Accolades**
- **Attributes**:  
  - `award_name`: Name of the award (e.g., Filmfare, National Film Award)  
  - `award_year`: Year of nomination or win  
  - `award_category`: Category (e.g., Best Actor, Best Screenplay)  
  - `nomination_type`: Win or nomination  
- **Source**:  
  - **Wikipedia** award sections for each film  
- **Collection Method**:  
  - Use the `wikipedia` Python library and each film’s `Wikipedia URL`  
  - Parse structured award tables or bullet lists from the "Accolades" or "Reception" sections  
- **Purpose**:  
  - Capture critical acclaim and artistic recognition  
  - Compare commercial and critical success side-by-side

---

### 3. **Poster Analyses**
- **Attributes**:  
  - `character_genders`: Gender of the actors depicted on the poster which is the largest   
  - `symbols`: Number of different types of symbols portrayed in the poster (e.g., Indian flag, sindoor on female character's forehead, etc)  
  - `character_poses`: Types of poses depicted by characters (namaste, salute, couple in an embrace, standing, fightig stance, etc)  
- **Source**:  
  - posters already collected for this project  
- **Collection Method**:  
  - Use Anthropic to run an analysis of each of the movie posters for the given attributes  
- **Purpose**:  
  - To assess visual representation and gender dynamics by analyzing whether male or female actors are more prominently featured, reinforcing or challenging on-screen gender roles identified in the movie’s themes.
  - To examine symbolic posturing and power portrayal, using actors’ stances (e.g., assertive, submissive, protective) to identify visual cues that align with or contradict the film's narrative sentiment (e.g., confrontational vs escapist). 
