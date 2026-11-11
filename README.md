# MongoDB Mongoose Movies API

A REST API for managing movies with Express, Mongoose, and MongoDB.

## Requirements

- Node.js compatible with Mongoose 9
- npm
- A running MongoDB instance, local or hosted

## Configure and run

Create a `.env` file in this directory with your MongoDB connection string:

```env
MONGO_FULL_URI=mongodb://127.0.0.1:27017/movies_db
PORT=8080
```

Install dependencies and start the API:

```sh
npm install
npm start
```

The server listens at `http://localhost:8080` by default. Set `PORT` to use a different port. For automatic restarts during development, run `npm run dev`.

Do not commit `.env`; it may contain database credentials. The `.env.example` filename is allowed by `.gitignore` for sharing a credentials-free template.

## API

All API routes use the `/api/v1/movies` base path and accept and return JSON.

| Method   | Path                          | Description                      |
| -------- | ----------------------------- | -------------------------------- |
| `GET`    | `/`                           | Check that the server is running |
| `POST`   | `/api/v1/movies`              | Create a movie                   |
| `GET`    | `/api/v1/movies`              | List all movies                  |
| `GET`    | `/api/v1/movies?genre=Action` | List movies by genre             |
| `GET`    | `/api/v1/movies/:id`          | Get a movie by MongoDB ID        |
| `PUT`    | `/api/v1/movies/:id`          | Update a movie by ID             |
| `DELETE` | `/api/v1/movies/:id`          | Delete a movie by ID             |

Movies have `title`, `genre`, and `year` fields; these are required when creating a movie. `director` is optional.

### Examples

Create a movie:

```sh
curl.exe -X POST http://localhost:8080/api/v1/movies -H "Content-Type: application/json" -d "{\"title\":\"Arrival\",\"director\":\"Denis Villeneuve\",\"genre\":\"Science Fiction\",\"year\":2016}"
```

List movies or filter by genre:

```sh
curl.exe "http://localhost:8080/api/v1/movies"
curl.exe "http://localhost:8080/api/v1/movies?genre=Science%20Fiction"
```

Get, update, or delete a movie using the MongoDB `_id` returned by the API:

```sh
curl.exe "http://localhost:8080/api/v1/movies/<id>"
curl.exe -X PUT http://localhost:8080/api/v1/movies/<id> -H "Content-Type: application/json" -d "{\"title\":\"Arrival\",\"director\":\"Denis Villeneuve\",\"genre\":\"Science Fiction\",\"year\":2016}"
curl.exe -X DELETE "http://localhost:8080/api/v1/movies/<id>"
```

Requests for movies that do not exist return `404`.

## Manual check

With MongoDB and the API running, execute:

```sh
node test.js
```

This script requests and prints the movie list. It is a manual check; the `npm test` script is currently a placeholder.
