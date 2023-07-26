---
title: 흐름 서비스 API를 사용하여 Phoenix Base 연결 만들기
description: 흐름 서비스 API를 사용하여 Phoenix 데이터베이스를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: efffd6ce1ed541ce20ee6500e42165465f2fa6a0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 만들기 [!DNL Phoenix] 를 사용한 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만들고 연결하는 방법에 대한 단계를 제공합니다. [!DNL Phoenix] 계정을 Adobe Experience Platform에 [!DNL Flow Service] API.

## 시작하기

이 안내서를 사용하려면 다음 Experience Platform 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Phoenix] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

연결하려면 다음 인증 자격 증명을 제공해야 합니다. [!DNL Phoenix] Experience Platform 계정.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 의 IP 주소 또는 호스트 이름 [!DNL Phoenix] 서버입니다. |
| `username` | 액세스하는 데 사용하는 사용자 이름 [!DNL Phoenix] 서버. |
| `password` | 사용자에 해당하는 암호입니다. |
| `port` | 이 작동하는 TCP 포트 [!DNL Phoenix] 서버는 를 사용하여 클라이언트 연결을 수신합니다. 을(를) 연결하는 경우 [!DNL Azure HDInsights]을 클릭한 다음 포트를 443으로 지정합니다. 이 매개 변수를 제공하지 않으면 기본값은 8765입니다. |
| `httpPath` | 에 해당하는 부분 URL [!DNL Phoenix] 서버입니다. 을 사용하는 경우 /hbasephoenix0 을 지정합니다. [!DNL Azure] HDInsights 클러스터. |
| `enableSsl` | 부울 값. SSL을 사용하여 서버 연결을 암호화할지 여부를 지정합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL Phoenix] 은(는) `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

시작에 대한 자세한 내용은 다음을 참조하십시오. [이 Phoenix 문서](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결을 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Phoenix] 요청 본문의 인증 자격 증명입니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Phoenix]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Phoenix test connection",
      "description": "Phoenix test connection",
      "auth": {
          "specName": "Basic Authentication",
      "params": {
          "host":  "{HOST}",
          "username": "{USERNAME}",
          "password":"{PASSWORD}",
          "port": {PORT},
          "httpPath": "{PATH}",
          "enableSsl": {SSL}
          }
      },
      "connectionSpec": {
          "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.host` | 의 호스트 [!DNL Phoenix] 서버입니다. |
| `auth.params.username` | 와(과) 연계된 사용자 이름 [!DNL Phoenix] 연결. |
| `auth.params.password` | 과(와) 연계된 암호 [!DNL Phoenix] 연결. |
| `auth.params.port` | 에 대한 TCP 포트 [!DNL Phoenix] 연결. |
| `auth.params.httpPath` | 에 대한 부분 http 경로 [!DNL Phoenix] 연결. |
| `auth.params.enableSsl` | 서버 연결이 SSL을 사용하여 암호화되는지 여부를 지정하는 부울 값입니다. |
| `connectionSpec.id` | 다음 [!DNL Phoenix] 연결 사양 ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다(`id`). 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Phoenix] 를 사용한 기본 연결 [!DNL Flow Service] API. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [를 사용하여 데이터 테이블의 구조 및 내용 탐색 [!DNL Flow Service] API](../../explore/tabular.md)
* [다음을 사용하여 데이터베이스 데이터를 플랫폼으로 가져올 데이터 흐름을 만듭니다. [!DNL Flow Service] API](../../collect/database-nosql.md)
