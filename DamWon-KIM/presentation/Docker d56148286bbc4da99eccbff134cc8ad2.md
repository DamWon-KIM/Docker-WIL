# Docker

가장 작은 웹 에플리케이션 실행해보기

![Untitled](Docker%20d56148286bbc4da99eccbff134cc8ad2/Untitled.png)

Docker

컨테이너 런타임 오픈소스로 개발자나 시스템 관리자가 애플리케이션을 보다 빠르고 단순하게 배포하고 실행하기 위한 플랫폼

도커 이미지란

 : **어플리케이션 실행에 필요한 프로그램 본체+라이브러리+관련 미들웨어[필요한 경우]+OS/네트워크 설정 값 등을 모아서 하나의 객체로 만든 것**

클라우드에서의 이미지

Image

**도커 컨테이너를 구성하는 파일 시스템과 실행할 어플리케이션 설정을 하나로 합친 것으로, 컨테이너를 생성하는 템플릿 역할을 한다.**

- 도커에서 서비스 운영에 필요한 서버 프로그램, 소스코드 및 라이브러리, 컴파일된 실행 파일을 묶는 형태 “Docker Image”
- 특정 프로세스를 실행하기 위한 모든 파일과 설정값[환경]을 지닌 것으로, 더 이상의 의존성 파일을 컴파일하거나 이것저것 설치할 필요 없는 상태의 파일
- 보통 수백 MB~수 GB가 넘는다. 가상머신의 이미지에 비하면 굉장히 적은 용량
- 하나의 이미지는 여러 컨테이너를 생성할 수 있고, 컨테이너가 삭제되더라도 이미지는 변하지 않고 그대로 남아 있음.
- github과 유사한 서비스인 DockerHub을 통해 버전 관리 및 배포[push & pull]가 가능하다.
- 다양한 API가 제공되어 원하는 만큼 자동화가 가능하다.
- Dockerfile이라는 파일로 이미지를 만들어서 소스와 함께 의존성 패키지 등 사용했던 설정 파일을 버전 관리하기 쉽도록 명시되어짐

레이어

**기존 이미지에 추가적인** 파일이 **필요할 때 다시 다운로드 받는 방법이 아닌 해당 파일을 추가하기 위한 개념**

- 이미지는 여러 개의 읽기 전용(read only) layer로 구성되고, 파일이 추가되면 새로운 layer가 생성된다.
- 도커는 여러 개의 layer를 묶어서 하나의 파일시스템으로 사용 할 수 있게 해준다. 그래서 이미지와 레이어는 같은 의미로도 사용
    
    ![Untitled](Docker%20d56148286bbc4da99eccbff134cc8ad2/Untitled%201.png)
    

도커 컨테이너(Docker Container)

**도커 이미지를 기반으로 생성되며, 파일 시스템과 어플리케이션이 구체화되어 실행되는 상태**

이미지(Image)를 실행한 상태로, 응용프로그램의 종속성과 함께 응용프로그램 자체를 패키징 or 캡슐화하여 격리된 공간에서 프로세스를 동작시키는 기술

- 한 서버는 여러 개의 컨테이너를 가져도 당연히 상관없으며, 컨테이너는 각각 독립적으로 실행된다.
- 컨테이너는 커널 공간과 호스트OS 자원(시스템 콜)을 공유한다.

![Untitled](Docker%20d56148286bbc4da99eccbff134cc8ad2/Untitled%202.png)

![Untitled](Docker%20d56148286bbc4da99eccbff134cc8ad2/Untitled%203.png)

![Untitled](Docker%20d56148286bbc4da99eccbff134cc8ad2/Untitled%204.png)

![Untitled](Docker%20d56148286bbc4da99eccbff134cc8ad2/Untitled%205.png)

**도커 컨테이너는 파일 시스템과 어플리케이션이 함께 담겨 있는 박스라고 보면 된다.**  

컨테이너 동작 생애 주기

: 실행 중, 정지, 파기의 3가지 상태

실행 중인 상태로 만들기 = docker container run 

정지시키기 = docker container stop

파기 = docker container rm

1. 이미지 캐시에서 로컬 이미지를 찾으려고 시도
2. 로컬에서 찾을 수 없는 경우, 리모트 이미지 레포지토리(Docker Hub)를 바라봄
3. 가장 최신 버전의 이미지를 다운 받고, 해당 이미지 기반 컨테이너를 생성
4. 도커 엔진 내의 사설 IP에 가상 IP를 부여
5. 호스트의 80 포트를 열고 컨테이너의 80 포트로 포워딩
6. 이미지 Dockerfile의 CMD를 통해 컨테이너 시작

![Untitled](Docker%20d56148286bbc4da99eccbff134cc8ad2/Untitled%206.png)

가상머신은,

Guest OS에 BIOS, 가상 CPU, 가상 메모리, 가상 디스크, 가상 NIC 등을 제공하여 마치 물리 서버에서 실행되는 것처럼 보입니다. 이 때문에 게스트OS 입장에서는 OS 시작과 정지 등의 운영에 있어서 물리서버와 아무런 차이점 없이 운영이 가능합니다.

컨테이너는 이와 달리 OS를 가상화하여 여러개의 컨테이너를 OS 커널에서 직접 실행합니다. 컨테이너는 기존의 가상화 기술보다 훨씬 가볍게 동작하며, OS 커널을 공유하고, 시작 시간이나 종료 시간이 빠르고, 메모리를 훨씬 적게 차지합니다.

Docker 자체에서 제공하는 Load Balance(이하 로드밸런싱) 기능

![Untitled](Docker%20d56148286bbc4da99eccbff134cc8ad2/Untitled%207.png)

[내부 로직 추측 자료]

alias 를 지정하지 않은 컨테이너 하나가 front 역할을 하고, 안에서 접속을 나눠주는 형식이다. front 컨테이너가 로드밸런서가 되는 것이 아닌, Docker 내부의 DNS가 round-robin 으로 IP를 지정해주는 것이다. front 컨테이너가 network 에 대해서 Docker DNS1 에게 IP를 요청하면, 해당 network 망 안에 있는 컨테이너 중 1개의 IP를 반환해주는 형식으로 보인다.

참고자료

[74. [Docker] Docker 의 Load Balance 기능 사용하기 : 네이버 블로그 (naver.com)](https://blog.naver.com/PostView.naver?blogId=alice_k106&logNo=220747224965&parentCategoryNo=&categoryNo=21&viewDate=&isShowPopularPosts=false&from=postView)

[컨테이너 기술과 가상화 기술 비교 - Opennaru, Inc.](http://www.opennaru.com/cloud/virtualization-vs-container/)