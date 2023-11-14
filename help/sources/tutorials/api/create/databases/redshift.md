---
title: 흐름 서비스 API를 사용하여 Amazon Redshift 기본 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Amazon Redshift에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 5%

---

# 만들기 [!DNL Amazon Redshift] 를 사용한 기본 연결 [!DNL Flow Service] API

>[!IMPORTANT]
>
>다음 [!DNL Amazon Redshift] 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 소스 카탈로그에서 사용할 수 있습니다.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Amazon Redshift] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Amazon Redshift] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 연결 대상 [!DNL Amazon Redshift], 다음 연결 속성을 제공해야 합니다.

| **자격 증명** | **설명** |
| -------------- | --------------- |
| `server` | 와(과) 연계된 서버 [!DNL Amazon Redshift] 계정입니다. |
| `port` | 이(가) 지원하는 TCP 포트 [!DNL Amazon Redshift] 서버는 를 사용하여 클라이언트 연결을 수신합니다. |
| `username` | 와(과) 연계된 사용자 이름 [!DNL Amazon Redshift] 계정입니다. |
| `password` | 과(와) 연계된 암호 [!DNL Amazon Redshift] 계정입니다. |
| `database` | 다음 [!DNL Amazon Redshift] 액세스 중인 데이터베이스입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL Amazon Redshift] 은(는) `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

시작에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL Amazon Redshift] 문서](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결을 만듭니다

>[!NOTE]
>
>의 기본 인코딩 표준 [!DNL Redshift] 유니코드입니다. 이는 변경할 수 없습니다.

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Amazon Redshift] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Amazon Redshift]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "amazon-redshift base connection",
      "description": "base connection for amazon-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| ------------- | --------------- |
| `auth.params.server` | 사용자 [!DNL Amazon Redshift] 서버입니다. |
| `auth.params.port` | 이 작동하는 TCP 포트 [!DNL Amazon Redshift] 서버는 를 사용하여 클라이언트 연결을 수신합니다. |
| `auth.params.database` | 와 연계된 데이터베이스 [!DNL Amazon Redshift] 계정입니다. |
| `auth.params.password` | 과(와) 연계된 암호 [!DNL Amazon Redshift] 계정입니다. |
| `auth.params.username` | 와(과) 연계된 사용자 이름 [!DNL Amazon Redshift] 계정입니다. |
| `connectionSpec.id` | 다음 [!DNL Amazon Redshift] 연결 사양 ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**응답**

응답이 성공하면 고유 식별자를 포함하여 새로 만든 연결이 반환됩니다(`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Amazon Redshift] 를 사용한 기본 연결 [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [다음을 사용하여 데이터베이스 데이터를 플랫폼으로 가져올 데이터 흐름을 만듭니다. [!DNL Flow Service] API](../../collect/database-nosql.md)
