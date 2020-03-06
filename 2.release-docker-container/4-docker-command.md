# 4. 도커 커맨드

### 컨테이너 실행

2.1 절에서는 도커 컨테이너를 다음과 같이 실행 했었습니다.

```bash
docker container run -t go_server:latest
```

그럼 전면에서 컨테이너가 출력하는 로그 등을 확인 할 수 있습니다. 그리고 CTRL+C 키를 이용해 빠져 나올 수 있습니다. 이때 `-d` 옵션을 붙여서 실행한다면 daemon\(d\)으로 백그라운드에서 동작하게 만들 수 있습니다. 

### 컨테이너 중지

```bash
docker container stop $(docker container ls --filter "ancestor=go_server" -q)
```

### 도커 이미지 빌드



### 실행중인 컨테이너 목록 조회

```bash
docker container ls
```

### 포트 포워딩

```bash
docker container run -d -p 9000:8080 example/echo:latest
```

위와 같이 `-p` 옵션을 이용해 로컬 포트와 컨테이너 포트를 포워딩 할 수 있습니다.

###  

