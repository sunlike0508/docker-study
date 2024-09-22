# 도커

도커는 컨테이너 기반의 오픈소스 가상화 플랫폼이다.

도커는 어떤 프로그램을 외부 환경과 격리시켜 구동할 수 있게 해주는 소프트웨어이다.

## 컨테이너

컨테이너란 OS상에서 논리적인 영역(컨테이너)을 구축하고, 애플리케이션이 작동하는데 필요한 요소들을 모아 별도의 서버처럼 동작하는 것.

필요한 요소만으로 구성되어 있어 오버헤드가 작음 : 즉, 가상머신은 os를 설치해야한다. (내가 필요한 부분이 아닌 불필요소도 다 설치를 해야함) 그러나 도커는 내가 필요한 부분만 설치.

<img width="694" alt="Screenshot 2024-09-22 at 14 55 26" src="https://github.com/user-attachments/assets/b4e7bcfd-0360-4a4d-b3f1-bebf1dbee7f7">

Infrastructure : 우리가 쓰는 장비. ex) ram, cpu

Host Operating System : 우리가 아는 OS

쉽게 얘기해서 예를 들어 내가 사용하고 싶은 맥 애플리케이션이 있다고 하자.(꼭 OS가 아니더라도, 특정 메모리나 어떤 시스템 요구사항에 따른 필요한 경우) 

그러면 내가 윈도우에서 이걸 쓰고 싶은데 사용을 못한다. 그러면 이 도커의 힘을 빌려서 내가 사용하고 싶은 어플리케이션을 도커 위에서 사용 가능.

물론 도커 이전에 가상머신(VM)이 있었지만 위에 이미지처럼 필요한 os를 가상머신 위에 다 설치해야했지만 도커는 그럴 필요가 없다.

도커는 기본적으로 리눅스 환경을 기반으로 한다. 조금 전에 이해하기 쉽게 맥과 윈도우 관계를 예로 들었는데 정확히는 리눅스 기반을 필요로 하는 애플리케이션만 도커를 사용할 수 있다. 

순전히 윈도우나 맥이 필요한 애플리케이션은 사용이 불가능하다. 

단지 리눅스를 지원하지 않는 os에서 리눅스 기반의 어플리케이션을 사용하고 싶을때, 그 os에 도커를 통해서 리눅스 기반의 애플리케이션을 사용하고 싶을 때를 전제로 한다.

## 도커 컨테이너 구조

도커 컨테이너는 컨테이너 레이어와 이미지 레이어로 구성되어 있음

<img width="452" alt="Screenshot 2024-09-22 at 15 13 12" src="https://github.com/user-attachments/assets/4fc84e70-aa5f-40cb-8a8a-f1b276c92786">

**1. 이미지 레이어**

이미지 레이어는 여러개의 layer로 나뉘어져 있음

이미지 레이어는 레포지토리(ex: 도커허브) 같은 곳에서 가져갈수 있음. 

읽기 전용 계층

다른 컨테이너와 공유할 수 있는 레이어

**2. 컨테이너 레이어**

이미지를 컨터에너 레이어에 올리면 하나의 계층이 추가됨. 이거를 컨테이너 레이어라고 부름. 

read, writer가 가능함.

최상단 레이어에 추가.

컨테이너를 실행하고 진행되는 변경사항은 이 계층에 저장됨

<img width="600" alt="Screenshot 2024-09-22 at 15 19 32" src="https://github.com/user-attachments/assets/2be3c0ef-8c60-4713-a737-abddef378fb0">

컨테이너 레이어는 각기 다른 컨테이너가 공유하지 않는 계층이기 때문에 위의 그림과 같이 이미지 레이어를 공유하고 각각 컨테이너 레이어를 공유하는 것을 볼 수 있음.


이미지 레이어를 공유함으로써 용량의 효율적 사용. 동일한 이미지를 사용하기 때문에 동일한 성능을 낼 수 있다.

## 도커 명령어 구조

도커의 모든 명령은 docker로 시작하며 어떤 대상에게 명령어를 실행할 것인지로 구분하면 보기 쉬움

```shell
docker {대상} {커맨드} {옵션} {인자}
```

ex) docker container(image, volume, network)

### 도커 커맨드

1) docker 입력

2) docker [커맨드 대상] --help ex) docker container --help

3) 위와 같은 방법으로 커맨드 수준을 높이고 뒤에 --help 입력 ex) docker container run --help

**커맨드 종류**

* start : 컨터이너 실행 -i
* stop : 컨테이머 정지
* create : 컨테이너 생성 --name, -e, -p, -v
* run : 이미지를 내려받고 컨테이너를 생성 및 실행 --name, -e, -p, -v, -d, -i, -t
* rm : 컨테이너 삭제 -f, -v
* exec : 컨테이너에서 프로그램 실행 -i, -t
* ls : 컨테이너 목록 출력 -a
* cp : 컨테이너와 호스트간 파일 복사
* commit : 컨테이너를 이미지로 변환

**옵션 종류**

