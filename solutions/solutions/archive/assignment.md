# Assignment

## Brief

Write the Python codes for the following questions.

## Instructions

Paste the answer as Python in the answer code section below each question.

### Question 1

Question: From the `movies` collection, return the documents with the `plot` that starts with `"war"` in acending order of released date, print only title, plot and released fields. Limit the result to 5.

Answer:

```python
for m in movies_collection.find({"plot": {"$regex": "^war", "$options": "i"}}).sort('released', pymongo.ASCENDING).limit(5):
        results.append({
            'title': m['title'],
            'released': m['released'],
            'plot': m['plot']
        })
```

### Question 2

Question: Group by `rated` and count the number of movies in each.

Answer:

```python
stage_group_rated = {
   "$group": {
         "_id": "$rated",
         "movie_count": { "$sum": 1 },
   }
}

pipeline = [
   stage_group_rated,
]
results = list(movies_collection.aggregate(pipeline))


```

### Question 3

Question: Count the number of movies with 3 comments or more.

Answer:

```python
stage_match_with_comments = {
   "$match": {
         "num_mflix_comments": {
            "$gte": 3
         }
   }
}

stage_count_movies = {
   "$count": "number_movies_with_3_comments_or_more"
   } 

pipeline = [
   stage_match_with_comments,
   stage_count_movies,
]
results = movies_collection.aggregate(pipeline)
count = list(results)[0]['number_movies_with_3_comments_or_more']

```

Alternative Answer:
```python
count = movies_collection.count_documents({"num_mflix_comments": {"$gte": 3}})
```

## Submission

- Submit the URL of the GitHub Repository that contains your work to NTU black board.
- Should you reference the work of your classmate(s) or online resources, give them credit by adding either the name of your classmate or URL.
