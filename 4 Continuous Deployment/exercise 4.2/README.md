# Exercise 4.2: Onboard your demo service to Keptn

In this exercise, you will configure Keptn to manage your demo service in an environment with two stages (dev, and production) and you will *onboard* your demo service. 

## Instructions

1. A so-called `shipyard` file describes your desired environment and the used deployment strategies. Create a file named `shipyard.yaml` with the following content:

    ```yaml
    stages:
    - name: "dev"
      deployment_strategy: "direct"
    - name: "production"
      deployment_strategy: "blue_green_service"
    ```

1. In Keptn, a `project` is a structure that allows you to organize a set of services. Create a project named `clc3` and with the environment as specified in the `shipyard.yaml` file:

    ```console
    keptn create project clc3 --shipyard=./shipyard.yaml
    ```

    * **Note:** Internally, this command will create a Git repository, which contains the complete configuration. Therefore, this repository will contain a branch for each of the stages defined in the shipyard file in order to store the configuration of the application for that stage.

1. Next, onboard your service into the `clc3` project. Therefore, our Kubernetes resources (i.e., the deployment and the service) are organized in so-called Helm charts. Here you can use the provided Helm chart contained in this repository. To onboard the `demo` service, execute the following command:

    ```console
    keptn onboard service demo --project=clc3 --chart=./demo
    ```

:rocket: Finally, Keptn has all the information needed to launch your service and even support a blue/green deployment strategy in production.
