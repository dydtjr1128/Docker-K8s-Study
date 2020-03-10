# 5. 도커 허브 연동하기

도커 허브는 깃허브와 비슷한 역할을 하는 장소로서 도커 이미지들을 담고 있는 공간입니다. [https://hub.docker.com/](https://hub.docker.com/) 로 도커 허브를 접속할 수있으며 레포지토리에 원하는 이미지를 업로드 할 수 있습니다. 우선 도커 허브를 사용하기 위해서는 도커 허브의 연동이 필요합니다. 깃허브 등의 아이디로 회원 가입을 할 수 있으므로 쉽게 가입 할 수 있습니다.

## 도커 허브 상태 확인

```bash
docker info | grep Username
```

위 명령으로 도커 상태를 확인 할 수 있습니다.

## 도커 로그인

```bash
docker login
```

도커 허브에 연동 된 아이디와 패스워드로 도커에 로그인 할 수 있습니다.

## 도커 로그아웃

```bash
docker logout
```

로그인 된 계정을 로그아웃 할 수 있습니다.

## 도커 네임스페이스 변경

```bash
docker image tag example/go-server:latest dydtjr1128/go-server:latest
```

도커 이미지를 도커 허브등의 외부 레포지토리에 올리기 위해 해당 네임스페이스\(`dydtjr1128/go-server`\)의 프로젝트 이름으로 태그를 변경해야 합니다. 도커 허브의 경우 자신 혹은 소속 기관이 소유한 레포지토리에만 이미지를 등록 할 수 있기 때문입니다.

## 도커 이미지 푸쉬\(push\)

```bash
docker push dydtjr1128/go-server:latest
```

 `go-server` 라는 이름의 이미지를  `dydtjr1128/go-server`레포지토리로 푸시 할 수 있습니다.

## 도커 이미지 풀\(pull\)

```bash
docker image pull -t dydtjr1128/go-server:latest
```

해당 레포지토리의 이미지를 위와 같이 풀 해 올 수 있습니다.

