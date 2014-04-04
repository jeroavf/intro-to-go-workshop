# Deploy with Docker

## Install Docker

Installation Instructions: http://docs.docker.io/en/latest/installation

#### Download

    curl -o docker https://get.docker.io/builds/Darwin/x86_64/docker-latest

#### Install
	
	chmod +x docker
    sudo cp docker /usr/local/bin/

#### Configure

    export DOCKER_HOST=tcp://${docker_host}:4243


## Create a Dockerfile

#### Edit

    ${GOPATH}/src/github.com/${username}/csv2json-server/Dockerfile

-

	# csv2json-server
	#
	# VERSION 0.0.1

	FROM       ubuntu
	EXPOSE     8080
	ADD        csv2json-server /usr/local/bin/csv2json-server
	ENTRYPOINT ["/usr/local/bin/csv2json-server"]

#### Run

    docker -H tcp://${docker_host}:4243 build -t ${username}/csv2json-server .
    docker -H tcp://${docker_host}:4243 images
    docker -H tcp://${docker_host}:4243 ps
    docker -H tcp://${docker_host}:4243 run -d -p 8080:8080 ${username}/csv2json-server
 

## Testing with curl

    curl -X POST http://${docker_host}:8080/csv2json --data-binary @${HOME}/famous-gophers.csv
