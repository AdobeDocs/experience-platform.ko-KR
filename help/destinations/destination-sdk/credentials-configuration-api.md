---
description: 이 페이지에서는 '/authoring/credentials' API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 설명합니다.
title: 자격 증명 끝점 API 작업
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 4%

---

# 자격 증명 끝점 API 작업 {#credentials}

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/credentials`

이 페이지에서는 를 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/credentials` API 엔드포인트.

이 종단점에서 지원하는 기능에 대한 설명은 다음을 참조하십시오.

* [스트리밍 대상 구성](destination-configuration.md) 는 스트리밍 대상에 대해 구성할 수 있는 기능입니다.
* [파일 기반 대상 구성](file-based-destination-configuration.md) 에서는 파일 기반 대상에 대해 구성할 수 있습니다.

## 를 사용해야 하는 경우 `/credentials` API 엔드포인트 {#when-to-use}

>[!IMPORTANT]
>
>대부분의 경우 *포함하지 않음* 를 사용해야 함 `/credentials` API 엔드포인트. 대신 를 통해 대상에 대한 인증 정보를 구성할 수 있습니다 `customerAuthenticationConfigurations` 의 매개 변수 `/destinations` 엔드포인트. 읽기 [인증 구성](./authentication-configuration.md#when-to-use) 추가 정보.

이 API 엔드포인트를 사용하고 을 선택합니다. `PLATFORM_AUTHENTICATION` 에서 [대상 구성](./destination-configuration.md#destination-delivery) Adobe과 대상 및 대상 사이에 글로벌 인증 시스템이 있는 경우 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 `/credentials` API 엔드포인트.

## 자격 증명 구성 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](./getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 자격 증명 구성 만들기 {#create}

에 POST 요청을 수행하여 새 자격 증명 구성을 만들 수 있습니다 `/authoring/credentials` 엔드포인트.

**API 형식**

```http
POST /authoring/credentials
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 자격 증명 구성을 만듭니다. 아래 페이로드에는 `/authoring/credentials` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| 매개 변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `username` | 문자열 | 자격 증명 구성 로그인 사용자 이름 |
| `password` | 문자열 | 자격 증명 구성 로그인 암호 |
| `url` | 문자열 | 인증 공급자의 URL |
| `clientId` | 문자열 | 클라이언트/응용 프로그램 자격 증명의 클라이언트 ID |
| `clientSecret` | 문자열 | 클라이언트/응용 프로그램 자격 증명의 클라이언트 암호 |
| `accessToken` | 문자열 | 인증 공급자가 제공한 액세스 토큰 |
| `expiration` | 문자열 | 액세스 토큰에 대한 유지 시간 |
| `refreshToken` | 문자열 | 인증 공급자가 제공한 토큰 새로 고침 |
| `header` | 문자열 | 인증에 필요한 모든 헤더 |
| `accessId` | 문자열 | Amazon S3 액세스 ID |
| `secretKey` | 문자열 | Amazon S3 비밀 키 |
| `sshKey` | 문자열 | SSH 인증이 있는 SFTP용 SSH 키 |
| `tenant` | 문자열 | Azure Data Lake 저장소 테넌트 |
| `servicePrincipalId` | 문자열 | Azure Data Lake 저장소에 대한 Azure 서비스 주체 ID |
| `servicePrincipalKey` | 문자열 | Azure Data Lake 저장소에 대한 Azure 서비스 주요 키 |
| `connectionString` | 문자열 | Azure Blob 저장소 연결 문자열 |

{style="table-layout:auto"}

**응답**

성공한 응답은 새로 만든 자격 증명 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

## 자격 증명 구성 나열 {#retrieve-list}

에 GET 요청을 수행하여 조직에 대한 모든 자격 증명 구성 목록을 검색할 수 있습니다 `/authoring/credentials` 엔드포인트.

**API 형식**


```http
GET /authoring/credentials
```

**요청**

다음 요청은 조직 및 샌드박스 구성에 따라 액세스 권한이 있는 자격 증명 구성 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

다음 응답은 사용한 조직 ID 및 샌드박스 이름을 기반으로 액세스 권한이 있는 자격 증명 구성 목록과 함께 HTTP 상태 200을 반환합니다. 1개 `instanceId` 은 하나의 자격 증명 구성에 대한 템플릿에 해당합니다. 간결성을 위해 응답이 잘립니다.

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## 기존 자격 증명 구성 업데이트 {#update}

에 PUT 요청을 수행하여 기존 자격 증명 구성을 업데이트할 수 있습니다 `/authoring/credentials` 업데이트하려는 자격 증명 구성의 인스턴스 ID를 제공하는 끝점입니다. 호출 본문에서 업데이트된 자격 증명 구성을 제공합니다.

**API 형식**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 업데이트할 자격 증명 구성의 ID입니다. |

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 기존 자격 증명 구성을 업데이트합니다.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## 특정 자격 증명 구성 검색 {#get}

에 GET 요청을 수행하여 특정 자격 증명 구성에 대한 세부 정보를 검색할 수 있습니다 `/authoring/credentials` 업데이트하려는 자격 증명 구성의 인스턴스 ID를 제공하는 끝점입니다.

**API 형식**

```http
GET /authoring/credentials/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 검색할 자격 증명 구성의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 자격 증명 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## 특정 자격 증명 구성 삭제 {#delete}

에 DELETE 요청을 수행하여 지정된 자격 증명 구성을 삭제할 수 있습니다 `/authoring/credentials` 요청 경로에서 삭제할 자격 증명 구성의 ID를 제공하고 끝점입니다.

**API 형식**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 다음 `id` 삭제할 자격 증명 구성 중에서 선택합니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 빈 HTTP 응답과 함께 HTTP 상태 200을 반환합니다.

## API 오류 처리

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계

이제 이 문서를 읽은 후에는 자격 증명 끝점을 사용할 시점과 을 사용하여 자격 증명 구성을 설정하는 방법을 알 수 있습니다 `/authoring/credentials` API 엔드포인트 또는 `/authoring/destinations` 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](./configure-destination-instructions.md) 대상 구성 프로세스에 이 단계가 어떤 영향을 주는지 이해하기 위해 노력합니다.
