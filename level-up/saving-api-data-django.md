# ![[Saving API data Django] - Level Up - Saving API data Django](./assets/hero.png)

Often times we use a third party API to get data for our application, and in that process we would like to save some of that data to our database. Let's imagine we are building an application that allows users to search for movies and save them to a watch list. You've already chosen the [OMDB](http://www.omdbapi.com/) API to get movie data from. Upon using the built in search functionality on the OMDB website you notice that the JSON responses you are getting back from the API are **HUGE**! Looking deeper at what is all included in that response you see there is a lot of data that you don't need for your application. 

So what do we do? We could save all of it but think if this application takes off. At only 10 users this applications data will be small and manageable. But think of it at 100, and 1000 you will have a lot of data that you don't need. Eventually you will run out of space on your database and you will have to pay for more space. So what do we do? We only save the data we need.

## Django Model for API Data

Instead of saving the entire JSON object in a Schema we can create a Schema that only has the properties we need. Looking at the [search endpoint](http://www.omdbapi.com/#parameters) we can see that we can search for movies in a couple of different ways:

- `i` - Search by movie ID
- `t` - Search by movie title - Must be exact match `s` is used for partial matches
- `type` - Search by movie type
- `y` - Search by movie year
- `r` - Search by movie rating

> 📚 There are other ways to search for movies but these are the ones we are going to use for this lesson.

Since these are the search items we can use these are the only properties we need to save to our database. All other items can be queried from the API when needed. But do we need all these properties? That is going to be up to you and the needs of your application. You could justifiably save all of them, but as a good rule of thumb if you don't need it don't save it.

For this application that is a simple user based watch list we are only going to save the id and the title. In the JSON response from the API the id is the `imdbID` property and the title is the `Title` property. Let's create a Django Model that only has those two properties:

```py
class Movie(models.Model):
    imdbID = models.CharField(max_length=255, unique=True)
    title = models.CharField(max_length=255)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```

Saving more properties might add some more functionality to our application like adding the rating or the year so a user would be able to filter their watch list by those properties. But for now we are going to keep it simple and only save the id and the title.
