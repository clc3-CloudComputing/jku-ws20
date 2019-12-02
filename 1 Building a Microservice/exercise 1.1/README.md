# Exercise 1.1: Working with Docker and Dockerfile

In this exercise, you will write a Dockerfile and you will build an image from this Dockerfile. For more information about a Dockerfile, click [here](https://docs.docker.com/engine/reference/builder/).

## Requirements

* [Docker](https://www.docker.com/) installed: 
    <details><summary>Click here for install instructions.</summary>
    <p>

    * Docker for Windows: https://docs.docker.com/docker-for-windows/install/

    * Docker for Mac: https://docs.docker.com/docker-for-mac/install

    </p>
    </details>

* [Docker Hub](https://hub.docker.com/) Account created:
    <details><summary>Click here for sign-up instructions.</summary>
    <p>

    * To sign up: https://hub.docker.com/signup

    </p>
    </details>

## Instructions

1. Create a Dockerfile with the following instructions:
    * Base image: `[xyz]`
    * Set maintainer label: `maintainer=[YOUR-EMAIL]`
    * Copy file `README.md` to the image folder `/opt/`
    * Show the content of the `README.md` during the build process

1. Build a Docker image based on the Dockerfile:
    * Image tag: `[YOUR-DOCKERHUB-ACCOUNT]/my-first-image:0.0.1`

    ```console
    docker image build -f Dockerfile -t [YOUR-DOCKERHUB-ACCOUNT]/my-first-image:0.0.1 ./ 
    ```

1. Execute the command a second time: 

    ```console
    docker image build -f Dockerfile -t [YOUR-DOCKERHUB-ACCOUNT]/my-first-image:0.0.1 ./
    ```

    :mag: What is your observation? 
  
1. List all images that are stored in your local registry:

    ```console
    docker images
    ```
