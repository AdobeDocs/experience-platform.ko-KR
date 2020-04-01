---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Experience Platform API 인증 및 액세스
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

---


# Experience Platform API 인증 및 액세스

이 문서에서는 Experience Platform API를 호출하기 위해 Adobe Experience Platform 개발자 계정에 대한 액세스 권한을 획득하기 위한 단계별 자습서를 제공합니다.

## API 호출을 위해 인증

응용 프로그램 및 사용자의 보안을 유지하려면 OAuth 및 JWT 파섹 그러면 JWT가 클라이언트 특정 정보와 함께 사용되어 개인 액세스 토큰을 생성합니다.

이 자습서에서는 다음 순서도에 설명된 액세스 토큰 작성을 통한 인증 단계를 설명합니다.
![](images/authentication/authentication-flowchart.png)

## 전제 조건

Experience Platform API를 성공적으로 호출하려면 다음이 필요합니다.

* Adobe Experience Platform을 이용할 수 있는 IMS 조직
* 등록된 Adobe ID 계정
* 개발자 **및 제품** 사용자로 **** 사용자를 추가할 수 있는 관리 콘솔 관리자

다음 섹션에서는 Adobe ID를 만들고 조직의 개발자 및 사용자가 되는 단계를 안내합니다.

### Adobe ID 만들기

Adobe ID 파섹