* -name : 컨테이너 이름
* -p : 포트 번호 지정
* -v : 볼륨 지정
* -e : 환경 변수 설정
* -d : 백그라운드 실행
* -i : 컨테이너에 터미널 연결
* -t : 특수 키를 사용가능하게 설정

## 도커 컨테이너와 통신하기

도커 컨테이너는 기본적으로 독립적인 환경에서 실행되기 때문에 컨테이너 밖에서 접근할 수 없음

컨테이너와 통신하기 위해서는 컨테이너를 가동시키면서 p 옵션을 사용하여 호스트의 포트와 컨테이너의 포트를 설정해야 함

```shell
-p ${host_port}:${container_port}
```

이 설정을 사용하기 위해서는 호스트(서버 또는 PC)에서 사용 중인 포트와 번호가 겹치지 않는지 확인이 필요함

<img width="532" alt="Screenshot 2024-09-22 at 15 53 25" src="https://github.com/user-attachments/assets/33fc5cea-0c64-4d46-84ae-a31a964172d7">

```shell
docker run --name test1 -d httpd

docker run --name test2 -d -p 8080:80 httpd
```

test1 이라는 이름으로 컨테이너를 생성한다. 

-d 는 백그라운드로 동작하겠다.

-p 8080:80 호스트의 포트는 8080, 컨테이너의 포트는 80으로 세팅하여 네트워크를 설정합니다.

위의 커맨드를 실행한 후에 docker 데스크탑으로 컨테이너 상태를 확인. 또는 커맨드를 입력하여 상태 확인.

```shell
docker ps -a

docker container ls -a
```

위의 실습을 마치면 실행을 중지하고 삭제하는 작업을 수행하는 것이 좋음

```shell
docker stop test1

docker rm test1
```

## 도커파일

dockerfile은 도커 이미지를 생성하기 위한 스크립트 파일

여러 키워드를 사용하여 도커파일을 작성하여 빌드를 보다 쉽게 수행

### dockerfile instruction

키워드라고 보면 됨.

* FROM
base가 되는 image를 지정, 주로 OS 이미지나 런타임 이미지를 지정함.

* RUN
이미지를 빌드할 떄 사용하는 커맨드를 설정할 때 사용

* ADD
이미지에 호스트의 파일이나 폴더를 추가하기 위해 사용

만약 이미지에 복사하려는 디렉토리가 존재하지 않으면 도커가 자동으로 생성

* Copy
호스트 환경의 파일이나 폴더를 이미지 안으로 복사하기 위해 사용

'ADD'와 동일하게 동작. 차이점은 URL을 지정하거나 압축파일을 자동으로 풀지 않음.

* EXPOSE
이미지가 통신에 사용할 포트를 지정할 때 사용

* ENV
환경 변수를 지정할 떄 사용

여기서 설정한 변수는 ${name, $name 의 형태로 사용할 수 있음

추가로 아래와 같은 문법을 사용하여 사용할 수도 있음

-${name:-else} : name 이 정의가 안되어 있다면 else가 사용됨

*CMD
도커 컨테이너가 실행될 때 실행할 커맨드를 지정

'RUN'과 비슷하지만 CMD는 도커 이미지를 빌드할 때 실행되는 것이 아니라 컨테이너를 시작할 때 실행된다는 것이 다름

*ENTRYPOINT
도커 이미지가 실행될 때 사용되는 기본 커맨드를 지정 (강제)

*WORKDIR
RUN, CMD, ENTRYPOINT 등을 사용한 커맨드를 실행하는 디렉토리를 지정

-w 옵션으로 오버라이딩을 할 수 있음

*VOLUME
퍼시스턴스 데이터를 저장할 경로를 지정할 때 사용

호스트의 디렉토리를 도커 컨테이너에 연결

주로 휘발성으로 사용되면 안되는 데이터를 저장할 때 사용

### 도커 빌드 커맨드

```shell
docker build ${option} ${dockerfile directory}
```

ex) docker build -t test . (. 온점 있는 거임)

생성된 이미지를 컨테이너로 실행하기 위해서는 run 커맨드를 사용

ex) docker run --name test_app -p 80:80 test

```shell
docker build -t test123:1.1 .
```

이렇게 하면 버전도 tagging 할 수 있다.

## docker compose

compose 파일은 도커 애플리케이션의 서비스, 네트워크 볼륨등의 설정을 yaml 형식으로 작성하는 파일

```docker
services:
  frontend:
    image: example/webapp
    ports:
      - "443:8043"
    networks:
      - front-tier
      - back-tier
    configs:
      - httpd-config
    secrets:
      - server-certificate

  backend:
    image: example/database
    volumes:
      - db-data:/etc/data
    networks:
      - back-tier

volumes:
  db-data:
    driver: flocker
    driver_opts:
      size: "10GiB"

configs:
  httpd-config:
    external: true

secrets:
  server-certificate:
    external: true

networks:
  # The presence of these objects is sufficient to define them
  front-tier: {}
  back-tier: {}
```




































