# ![Consuming an API - Level Up - Saving API Data with Mongoose](./assets/saving-api-data-mongoose.png)

**Learning objective:** By the end of this lesson students will be able to discern when it is appropriate to save detailed data to a database versus making additional API requests for specific data.

## Saving API data

It's common to use a third-party API to supply data for an application, and then allow users to interact with and even save some of that data. Let's imagine we are building an application that allows users to search for movies and save them to a watchlist. We've already chosen the [OMDb](http://www.omdbapi.com/) API to supply a large catalog of movie data. How do we allow users to save it?

As you have interacted with various endpoints, you probably noticed that the JSON responses you are getting back from this API are **huge**. Much of the data contained in these responses is probably not immediately valuable to the user and would not be relevant to saving the movie in their watchlist.

**So what do we do?**

Sure, you could save all the data in the response. Initially, with a small user base, this might seem manageable. But as your application scales, so do the demands on your data storage. Think about the long-term implications: managing data for thousands or millions of users becomes costly and complex. A smarter approach is to save only the essential data—**saving what you need, when you need it.**

## Save less query more

Rather than storing entire JSON responses, we can shape our data to save only the pertinent properties that can be used to run additional queries later. For example, referencing OMDb's [search endpoint documentation](http://www.omdbapi.com/#parameters), we can search for movies in a number of different ways:

- `i` - Search by movie ID
- `t` - Search by movie title - Must be exact match (_`s` is used for partial matches_)
- `type` - Search by movie type
- `y` - Search by movie year
- `r` - Search by movie rating

Since these are the search parameters we can use, these are the only properties we need to save to our database. All other items can be queried from the API as needed to fill in the UI.

But do we even need all these properties? That will be determined by the individual needs of your specific application. You could save all of them, but as a good rule of thumb, **_if you don't need it, don't save it_**.

For our example, we would only need to save the ID and title for our application's functionality, which is implementing a simple user-based watchlist. In the API's JSON response, the id is the `imdbID` property, and the title is the `Title` property.

This gives us the information needed to design our database.

## Mongoose schema for API data

Let's create a Mongoose Schema that only has those two properties:

```js
const movieSchema = new Schema(
  {
    imdbID: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
  },
  { timestamps: true }
);
```

Saving more properties might add functionality to our application, like adding the rating or the year so users can filter their watch list by those properties. But for now, we will keep it simple and only save the id and the title.
