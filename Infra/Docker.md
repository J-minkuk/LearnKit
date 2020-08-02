# Docker
* Docker 명령은 기본적으로 Docker Hub를 사용한다.
* Docker 저장소 서버는 Docker registry 서버라고 부른다.


## Command
설명 | 명령어 | 예시
----|-------|------
이미지 검색 | docker search <이미지 이름> | docker search ubuntu
이미지 받기 | docker pull <이미지 이름>:<태그> | docker pull ubuntu:latest<br>docker pull ubuntu:16.04
이미지 목록 출력 | docker images
컨테이너 생성 | docker run <옵션> <이미지 이름> <실행할 파일> | docker run -i -t --name test ubuntu /bin/bash<br>* -i(interactive), -t(Pseudo-tty) Bash shell에 입출력 가능<br>* --name 옵션으로 컨테이너 이름을 지정할 수 있지만, 지정하지 않는다면 Docker가 자동으로 이름을 생성한다.
컨테이너 시작 | docker start <컨테이너 이름> | docker start test
컨테이너 재시작 | docker restart <컨테이너 이름> | docker restart test
컨테이너 종료 | docker stop <컨테이너 이름 or 컨테이너ID> | docker stop test
컨테이너 접속 | docker attach <컨테이너 이름> | docker attach test<br>* exit 또는 Ctrl+D 컨테이너 정지<br>* Ctrl+P, Ctrl+Q 컨테이너를 정지하지 않고 나옴
컨테이너 목록 확인 | docker ps -a | -a 옵션을 사용하면 정지된 컨테이너까지 출력
컨테이너 삭제 | docker rm <컨테이너 이름> | docker rm test
이미지 삭제 | docker rmi <이미지 이름>:<태그> | docker rmi ubuntu:latest
이미지와 컨테이너 세부 정보 출력 | docker inspect <이미지 또는 컨테이너 이름>

## Dockerfile
키워드 | 설명 | 예시
-----|-------|------
FROM(필수) | 어떤 이미지를 기반으로 이미지를 생성할지 설정 | FROM ubuntu:latest
MAINTAINER | 이미지를 생성한 사람의 정보 | MAINTAINER David <david@mail.com>
RUN | FROM에서 설정한 이미지 위에서 스크립트 혹은 명령을 실행, RUN으로 실행한 결과가 새 이미지 생성되고, 실행 내역은 이미지의 히스토리에 남는다.<br>* FROM으로 설정한 이미지에 포함된 /bin/sh 실행 파일을 사용하게 되며 /bin/sh 실행 파일이 없으면 사용할 수 없다.<br>* RUN으로 실행한 결과는 캐시되며 다음 빌드 때 재사용한다. 재사용하지 않으려면 docker build 명령에서 --no-cache 옵션을 사용 | [RUN Example]
CMD | 컨테이너가 시작되었을 때 스크립트 혹은 명령을 실행, CMD는 Dockerfile에서 한 번만 사용 가능 | [CMD Example]
EXPOSE | 호스트와 연결할 포트 번호 설정, docker run 명령의 --expose 옵션과 동일 | [EXPOSE EXAMPLE][###EXPOSE Example]
ENV | 환경 변수 설정 (RUN, CMD, ENTRYPOINT에 적용됨) | [ENV Example]
USER | 명령을 실행할 사용자 계정 설정
WORKDIR | RUN, CMD, ENTRYPOINT의 명령이 실행될 경로 설정

### RUN Example
```
RUN apt-get install -y nginx
RUN echo "Hello Docker" > /tmp/hello
```
* sh 없이 바로 실행하기
```
RUN ["apt-get", "install", "-y", "nginx"]
RUN ["/user/local/bin/hello", "--help"]
```

### CMD Example
```
CMD touch /home/hello/hello.txt
```
* sh 없이 바로 실행하기
```
CMD ["redis-server"]
```
* sh 없이 바로 실행할 때 매개변수 설정하기
```
CMD ["<실행 파일>", "<매개변수1>", "<매개변수2>"]
CMD ["mysqld", "--datadir=/var/lib/mysql", "--user=mysql"]
```

### EXPOSE Example
```
EXPOSE 80
EXPOSE 443
```

### ENV Example
```
ENV HELLO 1234
CMD echo $HELLO
```