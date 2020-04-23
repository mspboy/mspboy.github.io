---
layout: post
title:  "Docker Virtualbox 설정"
date:   2020-03-04T19:25:52-00:00
author: dhp.lee
categories: DevOps
tags: lorem ipsum
---

### VirtualBox 설정

Windows 10 기준으로 로컬에서 이미지를 만들어서 레지스트리 Push 할 수 있도록 함

`ubuntu 16.04 LTS` 기준으로 작성

`Virtual Box 5.2v` --> [설치](https://www.virtualbox.org/wiki/Download_Old_Builds_5_2)
( `Ubuntu 16.04`   --> [다운로드](http://releases.ubuntu.com/16.04/) )

가상머신 생성 후, 부팅 이미지를 위 iso 파일로 한다(구글링 해보면 많이 나옴)

설치 후 `Virtual Box 5.2v`


#### 장치

<a href="/assets/devops/docker/01.png" data-lightbox="falcon9-small" data-title="Check out the Falcon 9 from SpaceX">
  <img src="/assets/devops/docker/01.png" title="장치 설정">
</a>

장치 탭에서
게스트 확장 CD 이미지 삽입 클릭 후 진행과정을 따름

##### 공유폴더 설정
공유폴더 설정을 눌러 Host와 Guest의 공유할 폴더를 설정
공유 폴더 설정 되었으면 마운트 ( 설정한 공유폴더 이름, 우분투의 실제 경로 순 )
{% highlight bash %}
sudo mount -t vboxsf "virtualbox_share" "/mnt/share"
{% endhighlight %}

##### 클립보드 공유, 드래그 앤 드롭 설정
둘다 편하게 양방향으로 설정

#### 네트워크 설정
인터넷도 연결되면서 Guest 환경으로 SSH로 접근할 수 있는 환경을 세팅

NatNetwork를 하나 생성한다( 그냥 옆에 + 버튼 누르면 자동 생성 )
<a href="/assets/devops/docker/02.png" data-lightbox="falcon9-small" data-title="Check out the Falcon 9 from SpaceX">
  <img src="/assets/devops/docker/02.png" title="네트워크 설정">
</a>

포트 포워딩을 진행
<a href="/assets/devops/docker/03.png" data-lightbox="falcon9-small" data-title="Check out the Falcon 9 from SpaceX">
  <img src="/assets/devops/docker/03.png" title="네트워크 설정">
</a>
여기에서 `Host IP`는 보통 `192.168.56.1` 이다
(Windows Host 에서 ipconfig를 치면 `VirtualBox Host-Only Network` 라 나옴. 없으면, Host-Only Network 생성 필요)

{% highlight bash %}
cd c:\Program Files\Oracle\VirtualBox
VBoxManage.exe -v
VBoxManage.exe hostonlyif create
{% endhighlight %}

`Guest IP`는 보통 Guest인 Ubuntu에서 ifconfig를 입력하고 내부 IP를 가져온다
(보통 10.0.2.15) 이다

모두 세팅 후
{% highlight bash %}
sudo apt update
sudo apt install openssh-sever
{% endhighlight %}
위 코드 진행

마지막으로
<a href="/assets/devops/docker/04.png" data-lightbox="falcon9-small" data-title="Check out the Falcon 9 from SpaceX">
  <img src="/assets/devops/docker/04.png" title="네트워크 설정" width="50%" height="50%">
</a>
<a href="/assets/devops/docker/05.png" data-lightbox="falcon9-small" data-title="Check out the Falcon 9 from SpaceX">
  <img src="/assets/devops/docker/05.png" title="네트워크 설정">
</a>
메인 VirtualBox 창에서 `설정` 클릭
네트워크 탭에서 `NatNetwork`
(따로 해야되는지 이유는 모르겠으나 일단 설정)

`완료하였으면 스냅샷을 꼭 찍어둔다`

그리고 putty로 접속을 해본다
<a href="/assets/devops/docker/06.png" data-lightbox="falcon9-small" data-title="Check out the Falcon 9 from SpaceX">
  <img src="/assets/devops/docker/06.png" title="Putty 접속">
</a>

일단 Host Windows 10 환경에서 Guest Ubuntu 초기 세팅이 완료 되었다.


### Docker 설정

docker 설치
{% highlight bash %}
sudo apt update
sudo apt install docker.io
{% endhighlight %}

#### docker 권한 설정

docker를 설치하고 docker 명령어 권한이 현재 유저에게 없다
{% highlight bash %}
sudo usermod -aG docker $USER
sudo setfacl -m user:$USER:rw /var/run/docker.sock
{% endhighlight %}
위 코드로 설정

모두 완료 하였으면, 아래 코드를 입력
{% highlight bash %}
docker ps
docker images
{% endhighlight %}
에러가 뜨지 않으면 완료

docker 이미지를 공인 레지스트리에서 받아오기로 해본다
{% highlight bash %}
docker pull ubuntu:18.04
{% endhighlight %}
아래 그림으로 진행
<a href="/assets/devops/docker/07.png" data-lightbox="falcon9-small" data-title="Check out the Falcon 9 from SpaceX">
  <img src="/assets/devops/docker/07.png" title="Putty 접속">
</a>

image pull을 완료한 상황
<a href="/assets/devops/docker/08.png" data-lightbox="falcon9-small" data-title="Check out the Falcon 9 from SpaceX">
  <img src="/assets/devops/docker/08.png" title="Putty 접속">
</a>