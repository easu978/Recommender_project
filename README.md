# Movie Choice
## Table of Contents

### Project Overview
The project utilizes one of the main two types of Recommender Systems algorithm, Content-Based, to give recommendations to users on the choice of movies they should watch next, by exploring the similarities of the ones they have watched before.

### Data Sources
This project was carried out using two sets of data; "u.data.csv" and "Movie_Id_Titles.csv" files. The former contained the user_id, item_id, rating, and timestamp, while the latter had just two columns - item_id, title.

### Tools
The following tools facilitated the execution of this project;
- Numpy
- Pandas
- Matplotlib
- Seaborn

### Exploratory Data Analysis(EDA)
The data was explored using Pandas and Seaborn, which gave insights on the most rated movies.
```python
column_names = ['user_id', 'item_id', 'rating', 'timestamp']
df = pd.read_csv('u.data', sep='\t', names=column_names)
movie_titles = pd.read_csv("Movie_Id_Titles")
movie_titles.head()
df = pd.merge(df,movie_titles,on='item_id')
df.head()
ratings = pd.DataFrame(df.groupby('title')['rating'].mean())
ratings.head()
ratings['number of ratings'] = pd.DataFrame(df.groupby('title')['rating'].count())
ratings.head()
```
```python
plt.figure(figsize=(9,4))
ratings['rating'].plot.hist(bins=70)
plt.xlabel('rating')
plt.savefig('rating.png')
```
![rating](https://github.com/easu978/Recommender_project/assets/151114298/d8d4b0b8-f271-42b8-a4c7-1a5ec585ed1a)

```python
plt.figure(figsize=(9,4))
sns.set_style('whitegrid')
ratings['num of ratings'].plot.hist(bins=70)
plt.xlabel('number of ratings')
plt.savefig('number of ratings.png')
```
![number of ratings](https://github.com/easu978/Recommender_project/assets/151114298/a6d9c0e6-e4f7-468e-9da4-cf6002aa71cc)


### Data Analysis

### Results/Findings

### Recommendations

### References
