---
keywords: Experience Platform;홈;인기 항목;oracle;
title: (베타) 흐름 서비스 API를 사용하여 Oracle Responsys 기본 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Oracle Responsys에 연결하는 방법에 대해 알아봅니다.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 4%

---

# (Beta) [!DNL Oracle Responsys] 를 사용한 기본 연결 [!DNL Flow Service] API

>[!NOTE]
>
>다음 [!DNL Oracle Responsys] 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블이 지정된 커넥터 사용에 대한 자세한 정보를 제공합니다.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Oracle Responsys] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): 플랫폼을 사용하면 다양한 소스에서 데이터를 수집할 수 있으며 을 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다 [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): 플랫폼은 하나를 파티션하는 가상 샌드박스를 제공합니다 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Oracle Responsys] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 연결 대상 [!DNL Oracle Responsys], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `endpoint` | 의 REST 인증 끝점 URL [!DNL Oracle Responsys] 인스턴스. |
| `clientId` | 에 대한 클라이언트 ID [!DNL Oracle Responsys] 인스턴스. |
| `clientSecret` | 의 클라이언트 암호 [!DNL Oracle Responsys] 인스턴스. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 의 연결 사양 ID 값 [!DNL Oracle Responsys] 소스는 다음과 같이 수정됩니다. `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

의 인증 자격 증명에 대한 자세한 정보 [!DNL Oracle Responsys], 다음을 참조하십시오. [[!DNL Oracle Responsys] 인증 안내서](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결을 만듭니다

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Oracle Responsys] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Oracle Responsys]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 매개변수 | 설명 |
| --- | --- |
| `name` | 의 이름 [!DNL Oracle Responsys] 기본 연결. 이 값을 사용하여 기본 연결을 조회할 수 있으므로 수사적 이름을 제공하는 것이 좋습니다. |
| `description` | (선택 사항) 기본 연결에 대한 추가 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `auth.specName` | 연결에 사용되는 인증 유형입니다. |
| `auth.params.endpoint` | 의 REST 인증 끝점 URL [!DNL Oracle Responsys] 서버입니다. |
| `auth.params.clientId` | 에 대한 클라이언트 ID [!DNL Oracle Responsys] 인스턴스. |
| `auth.params.clientSecret` | 의 클라이언트 암호 [!DNL Oracle Responsys] 인스턴스. |
| `connectionSpec.id` | 의 연결 사양 ID 값 [!DNL Oracle Responsys] 소스는 다음과 같이 수정됩니다. `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 기본 연결의 세부 정보를 반환합니다(`id`). 다음 단계에서 소스 연결을 만들려면 이 ID가 필요합니다.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Oracle Responsys] 를 사용한 기본 연결 [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [다음을 사용하여 마케팅 자동화 데이터를 플랫폼으로 가져오기 위한 데이터 흐름을 만듭니다. [!DNL Flow Service] API](../../collect/marketing-automation.md)
