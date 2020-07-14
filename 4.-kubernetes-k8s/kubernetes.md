# 쿠버네티스의 시작

쿠버네티스\(kubernetes\)는 k라는 문자와 s라는 문자 사이에 8글자가 있어 k8s라고도 불립니다.

`쿠버네티스`는  컨테이너들을 쉽고 빠르게 배포/확장 및 관리를 할수 있도록 도와주는 도구입니다. 이미 수많은 회사에서 사용하고 있고, 안정적으로 서비스되고 있는 시스템이기도 합니다.

도커는 단순히 run 하면 시작하고 stop하면 멈추지만 쿠버네티스는 도커보다 많은 설정이 필요합니다**.**

포스트를 작성하면서 개발은 윈도우에서 하고, WSL을 이용한 도커와 쿠버네티스를 사용할 예정입니다. 그렇기 때문에 [WSL 설치](https://dydtjr1128.github.io/windows/2020/06/01/Install-WSL2.html) 포스트를 기반으로 설치해서 사용합니다.

실제로 쿠버네티스는  Master node와 Worker node로 이루어져 있습니다. 여기서 node는 실제 물리 서버 혹은 가상머신을 뜻합니다. aws에 여러개를 만들거나 실제 환경을 구상하기에는 어려움이 따르므로 이를 가상으로 만들어 줄 수있는 `minikube`라는 것이 존재합니다. 저는 이 minikube를 이용해 쿠버네티스를 공부 해 볼 예정입니다.

## Minikube install 

### WSL 사용 버전

![](../.gitbook/assets/image%20%2811%29.png)

윈도우에 설치한 도커에서 위와 같이 우분투 추가 설정을 열어줍니다. 위오 같이 우분투 설정을 해 주고, Kubernetes 탭에서 Enable Kubernetes를 체크 해준 뒤 적용해 줍니다.

![](../.gitbook/assets/image%20%2818%29.png)

그 후에 쿠버네티스까지 실행된 부분이 확인 되면 ubuntu 창에서 `kubectl cluster-info`명령어를 통해 쿠버네티스 클러스터의 동작을 확인 할 수 있습니다.

```text
curl -Lo ./kind https://github.com/kubernetes-sigs/kind/releases/download/v0.7.0/kind-$(uname)-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/
```

이제 위의 명령어로 WSL 내부에서 쿠버네티스를 설치해 주어야 합니다.

이제 클러스터를 만들어 보겠습니다.

```text
echo $KUBECONFIG # 설정이 없는것을 확인합니다.

# wslClusterExample라는 이름의 클러스터를 생성합니다.
kind create cluster --name wslClusterExample 
```

![&#xD074;&#xB7EC;&#xC2A4;&#xD130; &#xC0DD;&#xC131;](../.gitbook/assets/image%20%2819%29.png)

wsl을 사용하는 경우 우분투 쉘에서 다음 명령어를 실행합니다.

```text
kubectl config set-cluster minikube --server=https://<minikubeip>:port --certificate-authority=/mnt/c/Users/<windows-user-name>/.minikube/ca.crt
kubectl config set-credentials minikube --client-certificate=/mnt/c/Users/<windows-user-name>/.minikube/cert.crt --client-key=/mnt/c/Users/<windows-user-name>/.minikube/client.key
kubectl config set-context minikube --cluster=minikube --user=minikube
```

위의 설정을 통해 `kubectl config view` 명령어로 정상 설치를 확인 할 수 있습니다.

![&#xC124;&#xCE58; &#xD655;&#xC778;](../.gitbook/assets/image%20%2814%29.png)



### 윈도우만 사용하는 버전

미니큐브는 가상환경이 필요하기 때문에 이미 가상환경 상태인 WSL의 우분투에는 설치 할 수 없습니다. 그렇기 때문에 `Hyper-V`가 지원되는지 확인 하고 윈도우 터미널에서 `choco install minikube` 명령어를 실행 해 줍니다.

![&#xC708;&#xB3C4;&#xC6B0; &#xD130;&#xBBF8;&#xB110;&#xC5D0;&#xC11C; &#xBBF8;&#xB2C8;&#xD050;&#xBE0C;&#xB97C; &#xC124;&#xCE58;](../.gitbook/assets/image%20%2815%29.png)

설치가 완료되었다면 `Get-NetAdapter` 명령어로 Hyper-V용 네트워크가 존재하는지 확인이 필요합니다.

![](../.gitbook/assets/image%20%2813%29.png)

존재 한다면 다음 명령어를 이용해 kubemini를 실행해 주면 됩니다.

```text
minikube start --vm-driver hyperv --hyperv-virtual-switch minikube
```



