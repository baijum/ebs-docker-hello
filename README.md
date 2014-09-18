# rcadena/ebs-docker-hello

Super simple golang webapp [docker](https://docker.io) image project
for running on 
[Amazon Elastic Beanstalk](http://aws.amazon.com/elasticbeanstalk/).

Runs a web server on :8080 and listens for `/`.  

Prints to stdout using `log`. 

Reads a template file from a [`templates`](templates) folder in `$GOPATH`.

It uses ["github.com/gorilla/mux"](http://www.gorillatoolkit.org/pkg/mux) 
for routing, though its use is simply to verify that vendor libs are 
imported during the container build.  But you could do without. 

It is based on [`google/golang-runtime`](https://index.docker.io/u/google/golang-runtime)


## Verify Locally
If you want to see if the docker image runs the app.

Build the image:

```shell
docker build --rm --tag=ebs-docker-hello .
```

Run the image in a new container

```shell
docker run -p 8080 -d ebs-docker-hello
```

Make a request:

```shell
$: curl localhost:8080

<!DOCTYPE html>
<html>
<head>
<title>Docker on Beanstalk</title>
</head>
<body>
    <center>
        Hello Docker on Beanstalk!
    </center>
</body>
```

## Run on AWS
This is quite involved.  A blog post and a video tutorial is coming up.


## Notes

Currently the [`Dockerfile`](Dockerfile) specifies the full `$GOPATH` as
`/gopath/src/app`.  Docker v1.3 will expand environment variables in 
`WORKDIR` so that the file can then just say:

```shell
WORKDIR $GOPATH
```


