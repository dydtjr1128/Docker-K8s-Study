# 1. 간단한 도커 이미지 만들기

간단한 예제를 이용해 도커 이미지를 만들고 실행 해 보도록 하겠습니다. go 언어를 이용하여 만든 간단한 웹서버에 대한 코드입니다.

{% tabs %}
{% tab title="server.go" %}
```go
package main
import (
    "fmt"
    "log"
    "net/http"
)

func main() {
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        log.Println("received request")
        fmt.Fprintf(w, "Hello Docker!!")
    })
    
    log.Println("Start server")
    server:= &http.Server {
        Addr: ":8080",
    }
    if err:= server.ListenAndServe(); err != nil {
        log.Println(err)
    }
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Dockerfile" %}
```go
FROM golang:1.9

RUN mkdir /echo
COPY server.go /echo

CMD ["go", "run", "/echo/server.go"]
```
{% endtab %}
{% endtabs %}

위와 같이 2개의 파일이 준비되었다면 도커 명령어를 쳐 주면 됩니다.

```text
docker image build -t go_server:latest .
```

그 후에 만들어준 이미지 파일을 실행하고 다른 쉘을 켜 확인 해 볼 수 있습니다.

```text
docker container run -t -p 9000:8080 go_server:latest
```

위의 코드는 실행 시 호스트 os의 9000과 도커 내부의 8080과 연결해 실행하겠다는 의미입니다.

```text
curl http://localhost:9000
```

또 다른 쉘을 켜 위와 같이 접속을 하면정상적으로 출력이 되는 모습을 확인 할 수 있습니다.

```text
2020/03/04 06:40:39 Start server
2020/03/04 06:42:43 received request
```

