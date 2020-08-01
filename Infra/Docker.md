# Docker Command
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

