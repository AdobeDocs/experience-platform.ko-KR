---
title: 흐름 서비스 API를 사용하여 PathFactory 기본 연결 만들기
description: 흐름 서비스 API를 사용하여 Experience Platform에 대해 PathFactory 계정을 인증하는 방법을 알아봅니다.
badge: Beta
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL PathFactory] 기본 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)를 사용하여 [!DNL PathFactory]에 대한 기본 연결을 만드는 방법을 알아보려면 이 문서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL PathFactory]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집 {#gather-credentials}

Experience Platform에서 PathFactory 계정에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 사용자 이름 | [!DNL PathFactory] 계정 사용자 이름입니다. 시스템에서 계정을 식별하는 데 필수적입니다. |
| 암호 | [!DNL PathFactory] 계정과 연결된 암호입니다. 무단 액세스를 방지하기 위해 보안을 유지해야 합니다. |
| 도메인 | [!DNL PathFactory] 계정과 연결된 도메인입니다. 일반적으로 [!DNL PathFactory] URL 내의 고유 식별자를 참조합니다. |
| 액세스 토큰 | 시스템과 [!DNL PathFactory] 간의 보안 통신을 보장하기 위해 API 인증에 사용되는 고유한 토큰입니다. |
| API 엔드포인트 | 데이터 액세스를 위한 특정 API 엔드포인트: 방문자, 세션 및 페이지 보기. 각 끝점은 검색할 수 있는 서로 다른 데이터 세트에 해당합니다. **참고:** 이는 [!DNL PathFactory]에 의해 미리 정의되며 액세스하려는 데이터에만 해당됩니다. <ul><li>**방문자 끝점**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**세션 끝점**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**페이지 보기 끝점**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

자격 증명의 보안 및 사용 방법, 액세스 토큰을 가져와서 새로 고치는 방법에 대한 자세한 내용은 [[!DNL PathFactory] 지원 센터](https://support.pathfactory.com/categories/adobe/)를 참조하십시오. 이 리소스는 자격 증명 관리와 효과적이고 안전한 API 통합에 대한 포괄적인 안내서를 제공합니다.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL PathFactory] 인증 자격 증명을 요청 본문의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL PathFactory]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.clientId` | [!DNL PathFactory] 응용 프로그램과 연결된 클라이언트 ID입니다. |
| `auth.params.clientSecret` | [!DNL PathFactory] 응용 프로그램과 연결된 클라이언트 암호입니다. |
| `connectionSpec.id` | [!DNL PathFactory] 연결 사양 ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 연결을 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL PathFactory] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 마케팅 자동화 데이터를 Experience Platform으로 가져오기 위한 데이터 흐름을 만듭니다.](../../collect/marketing-automation.md)
