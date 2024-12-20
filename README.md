# elsarene_random_movie_suggestion
Generates a random movie from a JSON files and displays it as card.

All you have to do is got to the site and refresh for a new one.
Recommendations are not duplicated.

Demo here:
https://elsarene.fly.dev/

### Dependencies and running

This project requires `Golang` and `Node` specifically `npm`(for Tailwindcss).

All the dependencies are listed in `go.mod` and `package.json` files

To install everything run these commands:

```
npm install
```
```
go mod dowload
```

The styles also need to be generated by Tailwindcss, because they are not included in the repo.
This project includes a Makefile so you can just run.

```
make tailwind
```
or if this does not work for some reason then:
```
tailwindcss -i ./web/styles/styles.css -o ./web/static/css/styles.css
```
In order for the program to work some ENVironment variables need to be set.

```
# Api key for OMDb
API_KEY = ""

# Filepath for JSON data of all the movies in data/id_data.json
FILEPATH = "data/id_data.json"

# Secret token to acces the secret endpoint that endables listing, adding and deleting movies from server
SECRET_TOKEN = "secret-token"

PORT="8080"
```

To run the program:
```
make run
```
or
```
go run cmd/main.go
```

### Docker

This project includes `Dockerfile`

To use it you need to have Docker installed on your computer.

To build a Docker image:
```
sudo docker build -t <your-image-name><:tag>
```
`tag` can be left out, then latest is automatocally added

Example:
```
sudo docker build -t movie-generator:1.0
````

To run :
```
sudo docker run -p <your port>:<port set in ENV variable> <image name or ID>
```
Example:
```
sudo docker run -p 7000:8080 movie-generator:1.0
```

### Tech stack used

`Golang` (backend/server)<br>
`Templ` (templating with types)<br>
`Tailwindcss` (for css)<br>
`HTMX` (frontend JS 'framework')<br>
`DaisyUI` (Tailwind UI library)<br>
`OMDb` (API for movie data)<br>
`Javascript` (frontend stuff, managing localstorage)

You can also add or delete movies from the list using the secret endpoint.

The secret endpoint is:
```
/secret/{token}/{action}/{id}
```

Where:
- `{token}` is the secret token
- `{action}` is the action to perform, which is either `add` or `delete`
- `{id}` is the id of the IMDB movie id to add or delete from the list

Example:

```
/secret/secret-token/add/tt12345678
```

NOTE: This I guess does not work well with Docker. Because each container is standalone.
