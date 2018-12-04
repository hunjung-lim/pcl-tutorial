# 환경 구성

실습을 위해 구성한 환경은 아래와 같습니다.

- Host PC : Ubuntu 18.04 with ROS (Optional)
- Guest PC(Docker) : Ubuntu 16.04 with Python-PCL

## Host PC

일반적인 방법은 Docker 없이 Host PC에 ubuntu, ROS, python-pcl을 [모두 설치](./02_ubunut.md) 하여 사용하는 것이지만, 개발환경 분리를 위하여 Docker를 이용하였습니다.

Docker기반으로 구성할 경우 대부분의 작업은 Guest PC에서 이루어 지기 때문에 특별한 요구사항은 없습니다. (따라서, windows에서도 재현 가능합니다.)

하지만, 처리 결과를 실시간 확인하기 위해서 ROS의 rviz라는 시각화 툴을 사용하기 위해 선택적으로 [ROS설치](./04_ros.md)를 권장 합니다. (Docker에서도 rviz를 실행 할수 있지만 지연이 좀 발생합니다.)

## Guest PC(Docker)

Ubuntu 16, ROS, PCL-python, Open3D, Jupyter가 설치된 Docker를 [[여기]](https://hub.docker.com/r/adioshun/pcl_to_all/)에 올려 두었습니다.

자세한 실행 방법은 [환경구성-Docker활용](./03_docker.md)를 참고 바랍니다.

> 윈도우를 사용하시는 분은 VMWARE를 사용하거나, 윈도우용 Docker를 이용해도 됩니다.
