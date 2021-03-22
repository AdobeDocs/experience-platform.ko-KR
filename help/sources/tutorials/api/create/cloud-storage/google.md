---
keywords: Experience Platform;홈;인기 항목;Google 클라우드 스토리지;google 클라우드 스토리지;google;home;popular topics;Google
solution: Experience Platform
title: Flow Service API를 사용하여 Google 클라우드 스토리지 소스 연결 만들기
topic: 개요
type: 튜토리얼
description: Flow Service API를 사용하여 Google Cloud 스토리지 계정에 Adobe Experience Platform을 연결하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: f6a63ca1e21b3c3f6a55574f31fdf04038b7e5c4
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 2%

---


# [!DNL Flow Service] API를 사용하여 [!DNL Google Cloud Storage] 소스 연결 만들기

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 [!DNL Experience Platform] 계정을 연결하는 단계를 안내합니다.[!DNL Google Cloud Storage]

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 Google 클라우드 스토리지 계정에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Google Cloud Storage] 계정과 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 액세스 키 ID | 플랫폼에 대한 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 61자의 영숫자 문자열입니다. |
| 비밀 액세스 키 | 플랫폼에 대한 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 40자의 기본-64로 인코딩된 문자열. |

이러한 값에 대한 자세한 내용은 [Google Cloud 저장소 HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 안내서를 참조하십시오. 자신의 액세스 키 ID 및 비밀 액세스 키를 생성하는 방법에 대한 자세한 내용은 [[!DNL Google Cloud Storage] overview](../../../../connectors/cloud-storage/google-cloud-storage.md)을 참조하십시오.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 만들기

연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 [!DNL Google Cloud Storage] 계정에는 하나의 연결만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

[!DNL Google Cloud Storage] 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. [!DNL Google Cloud Storage]에 대한 연결 사양 ID는 `32e8f412-cdf7-464c-9885-78184cb113fd`입니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage connection",
        "description": "Connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
            }
        },
        "connectionSpec": {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.accessKeyId` | [!DNL Google Cloud Storage] 계정과 연결된 액세스 키 ID입니다. |
| `auth.params.secretAccessKey` | [!DNL Google Cloud Storage] 계정과 연결된 비밀 액세스 키. |
| `connectionSpec.id` | [!DNL Google Cloud Storage] 연결 사양 ID:`32e8f412-cdf7-464c-9885-78184cb113fd` |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 다음 튜토리얼에서 클라우드 스토리지 데이터를 살펴보려면 이 ID가 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 다음 단계

이 자습서를 따라 API를 사용하여 [!DNL Google Cloud Storage] 연결을 만들고 고유한 ID를 응답 본문의 일부로 받았습니다. 이 연결 ID를 Flow Service API](../../explore/cloud-storage.md) 또는 [인제스트 Portable 데이터를 사용하여 [클라우드 스토리지 탐색에 사용할 수 있습니다. Flow Service API](../../cloud-storage-parquet.md)