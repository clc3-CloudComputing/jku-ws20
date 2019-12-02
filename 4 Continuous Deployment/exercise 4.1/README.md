# Exercise 4.1: Installing Keptn on your Cluster

In this exercise, you will install [Keptn](https://keptn.sh/) on your Kubernetes cluster by using the **Keptn CLI**.

## Instructions

1. Install the Keptn CLI by following the steps described in the [documentation](https://keptn.sh/docs/0.6.0/installation/setup-keptn/).

1. In your terminal, execute the following command

  ```console
  keptn install --platform=<gke|aks> --keptn-version=release-0.6.0.beta
  ```

  :hourglass_flowing_sand: The install will take **5-10 minutes** to perform. If the installation was successful, the CLI outputs "Successfully authenticated", which means your Keptn CLI is now connected to the cluster.
