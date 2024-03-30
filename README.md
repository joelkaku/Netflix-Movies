![netflix image](https://github.com/joelkaku/Netflix-Movies/assets/131392907/c3790652-1242-47e5-9caa-44c5ba3fc4fb)

### Unveiling the Stories Behind the Stream: An Exploratory Data Analysis of Netflix with Python

**Netflix**! What started in 1997 as a DVD rental service has since exploded into one of the largest entertainment and media companies.

In this project, I delve into the captivating world of Netflix, leveraging the power of Python to analyze its vast dataset. I aim to uncover hidden patterns, intriguing trends, and valuable insights that lie beneath the surface of our viewing habits. The columns and their descriptions are shown below:


### **netflix_data.csv**
| Column | Description |
|--------|-------------|
| `show_id` | The ID of the show |
| `type` | Type of show |
| `title` | Title of the show |
| `director` | Director of the show |
| `cast` | Cast of the show |
| `country` | Country of origin |
| `date_added` | Date added to Netflix |
| `release_year` | Year of Netflix release |
| `duration` | Duration of the show in minutes |
| `description` | Description of the show |
| `genre` | Show genre |

- Import the necessary libraries:
```
# Importing pandas, numpy and matplotlib
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
```

- Load the CSV file and store as netflix_df:
```
# importing the csv with pandas into a netflix dataframe
netflix_df = pd.read_csv("netflix_data.csv")
```

- Filter the data for movies only and store as netflix_subset:
```
# subsetting for Movies only
netflix_subset = netflix_df[netflix_df["type"]== "Movie"]
```

- Investigate and subset the Netflix movie data, keeping only the columns "title", "country", "genre", "release_year", "duration", in a new DataFrame called netflix_movies:
```
netflix_movies = netflix_subset[["title", "country", "genre", "release_year", "duration"]]
```

- Filter netflix_movies to find the movies that are strictly shorter than 60 minutes, saving the resulting DataFrame as short_movies:
```
short_movies = netflix_movies[netflix_movies['duration'] < 60]
```

- Using a for loop and if/elif statements, iterate through the rows of netflix_movies and assign colors of your choice to four genre groups ("Children", "Documentaries", "Stand-Up", and "Other" for everything else):
```
# iterating over the rows to assign colours to different genres in the genre column
# the colors are appended to a predefined list
colors = []
for lab, row in netflix_movies.iterrows():
    if row["genre"] == "Children":
        colors.append("Red")
    elif row["genre"] == "Documentaries":
        colors.append("Yellow")
    elif row["genre"] == "Stand-Up":
        colors.append("Green")
    else:
        colors.append("Blue")
```

- Create a scatter plot for movie duration by release year using the colors list to color the points and using the labels "Release year" for the x-axis, "Duration (min)" for the y-axis, and the title "Movie Duration by Year of Release":
```
# visualising the distribution of movie durations by release year using a scatter plot      
fig = plt.figure(figsize=(12, 8)) 
plt.scatter(netflix_movies["release_year"], netflix_movies["duration"], c = colors)
plt.xlabel("Release year")
plt.ylabel("Duration (min)")
plt.title("Movie Duration by Year of Release")

#calculating the equation for trendline
z = np.polyfit(netflix_movies["release_year"], netflix_movies["duration"], 1)
p = np.poly1d(z)

#adding trendline to plot
plt.plot(netflix_movies["release_year"], p(netflix_movies["release_year"]),color="black", linewidth=2, linestyle="--")

plt.show()
```
![matplotlip](https://github.com/joelkaku/Netflix-Movies/assets/131392907/3df79006-c3ce-45b8-9808-21c56924d27b)


### Deductions:

The scatter plot provides insights into the trend of movie durations over time. Let’s break down the key observations:

- **Overall Trend:**
The plot shows a downward trend in average movie durations.
In the earlier years (around 1940 to 1970), movies had a wide range of durations but generally were longer.
However, there is a noticeable decline in movie lengths over the last decade.
- **Recent Years:**
Post-2000, movie durations are more clustered between 50 and 150 minutes.
This suggests that filmmakers are favoring shorter movies in recent times.
- **Business Implications:**
Filmmakers and streaming platforms like Netflix may be adapting to changing viewer preferences.
Shorter movies could lead to higher engagement, as audiences may find them more accessible and easier to watch.
Longer movies on the other hand, would keeps viewers glued to their screens for longer, thus increasing revenue for Netflix through prolonged screen time.  

It is worth noting, however, that this analysis is based on the provided data, and other factors (such as genre, audience demographics, and cultural shifts) may also influence movie durations. Further exploration and context-specific analysis would be valuable to draw more robust conclusions
