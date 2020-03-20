# 6. 운영과 관리를 위한 명령

지금 까지는 도커의 이미지와 컨테이너를 다루는 기본적인 명령들을 살펴 보았습니다. 이번에는 운영 및 관리를 위한 명령을 알아보려고 합니다.

### prune - 컨테이너 및 이미지 파기

`prune` 명령어는 이미지 및 컨테이너를 파기 할 때 사용하는 명령입니다. 도커를 장기간 사용하다보면 디스크에 저장된 컨테이너와 이미지가 많아지는데, 이 때 prune 명령을 이용해 일괄적으로 삭제 할 수 있습니다.

`docker container prune` : 실행중이 아닌 모든 컨테이너를 삭제합니다.

`docker image prune` : 태그가 붙지 않은\(dangling\) 모든 이미지를 삭제합니다.

`docker system prune` : 사용하지 않는 도커 이미지 및 컨테이너, 볼륨 네트워크 등 모든 도커 리소스를 일괄적으로 삭제합니다.

### stats - 사용현황 확인하기

stats은 시스템 리소스 사용 현황을 컨테이너 단위로 확인 할 수 있도록 도와줍니다. 유닉스 계열 운영체제의 top 명령과 같은 역할을 합니다.

```text
docker container stats [options] [대상_컨테이너_ID]
```

`docker container stats` : 모든 컨테이너의 상태를 보여줍니다.


