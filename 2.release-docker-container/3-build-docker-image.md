# 3. 이미지 빌드

2.1절 에서는 `docker image build -t go_server:latest .`  명령으로 빌드를 진행 했었습니다.

`docker image build -t 이미지명:태그명 Dockerfile의_경로` 와  같은 방식으로 표기를 합니다. -t 옵션을 이용해 이미지명과 태그명을 지정할 수있으며 태그명을 생략 시 latest로 자동적으로 태그가 붙습니다. -t를 사용하지 않아도 빌드가 되지만 그런 경우 해시값을 이용해 빌드 한 파일을 찾아야하므로 무조건적으로 붙인다고 생각하는것이 좋습니다.

```bash
Step 1/4 : FROM golang:1.9
1.9: Pulling from library/golang
55cbf04beb70: Pull complete
1607093a898c: Pull complete
9a8ea045c926: Pull complete
d4eee24d4dac: Pull complete
9c35c9787a2f: Pull complete
8b376bbb244f: Pull complete
0d4eafcc732a: Pull complete
186b06a99029: Pull complete
Digest: sha256:8b5968585131604a92af02f5690713efadf029cc8dad53f79280b87a80eb1354
Status: Downloaded newer image for golang:1.9
 ---> ef89ef5c42a9
Step 2/4 : RUN mkdir /echo
 ---> Using cache
 ---> 928392d1f437
Step 3/4 : COPY server.go /echo
 ---> d186b62f0a79
Step 4/4 : CMD ["go", "run", "/echo/server.go"]
 ---> Running in 7edb6fb65f9b
Removing intermediate container 7edb6fb65f9b
 ---> d8adb0a49d2c
Successfully built d8adb0a49d2c
Successfully tagged go_server:latest
```

빌드의 결과로 위와 같이 golang을 가져와 묶어주는 것을 확인 할 수 있습니다.

또한 `docker image ls` 명령으로 저장된 도커 컨테이너 이미지들을 확인 할 수도 있습니다.

{% hint style="info" %}
`Dockerfile이 아닌 다른 이름의 파일로 빌드 하고 싶은 경우` -f옵션을 사용하여 빌드 할 수있습니다. ex\) `docker image build -f Dockerfile-example -t go_server:latest`
{% endhint %}

