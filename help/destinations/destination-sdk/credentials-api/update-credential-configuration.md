---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 기존 자격 증명 구성을 업데이트하는 데 사용되는 API 호출을 보여 줍니다.
title: 자격 증명 구성 업데이트
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 5%

---

# 자격 증명 구성 업데이트

>[!IMPORTANT]
>
>**API 끝점**: `platform.adobe.io/data/core/activation/authoring/credentials`

이 페이지에서는 `/authoring/credentials` API 끝점을 사용하여 기존 자격 증명 구성을 업데이트하는 데 사용할 수 있는 API 요청 및 페이로드를 구현합니다.

## `/credentials` API 끝점을 사용해야 하는 경우 {#when-to-use}

>[!IMPORTANT]
>
>대부분의 경우 ***API 끝점 `/credentials`을(를) 사용하지***&#x200B;할 필요가 없습니다. 대신 `/destinations` 끝점의 `customerAuthenticationConfigurations` 매개 변수를 통해 대상에 대한 인증 정보를 구성할 수 있습니다.
> 
>지원되는 인증 유형에 대한 자세한 내용은 [고객 인증 구성](../functionality/destination-configuration/customer-authentication.md)을 참조하십시오.

Adobe과 대상 플랫폼 사이에 전역 인증 시스템이 있고 [!DNL Platform] 고객이 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없는 경우에만 이 API 끝점을 사용하여 자격 증명 구성을 만드십시오. 이 경우 `/credentials` API 끝점을 사용하여 자격 증명 구성을 만들어야 합니다.

글로벌 인증 시스템을 사용하는 경우 [새 대상 구성을 만드는 경우](../authoring-api/destination-configuration/create-destination-configuration.md)에 [대상 게재](../functionality/destination-configuration/destination-delivery.md) 구성에서 `"authenticationRule":"PLATFORM_AUTHENTICATION"`을(를) 설정해야 합니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 자격 증명 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 자격 증명 구성 업데이트 {#update}

업데이트된 페이로드로 `/authoring/credentials` 끝점에 `PUT`을(를) 요청하여 [기존](create-credential-configuration.md) 자격 증명 구성을 업데이트할 수 있습니다.

기존 자격 증명 구성 및 해당 `{INSTANCE_ID}`을(를) 가져오려면 [자격 증명 구성 검색](retrieve-credential-configuration.md)에 대한 문서를 참조하십시오.

**API 형식**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 업데이트할 자격 증명 구성의 ID입니다. 기존 자격 증명 구성 및 해당 `{INSTANCE_ID}`을(를) 가져오려면 [자격 증명 구성 검색](retrieve-credential-configuration.md)을 참조하십시오. |

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

**자격 증명 구성 [!DNL Amazon S3]을(를) 업데이트합니다**

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

**자격 증명 구성 [!DNL SSH]을(를) 업데이트합니다**

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
| `sshKey` | 문자열 | [!DNL SSH] 인증을 가진 [!DNL SFTP]의 [!DNL SSH] 키 |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 업데이트된 자격 증명 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Azure 데이터 레이크 저장소]

**자격 증명 구성 [!DNL Azure Data Lake Storage]을(를) 업데이트합니다**

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
| `servicePrincipalId` | 문자열 | [!DNL Azure Data Lake Storage]에 대한 [!DNL Azure Service Principal] ID |
| `servicePrincipalKey` | 문자열 | [!DNL Azure Data Lake Storage]에 대한 [!DNL Azure Service Principal Key] |

{style="table-layout:auto"}

+++

+++응답

성공한 응답은 업데이트된 자격 증명 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

>[!TAB Azure Blob 저장소]

**자격 증명 구성 [!DNL Azure Blob]을(를) 업데이트합니다**

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

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 `/authoring/credentials` API 끝점을 사용하여 자격 증명 구성을 업데이트하는 방법을 배웁니다. [Destination SDK을 사용하여 대상을 구성하는 방법](../guides/configure-destination-instructions.md)을 읽고 대상 구성 프로세스에 이 단계가 어디에 맞는지 파악하십시오.
