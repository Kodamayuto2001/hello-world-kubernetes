# hello-world-minikube

```
> minikube start
```
![image](https://user-images.githubusercontent.com/55943803/170063593-6c56e2aa-df08-4be2-bed9-35b2dd349ad6.png)


```
> minikube dashboard
```
![image](https://user-images.githubusercontent.com/55943803/170067275-26ae2ca1-6e6c-4226-8216-de084b82fb26.png)


```
> kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4
deployment.apps/hello-minikube created
```

```
> kubectl get deployments
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
hello-minikube   1/1     1            1           6m17s
```

```
> kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
hello-minikube-7bc9d7884c-6xz8q   1/1     Running   0          7m31s
```

```
> kubectl get events
LAST SEEN   TYPE      REASON                                             OBJECT                                 MESSAGE
8m12s       Normal    Scheduled                                          pod/hello-minikube-7bc9d7884c-6xz8q    Successfully assigned default/hello-minikube-7bc9d7884c-6xz8q to minikube
8m11s       Normal    Pulling                                            pod/hello-minikube-7bc9d7884c-6xz8q    Pulling image "k8s.gcr.io/echoserver:1.4"
7m59s       Normal    Pulled                                             pod/hello-minikube-7bc9d7884c-6xz8q    Successfully pulled image "k8s.gcr.io/echoserver:1.4" in 11.979392s
7m59s       Normal    Created                                            pod/hello-minikube-7bc9d7884c-6xz8q    Created container echoserver
7m59s       Normal    Started                                            pod/hello-minikube-7bc9d7884c-6xz8q    Started container echoserver
8m12s       Normal    SuccessfulCreate                                   replicaset/hello-minikube-7bc9d7884c   Created pod: hello-minikube-7bc9d7884c-6xz8q
8m12s       Normal    ScalingReplicaSet                                  deployment/hello-minikube              Scaled up replica set hello-minikube-7bc9d7884c to 1
24m         Normal    NodeHasSufficientMemory                            node/minikube                          Node minikube status is now: NodeHasSufficientMemory
24m         Normal    NodeHasNoDiskPressure                              node/minikube                          Node minikube status is now: NodeHasNoDiskPressure
24m         Normal    NodeHasSufficientPID                               node/minikube                          Node minikube status is now: NodeHasSufficientPID
24m         Normal    Starting                                           node/minikube                          Starting kubelet.
24m         Normal    NodeHasSufficientMemory                            node/minikube                          Node minikube status is now: NodeHasSufficientMemory
24m         Normal    NodeHasNoDiskPressure                              node/minikube                          Node minikube status is now: NodeHasNoDiskPressure
24m         Normal    NodeHasSufficientPID                               node/minikube                          Node minikube status is now: NodeHasSufficientPID
24m         Normal    NodeAllocatableEnforced                            node/minikube                          Updated Node Allocatable limit across pods
24m         Normal    NodeReady                                          node/minikube                          Node minikube status is now: NodeReady
24m         Normal    RegisteredNode                                     node/minikube                          Node minikube event: Registered Node minikube in Controller
24m         Normal    Starting                                           node/minikube
23m         Normal    Starting                                           node/minikube                          Starting kubelet.
23m         Normal    NodeHasSufficientMemory                            node/minikube                          Node minikube status is now: NodeHasSufficientMemory
23m         Normal    NodeHasNoDiskPressure                              node/minikube                          Node minikube status is now: NodeHasNoDiskPressure
23m         Normal    NodeHasSufficientPID                               node/minikube                          Node minikube status is now: NodeHasSufficientPID
23m         Normal    NodeAllocatableEnforced                            node/minikube                          Updated Node Allocatable limit across pods
7m58s       Warning   listen tcp4 :30067: bind: address already in use   node/minikube                          can't open port "nodePort for default/hello-minikube" (:30067/tcp4), skipping it
```
