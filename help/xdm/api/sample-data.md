---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;샘플 데이터;샘플 데이터;rpc;
solution: Experience Platform
title: 샘플 데이터 API 끝점
description: 스키마 레지스트리 API의 /sampledata 끝점을 사용하면 기존 XDM 스키마의 구조에 매핑된 샘플 데이터를 생성할 수 있습니다.
exl-id: 424d33ca-0624-4891-bf83-044ac2861579
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 1%

---

# 샘플 데이터 끝점

데이터를 Adobe Experience Platform에 수집하려면 데이터의 형식 및 구조가 기존 XDM(경험 데이터 모델) 스키마를 준수해야 합니다. 특정 데이터 세트에 대한 스키마의 복잡성에 따라 데이터 세트에서 수집 시 예상하는 데이터의 정확한 모양을 결정하는 것이 어려울 수 있습니다.

[!DNL Schema Registry] API에서 `/sampledata` 끝점을 사용하여 이전에 만든 스키마에 대한 예제 수집 개체를 생성할 수 있습니다.

## 시작하기

이 가이드에 사용된 끝점은 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

샘플 데이터 끝점은 [!DNL Schema Registry]에서 지원하는 RPC(원격 프로시저 호출)의 일부입니다. [!DNL Schema Registry] API의 다른 끝점과 달리 RPC 끝점에는 `Accept` 또는 `Content-Type`과(와) 같은 추가 헤더가 필요하지 않으며 `CONTAINER_ID`을(를) 사용하지 않습니다. 대신 아래 API 호출에 나와 있는 대로 `/rpc` 네임스페이스를 사용해야 합니다.

## 스키마에 대한 샘플 데이터 검색

엔드포인트에 대한 GET 요청 경로에 스키마 ID를 지정하여 스키마 라이브러리 내의 모든 스키마에 대한 샘플 데이터를 검색할 수 있습니다.

**API 형식**

```http
GET /rpc/sampledata/{SCHEMA_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 샘플 데이터를 생성할 스키마의 `meta:altId` 또는 URL로 인코딩된 `$id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 충성도 멤버 스키마에 대한 샘플 데이터를 생성합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/sampledata/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 스키마에 대한 샘플 데이터 개체를 반환합니다.

```json
{
    "@id": "/uri-reference",
    "_{TENANT_ID}": {
        "favoriteHotel": "string",
        "loyalty": {
            "loyaltyId": "string",
            "loyaltyLevel": "string",
            "loyaltyPoints": 4862,
            "memberSince": "2018-11-12T20:20:39+00:00"
        }
    },
    "repo:createDate": "2004-10-23T12:00:00-06:00",
    "repo:modifyDate": "2004-10-23T12:00:00-06:00",
    "xdm:createdByBatchID": "/uri-reference",
    "xdm:faxPhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:homeAddress": {
        "@id": "/uri-reference",
        "repo:createDate": "2004-10-23T12:00:00-06:00",
        "repo:modifyDate": "2004-10-23T12:00:00-06:00",
        "schema:description": "string",
        "schema:elevation": 31148.05,
        "schema:latitude": 29.25,
        "schema:longitude": -145.42,
        "xdm:city": "string",
        "xdm:country": "string",
        "xdm:countryCode": "US",
        "xdm:createdByBatchID": "/uri-reference",
        "xdm:dmaID": 1612,
        "xdm:label": "string",
        "xdm:lastVerifiedDate": "2018-01-12",
        "xdm:modifiedByBatchID": "/uri-reference",
        "xdm:msaID": 26375,
        "xdm:postOfficeBox": "string",
        "xdm:postalCode": "string",
        "xdm:primary": false,
        "xdm:region": "string",
        "xdm:repositoryCreatedBy": "string",
        "xdm:repositoryLastModifiedBy": "string",
        "xdm:state": "string",
        "xdm:stateProvince": "US-CA",
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:street1": "string",
        "xdm:street2": "string",
        "xdm:street3": "string",
        "xdm:street4": "string"
    },
    "xdm:homePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:identityMap": {
        "key": [
            {
                "xdm:authenticatedState": "ambiguous",
                "xdm:id": "string",
                "xdm:primary": false
            }
        ]
    },
    "xdm:mobilePhone": {
        "xdm:extension": "string",
        "xdm:number": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:validity": "consistent"
    },
    "xdm:modifiedByBatchID": "/uri-reference",
    "xdm:person": {
        "xdm:birthDate": "2018-01-12",
        "xdm:birthDayAndMonth": "01-23",
        "xdm:birthYear": 6427,
        "xdm:gender": "not_specified",
        "xdm:maritalStatus": "not_specified",
        "xdm:name": {
            "xdm:courtesyTitle": "string",
            "xdm:firstName": "string",
            "xdm:fullName": "string",
            "xdm:lastName": "string",
            "xdm:middleName": "string",
            "xdm:suffix": "string"
        },
        "xdm:nationality": "US",
        "xdm:taxId": "string"
    },
    "xdm:personalEmail": {
        "xdm:address": "john.smith@abc.com",
        "xdm:label": "string",
        "xdm:primary": false,
        "xdm:status": "active",
        "xdm:statusReason": "string",
        "xdm:type": "unknown"
    },
    "xdm:repositoryCreatedBy": "string",
    "xdm:repositoryLastModifiedBy": "string"
}
```