1. Adobe [I/O 콘솔로 이동](https://console.adobe.io)
2. 새 계정 **만들기를 클릭합니다.**
3. 등록 프로세스 완료


### 조직을 위한 경험 플랫폼의 개발자 및 사용자 되기

Adobe I/O에 대한 통합을 만들기 전에 계정에 IMS 조직의 제품에 대한 개발자 권한이 있어야 합니다. Admin Console에서 개발자 계정에 대한 자세한 내용은 개발자 관리를 위한 [지원 문서를](https://helpx.adobe.com/enterprise/using/manage-developers.html) 참조하십시오.

**개발자 이용**

조직의 Admin Console 관리자에게 문의하여 관리 콘솔을 사용하여 조직의 제품 중 하나에 대한 개발자로 [추가하십시오](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

관리자는 한 개 이상의 제품 프로필에 귀하를 개발자로 할당해야 계속 진행할 수 있습니다.

![](images/authentication/add-developer.png)

개발자로 지정되면 Adobe I/O에 대한 통합을 만들 수 있는 액세스 권한이 [부여됩니다](https://console.adobe.io/). 이러한 통합은 외부 앱 및 서비스에서 Adobe API로의 파이프라인입니다.

**사용자 액세스 권한 얻기**

또한 Admin Console 관리자가 귀하를 사용자로 제품에 추가해야 합니다.

![](images/authentication/assign-users.png)

개발자를 추가하는 프로세스와 마찬가지로, 관리자는 계속하려면 하나 이상의 제품 프로필에 사용자를 할당해야 합니다.

![](images/authentication/assign-user-details.png)


## 1회 설정

다음 단계는 한 번만 수행하면 됩니다.

* Adobe I/O 콘솔에 로그인
* 통합 만들기
* 액세스 값 복사

통합 및 액세스 값이 있으면 나중에 인증에 다시 사용할 수 있습니다. 각 단계는 아래에 자세히 설명되어 있습니다.

### Adobe I/O 콘솔에 로그인

Adobe [I/O 콘솔로](https://console.adobe.io/) 이동하여 Adobe ID로 로그인합니다.

로그인하고 나면 화면 상단에 **있는 통합** 탭을 클릭합니다. 통합은 선택한 IMS 조직에 대해 생성된 서비스 계정입니다. 통합이 생성된 IMS 조직에만 호출을 수행할 수 있습니다.

>[!NOTE]
>계정이 여러 조직과 연결되어 있는 경우 화면 오른쪽 상단의 드롭다운 메뉴를 통해 계정을 쉽게 전환할 수 있습니다.

### 통합 만들기

통합 **페이지에서** 새 **통합을** 클릭하여 프로세스를 시작합니다. 이 프로세스에는 다음 세 가지 단계가 포함됩니다.
* 통합 유형 선택
* 통합할 Adobe 서비스 선택
* 통합 세부 사항, 공개 키 및 제품 프로필 추가

![](images/authentication/integrations.png)

#### 통합 유형 선택

다음 화면에서는 API에 액세스할지 또는 거의 실시간으로 이벤트를 수신할지를 묻습니다. API **액세스를** 선택한 다음 계속을 **선택합니다**.

![](images/authentication/create-new-integration.png)

#### 통합할 Adobe 서비스 선택

계정이 여러 IMS 조직과 연결된 경우 오른쪽 상단의 드롭다운 메뉴를 사용하여 두 조직 간에 전환할 수 있습니다. Adobe **Experience Platform에서** **Workshop** and Experience Platform API를 **선택하여** API에 액세스합니다.

![](images/authentication/integration-select-service.png)

계속을 **클릭하여** 다음 섹션으로 이동합니다.

#### 통합 세부 사항, 공개 키 및 제품 프로필 추가

다음 화면에 통합 세부 사항을 입력하고 공개 키 인증서를 입력한 다음 제품 프로필을 선택하라는 메시지가 표시됩니다.

![](images/authentication/integration-details.png)

먼저 통합 세부 정보를 입력합니다. 그런 다음 제품 프로필을 선택합니다. 제품 프로필은 이전 단계에서 선택한 서비스에 속한 기능 그룹에 대한 세부 액세스 권한을 부여합니다.

인증서 섹션의 경우 인증서를 생성해야 합니다.

**MacOS 및 Linux 플랫폼의 경우:**

명령줄을 열고 다음 명령을 실행합니다.

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**Windows 플랫폼의 경우:**

1. 공개 클라이언트를 다운로드하여 공개 인증서 생성(예: Open [windows 클라이언트](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip))

1. 폴더를 추출하여 C:/libs/ 위치에 복사합니다.

1. 명령줄 프롬프트를 열고 다음 명령을 실행합니다.

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

자신에 대한 일부 정보를 입력하라는 메시지가 표시되는 다음과 유사한 응답을 받게 됩니다.

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

정보를 입력하면 두 개의 파일이 생성됩니다. `certificate_pub.crt` 및 `private.key`Adobe

>[!NOTE]
>`certificate_pub.crt` 365일 후에 만료됩니다. 위의 `days` `openssl` 명령에서 의 값을 변경하여 기간을 더 길게 만들 수 있지만 자격 증명을 주기적으로 회전하는 것은 좋은 보안 방법입니다.

The `private.key` will be used to generate our JWT in the later section.

API 키를 만드는 `certificate_pub.crt` 데 사용됩니다. Adobe I/O 콘솔로 돌아가서 파일 **선택을** 클릭하여 `certificate_pub.crt` 파일을 업로드합니다.

통합 **만들기를** 클릭하여 프로세스를 완료합니다.

### 액세스 값 복사

통합을 만든 후 세부 사항을 볼 수 있습니다. 클라이언트 **암호** 검색을 클릭하면 화면이 다음과 같이 표시됩니다.

![](images/authentication/access-values.png)

조직 ID `{API KEY}`인 에 대한 값을 복사하며, 다음 `{IMS ORG}` `{CLIENT SECRET}` 단계에서 사용할 수 있습니다.

## 각 세션에 대한 인증

최종 단계는 API 호출을 인증하는 데 사용할 `{ACCESS_TOKEN}` 사용자 생성 단계입니다. 액세스 토큰은 Adobe Experience Platform에 대한 모든 API 호출의 인증 헤더에 포함되어야 합니다. 액세스 토큰은 24시간 후 만료되며, 이후에는 API를 계속 사용하려면 새 토큰이 생성되어야 합니다.

### JWT 만들기

Adobe I/O 콘솔의 통합 세부 사항 페이지에서 JWT **탭으로 이동합니다** .

![](images/authentication/generate-jwt.png)

이전 섹션에서 만든 `private.key` 항목을 입력하라는 메시지가 표시됩니다. 명령줄을 열어 `private.key` 파일의 내용을 봅니다.

```shell
cat private.key
```

출력물은 다음과 같습니다.

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

전체 출력을 복사하여 텍스트 필드에 붙여 넣은 다음 JWT **생성을 클릭합니다**. 생성된 JWT를 다음 단계로 복사합니다.

![](images/authentication/generated-jwt.png)

### 액세스 토큰 생성

cURL 명령을 통해 액세스 토큰을 생성할 수 있습니다. cURL이 설치되어 있지 않은 경우 를 사용하여 설치할 수 `npm install curl`있습니다. cURL에 대한 자세한 내용은 [여기에서 확인할 수 있습니다.](https://curl.haxx.se/)

cURL이 설치되면 다음 명령에 있는 필드를 `{API_KEY}`사용자 자신의 `{CLIENT_SECRET}`및 `{JWT_TOKEN}`:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

성공하면 다음과 같은 결과가 나타납니다.

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

액세스 토큰은 `access_token` 키 아래에 있는 값입니다. 이 액세스 토큰은 `expires_in` 8639947밀리초(24시간) 그런 다음 위의 동일한 단계를 수행하여 새 액세스 토큰을 생성해야 합니다.

이제 Adobe Experience Platform에서 API 요청을 수행할 준비가 되었습니다.

### 테스트 액세스 코드

액세스 토큰이 유효한지 테스트하려면 다음 API 호출을 시도할 수 있습니다. 이 호출은 `global` 컨테이너 내의 모든 클래스를 나열합니다.

>[!NOTE]
>`{API_KEY}` 를 `{IMS_ORG}` 참조하십시오.

**요청**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


답변이 아래에 표시된 응답과 유사한 경우 응답이 `access_token` 유효하고 작동합니다. 이 응답은 공간에 대해 잘렸습니다.

**응답**

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## JWT 인증 및 API 호출에 Postman 사용

[Postman](https://www.getpostman.com/) 은 RESTful API를 사용하여 작업하는 데 널리 사용되는 도구입니다. 이 [중간 게시물은](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) JWT 인증을 자동으로 수행하고 이를 사용하여 Adobe Experience Platform API를 사용하도록 Postman을 설정하는 방법에 대해 설명합니다.