---
title: VAPID - (2)
tags:
  - Web
  - PWA
  - Push
  - Encrypt
  - VAPID
categories:
  - Web
  - PWA
date: 2019-02-08 13:34:57
---


# Voluntary Application Server Identification (VAPID) for Web Push - (2)
![Web Encryption](/images/cyber-security.png)

## VAPID

### 준비
어플리케이션 서버들은 인증 (Self-Identification) 을 위해, **비대칭키를 생성하고 보관**하여야 한다.
> 이 비대칭키는 P-256 곡선을 이용한 타원곡선서명 알고리즘(ECDSA) 를 사용해야 한다.

웹 푸시 메시지를 보낼때, **어플리케이션 서버는 JSON Web Token(JWT) 을 메시지에 포함**해야 한다.

### JSON Web Token
**토큰은 서명키(비밀키)에 의해 서명되어져야 한다.**
이 토큰은 Authorization 헤더 필드에 포함되어 발송되어야 한다. (vapid scheme 을 사용하여)

또한 이 토큰에는 몇가지 필드가 반드시 필요하다.

- aud
Audience
메시지를 받게될 브라우저의 URL 이다. ([Unicode Serialization of Origin](https://tools.ietf.org/html/rfc6454#section-6.1) 에 의해 처리)

- exp
Expiry
푸시 메시지를 발송시점보다 24시간 이상 길어서는 안된다.

만약, 서명에 이상이 있거나 필드들(aud, exp) 가 유효하지 못하면 403(Forbidden) 상태코드를 얻게 된다.

## 참고
[VAPID (https://tools.ietf.org/html/rfc8292)](https://tools.ietf.org/html/rfc8292)
