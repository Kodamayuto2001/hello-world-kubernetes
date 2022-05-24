# hello-world-minikube

```
> minikube start
😄  Microsoft Windows 10 Home 10.0.19044 Build 19044 上の minikube v1.25.2
✨  docker ドライバーが自動的に選択されました。他の選択肢: virtualbox, ssh
👍  minikube クラスター中のコントロールプレーンの minikube ノードを起動しています
🚜  ベースイメージを取得しています...
💾  Kubernetes v1.23.3 のダウンロードの準備をしています
    > preloaded-images-k8s-v17-v1...: 505.68 MiB / 505.68 MiB  100.00% 28.87 Mi
    > gcr.io/k8s-minikube/kicbase: 379.06 MiB / 379.06 MiB  100.00% 9.28 MiB p/
🔥  docker container (CPUs=2, Memory=3500MB) を作成しています.../ E0524 23:36:30.942608   18836 kic.go:267] icacls failed applying permissions - err - [%!s(<nil>)], output - [�����t�@�C��: C:\Users\yuto2\.minikube\machines\minikube\id_rsa
1 �̃t�@�C���������ɏ��������܂����B0 �̃t�@�C���������ł��܂����ł���]

🐳  Docker 20.10.12 で Kubernetes v1.23.3 を準備しています...
    ▪ kubelet.housekeeping-interval=5m
    ▪ 証明書と鍵を作成しています...
    ▪ コントロールプレーンを起動しています...
    ▪ RBAC のルールを設定中です...
🔎  Kubernetes コンポーネントを検証しています...
    ▪ gcr.io/k8s-minikube/storage-provisioner:v5 イメージを使用しています
🌟  有効なアドオン: storage-provisioner, default-storageclass

❗  C:\Program Files\Docker\Docker\resources\bin\kubectl.exe のバージョンは 1.21.3 で、Kubernetes 1.23.3 と互換性が ないかもしれません。
    ▪ kubectl v1.23.3 が必要ですか？ 'minikube kubectl -- get pods -A' を試してみてください
🏄  完了しました！ kubectl が「"minikube"」クラスタと「"default"」ネームスペースを使用するよう構成されました
```

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

```
> kubectl get services
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hello-minikube   NodePort    10.110.183.166   <none>        8080:30067/TCP   12m
kubernetes       ClusterIP   10.96.0.1        <none>        443/TCP          29m
```

```
> kubectl port-forward service/hello-minikube 7080:8080
Forwarding from 127.0.0.1:7080 -> 8080
Forwarding from [::1]:7080 -> 8080
Handling connection for 7080
Handling connection for 7080
```

```
> curl.exe http://localhost:7080/
CLIENT VALUES:
client_address=127.0.0.1
command=GET
real path=/
query=nil
request_version=1.1
request_uri=http://localhost:8080/

SERVER VALUES:
server_version=nginx: 1.10.0 - lua: 10001

HEADERS RECEIVED:
accept=*/*
host=localhost:7080
user-agent=curl/7.79.1
BODY:
-no body in request-
```

```
> minikube tunnel
✅  Tunnel successfully started

📌  注意: トンネルにアクセスするにはこのプロセスが存続しなければならないため、このターミナルはクローズしないでください ...

🏃  balanced サービス用のトンネルを起動しています。
```

```
> kubectl get services balanced
NAME       TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
balanced   LoadBalancer   10.97.22.208   127.0.0.1     8080:32332/TCP   39s
```

```
> minikube pause
⏸️  minikube ノードを一時停止しています ...
⏯️  kube-system, kubernetes-dashboard, storage-gluster, istio-operator に存在する 18 個のコンテナーを一時停止しまし
た
```

```
minikube unpause
⏸️  minikube ノードを再稼働させています ...
⏸️  次のネームスペースに存在する 18 個のコンテナーを再稼働させました: kube-system, kubernetes-dashboard, storage-gluster, istio-operator
```

```
> minikube stop
✋  「minikube」ノードを停止しています...
🛑  SSH 経由で「minikube」の電源をオフにしています...
🛑  1 台のノードが停止しました。
```

```
> minikube config set memory 16384
❗  これらの変更は minikube delete の後に minikube start を実行すると反映されます
```

