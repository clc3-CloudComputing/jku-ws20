# Exercise 3.4: Creating a Service

In this exercise, you will specify a service for your deployment by defining a service manifest (`service.yaml`). This manifest will be applied to your Kubernetes cluster to create a service resource. When the service is available, you can retrieve its *LoadBalancer Ingress* IP to access your demo app via a web browser.

## Instructions

1. Create a file `service.yaml` with the following content:

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: demo
      labels:
        app: demo
    spec:
      ports:
      - port: 80
        protocol: TCP
        targetPort: 8888
      selector:
        app: demo
      type: LoadBalancer
    ```

    * The `ports`-section specifies that the Service forwards all traffic on port 80 to the Pod's port on 8888.

    * The `selector` tells the Service to which Pods the requests should be routed. Here, the requests are forwarded to any Pods matching the label `app: demo`.

1. Apply the *service* to your Kubernetes cluster using: 
    
    ```console
    kubectl apply -f service.yaml
    ```

1. Your service now acts as *LoadBalancer* and received an externally accessible IP address. You can obtain this IP with:

    ```console
    kubectl describe service demo
    ```

    ```source
    Name:                     demo
    Namespace:                default
    Labels:                   app=demo
    Annotations:              kubectl.kubernetes.io/last-applied-configuration:
                                {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"app":"demo"},"name":"demo","namespace":"default"},"spec":{"por...
    Selector:                 app=demo
    Type:                     LoadBalancer
    IP:                       10.0.87.134
    LoadBalancer Ingress:     20.185.79.32
    Port:                     <unset>  9999/TCP
    TargetPort:               8888/TCP
    NodePort:                 <unset>  31343/TCP
    Endpoints:                10.244.1.4:8888
    Session Affinity:         None
    External Traffic Policy:  Cluster
    Events:
      Type    Reason                Age   From                Message
      ----    ------                ----  ----                -------
      Normal  EnsuringLoadBalancer  15s   service-controller  Ensuring load balancer
      Normal  EnsuredLoadBalancer   11s   service-controller  Ensured load balancer


    Name:              kubernetes
    Namespace:         default
    Labels:            component=apiserver
                      provider=kubernetes
    Annotations:       <none>
    Selector:          <none>
    Type:              ClusterIP
    IP:                10.0.0.1
    Port:              https  443/TCP
    TargetPort:        443/TCP
    Endpoints:         52.191.222.87:443
    Session Affinity:  None
    Events:            <none>
    ```

1. Use the IP address of the *LoadBalancer Ingress* to access your website.

    :mag: Enter the IP in a browser.
