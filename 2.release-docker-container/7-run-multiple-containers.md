# 7. 여러 컨테이너 실행하기

서버를 운용할때 하나로만 운영하는게 아니라 마이크로 서비스를 할 수 도있고, 거기에 로드밸런서가 필여할 수도 있는등 다양한 의존관계로 하나의 시스템이 구성됩니다. 그렇기 때문에 앞에서 배운 방법 다음으로 다양한 컨테이너간 의존관계, 동작방식등을 고려해야 합니다.

여기에서는 `docker compose` 명령을 통해서 다양한 컨테이너 조작법을 공부해 보려고 합니다.

## docker-compose

도커 컴포즈에서 Compose는 yaml 포맷으로 기술된 설정 파일로, 여러 컨테이너의 실행을 한번에 관리 할 수 있도록 해줍니다.

```text
>docker-compose version
docker-compose version 1.25.4, build 8d51620a
docker-py version: 4.1.0
CPython version: 3.7.4
OpenSSL version: OpenSSL 1.1.1c  28 May 2019
```

위와 같이 출력된다면 도커 컴포즈를 사용 할 수 있는 상태입니다.

{% tabs %}
{% tab title="docker-compose.yml" %}
```text
version: "3"
services:
	echo:
		image: dydtjr1128/go-server:latest
		ports:
            - 9000:8080
```
{% endtab %}
{% endtabs %}

version은 해당 `docker-compose.yml` 가 존재하는 경로에서 `docker-compose up -d` 명령으로 실행 할 수 있습니다.

