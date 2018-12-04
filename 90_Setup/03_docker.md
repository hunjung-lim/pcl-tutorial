# Docker 환경 구성하기

## 설치 및 실행

도커 이미지 받기 : `$ docker push adioshun/pcl_to_all:20181122`

도커 실행 : `$ docker run -it --net=host --volume /workspace:/workspace --name 'pcl_to_all' adioshun/pcl_to_all:20181122 /bin/bash`

- `--net=host` : Host PC에서 ROS메시지를 받아 시각화 작업시 필요
- `--volume` : jupyter의 기본 작업 폴더로 Host PC와의 폴더 동기화를 위해 필요

컨테이너 실행 : `$ docker start pcl_to_all`

실행 확인(Option) : `$ docker ps -a`

도커 접속 : `$ docker exec -it pcl_to_all bash`

## Docker 내 실행

쥬피터 실행 : `jupyter notebook --allow-root`

웹프라우져 접속 : http://localhost:8888 (접속 암호 : ubuntu)
