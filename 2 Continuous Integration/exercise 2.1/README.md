# Exercise 2.1: Setup Continuous Integration

In this exercise, you will set up a *Continuous Integration* (CI) workflow using GitHub as a version control system, Travis CI as a build tool, and DockerHub as artifact repository manager. This workflow will execute the unit tests of the source code and build the code. To trigger it, a change of the codebase must be performed. 

## Setup

![GitHub, Travis CI, DockerHub](./assets/lab_setup.png)

## Requirements

* GitHub account :octocat: 
    <details><summary>Click here for sign-up instructions.</summary>
    <p>

    To sign up:  https://github.com/join

    </p>
    </details>

## Instructions

1. Create a **public** GitHub repository called: `mini-ci-example`

1. Add and commit `main.go`, `main_test.go`, `fib.go`, `fib_test.go`, and `go.mod` to your repository via drag-and-drop.

1. Active Travis CI for your GitHub repository.

    * Follow instructions on: https://docs.travis-ci.com/user/tutorial/#to-get-started-with-travis-ci

1. Create file `.travis.yml` in your repository and copy-paste content from the provided `.travis.yml` file. 

    ```yaml
    os: linux
  
    language: go

    go:
    - 1.13.x

    script:   
    # Test the code
    - go test -v ./...
    # Build the code 
    - CGO_ENABLED=0 GOARCH=amd64 go build -o demo
    ```

1. Trigger a Travis CI build by a code change, e.g., change "Hello" to "Hi there" in the file `./main.go`

1. Watch Travis executing your tests and building the artifact.

    :mag: What is your observation? 

* *Optional*: To add Travis CI status to the README.md, follow instructions on: https://docs.travis-ci.com/user/status-images/

    ![Travis CI Status](./assets/travis_status.png)

    ```
    [![Build Status](https://travis-ci.com/YOUR-GITHUB-ACCOUNT/mini-ci-example.svg?branch=main)](https://travis-ci.com/YOUR-GITHUB-ACCOUNT/mini-ci-example)
    ```
