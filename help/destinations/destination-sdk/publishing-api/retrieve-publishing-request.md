---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 대상 게시 요청에 대한 세부 정보를 검색하는 데 사용되는 API 호출을 예시합니다.
title: 대상 게시 요청 검색
exl-id: fceef12d-a52c-4259-a91e-7af88b132800
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 2%

---

# 대상 게시 요청 검색

>[!IMPORTANT]
>
>다른 Experience Platform 고객이 사용할 제품화된(공개) 대상을 제출하는 경우 이 API 끝점만 사용하면 됩니다. 직접 사용할 개인 대상을 만드는 경우 게시 API를 사용하여 대상을 공식적으로 제출할 필요가 없습니다.

>[!IMPORTANT]
>
>**API 끝점**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

대상을 구성하고 테스트한 후 검토 및 게시를 위해 Adobe에 제출할 수 있습니다. 대상 제출 프로세스의 일부로 수행해야 하는 다른 모든 단계에 대해 [Destination SDK에서 작성된 대상을 검토하려면 제출](../guides/submit-destination.md)을 읽으십시오.

다음과 같은 경우에 게시 요청을 제출하려면 게시 대상 API 엔드포인트를 사용합니다.

* Destination SDK 파트너는 모든 Experience Platform 고객이 사용할 수 있도록 모든 Experience Platform 조직에서 제품화된 대상을 사용할 수 있도록 하고자 합니다.
* 구성에 대해 *모든 업데이트*&#x200B;합니다. 구성 업데이트는 Experience Platform 팀에서 승인하는 새 게시 요청을 제출한 후에만 대상에 반영됩니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 게시 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 대상 게시 요청 나열 {#retrieve-list}

`/authoring/destinations/publish` 끝점에 GET 요청을 하여 IMS 조직에 게시하기 위해 제출된 모든 대상 목록을 검색할 수 있습니다.

**API 형식**

다음 API 형식을 사용하여 계정에 대한 모든 게시 요청을 검색합니다.

```http
GET /authoring/destinations/publish
```

`{DESTINATION_ID}` 매개 변수로 정의된 특정 게시 요청을 검색하려면 다음 API 형식을 사용하십시오.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**요청**

다음 두 요청은 요청에서 `DESTINATION_ID` 매개 변수를 전달하는지 여부에 따라 IMS 조직에 대한 모든 게시 요청 또는 특정 게시 요청을 검색합니다.

아래에서 각 탭을 선택하여 해당 페이로드를 확인합니다.

>[!BEGINTABS]

>[!TAB 모든 게시 요청 검색]

+++요청

다음 요청은 [!DNL IMS Org ID] 및 샌드박스 구성을 기반으로 제출한 게시 요청 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++응답

다음 응답은 사용한 IMS 조직 ID와 샌드박스 이름을 기반으로 하여 액세스 권한이 있는 게시를 위해 제출된 모든 대상 목록과 함께 HTTP 상태 200을 반환합니다. 하나의 `configId`은(는) 하나의 대상에 대한 게시 요청에 해당합니다.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `destinationId` | 문자열 | 게시를 위해 제출한 대상 구성의 대상 ID. |
| `publishDetailsList.configId` | 문자열 | 제출된 대상에 대한 대상 게시 요청의 고유 ID. |
| `publishDetailsList.allowedOrgs` | 문자열 | 대상을 사용할 수 있는 Experience Platform 조직을 반환합니다. <br> <ul><li> `"destinationType": "PUBLIC"`에 대해 이 매개 변수는 `"*"`을 반환합니다. 즉, 모든 Experience Platform 조직에서 대상을 사용할 수 있습니다.</li><li> `"destinationType": "DEV"`의 경우 이 매개 변수는 대상을 작성 및 테스트하는 데 사용한 조직의 조직 ID를 반환합니다.</li></ul> |
| `publishDetailsList.status` | 문자열 | 대상 게시 요청의 상태입니다. 가능한 값은 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`입니다. 값이 `PUBLISHED`인 대상은 라이브이며 Experience Platform 고객이 사용할 수 있습니다. |
| `publishDetailsList.destinationType` | 문자열 | 대상의 유형입니다. 값은 `DEV` 및 `PUBLIC`일 수 있습니다. `DEV`은(는) Experience Platform 조직의 대상에 해당합니다. `PUBLIC`은(는) 게시를 위해 제출한 대상에 해당합니다. Git 용어로 이 두 가지 옵션을 생각해 보십시오. 여기서 `DEV` 버전은 로컬 작성 분기를 나타내고 `PUBLIC` 버전은 원격 주 분기를 나타냅니다. |
| `publishDetailsList.publishedDate` | 문자열 | 게시를 위해 대상이 제출된 날짜(시간 기준)입니다. |

{style="table-layout:auto"}

+++

>[!TAB 특정 게시 요청 검색]

+++요청

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 게시 상태를 검색할 대상의 ID입니다. |

+++

+++응답

API 호출에서 `DESTINATION_ID`을(를) 전달한 경우 응답은 지정된 대상 게시 요청에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `destinationId` | 문자열 | 게시를 위해 제출한 대상 구성의 대상 ID. |
| `publishDetailsList.configId` | 문자열 | 제출된 대상에 대한 대상 게시 요청의 고유 ID. |
| `publishDetailsList.allowedOrgs` | 문자열 | 대상을 사용할 수 있는 Experience Platform 조직을 반환합니다. <br> <ul><li> `"destinationType": "PUBLIC"`에 대해 이 매개 변수는 `"*"`을 반환합니다. 즉, 모든 Experience Platform 조직에서 대상을 사용할 수 있습니다.</li><li> `"destinationType": "DEV"`의 경우 이 매개 변수는 대상을 작성 및 테스트하는 데 사용한 조직의 조직 ID를 반환합니다.</li></ul> |
| `publishDetailsList.status` | 문자열 | 대상 게시 요청의 상태입니다. 가능한 값은 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`입니다. 값이 `PUBLISHED`인 대상은 라이브이며 Experience Platform 고객이 사용할 수 있습니다. |
| `publishDetailsList.destinationType` | 문자열 | 대상의 유형입니다. 값은 `DEV` 및 `PUBLIC`일 수 있습니다. `DEV`은(는) Experience Platform 조직의 대상에 해당합니다. `PUBLIC`은(는) 게시를 위해 제출한 대상에 해당합니다. Git 용어로 이 두 가지 옵션을 생각해 보십시오. 여기서 `DEV` 버전은 로컬 작성 분기를 나타내고 `PUBLIC` 버전은 원격 주 분기를 나타냅니다. |
| `publishDetailsList.publishedDate` | 문자열 | 게시를 위해 대상이 제출된 날짜(시간 기준)입니다. |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API 오류 처리

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. Experience Platform 문제 해결 안내서에서 [API 상태 코드](../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.
