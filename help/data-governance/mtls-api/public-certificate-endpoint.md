---
title: 공개 인증서 끝점
description: MTLS 서비스 API의 /public-certificate 종단점을 사용하여 공개 인증서를 검색하는 방법을 알아봅니다.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---

# 공개 인증서 끝점

>[!NOTE]
>
>Adobe은 더 이상 공개 mTLS 인증서의 정적 다운로드를 지원하지 않습니다. 이 API를 사용하여 통합에 대한 유효한 인증서를 검색합니다. 이제 서비스 중단을 방지하기 위해 자동 검색이 필요합니다.

이 안내서에서는 공개 인증서 끝점을 사용하여 조직의 Adobe 애플리케이션에 대한 공개 인증서를 안전하게 검색하는 방법을 설명합니다. 여기에는 개발자가 데이터 교환을 인증하고 확인하는 데 도움이 되는 샘플 API 호출 및 세부 지침이 포함되어 있습니다.

## 시작하기

계속하기 전에 [시작 안내서](./getting-started.md)에서 필수 헤더와 예제 API 호출을 해석하는 방법에 대한 중요한 세부 정보를 검토하십시오.

## API 경로 {#paths}

다음 정보는 mTLS 서비스 API를 사용하는 데 필요한 필수 API 경로입니다. 여기에는 플랫폼 게이트웨이 URL, API의 기본 경로 및 공개 인증서를 검색하기 위한 전체 경로의 예가 포함됩니다.

- 플랫폼 게이트웨이 URL: `https://platform.adobe.io/`
- 이 API의 기본 경로: `/data/core/mtls`
- 전체 경로의 예: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## 공개 인증서 검색 {#list}

조직의 Adobe 응용 프로그램에 대한 공개 인증서를 검색하도록 `/v1/certificate/public-certificate` 끝점에 GET 요청을 만듭니다.

**API 형식**

```http
GET /v1/certificate/public-certificate
```

공개 인증서를 검색할 때 다음의 선택적 쿼리 매개 변수를 사용할 수 있습니다.

| 쿼리 매개변수 | 설명 | 예 |
| --------------- | ----------- | ------- |
| `page` | 요청 결과가 시작될 페이지를 지정합니다. | `page=5` |
| `limit` | 페이지당 검색할 최대 공개 인증서 수입니다. | `limit=20` |

{style="table-layout:auto"}

**요청**

조직과 연결된 공개 인증서를 반환하는 샘플 요청은 아래의 축소 가능 섹션에 표시됩니다.

+++샘플 요청

```shell
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**응답**

성공적인 응답은 HTTP 상태 200을 반환하고 조직에 대한 공개 인증서를 나열합니다.

+++샘플 성공 응답

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| 속성 | 설명 |
| --- | --- |
| `certCommonName` | 인증서의 일반 이름(CN)이며, 일반적으로 인증서를 발급하는 서버나 엔티티의 이름 또는 ID를 나타냅니다. |
| `publicCertificate` | 통신을 인증하고 암호화하는 데 사용되는 문자열 형식의 실제 공개 인증서입니다. |
| `expiryDate` | 공개 인증서가 만료되는 날짜 및 시간으로 ISO 8601(UTC) 형식으로 지정됩니다. |

{style="table-layout:auto"}

+++

## 인증서 라이프사이클 자동화 {#certificate-lifecycle-automation}

Adobe은 공개 mTLS 인증서의 라이프사이클을 자동화하여 연속성을 보장하고 서비스 중단을 줄입니다.

- 인증서는 만료 60일 전에 재발급됩니다.
- 인증서는 만료 30일 전에 해지됩니다.

>[!NOTE]
>
>이러한 타임라인은 인증서 수명을 최대 47일로 줄이는 것을 목표로 하는 [CA/B 포럼 지침](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days)에 맞춰 시간이 지남에 따라 단축됩니다.

API를 통해 자동 검색을 지원하려면 통합을 업데이트해야 합니다. 수동 인증서 다운로드나 정적 복사본을 사용하면 인증서가 만료되거나 해지될 수 있으므로 사용하지 마십시오.

## 다음 단계

API를 사용하여 공개 인증서를 검색한 후 인증서가 만료되기 전에 통합을 업데이트하여 이 끝점을 정기적으로 호출합니다. 이 호출을 대화식으로 테스트하려면 [MTLS API 참조 페이지](https://developer.adobe.com/experience-platform-apis/references/mtls-service/)를 방문하세요. 인증서 기반 통합에 대한 자세한 지침은 [Adobe Experience Platform의 데이터 암호화 개요](../../landing/governance-privacy-security/encryption.md) 또는 [데이터 거버넌스 개요](../home.md)를 참조하십시오.
