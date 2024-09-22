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















