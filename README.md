# Spotify Advanced SQL Project and Query Optimization

This project demonstrates advanced SQL concepts using a Spotify dataset.  
It includes database schema design, query writing (easy → advanced), and query optimization techniques such as indexing and execution plan analysis.

📂 [Click here to download the dataset](https://www.kaggle.com/datasets/sanjanchaudhari/spotify-dataset)

![Spotify Logo](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_logo.jpg)

## Overview
This project involves analyzing a Spotify dataset with various attributes about tracks, albums, and artists using **SQL**. It covers an end-to-end process of normalizing a denormalized dataset, performing SQL queries of varying complexity (easy, medium, and advanced), and optimizing query performance. The primary goals of the project are to practice advanced SQL skills and generate valuable insights from the dataset.

```sql
-- create table
DROP TABLE IF EXISTS spotify;
CREATE TABLE spotify (
    artist VARCHAR(255),
    track VARCHAR(255),
    album VARCHAR(255),
    album_type VARCHAR(50),
    danceability FLOAT,
    energy FLOAT,
    loudness FLOAT,
    speechiness FLOAT,
    acousticness FLOAT,
    instrumentalness FLOAT,
    liveness FLOAT,
    valence FLOAT,
    tempo FLOAT,
    duration_min FLOAT,
    title VARCHAR(255),
    channel VARCHAR(255),
    views FLOAT,
    likes BIGINT,
    comments BIGINT,
    licensed BOOLEAN,
    official_video BOOLEAN,
    stream BIGINT,
    energy_liveness FLOAT,
    most_played_on VARCHAR(50)
);
```
## Project Steps

### 1. Data Exploration
The first step was to understand the dataset thoroughly. The dataset contains attributes such as:
- `Artist`: The performer of the track.
- `Track`: The name of the song.
- `Album`: The album to which the track belongs.
- `Album_type`: The type of album (e.g., single or album).
- Audio features such as `danceability`, `energy`, `loudness`, `tempo`, and more.

### 2. Querying the Data
After loading the data, SQL queries were written to explore and analyze the dataset. Queries were structured into three difficulty levels to progressively build proficiency:

- **Easy** → Basic retrieval, filtering, and aggregations.  
- **Medium** → Grouping, joins, and more complex aggregations.  
- **Advanced** → Subqueries, CTEs, window functions, and optimization techniques.  

### 3. Query Optimization
At the advanced stage, the focus shifted to improving performance:  
- **Baseline Analysis**: Used `EXPLAIN ANALYZE` to check query cost and execution time.  
- **Indexing**: Added indexes on frequently queried columns such as `artist` to improve performance.  
- **Post-Optimization Check**: Compared execution plans before and after indexing.  

**Result:** Execution time reduced from ~7 ms to ~0.15 ms after indexing.  

---

## 15 Practice Questions

### Easy Level
1. Retrieve the names of all tracks that have more than 1 billion streams.  
2. List all albums along with their respective artists.  
3. Get the total number of comments for tracks where `licensed = TRUE`.  
4. Find all tracks that belong to the album type `single`.  
5. Count the total number of tracks by each artist.  

### Medium Level
1. Calculate the average danceability of tracks in each album.  
2. Find the top 5 tracks with the highest energy values.  
3. List all tracks along with their views and likes where `official_video = TRUE`.  
4. For each album, calculate the total views of all associated tracks.  
5. Retrieve the track names that have been streamed on Spotify more than YouTube.  

### Advanced Level
1. Find the top 3 most-viewed tracks for each artist using window functions.  
2. Write a query to find tracks where the liveness score is above the average.  
3. Use a `WITH` clause to calculate the difference between the highest and lowest energy values for tracks in each album.  

```sql
WITH cte AS (
    SELECT 
        album,
        MAX(energy) AS highest_energy,
        MIN(energy) AS lowest_energy
    FROM spotify
    GROUP BY album
)
SELECT 
    album,
    highest_energy - lowest_energy AS energy_diff
FROM cte
ORDER BY energy_diff DESC;
```
   
5. Find tracks where the energy-to-liveness ratio is greater than 1.2.  
6. Calculate the cumulative sum of likes for tracks ordered by the number of views using window functions.  

---

## Query Optimization Technique 

To improve query performance, the following optimization steps were applied:

- **Initial Query Performance Analysis (`EXPLAIN`)**  
  - Baseline query tested on the `artist` column.  
  - Results:  
    - Execution time: **7 ms**  
    - Planning time: **0.17 ms**  
  - ![EXPLAIN Before Index](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_explain_before_index.png)  

- **Index Creation**  
  - Added an index on the `artist` column to speed up lookups.  
  - SQL command:  
    ```sql
    CREATE INDEX idx_artist ON spotify_tracks(artist);
    ```

- **Performance After Indexing**  
  - Execution time reduced to **0.153 ms**  
  - Planning time reduced to **0.152 ms**  
  - ![EXPLAIN After Index](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_explain_after_index.png)  

- **Graphical Performance Comparison**  
  - Execution and planning times dropped significantly after indexing.  
  - ![Performance Graph](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_graphical%20view%203.png)  
  - ![Performance Graph](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_graphical%20view%202.png)  
  - ![Performance Graph](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_graphical%20view%201.png)  

**Conclusion:** Indexing drastically improved query performance, reducing execution time from ~7 ms to ~0.15 ms.  

---

## Technology Stack
- **Database**: PostgreSQL  
- **SQL Queries**: DDL, DML, Aggregations, Joins, Subqueries, Window Functions  
- **Tools**: pgAdmin 4 (or any SQL editor), PostgreSQL installation (Homebrew, Docker, or direct)  

---

## How to Run the Project
1. Install PostgreSQL and pgAdmin (or any SQL editor).  
2. Create the database schema and tables using the provided structure.  
3. Load the dataset into the database.  
4. Execute SQL queries (easy → medium → advanced).  
5. Apply indexing and review execution plans for optimization.  

---

## Next Steps
- Build dashboards in **Tableau** or **Power BI** for visualization.  
- Scale the dataset for broader analysis and testing.  
- Explore advanced optimization: partitioning, clustering, and composite indexes.  

---

## License
This project is licensed under the MIT License.