```
> minikube addons list
|-----------------------------|----------|--------------|--------------------------------|
|         ADDON NAME          | PROFILE  |    STATUS    |           MAINTAINER           |
|-----------------------------|----------|--------------|--------------------------------|
| ambassador                  | minikube | disabled     | third-party (ambassador)       |
| auto-pause                  | minikube | disabled     | google                         |
| csi-hostpath-driver         | minikube | disabled     | kubernetes                     |
| dashboard                   | minikube | enabled ✅   | kubernetes                     |
| default-storageclass        | minikube | enabled ✅   | kubernetes                     |
| efk                         | minikube | disabled     | third-party (elastic)          |
| freshpod                    | minikube | disabled     | google                         |
| gcp-auth                    | minikube | disabled     | google                         |
| gvisor                      | minikube | disabled     | google                         |
| helm-tiller                 | minikube | disabled     | third-party (helm)             |
| ingress                     | minikube | disabled     | unknown (third-party)          |
| ingress-dns                 | minikube | disabled     | google                         |
| istio                       | minikube | disabled     | third-party (istio)            |
| istio-provisioner           | minikube | disabled     | third-party (istio)            |
| kong                        | minikube | disabled     | third-party (Kong HQ)          |
| kubevirt                    | minikube | disabled     | third-party (kubevirt)         |
| logviewer                   | minikube | disabled     | unknown (third-party)          |
| metallb                     | minikube | disabled     | third-party (metallb)          |
| metrics-server              | minikube | disabled     | kubernetes                     |
| nvidia-driver-installer     | minikube | disabled     | google                         |
| nvidia-gpu-device-plugin    | minikube | disabled     | third-party (nvidia)           |
| olm                         | minikube | disabled     | third-party (operator          |
|                             |          |              | framework)                     |
| pod-security-policy         | minikube | disabled     | unknown (third-party)          |
| portainer                   | minikube | disabled     | portainer.io                   |
| registry                    | minikube | disabled     | google                         |
| registry-aliases            | minikube | disabled     | unknown (third-party)          |
| registry-creds              | minikube | disabled     | third-party (upmc enterprises) |
| storage-provisioner         | minikube | enabled ✅   | google                         |
| storage-provisioner-gluster | minikube | disabled     | unknown (third-party)          |
| volumesnapshots             | minikube | disabled     | kubernetes                     |
|-----------------------------|----------|--------------|--------------------------------|
```

```
> minikube start -p aged --kubernetes-version=v1.16.1
😄  Microsoft Windows 10 Home 10.0.19044 Build 19044 上の [aged] minikube v1.25.2
✨  docker ドライバーが自動的に選択されました。他の選択肢: virtualbox, ssh

❌  MK_USAGE が原因で終了します: Docker Desktop は 5942MB のメモリーしか使用できませんが、16384MB のメモリー使用を指定されました
```

```
minikube config set memory 5942
❗  これらの変更は minikube delete の後に minikube start を実行すると反映されます
```

```
> minikube start -p aged --kubernetes-version=v1.16.1
😄  Microsoft Windows 10 Home 10.0.19044 Build 19044 上の [aged] minikube v1.25.2
✨  docker ドライバーが自動的に選択されました。他の選択肢: virtualbox, ssh
👍  aged クラスター中のコントロールプレーンの aged ノードを起動しています
🚜  ベースイメージを取得しています...
🔥  docker container (CPUs=2, Memory=5942MB) を作成しています...
🐳  Docker 20.10.12 で Kubernetes v1.16.1 を準備しています...
    ▪ kubelet.housekeeping-interval=5m
    > kubectl.sha1: 41 B / 41 B [----------------------------] 100.00% ? p/s 0s
    > kubelet.sha1: 41 B / 41 B [----------------------------] 100.00% ? p/s 0s
    > kubeadm.sha1: 41 B / 41 B [----------------------------] 100.00% ? p/s 0s
    > kubeadm: 42.20 MiB / 42.20 MiB [-------------] 100.00% 16.50 MiB p/s 2.8s
    > kubelet: 117.43 MiB / 117.43 MiB [-----------] 100.00% 23.52 MiB p/s 5.2s
    > kubectl: 44.52 MiB / 44.52 MiB [--------------] 100.00% 8.24 MiB p/s 5.6s
    ▪ 証明書と鍵を作成しています...
    ▪ コントロールプレーンを起動しています...
    ▪ RBAC のルールを設定中です...
🔎  Kubernetes コンポーネントを検証しています...
    ▪ gcr.io/k8s-minikube/storage-provisioner:v5 イメージを使用しています
🌟  有効なアドオン: storage-provisioner, default-storageclass

❗  C:\Program Files\Docker\Docker\resources\bin\kubectl.exe のバージョンは 1.21.3 で、Kubernetes 1.16.1 と互換性が
ないかもしれません。
    ▪ kubectl v1.16.1 が必要ですか？ 'minikube kubectl -- get pods -A' を試してみてください
🏄  完了しました！ kubectl が「"aged"」クラスタと「"default"」ネームスペースを使用するよう構成されました
```

```
> minikube delete --all
🔥  docker の「aged」を削除しています...
🔥  C:\Users\yuto2\.minikube\machines\aged を削除しています...
💀  クラスター「aged」の全てのトレースを削除しました。
🔥  docker の「minikube」を削除しています...
🔥  C:\Users\yuto2\.minikube\machines\minikube を削除しています...
💀  クラスター「minikube」の全てのトレースを削除しました。
🔥  全てのプロファイルの削除に成功しました
```
