---
layout: post
title:  "아파치 MPM EVENT MODE, FastCGI와 PHP-FPM 관계"
date:   2019-02-16 00:00:00 +0900
categories: apache
---

서버 스크립트 PHP를 사용하는 환경에서,

아파치 MPM 이벤트 모드를 사용고자 하였다. 

왜? 스레드를 활용한 자원의 효율적인 사용으로 쾌적한 서버 상태에 유리하다. 

- MPM 선택(https://httpd.apache.org/docs/2.4/ko/misc/perf-tuning.html)

```
아파치 2.x는 다중처리모듈 (MPMs)이라는 교체할 수 있는 동기화 모델을 지원한다. 아파치를 컴파일할때 MPM을 선택해야 한다. beos, mpm_netware, mpmt_os2, mpm_winnt와 같이 특정 플래폼에서만 사용할 수 있는 MPM도 있다. 일반적인 유닉스류 시스템은 여러 MPM 중에 하나를 선택할 수 있다. 웹서버의 속도와 확장성(scalability)은 어떤 MPM을 선택했냐에 달렸다:

worker MPM은 여러 자식 프로세스가 각각 여러 쓰레드를 사용한다. 각 쓰레드는 한번에 한 연결을 담당한다. 일반적으로 worker는 prefork MPM 보다 적은 메모리를 사용하므로 통신량이 많은 서버에 적절하다.

prefork MPM은 쓰레드가 한개인 자식 프로세스를 여러개 사용한다. 각 프로세스는 한번에 한 연결을 담당한다. 여러 시스템에서 prefork의 속도는 worker와 비슷하지만, 더 많은 메모리를 사용한다. 다음과 같은 상황에서 쓰레드를 사용하지 않는 prefork 방식이 worker에 비해 이점을 가진다: 쓰레드에 안전하지 (thread-safe) 않은 제삼자가 만든 모듈을 사용할 수 있고, 쓰레드 디버깅 지원이 빈약한 플래폼에서 쉽게 디버깅할 수 있다.
이 MPM들과 다른 MPM에 대해 더 자세한 정보는 MPM 문서를 참고하길 바란다.
```

PHP와 아파치 MPM 이벤트 모드를 사용하기 위해서는 
- MPM 이벤트 모드 옵션을 주고 아파치 컴파일.
  - configure --with-mpm=event(https://httpd.apache.org/docs/2.4/mod/event.html)
- 이벤트 모드에서는 mod_php(nts)를 사용할 수 없기 때문에 PHP-FPM을 사용한다.  
  - apt-get install php-fpm
- 아파치에서 PHP-FPM을 사용하기 위해서는 아파치 FastCGI 모듈(mod_proxy_fcgi.so)을 사용해야 한다.
  - /etc/php/[VERSION]/fpm/pool.d/www.conf
    - UNIX SOCKET 또는 TCP SOCKET 선택하여 설정
      - listen = /run/php/php7.2-fpm.sock(권한 설정 확인 필요)       
      - listen = 127.0.0.1:9000
  - httpd.conf
    - LoadModule proxy_module modules/mod_proxy.so
    - LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so
    - www.conf 참고하여 설정 추가
      
```
<FilesMatch "\.php$">

    <If "-f %{REQUEST_FILENAME}">

        # Pick one of the following approaches

        # Use the standard TCP socket

        #SetHandler "proxy:fcgi://localhost/:9000"

        # If your version of httpd is 2.4.9 or newer (or has the back-ported feature), you can use the unix domain socket

        #SetHandler "proxy:unix:/path/to/app.sock|fcgi://localhost/"

    </If>

</FilesMatch>
```      
