# [Web](https://github.com/hyojaekim/TIL/tree/master/Web) / [🏠 Home](https://github.com/hyojaekim/TIL)

# JWT란?

통신 시 권한 인가(Authorization)를 위해 사용하는 토큰이다. URL에 대해 안전한 문자열로 구성되어 있기 때문에 HTTP 어디든(URL, Header 등) 위치할 수 있다.

---

# 구조와 생성

`HEADER.PAYLOAD.SIGNATURE`

헤더(Header), 페이로드(Payload), 서명(Signature) 세 부분을 점(.)으로 구분하는 구조다.

## Header

JWT를 검증하는데 필요한 정보를 가진 JSON 객체는 Base64 URL-Safe 인코딩된 문자열이다.

헤더(Header)는 JWT를 어떻게 검증하는가에 대한 내용을 담고 있다.

참고로 alg는 서명 시 사용하는 알고리즘이고, kid는 서명 시 사용하는 키(Public/Private Key)를 식별하는 값이다.

```json
{
    "alg": "ES256",
    "kid": "Key ID"
}
```

위와 같은 JSON 객체를 문자열로 직렬화하고 UTF-8과 Base64 URL-Safe로 인코딩하면 다음과 같이 헤더를 생성할 수 있다.

```java
Base64URLSafe(UTF-8('{"alg": "ES256","kid": "Key ID"}')) -> eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRCJ9
```

## Payload

JWT의 내용이다. 페이로드(Payload)에 있는 속성들을 클레임 셋(Claim Set)이라 부른다.

클레임 셋은 JWT에 대한 내용(토큰 생성자(클라이언트)의 정보, 생성 일시 등)이나 클라이언트와 서버 간 주고 받기로 한 값들로 구성된다.

```json
{
    "iss": "jinho.shin",
    "iat": "1586364327"
}
```

위와 같은 JSON 객체를 문자열로 직렬화하고 Base64 URL-Safe로 인코딩하면 다음과 같이 페이로드를 생성할 수 있다.

```java
Base64URLSafe('{"iss": "jinho.shin","iat": "1586364327"}') -> eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6ImppbmhvLnNoaW4ifQ
```

## Signature

점(.)을 구분자로 해서 헤더와 페이로드를 합친 문자열을 서명한 값이다.

서명은 헤더의 alg에 정의된 알고리즘과 비밀 키를 이용해 성성하고 Base64 URL-Safe로 인코딩한다.

```json
Base64URLSafe(Sign('ES256', '${PRIVATE_KEY}',
'eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRCJ9.eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6ImppbmhvLnNoaW4ifQ'))) ->
MEQCIBSOVBBsCeZ_8vHulOvspJVFU3GADhyCHyzMiBFVyS3qAiB7Tm_MEXi2kLusOBpanIrcs2NVq24uuVDgH71M_fIQGg
```

## Header + Payload + Signature = JWT

점을 구분자로 해서 헤더, 페이로드, 서명을 합치면 JWT가 완성된다.

```json
eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRCJ9.eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6ImppbmhvLn
NoaW4ifQ.eyJhbGciOiJFUzI1NiIsImtpZCI6IktleSBJRC9.eyJpYXQiOjE1ODYzNjQzMjcsImlzcyI6Imp
pbmhvLnNoaW4ifQ.MEQCIBSOVBBsCeZ_8vHulOvspJVFU3GADhyCHyzMiBFVyS3qAiB7Tm_ME
Xi2kLusOBpanIrcs2NVq24uuVDgH71M_fIQGg
```

완성된 JWT는 헤더의 alg, kid 속성과 공개 키를 이용해 검증할 수 있다.

서명 검증이 성공하면 JWT의 모든 내용을 신뢰할 수 있게되고, 페이로드의 값으로 접근 제어나 원하는 처리를 할 수 있게된다.

---

# 주의점

1. 사용자의 권한이나 정보가 변경되면 새로운 JWT를 발급해야 한다.
2. 경우에 따라 JWT의 크기가 커질 수 있다.
3. JWT는 암호화 된 것이 아니라 Base64로 디코딩하면 내용을 확인할 수 있다.
따라서 민감한 정보는 포함되지 않아야 한다.

---

# 결론

JWT의 넓은 범용성, 무결성 보장, 필요한 값을 자체 포함할 수 있는 성질 때문에 많은 곳에서 JWT를 사용하고 있다. 따라서 앞으로 더 많은 곳에서 사용할 수 있을 것이다.

특히 MSA에서 서비스 간 통신 시 권한 서비스와의 의존성을 줄일 수 있어 서버와 서버 간 통신에 매우 유용하다.

MSA 환경에서 권한 인가의 한 가지 방법으로 JWT를 사용한다면 더 MSA에 어울리고 더 클라우드 네이티브(Cloud Native)한 서비스를 만들 수 있을 것이라고 생각한다.



- [참고 자료](https://meetup.toast.com/posts/239)


### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Web/JWT.md#Web---home)
