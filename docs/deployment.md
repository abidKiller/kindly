## Docker

### Requirements

* [Docker](https://docs.docker.com/install/overview/)

### Installation

Build the API with docker by running 

```bash
docker build -f "api/Dockerfile" -t kindly_api:latest "api"
```

> ⚠️  If the build errors out with `executor failed running: exit code: 137`, you are likely running out of memory. Initial installations of Docker come preconfigured by allocating 2GB of memory to Docker. You need to adjust that setting by going to **Docker Settings -> Advanced** and increasing the memory available

A container image of this API is also found on [Dockerhub](https://hub.docker.com/r/nathanfletcher/kindly_api)

Build the demo client with docker by running 

```bash
docker build -f "client/Dockerfile" -t kindly_client:latest "client"
```

A container image of the client is also found on [Dockerhub](https://hub.docker.com/r/nathanfletcher/kindly_client)

### Running

Run the API using docker with this command:

```bash
docker run --rm -it  -p 8080:8080/tcp kindly_api:latest
```

Run the demo client using docker with this command:

```bash
docker run --rm -it  -p 3000:3000/tcp kindly_client:latest
```

## Reference

### List all available endpoints

List all endpoints available through this API.

```
GET /
```
#### Code Samples

**Shell**

```bash
curl http://localhost:8080/
```

#### Default Response

```
Status: 200 OK
```
```json
{
    "detect": "/detect"
}
```

### Send text for detection endpoints

Send a piece of text and through this API to determine if it is offensive to post or not.

```
POST /
```

```PAYLOAD```
```
{
    "text":"this movie is great"
}
```
#### Code Samples

**Shell**

```bash
curl \
  -X POST \
  -H "Content-Type: application/json" \
  http://localhost:8080/detect \
  -d '{"text":"this movie is great"}'
```

#### Default Response

```
Status: 200 OK
```
```json
{
    "result": {
        "not-offensive": "0.8308081",
        "offensive": "0.1691919"
        },
    "text": "this movie is great"
}

```