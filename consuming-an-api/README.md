# ![[Consuming an API] - Consuming an API](./assets/tktk-hero.png)

**Learning objective:** By the end of this lesson, students will be able to make a request to a third-party API using Postman and cURL.

## Consuming an API

For this lesson, we will use two tools to consume from the OMDB API.

The first is [cURL](https://curl.se/). cURL is a command line tool that will enable us to make requests to APIs from the command line.

The second is [Postman](https://www.postman.com/). Postman is a tool that allows us to make requests to APIs and see the responses.

## Consume an API using cURL

Looking at the [OMDb documentation for usage](https://www.omdbapi.com/#usage), we can see that the base URL for the API is `http://www.omdbapi.com/`. We can also see that the API requires an API key. As shown in the documentation, we can pass the API key as a query parameter in the URL, like so, `http://www.omdbapi.com/?apikey=[yourkey]&`.

Let's together build the command and make a request to the API using cURL.

First, we have to save the API key as an environment variable. In the terminal, run the following command:

```bash
API_KEY=your_api_key
```

So, for example, if the API key you received from OMDb is `abc123456`, you would enter:

```bash
API_KEY=abc123456
```

We can test that the environment variable was set correctly by running the following command:

```bash
echo $API_KEY
```

> ❗️ To access the value stored in the variable, be sure to prepend the `$` to the variable. It's subtle, but it's there! You will also be doing the same in one of the steps below, so watch out for that too.

> 📚 Even though this is a local environment, and we don't have to save our API key as an environment variable, we will do it anyway since it is following best practices. This is to get us in the habit of doing it when working with APIs in our applications.

Once the environment variable is set, we can request the API. Let's look at the [documentation](https://www.omdbapi.com/#usage) again and see if we can find anything on **Stargate**.

You'll notice there are two different URLs to which we can make requests. One is for ***all movie data*** (`http://www.omdbapi...`), and the other is for just ***poster images*** (`http.//img.omdbapi...`).

Let's make a request to the **movie data** URL. That gives us the following base URL along with the API key query parameter:

```bash
http://www.omdbapi.com/?apikey=[yourkey]&
```

We will need to replace the placeholder of `[yourkey]` with our API key (be sure to remove the square brackets too `[` `]`). That leaves us with this:

```bash
http://www.omdbapi.com/?apikey=$API_KEY&
```

> ❗️ Notice the `$` again when using the variable `API_KEY`.

We still need to specifically query for **Stargate**. Looking back at the [documentation for parameters](https://www.omdbapi.com/#parameters), we find that we can ***search*** for movies by ***title*** using the `s` query parameter. Let's add that to our URL with the title of our movie:

```bash
http://www.omdbapi.com/?apikey=$API_KEY&s=stargate
```

> 📚 You may have wondered why the `&` was included in the URL. The provider included that knowing that we will for sure be adding additional parameters to the query string to narrow our search.

**Perfect!** Now we have a completed URL and can make a request. To make a **GET** request using **cURL**, we must pass the URL as an argument to the `curl` command and put our URL within `""`. Let's run the following command:

```bash
curl "http://www.omdbapi.com/?apikey=$API_KEY&s=stargate"
```

We should get back a bunch of data about **Stargate**. We can see that the data is in **JSON format** by default, and it's all squished together and hard to read. Luckily, cURL has a **built-in flag** to format the JSON for us. Let's run the following command:

```bash
curl "http://www.omdbapi.com/?apikey=$API_KEY&s=stargate" | json_pp
```

> 📚 The `|` character is called a pipe. It takes the output from the command on the left and passes it as input to the command on the right. In this case, we are taking the output from the `curl` command and passing it as input to the `json_pp` command.

Pretty!

## Consume an API using Postman

Now that we have requested the OMDB API using cURL let's request using Postman. Open up Postman and create a new request. In the URL bar, enter the following URL:

`"http://www.omdbapi.com/?apikey=$API_KEY&s=stargate"`

Once you have added the URL, you should see the Query Params section of the request update with the `spiky` and `s` query parameters. The `apikey` query parameter should have the value of your API key, and the `s` query parameter should have the value of `stargate`. If you don't see the query parameters, make sure you have the Params tab selected.

![Postman Query Params](./assets/postman-query-params.png)

You can select the value of the `apikey` query params and replace `$API_KEY` with your API key. Once you have done that, click the Send button. You should get back the same data we got back when we made the request using cURL. This time, the data is formatted for us and is much easier to read.

## You do: Consume an API using Postman

Now that we have made a request to the OMDB API using both Postman and cURL, it's your time to venture forth and try this out yourself. Using the OMDB API documentation, make a request to the API using both Postman and cURL. Try making a request to the movie data URL and the poster images URL. Try searching for different movies and see what data you get back.
