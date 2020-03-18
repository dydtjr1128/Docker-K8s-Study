# 8. 여러 컨테이너 컴포즈로 실행 예제

7절에서 공부한 내용으로 다양한 컨테이너 들을 실행 할 수 있습니다. 여기에서는 젠킨스를 예로 들어보겠습니다.

{% tabs %}
{% tab title="docker-compose.yml" %}
```text
version: "3"
services:
    master:
        container_name: master
        image: jenkinsci/jenkins:2.142-slim
        ports:
            - 8080:8080
        volumes:
            - ./jenkins_home:/var/jenkins_home
```
{% endtab %}
{% endtabs %}

여기에서 처음으로 volumes라는 개념이 등장합니다. volumes는 port와 비슷하게 저장소를 로컬과 컨테이너를 연결 해 주는 역할을 합니다. 위의 예제에서는 `/jenkins_home` 라는 저장소를 컨테이너의 `/var/jenkins_home` 저장소와 연결시켜 주었습니다. 파일 복사가 아닌 공유의 용도로서 폴더를 마운트 시켜주게됩니다.

![&#xC911;&#xAC04;&#xC5D0; &#xCD9C;&#xB825;&#xB41C; &#xC554;&#xD638;](../.gitbook/assets/image%20%287%29.png)

이 부분을 잘 기해 두어야 나중에 사용 할 수 있습니다. 그 후에 [http://localhost:8080](http://localhost:8080) 으로  접속해 젠킨스 페이지를 확인 할 수 있습니다.

```text
docker container exec -it master ssh-keygen -t rsa
```

위의 명령으로 sha 키를 만들어 줍니다.

{% tabs %}
{% tab title="docker-compose.yml" %}
```text
version: "3"
services:
    master:
        container_name: master
        image: jenkinsci/jenkins:2.142-slim
        ports:
            - 8080:8080
        volumes:
            - ./jenkins_home:/var/jenkins_home
        links
            - slave01
    slave01:
        container_name: slave01
        image: jenkinsci/ssh-slave
        environment:
            - JENKINS_SLAVE_SSH_PUBKEY=ssh-rsa AAAAB3NzaC..........
```
{% endtab %}
{% endtabs %}

그리고 위와 같이 자식의 젠킨스 컨테이너를 추가해주고, jenkins\_home/.ssh/jenkins\_home.ssh의 코드를 넣어줍니다.

