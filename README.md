
# ALX Project 0x14: API Explorer – CineSeek

## API Overview

The MoviesDatabase API is a powerful RESTful service designed for movie discovery. It provides structured data for films including titles, release dates, genres, descriptions, images, and ratings. It supports various query parameters such as filtering by year, genre, and pagination to streamline the data fetching process.

Key features:
- Fetch movies by title, genre, and year
- Supports pagination and sorting
- Rich metadata including posters, descriptions, and ratings
- Fast, scalable access via authenticated requests

## API Version

**Version**: v1

## Available Endpoints

Method	Endpoint	Description
GET	/titles	Fetch a list of movies or series, with optional filtering (e.g., genre, year, etc.)
GET	/titles/{id}	Get detailed information about a specific movie or show by ID
GET	/titles/{id}/ratings	Get rating information for a specific title
GET	/titles/{id}/aka	Fetch alternate titles (AKAs) for a specific title ID
GET	/titles/x/titles-by-ids	Fetch multiple titles by an array of IDs
GET	/titles/series/{seriesId}	Get general information about a TV series by its series ID
GET	/titles/series/{seriesId}/{season}	Get season-specific information for a TV series
GET	/titles/seasons/{seriesId}	Retrieve all seasons for a given series ID
GET	/titles/episode/{id}	Get information about a specific TV episode by its ID
GET	/titles/x/upcoming	Get a list of upcoming movies or TV shows
GET	/titles/random	Fetch a random movie or TV title

## Request and Response Format

### Example Request

```http
GET /titles?genre=Action&year=2023&page=1 HTTP/1.1
Host: moviesdatabase.p.rapidapi.com
X-RapidAPI-Key: API_KEY
X-RapidAPI-Host: moviesdatabase.p.rapidapi.com
````

### Example Response

```json
{
  "results": [
    {
      "id": "tt1234567",
      "titleText": { "text": "Example Movie" },
      "releaseYear": { "year": 2023 },
      "primaryImage": {
        "url": "https://image.url/example.jpg"
      },
      "ratingsSummary": {
        "aggregateRating": 7.8
      }
    }
  ],
  "page": 1,
  "next": "/titles?genre=Action&year=2023&page=2"
}
```

## Authentication

Authentication is done using API key headers:

* `X-RapidAPI-Key`: API key
* `X-RapidAPI-Host`: `moviesdatabase.p.rapidapi.com`

## Error Handling

| Status Code | Meaning                                 | Handling Strategy                    |
| ----------- | --------------------------------------- | ------------------------------------ |
| `401`       | Unauthorized – Invalid API key          | Check and refresh credentials        |
| `429`       | Too Many Requests – Rate limit exceeded | Back off and retry after delay       |
| `500`       | Internal Server Error                   | Retry or alert user with fallback UI |

Always use `try/catch` blocks when fetching and validate response codes before proceeding.

## Usage Limits and Best Practices

* **Rate Limits**:

  * Free plan: 1000 requests/hour, up to 500,000/month
  * Pro plan: 5 requests/second with \$0.01 per request

* **Best Practices**:

  * Implement pagination instead of fetching large data sets at once
  * Use client-side caching to minimize API calls
  * Use loading states and fallback UIs to enhance user experience
  * Never hardcode API keys – use `.env.local` and access securely

