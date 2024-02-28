# Movie Choice
## Table of Contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Recommending Similar Movies](#recommending-similar-movies)
- [Results/Findings](#results/findings)
- [Recommendations](#recommendations)
- [References](#references)

### Project Overview
The project utilizes one of the main two types of Recommender Systems algorithm - Content-Based - to give recommendations to users on the choice of movies they should watch next, by exploring the similarities of the ones they have watched before.

![plot3](https://github.com/easu978/Recommender_project/assets/151114298/17445294-1858-46a7-897b-d2a48ab6085f)

### Data Sources
This project was carried out using two sets of data; "u.data.csv" and "Movie_Id_Titles.csv" files. The former contained the user_id, item_id, rating, and timestamp, while the latter had just two columns - item_id, title.
```python
column_names = ['user_id', 'item_id', 'rating', 'timestamp']
df = pd.read_csv('u.data', sep='\t', names=column_names)
df.head()
movie_titles = pd.read_csv("Movie_Id_Titles")
movie_titles.head()
```

### Tools
The following tools facilitated the execution of this project;
- Numpy
- Pandas
- Matplotlib
- Seaborn

### Exploratory Data Analysis(EDA)
The data was explored using Pandas and Seaborn, which gave insights on the most rated movies.
```python
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
ratings['number of ratings'].plot.hist(bins=70)
plt.xlabel('number of ratings')
plt.savefig('number of ratings.png')
```
![number of ratings](https://github.com/easu978/Recommender_project/assets/151114298/a6d9c0e6-e4f7-468e-9da4-cf6002aa71cc)




### Recommending Similar Movies
Here, a matrix of all the movies was created. The matrix has 'user_id' as its rows; movie title as its columns; and its values came from the rating given to the movie by the users. Also, 10 most rated movies were sampled by exploring the 'number of ratings' column, while sorting values accordingly; and two of the first 5 most rated movies were chosen to build a recommendation system
```python
movie_matrix = df.pivot_table(index='user_id',columns='title',values='rating')
movie_matrix.head(11)
ratings.sort_values('number of ratings',ascending=False).head(10)
```
```python
starwars_user_ratings = movie_matrix['Star Wars (1977)']
liarliar_user_ratings = movie_matrix['Liar Liar (1997)']
starwars_user_ratings.head()
```
```python
similar_to_starwars = movie_matrix.corrwith(starwars_user_ratings)
similar_to_liarliar = movie_matrix.corrwith(liarliar_user_ratings)
```
```python
corr_starwars = pd.DataFrame(similar_to_starwars,columns=['Correlation'])
corr_starwars.dropna(inplace=True)
corr_starwars.head()

corr_starwars.sort_values('Correlation',ascending=False).head(10)
```
```python
corr_starwars = corr_starwars.join(ratings['num of ratings'])
corr_starwars.head()
corr_starwars[corr_starwars['num of ratings']>100].sort_values('Correlation',ascending=False).head()
```
### Results/Findings

### Recommendations

### References
