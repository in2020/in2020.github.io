---
layout: post
title:  "아파치 설정 httpd.conf"
date:   2019-02-17 09:00:00 +0900
categories: apache
---

[참고](https://www.lesstif.com/pages/viewpage.action?pageId=18219482)

# 전역 설정
- ServerTokens Prod
- KeepAlive On
- MaxKeepAliveRequests #
- KeepAliveTimeout #
- Listen 80
- User apache
- Group apache

# 서버 설정
- AllowOverride None
- <Directory "/dir/path">
- <Location "/uri/path">
- <Files "*.php">

# 가상 호스트 설정

이름 기반 가상호스트

~~~

<VirtualHost *:80>
    ServerName server1.example.com
    DocumentRoot /var//www/server1
 
    ErrorLog logs/server1-error_log
    TransferLog logs/server1-access_log
 </VirtualHost>

~~~