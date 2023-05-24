---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 기존 자격 증명 구성을 업데이트하는 데 사용되는 API 호출을 보여 줍니다.
title: 자격 증명 구성 업데이트
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 8%

---


# 자격 증명 구성 업데이트

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/credentials`

이 페이지는 기존 자격 증명 구성을 업데이트하는 데 사용할 수 있는 API 요청 및 페이로드를 구현합니다. `/authoring/credentials` API 엔드포인트.

## 사용 시기 `/credentials` API 엔드포인트 {#when-to-use}

>[!IMPORTANT]
>
>대부분의 경우 ***금지*** 을(를) 사용해야 함 `/credentials` API 엔드포인트. 대신 를 통해 대상에 대한 인증 정보를 구성할 수 있습니다. `customerAuthenticationConfigurations` 매개 변수 `/destinations` 엔드포인트.
> 
>읽기 [고객 인증 구성](../functionality/destination-configuration/customer-authentication.md) 를 참조하십시오.

이 API 끝점을 사용하여 Adobe과 대상 플랫폼 및 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 다음을 사용하여 자격 증명 구성을 만들어야 합니다. `/credentials` API 엔드포인트.

글로벌 인증 시스템을 사용하는 경우 다음을 설정해야 합니다. `"authenticationRule":"PLATFORM_AUTHENTICATION"` 다음에서 [대상 게재](../functionality/destination-configuration/destination-delivery.md) 구성, 시기 [새 대상 구성 만들기](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 자격 증명 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 자격 증명 구성 업데이트 {#update}

다음을 업데이트할 수 있습니다. [기존](create-credential-configuration.md) 다음을 수행하여 자격 증명 구성 `PUT` 에 대한 요청 `/authoring/credentials` 업데이트된 페이로드가 있는 엔드포인트.

기존 자격 증명 구성 및 해당 자격 증명을 획득하려면 `{INSTANCE_ID}`, 다음에 대한 문서 참조: [자격 증명 구성 검색](retrieve-credential-configuration.md).

**API 형식**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 업데이트할 자격 증명 구성의 ID입니다. 기존 자격 증명 구성 및 해당 자격 증명을 획득하려면 `{INSTANCE_ID}`, 참조 [자격 증명 구성 검색](retrieve-credential-configuration.md). |

다음 요청은 페이로드에 제공된 매개 변수에 의해 정의된 기존 자격 증명 구성을 업데이트합니다.

아래에서 각 탭을 선택하여 해당 페이로드를 확인합니다.

>[!BEGINTABS]

>[!TAB 기본]

**기본 자격 증명 구성 업데이트**

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| 매개변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `url` | 문자열 | 인증 공급자의 URL |
| `username` | 문자열 | 자격 증명 구성 로그인 사용자 이름 |
| `password` | 문자열 | 자격 증명 구성 로그인 암호 |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 업데이트된 자격 증명 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Amazon S3]

**업데이트 [!DNL Amazon S3] 자격 증명 구성**

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| 매개변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `accessId` | 문자열 | [!DNL Amazon S3] 액세스 ID |
| `secretKey` | 문자열 | [!DNL Amazon S3] 비밀 키 |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 업데이트된 자격 증명 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB SSH]

**업데이트 [!DNL SSH] 자격 증명 구성**

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| 매개변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `username` | 문자열 | 자격 증명 구성 로그인 사용자 이름 |
| `sshKey` | 문자열 | [!DNL SSH] 키 [!DNL SFTP] 포함 [!DNL SSH] 인증 |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 업데이트된 자격 증명 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Azure 데이터 레이크 스토리지]

**업데이트 [!DNL Azure Data Lake Storage] 자격 증명 구성**

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| 매개변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `url` | 문자열 | 인증 공급자의 URL |
| `tenant` | 문자열 | Azure Data Lake 저장소 테넌트 |
| `servicePrincipalId` | 문자열 | [!DNL Azure Service Principal] 의 ID [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | 문자열 | [!DNL Azure Service Principal Key] for [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 업데이트된 자격 증명 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Azure Blob 저장소]

**업데이트 [!DNL Azure Blob] 자격 증명 구성**

+++요청

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| 매개변수 | 유형 | 설명 |
| -------- | ----------- | ----------- |
| `connectionString` | 문자열 | [!DNL Azure Blob Storage] 연결 문자열 |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 업데이트된 자격 증명 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!ENDTABS]

## API 오류 처리 {#error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계 {#next-steps}

이제 이 문서를 읽고 다음을 사용하여 자격 증명 구성을 업데이트하는 방법을 알게 되었습니다. `/authoring/credentials` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](../guides/configure-destination-instructions.md) 대상을 구성하는 프로세스에 이 단계가 어디에 적합한지 이해할 수 있습니다.
