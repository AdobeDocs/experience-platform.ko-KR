---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 자격 증명 구성을 검색하는 데 사용되는 API 호출을 보여 줍니다.
title: 자격 증명 구성 검색
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 자격 증명 구성 검색

>[!IMPORTANT]
>
>**API 끝점**: `platform.adobe.io/data/core/activation/authoring/credentials`

이 페이지에서는 `/authoring/credentials` API 끝점을 사용하여 자격 증명 구성을 검색하는 데 사용할 수 있는 API 요청 및 페이로드를 구현합니다.

## `/credentials` API 끝점을 사용해야 하는 경우 {#when-to-use}

>[!IMPORTANT]
>
>대부분의 경우 ***API 끝점 `/credentials`을(를) 사용하지***&#x200B;할 필요가 없습니다. 대신 `/destinations` 끝점의 `customerAuthenticationConfigurations` 매개 변수를 통해 대상에 대한 인증 정보를 구성할 수 있습니다.
> 
>지원되는 인증 유형에 대한 자세한 내용은 [고객 인증 구성](../functionality/destination-configuration/customer-authentication.md)을 참조하십시오.

Adobe과 대상 플랫폼 사이에 글로벌 인증 시스템이 있고 [!DNL Experience Platform] 고객이 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없는 경우에만 이 API 끝점을 사용하여 자격 증명 구성을 만드십시오. 이 경우 `/credentials` API 끝점을 사용하여 자격 증명 구성을 만들어야 합니다.

글로벌 인증 시스템을 사용하는 경우 [새 대상 구성을 만드는 경우](../authoring-api/destination-configuration/create-destination-configuration.md)에 [대상 게재](../functionality/destination-configuration/destination-delivery.md) 구성에서 `"authenticationRule":"PLATFORM_AUTHENTICATION"`을(를) 설정해야 합니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 자격 증명 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 자격 증명 구성 검색 {#retrieve}

`/authoring/credentials` 끝점에 대해 `GET` 요청을 수행하여 [기존](create-credential-configuration.md) 자격 증명 구성을 검색할 수 있습니다.

**API 형식**

다음 API 형식을 사용하여 계정에 대한 모든 자격 증명 구성을 검색합니다.

```http
GET /authoring/credentials
```

`{INSTANCE_ID}` 매개 변수로 정의된 특정 자격 증명 구성을 검색하려면 다음 API 형식을 사용하십시오.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

다음 두 요청은 요청에서 `INSTANCE_ID` 매개 변수를 전달하는지 여부에 따라 IMS 조직의 모든 자격 증명 구성 또는 특정 자격 증명 구성을 검색합니다.

아래에서 각 탭을 선택하여 해당 페이로드를 확인합니다.

>[!BEGINTABS]

>[!TAB 모든 자격 증명 구성 검색]

+++요청

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++응답

성공한 응답은 사용한 [!DNL IMS Org ID] 및 샌드박스 이름을 기반으로 액세스 권한이 있는 자격 증명 구성 목록과 함께 HTTP 상태 200을 반환합니다. 하나의 `instanceId`이(가) 하나의 자격 증명 구성에 해당합니다.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB 특정 자격 증명 구성 검색]

+++요청

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 검색할 자격 증명 구성의 ID입니다. |

+++

+++응답

성공적인 응답은 요청에 제공된 `instanceId`에 해당하는 자격 증명 구성의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## API 오류 처리 {#error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. Experience Platform 문제 해결 안내서에서 [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계 {#next-steps}

이제 이 문서를 읽고 `/authoring/credentials` API 끝점을 사용하여 자격 증명 구성에 대한 세부 정보를 검색하는 방법을 알게 되었습니다. [Destination SDK을 사용하여 대상을 구성하는 방법](../guides/configure-destination-instructions.md)을 읽어 대상을 구성하는 프로세스에 이 단계가 어디에 맞는지 이해합니다.
