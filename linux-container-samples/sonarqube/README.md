# Downloading and running sonarqube in container

## How to use

- clone this repository in your local machine or server where docker is running and `cd` into `sonarqube` folder

- To spin up services defined in docker-compose.yml file
  - use docker stack deploy (requires docker swarm mode)

    ```bash
    docker stack deploy --compose-file docker-compose.yml stk-sonarqube
    ```

  - use docker compose

    ```bash
    docker-compose up
    ```

    use docker compose in detached mode - starts the containers in the background

    ```bash
    docker-compose up --detach
    ```

- Log in to <http://localhost:9000> with System Administrator credentials (login=admin, password=admin).
Once your server is installed and running, you may also want to [Install Plugins](https://docs.sonarqube.org/latest/setup/install-plugin/). Then you're ready to begin [Analyzing Source Code](https://docs.sonarqube.org/latest/analysis/overview/) .

- To stop the services

  - If deployed by using docker stack use

    ```bash
    docker stack rm stk-sonarqube
    ```

  - If deployed by using docker-compose use

    ```bash
    docker-compose down
    ```

## Components defined in docker-compose.yml

1. services
    - sonarqube
      - runs sonarqube:8.3.1-community docker image as a contianer
2. volumes

    volumes helps prevent the loss of information when updating to a new version or upgrading to a higher edition
     - sonarqube_data
       - contains data files, such as the embedded H2 database and Elasticsearch indexes
     - sonarqube_logs
       - contains SonarQube logs about access, web process, CE process, and Elasticsearch
     - sonarqube_extensions
       - contains plugins, such as language analyzers

3. networks
    - net-sonarqube
      - no special configuration uses the default driver

## Reference

- <https://docs.sonarqube.org/latest/setup/install-server/>