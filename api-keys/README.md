# ![Consuming an API - API Keys](./assets/tktk-hero.png)

**Learning objective:** By the end of this lesson, students will be able to obtain an API key and know how to handle it safely.

## API Keys

**An API key is a unique identifier that API providers create to control access to their API and how it is used.**

They are usually a long string of random characters that the API provider generates. When making a request to the API, they are typically passed as a query parameter in the URL.

Since API keys are a unique identifier, they should be kept secret. If someone else gets a hold of your API key, they can use it to make requests to the API under your identity. If you are paying for the API, this can result in charges on your account that most companies will hold you responsible for. If you use an API key in your application, you should never commit it to your repository. Instead, you should store it in an environment variable in a file that will be ignored when changes are pushed up to GitHub.

## Obtaining an API Key - OMDb API

For this lesson, we will use the [OMDb API](http://www.omdbapi.com/). This API allows us to search for movies and get information about them. To use this API, we need to get an API key.

Let's complete the following steps:

- Go to the [OMDb API](http://www.omdbapi.com/) website
- At the top of the page, click on the "API Key" link in the navbar
- Select the "FREE!" plan
- Fill out the form and click "Submit"

> 📚 Note: the rate limit for the free plan is 1000 requests per day.

Once you have created your account, your API key will be sent to the email you used to sign up. ***Visit your email and copy the API key.***

> ✅ Be sure to activate your API key by clicking on a link in the email. Follow all instructions given in the email. As noted, third-party APIs are created by someone else, so changes in how we use the API can happen anytime. When in doubt, always follow the API documentation or instructions.

### Keep it secret, keep it safe

We have collected our very first API key. ***Now what?***

**We need to keep it secret.** Luckily, the worst things that can happen if someone gets a hold of our OMDb API key is they can make requests and exceed our over-rate limit or get our account banned. Not great, but neither are the end of the world. However, we should still treat it as a password and adhere to best practices and keep it secret.

We should never commit our API keys to our repository when developing an application. Instead, we should store them in an environment variable and access them from there. This way, we can keep them secret without worrying about them being exposed in our code.

## Review Questions

1. What is an API key?
2. Why should we keep our API keys secret?