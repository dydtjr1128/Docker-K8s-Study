# 4. 도커 커맨드

### 컨테이너 실행

2.1 절에서는 도커 컨테이너를 다음과 같이 실행 했었습니다.

```bash
docker container run -t go_server:latest
```

그럼 전면에서 컨테이너가 출력하는 로그 등을 확인 할 수 있습니다. 그리고 CTRL+C 키를 이용해 빠져 나올 수 있습니다. 이때 `-d` 옵션을 붙여서 실행한다면 daemon\(d\)으로 백그라운드에서 동작하게 만들 수 있습니다. 

### 컨테이너 이름 짓기

```bash
docker container run -t --name my_go_server go_server:latest
```

위와 같이 `my_go_server` 라는 이름으로 컨테이너를 실행 할 때 이름을 지어 줄 수 있습니다.

### 컨테이너 중지

```bash
docker container stop $(docker container ls --filter "ancestor=go_server" -q)
```

### 컨테이너 재시작

```bash
docker container restart go_server:latest
```

### 컨테이너 제거

```bash
docker container rm go_server:latest
```

중지된 컨테이너를 완전히 파기하려면 위와 같이 rm 명령어를 이용해 파기 할 수 있습니다.

다음과 같이 여러개의 중지된 컨테이너들을 확인 할 수도 있습니다.

```bash
docker container ls --filter "status=exited"
```

```bash
docker container run -t --name my_go_server --rm go_server:latest
```

`my_go_server` 라는 이름을 가진 컨테이너가 이미 존재 할 때 같은 이름으로 생성 시 오류를 발생시키는데, 이때 --rm 옵션을 적용해 컨테이너를 실행한다면 컨테이너 중지 시 제거까지 해주어 오류 발생 여지를 줄여줍니다.

### 가지고 있는 이미지 목록 조회

```bash
docker images
```

```bash
docker image ls
```

### 실행중인 컨테이너 목록 조회

```bash
docker container ls
```

### 포트 포워딩

```bash
docker container run -d -p 9000:8080 example/echo:latest
```

위와 같이 `-p` 옵션을 이용해 로컬 포트와 컨테이너 포트를 포워딩 할 수 있습니다.

### 컨테이너 목록 필터링

```bash
docker container ls --filter "필터명=값"
```

 필터명에는 name\(컨테이너 명\), ancestor 등이 존재합니다.

### 컨테이너에 표준출력 연결

```bash
docker container logs -f $(docker container ls --filter "ancestor=go_server" -q)
```

위와 같이 ancestor에 해당하는 컨테이너의 로그를 표준출력에 보여줄 수 있습니다.

### 실행중인 컨테이너에서 명령 실행

```bash
docker container exec echo pwd
```

위와 같이 현재 실행중인 컨테이너에서 현재 경로를 가져오는 echo pwd 라는 명령을 내릴 수 있습니다.

표준 입력 연결을 유지하는 `-i` 옵션과 유사 터미널을 할당하는 `-t` 옵션을 조합해 컨테이너를 셸에서 다룰수 있게 해줍니다.

```bash
cker container exec -it echo sh
pwd
/go <- 출력
```

### 파일 복사하기

```bash
docker container cp dummy.txt go_server:/usr
```

위와 같이 dummy.txt라는 파일을 도커 컨테이너인 go\_server 하위 usr 폴더에 복사 할 수 있습니다.

