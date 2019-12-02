# Exercise 4.3: Deploying the demo service using a blue/green strategy

In this exercise, you will deploy the demo service into your Kubernetes cluster using Keptn. In the `dev` environment the deployment will be replaced, but in the `production` environment a blue/green deployment strategy is applied. Latter ensures zero downtime for end-users.

## Instructions

1. To inform Keptn about the availability of a new artifact, execute the following command:

    ```console
    keptn send event new-artifact --project=clc3 --service=demo --image=docker.io/YOUR-DOCKERHUB-ACCOUNT/demo:latest
    ```

    :rocket: Keptn will automatically trigger a multi-stage deployment of that service.

1. The *Keptn’s bridge* provides a website, which allows to browse the deployment process of Keptn for the `dev` and `production` environment. You can access the Keptn's bridge by a port-forward from your local machine to the pod of the bridge in the Kubernetes cluster. Therefore execute:

    ```console
    kubectl port-forward svc/bridge -n keptn 9000:8080
    ```
     
    :mag: The Keptn’s bridge is then available on: [http://localhost:9000](http://localhost:9000). Open it to see the ongoing deployment workflow.

1. Finally, you can view the demo service running in the `dev` as well as `production` environment.
Therefore, first query information of your domain with
    ```console
    kubectl get cm keptn-domain -n keptn -o=jsonpath='{.data.app_domain}'
    ```
    ```console
    x.x.x.x.xip.io
    ```

    Using this domain, you can now access your demo service in dev under [http://demo.clc3-dev.x.x.x.x.xip.io](http://demo.clc3-dev.x.x.x.x.xip.io) and in production under [http://demo.clc3-production.x.x.x.x.xip.io](http://demo.clc3-production.x.x.x.x.xip.io).

1. Next, we prepare a new version of our demo service. Therefore, change the following line in `main.go` in your repository from
    ```console
    fmt.Fprintf(w, "Hi there, it is %d:%d", t.Hour(), getMinute(t.Minute(), t.Second()))
    ```
    to
    ```console
    fmt.Fprintf(w, "Hello there, it is %d:%d", t.Hour(), getMinute(t.Minute(), t.Second()))
    ```
    This triggers now the CI pipline, which compiles the code and pushes a new Docker image with a tag equals to the Git-commit.

1. Again inform keptn about the availability of a new artifact by executing the following command:
    
    ```console
    keptn send event new-artifact --project=clc3 --service=demo --image=docker.io/YOUR-DOCKERHUB-ACCOUNT/demo:GIT_SHA
    ```

1. Now you can check your service in production and you will see that the new version is available with zero downtime.