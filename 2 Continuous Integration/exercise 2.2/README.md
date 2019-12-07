# Exercise 2.2: Build and push a Container Image to DockerHub

In this exercise, you will integrate DockerHub into the CI workflow in order to push an image to your DockerHub account. Therefore, a Dockerfile needs to be added to the repository, and the steps to build, tag, and push an image need to be extended to the Travis pipeline. 

## Requirements

* DockerHub Account account
    <details><summary>Click here for sign-up instructions.</summary>
    <p>

    To sign up: https://hub.docker.com/signup

    </p>
    </details>

* Exercise 2.1 completed

## Instructions

1. Setup credentials for DockerHub in Travis:
    1. Click on: `More options`

    1. Add an environment variable `REGISTRY_USER` with your DockerHub registry user name

    1. Add an environment variable `REGISTRY_PASSWORD` with your DockerHub registry password. :exclamation: **Important:**  Do not display value in build log :exclamation:

1. Add and commit the provided `Dockerfile` to your repository.

1. Extend the `.travis.yaml` pipeline with the Docker service:

    ```yaml
    services:
    - docker
    ```

1. Extend the `.travis.yaml` pipeline with a Docker `login` command in the `script` block:

    ```yaml
    script:
    - go test -v ./...
    - CGO_ENABLED=0 go build -o demo

    - echo "$REGISTRY_PASSWORD" | docker login --username $REGISTRY_USER --password-stdin
    ```
    
1. Extend the `.travis.yaml` pipeline with a Docker `build` command in the `script` block:

    ```yaml
    script:
    ...
    - docker build -f Dockerfile -t YOUR-DOCKERHUB-ACCOUNT/demo:latest ./
    ```

1. Extend the `.travis.yaml` pipeline with a Docker `tag` command in the `script` block. The tag has to be the Git commit SHA of this build:

    ```yaml
    script:
    ...
    - GIT_SHA="$(git rev-parse --short HEAD)"
    - docker tag YOUR-DOCKERHUB-ACCOUNT/demo:latest YOUR-DOCKERHUB-ACCOUNT/demo:$GIT_SHA
    ```

1. Extend the `.travis.yaml` pipeline with a Docker `push` command in the `script` block:
   
    ```yaml
    script:
    ...
    - docker push YOUR-DOCKERHUB-ACCOUNT/demo:latest
    - docker push YOUR-DOCKERHUB-ACCOUNT/demo:$GIT_SHA
    ```

1. Finally, trigger a Travis build by a code change. 

1. Watch Travis executing your tests, building the artifact, and pushing it to DockerHub.

:mag: Go to your DockerHub account and find your image. Can you find it?