# 2. 인스트럭션\(Instruction\)

## FROM 인스트럭션

FROM 인스트럭션은 도커 이미지의 바탕이 될 베이스 이미지를 지정합니다. Dockerfile로 이미지를 빌드 할 때 먼저 FROM 인스트럭션으로 지정된 이미지를 받아옵니다.

이미지는 도커허브\(Docker Hub\)라는 호스팅 된 서비스로 가져옵니다. 깃허브와 비슷하다고 생각 할 수 있습니다.

이전 [2.1](https://dydtjr1128.gitbook.io/understanding-docker/2.release-docker-container/1-make-simple-docker-image)절에서 봤듯이 `FROM golang:1.9` 라는 뜻은 GO 언어의 런타임인 `golang`을 가져오는것이고 `:` 뒤에 붙은 `1.9`는 태그로서 1.9라는 식별자\(버전 등을 나타냄\)로 가져오겠다는 의미입니다. 각 버전은 해시값으로 관리되는데 보기가 어려우므로 태그를 이용해서 지정해 둘 수 있는것입니다.

## RUN 인스트럭션

RUN 인스트럭션은 도커 이미지가 빌드 될 때 컨테이너 안에서 실행 할 명령을 정의하는 인스트럭션입니다. 2.1절에서 나온 `RUN mkdir /echo` 라는 부분은 /echo라는 폴더를 만들라는 명령으로 기본값인 루트 하위에 생성하라는 의미입니다.

## COPY 인스트럭션

COPY 인스트럭션은 동작중인 호스트 머신의 파일, 디렉터리를 도커 컨테이너 안으로 복사하는 인스트럭션입니다. `COPY server.go /echo` 라는 명령에서 server.go 라는 파일을 하위 echo 폴더에 복사해 넣으라는 의미입니다.

## CMD 인스트럭션

CMD 인스트럭션은 도커 컨테이너를 실행 할 때\(`docker container run -t -p 9000:8080 go_server:latest`\) 컨테이너 안해서 실행 할 프로세스를 지정합니다. 2.1절에서 원하는 go파일의 실행 명령은 `go run /echo/server.go` 이고 CMD 인스트럭션에서는 공백으로 나눈 배열로 나타내기 때문에 `CMD ["go", "run", "/echo/server.go"]` 과 같이 표시합니다.

## ENTRYPOINT 인스트럭션

ENTRYPOINT 인스트럭션은 2.1절에서 나오지는 않았지만 중요한 인스트럭션 중 하나입니다. 이를 사용하면 컨테이너의 명령 실행 방식을 조절 할 수 있습니다. CMD와 마찬가지로 컨테이너를 실행 할 때 실행 할 프로세스를 지정하는 인스트럭션으로 ENTRYPOINT 인스트럭션을 지정하면 CMD의 인자가 ENTRYPOINT 에서 실행하는 파일에 인자로 주어집니다.

만약 ENTRYPOINT 를 사용하여 컨테이너 수행 명령을 정의한 경우, 해당 컨테이너가 수행될 때 반드시 **ENTRYPOINT 에서 지정한 명령을 수행되도록 지정** 합니다. 하지만, CMD를 사용하여 수행 명령을 경우에는 **컨테이너를 실행할때 인자값을 주게 되면 Dockerfile 에 지정된 CMD 값을 대신 하여 지정한 인자값으로 변경하여 실행**되게 됩니다.
