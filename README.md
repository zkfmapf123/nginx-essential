# Nginx

## Before Read

- Need Linux Environment (https://github.com/zkfmapf123/devops-ec2-docker)
- Download Nginx MainLine Version

```
    wget https://nginx.org/download/nginx-x.xx.x.tar.gz
    tar -zxvf nginx-x.xx.x
    cd nginx-x.xx.x

    // need compiler
    sudo apt-get install build-essential

    // need PCRE library
    sudo apt-get install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev

    // cd nginx-x.xx.x
    ./configure --sbin-path=/usr/bin/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --with-pcre --pid-path=/var/run/nginx.pid

    make
    make install or sudo make install

    ls -l /etc/nginx
    nginx -v
```

## NginX

- ./configure
  - 구성옵션 설정
  - 사용자의 빌드 옵션에 맞춰서 수정가능

## Install

```
    // in linux or ubuntu server

    sudo apt-get install nginx
```

## Configure-file

- nginx.service -> nginx 에서 systemd를 사용하기 위한 설정파일

## Nginx vs Apache

- Apache

  - 클라이언트 요청마다 새로운 프로세스나 스레드를 생성하는 멀티프로세스 아키텍처 사용
  - 모듈 유연 + 확장성 -> 다양한 모듈을 사용하여 확장성을 높일 수 있음
  - 프로세스와 스레드 생성 -> 메모리 사용량 올라감
  - 많은 요청 시 -> 성능 저하
  - 정적인 콘텐츠를 처리 + 대규모 시스템 (안정성, 확장성) -> 동시접속자가 많은 경우에는 성능저하가 일어날 수 있음 (트래픽)
  - Reverse Proxy, Load Balacing, Caching 기능 존재하나 nginx보다 미비

- Nginx
  - 단일 프로세스 또는 스레드처리 -> 이벤트기반 아키텍처
  - 메모리 절약, 동시에 처리 -> 연결수가 더 많음
  - 비동기 I/O 사용 -> 요청대기시간 짧고, 높은 처리량
  - Revese Proxy, Load Balancing, Caching -> 적은 메모리로 대규모 트래픽 처리 가능
  - 동적인 콘텐츠 + 부하분산이 필요한 대규모 트래픽 시스템

## HTTP Stress test

```
    // client
    ab -n 10000 [uri]

    // server
    sudo apt-get install iftop
    sudo iftop -i eth0
```

## Reference

<p><a href="https://nginx-playground.wizardzines.com">nginx playground</a></p>
<p><a href="https://nginx.org/en/download.html">nginx org</a></p>
<p><a href="https://www.nginx.com/resources/wiki/start/topics/examples/systemd/">nginx systemd 사용 문서</p>
