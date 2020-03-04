# 3. 어플리케이션 관점에서의 도커

도커 스타일의 배포 방식을 이해하기 위해서 간단한 예제를 만들어 테스트 해 보겠습니다.

{% code title="hello.sh" %}
```bash
#!/bin/sh
echo "Hello, World!"
```
{% endcode %}

위와 같이 `hello.sh` 라고 하는 어플리케이션이 있다고 가정하고 이 어플리케이션을 도커 컨테이너에 담는 예제를 구현하도록 하겠습니다.

1번째 라인은 기본 쉘을 사용하기 위해서 필수적으로 선언해야 하는 내용입니다.

같은 경로에 `Dockerfile`을 작성해야 합니다.

{% code title="Dockerfile" %}
```bash
FROM ubuntu:16.04

COPY hello.sh /usr/local/bin

WORKDIR /usr/local/bin

RUN chmod 777 hello.sh

CMD ["hello.sh"]
```
{% endcode %}

* FROM : 컨테이너의 원형이 될 도커이미지\(운영체제\)를 정의하는 부분입니다.
* COPY : 기본적으로 `/` 경로에 저장될 `hello.sh` 파일을 `/usr/local/bin` 경로로 복사하는 부분입니다.
* WORKDIR : 기본 작업 경로인 `/` 에서 경로를 `/usr/local/bin`로 변경합니다.
* RUN : 빌드중에 적용할 스크립트를 작성하는 부분으로 여기서는 권한 설정하는 역할을 합니다.
* CMD : 도커 컨테이너로 실행하기 전에 먼저 실행할 명령을 정의하는 부분입니다. 여기서는 어플리케이션을 실행하는 명령을 지정했습니다.

위와 같이 2개의 파일을 만들었으면 이제 도커를 이용해서 빌드 할 차례 입니다.

```bash
sudo docker image build -t hello:latest .
```

* `image build` : 이미지를 빌드하겠다는 파라미터 입니다.
* `-t hello:latest` : 타겟\(버전\)을 hello의 latest 로 표기하겠다는 의미입니다.
* `.` : 현재 디렉토리를 빌드하겠다는 의미입니다.

{% hint style="info" %}
docker 명령어는 항상 관리자 권한에서 동작해야 하므로 sudo 혹은 su 에서 실행해야 합니다.
{% endhint %}

```bash
sudo docker container run hello:latest
```

이 후에 결과로 \`Hello, World\`가 출력되는것을 확인 할 수있습니다.

