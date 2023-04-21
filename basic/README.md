## Nginx 

## Install

```
    brew install nginx (mac)
    brew services restart nginx
```

## 문법검사

```
    nginx -t
```

## config 

### 1. nginx.conf include 설정

```
    find / -name nginx
    sudo vi /usr/local/etc/nginx/nginx.conf

    http {
        ...

        include conf-settings/*;
    }

    pwd (usr/local/etc/nginx)
    mkdir conf-settings

    donggyu.conf 파일을 conf-settings 폴더내에 위치
```

### 2. curl test

```
    curl donggyu.com:82

    # prefix
    curl donggyu.com:82/job
    curl donggyu.com:82/job/a
    curl donggyu.com:82/job/b ...

    # exact
    curl donggyu.com:82/profile
```

### iamge, text 파일 설정

```
    /tmp/public 에 위치 (root 문법)

    curl donggyu.com:82/public/kg.jpeg
    curl donggyu.com:82/public/profile.txt
```

## Nginx Load Balance
- Scale up vs Scale out
- Scale out must needs Load Balancing

### nginx LoadBalance Policy
- https://intrepidgeeks.com/tutorial/nginx-server-load-balancing-strategy-6-kinds
- 기본은 roudn robin

```
    upstream backend {
    least_conn; 
    server localhost:8001; 
    server localhost:8002; 
    server localhost:8003;
}

server {
    listen 80

    location / {
        # setting client host
        proxy_set_header Host $host
        
        # use upstream server
        proxy_set_header Connection ""; 

        # proxy_pass
        proxy_pass http://backend-dongguy

    }
}
```

- 80번 요청이 들어오면 8001 ~ 8003 3개의 서버로 로드밸런싱이 진행된다.
- 해당 로드밸런싱은 upstream server에서 기재된 알고리즘에 의해 진행된다.

## Example LoadBalance Nodejs Server
- ... Todo