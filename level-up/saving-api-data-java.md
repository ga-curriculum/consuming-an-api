# ![[Saving API data Java] - Level Up - Saving API data Java](./assets/tktk-hero.png)

Often, we use a third-party API to get data for our application, and in that process, we would like to save some of that data to our database.

Let's imagine we are building an application that allows users to search for movies and save them to a watch list. You've already chosen the [OMDb](http://www.omdbapi.com/) API to request movie data.

Upon using the built-in search functionality on the OMDb website, you notice that the JSON responses you are getting back from the API are **HUGE**! Looking deeper at what is included in that response, you see a lot of data you don't need for your application. 

**So what do we do?**

We could save all of it. At only 10 users, this application's data will be small and manageable. But think about if this application takes off! At 100 users, or even better, at 1000! You will have a lot of data you don't need.

Eventually, you will need more space on your database and that space comes at an additional expense. So again, what do we do?

## Java Model for API Data

Instead of saving the entire JSON object in a Schema, we can create a Schema that only has the properties we need. Looking at the [search endpoint](http://www.omdbapi.com/#parameters), we can see that we can search for movies in a couple of different ways:

- `i` - Search by movie ID
- `t` - Search by movie title - Must be exact match `s` is used for partial matches
- `type` - Search by movie type
- `y` - Search by movie year
- `r` - Search by movie rating

> 📚 There are other ways to search for movies, but these are the ones we will use for this lesson.

Since these are the search items we can use, these are the only properties we need to save to our database. All other items can be queried from the API when needed. But do we need all these properties? That is going to be up to you and the needs of your application. You could justifiably save all of them, but as a good rule of thumb, if you don't need it, don't save it.

We will only save the ID and title for this application, which is a simple user-based watch list. In the API's JSON response, the id is the `imdbID` property, and the title is the `Title` property. Let's create a Java Model that only has those two properties:

```java
@Entity
@Table(name = "movies")
public class Movie {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String imdbID;
    private String title;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;

    public Movie() {
        // Default constructor
    }

    public Movie(String imdbID, String title) {
        this.imdbID = imdbID;
        this.title = title;
    }

    // Getters and setters...
}
```

Saving more properties might add functionality to our application, like adding the rating or the year so users can filter their watch list by those properties. But for now, we will keep it simple and only save the id and the title.

