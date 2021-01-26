# Downloading and running Jenkins in Docker

## How to use

- clone this repository in your local machine or server where docker is running and `cd` into `jenkins` folder

- To spin up services defined in docker-compose.yml file

  - use docker compose

    ```bash
    docker-compose up
    ```

    use docker compose in detached mode - starts the containers in the background

    ```bash
    docker-compose up --detach
    ```

- Browse to <http://localhost:8080/> and wait untill the Unlock Jenkins page appears
- Proceed to the [Post-installation setup wizard](https://www.jenkins.io/doc/book/installing/#setup-wizard).
- To stop the services

    ```bash
    docker-compose down
    ```

## Components defined in docker-compose.yml

1. services
    - jenkins-blueocean
      - runs jenkinsci/blueocean docker image as a container
    - jenkins-docker
      - runs docker:dind image
      - required to execute docker commands with Jenkins nodes
      - learn more about docker:dind image here <https://hub.docker.com/_/docker>

2. volumes
    - jenkins-docker-certs
      - to share Docker client TLS certificates needed to connect to Docker daemon and persist the Jenkins data
    - jenkins-data
      - helps prevent the loss of information when updating to a new version or upgrading to a higher edition

3. networks
    - net-jenkins
      - no special configuration uses the default driver

## Limitation

- You cannot deploy using `docker stack deploy` with `privileged: true` for `docker:dind` image however you can use `docker-compose up`
- `privileged: true` is not currently supported
  <https://github.com/moby/moby/issues/24862>

## Reference

- <https://www.jenkins.io/doc/book/installing/>
