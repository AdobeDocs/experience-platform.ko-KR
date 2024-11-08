---
title: 흐름 서비스 API를 사용하여 Phoenix Base 연결 만들기
description: 흐름 서비스 API를 사용하여 Phoenix 데이터베이스를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Phoenix] 기본 연결 만들기

>[!WARNING]
>
>[!DNL Phoenix] 원본은 2025년 5월 말에 사용되지 않습니다.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만들고 [!DNL Flow Service] API를 사용하여 [!DNL Phoenix] 계정을 Adobe Experience Platform에 연결하는 방법에 대한 단계를 제공합니다.

## 시작하기

이 안내서를 사용하려면 다음 Experience Platform 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Phoenix]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Phoenix] 계정을 Experience Platform에 연결하려면 다음 인증 자격 증명을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | [!DNL Phoenix] 서버의 IP 주소 또는 호스트 이름입니다. |
| `username` | [!DNL Phoenix] 서버에 액세스하는 데 사용하는 사용자 이름입니다. |
| `password` | 사용자에 해당하는 암호입니다. |
| `port` | [!DNL Phoenix] 서버가 클라이언트 연결을 수신 대기하는 데 사용하는 TCP 포트입니다. [!DNL Azure HDInsights]에 연결하는 경우 포트를 443으로 지정하십시오. 이 매개 변수를 제공하지 않으면 기본값은 8765입니다. |
| `httpPath` | [!DNL Phoenix] 서버에 해당하는 부분 URL. [!DNL Azure] HDInsights 클러스터를 사용하는 경우 /hbasephoenix0을 지정하십시오. |
| `enableSsl` | 부울 값. SSL을 사용하여 서버 연결을 암호화할지 여부를 지정합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Phoenix]의 연결 사양 ID는 `102706fb-a5cd-42ee-afe0-bc42f017ff43`입니다. |

시작에 대한 자세한 내용은 [이 Phoenix 문서](https://python-phoenixdb.readthedocs.io/en/latest/api.html)를 참조하세요.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결을 만들려면 요청 본문에 [!DNL Phoenix] 인증 자격 증명을 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Phoenix]에 대한 기본 연결을 만듭니다.

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
| `auth.params.host` | [!DNL Phoenix] 서버의 호스트입니다. |
| `auth.params.username` | [!DNL Phoenix] 연결과 연결된 사용자 이름입니다. |
| `auth.params.password` | [!DNL Phoenix] 연결과 연결된 암호입니다. |
| `auth.params.port` | [!DNL Phoenix] 연결에 대한 TCP 포트입니다. |
| `auth.params.httpPath` | [!DNL Phoenix] 연결에 대한 부분 http 경로입니다. |
| `auth.params.enableSsl` | 서버 연결이 SSL을 사용하여 암호화되는지 여부를 지정하는 부울 값입니다. |
| `connectionSpec.id` | [!DNL Phoenix] 연결 사양 ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**응답**

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보가 반환됩니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Phoenix] 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 플랫폼으로 가져올 데이터 흐름을 만드십시오.](../../collect/database-nosql.md)
