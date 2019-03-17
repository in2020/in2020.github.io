---
layout: post
title:  "아파치 빌드 옵션"
date:   2019-03-17 22:00:00 +0900
tags: [apache]
categories: apache
---

# APR

~~~

"--with-apr=/usr/local/apr" \
"--with-apr-util=/usr/local/apr-util" \

~~~

- 참조

(https://apr.apache.org/)  
(https://en.wikipedia.org/wiki/Apache_Portable_Runtime)  

- The range of platform-independent functionality provided by APR includes

~~~

Memory allocation and memory pool functionality
Atomic operations
Dynamic library handling
File I/O
Command-argument parsing
Locking
Hash tables and arrays
Mmap functionality
Network sockets and protocols
Thread, process and mutex functionality
Shared memory functionality
Skip list functionality
Time routines
User and group ID services

~~~

- Open source projects using APR

~~~

Apache HTTP Server
Flood load tester
FreeSwitch
JXTA-C
mod_jk v2 and mod_webapp (part of Tomcat)
Apache Subversion
libbtt (part of mod_bt)
Apache Serf
ActiveMQ CPP
LKLFTPD and LKL
OpenAMQ messaging server
managelogs
LibreOffice

~~~

# SO

~~~

"--enable-module=so" \
"--enable-so" \
"--enable-mods-shared=most" \

~~~

- 참조

https://www.phpschool.com/gnuboard4/bbs/board.php?bo_table=tipntech&wr_id=6413  
https://httpd.apache.org/docs/2.2/ko/programs/configure.html  

- --enable-so

mod_so가 제공하는 DSO 기능을 사용한다. --enable-mods-shared 옵션을 사용하면 자동으로 이 모듈을 포함한다.

- 동적공유객체 (DSO)

모듈을 httpd 실행파일과 분리하여 동적공유객체(Dynamic Shared Objects, DSO)로 컴파일할 수 있다. DSO 모듈은 서버를 컴파일할때 컴파일하거나, Apache Extension Tool (apxs)을 사용하여 나중에 컴파일하여 추가할 수 있다.

- --enable-mods-shared=most

동적공유모듈로 컴파일할 모듈 목록을 지정한다. 즉, 이 모듈들은 LoadModule 지시어를 사용하여 동적으로 읽어들여야 한다.  
most는 대부분의 모듈을 DSO 모듈로 컴파일한다.

# SSL

~~~

"--enable-ssl" \
"--with-ssl=/usr/bin/openssl" \
"--enable-ssl-staticlib-deps" \
"--enable-mods-static=ssl" \

~~~

http + ssl = https