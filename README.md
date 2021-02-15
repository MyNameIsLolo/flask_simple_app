# Flask simple app

This app is a Flask simple app for testing purpose !!

## Jenkins pipeline
The provided Jenkinsfile is for testing with Pytest and for building / pushing the Docker image to DockerHub

## Docker image
The Docker image can be pull from DockerHub :
```
docker pull <repo>/flask_simple_app:<tag>
```
It can be run with the following command :
```
docker run -p 5000:5000 -d --name <container name> <repo>/flask_simple_app:<tag>
```

## Interact with the Flask app
GET request example :
```
curl localhost:5000/endpoint
```
POST request example :
```
curl -d '{"request_id":"123", "payload":{"py":"pi", "java":"scrip"}}' -H "Content-Type: application/json" -X POST localhost:5000/post/test -H "authorization-sha256: 123"
```
