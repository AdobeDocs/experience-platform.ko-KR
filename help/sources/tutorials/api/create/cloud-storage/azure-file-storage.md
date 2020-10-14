---
keywords: Experience Platform;home;popular topics;Azure;Azure File Storage;Azure file storage
solution: Experience Platform
title: Flow Service API를 사용하여 Azure 파일 저장소 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 Azure 파일 저장소를 Experience Platform에 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: d332226541685108b58d88096146ed6048606774
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---


# API를 사용하여 [!DNL Azure File Storage] 커넥터 [!DNL Flow Service] 만들기

>[!NOTE]
>
>커넥터의 [!DNL Azure File Storage] 베타입니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../../../home.md#terms-and-conditions) 참조하십시오.

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 연결 단계 [!DNL Azure File Storage] 를 안내합니다 [!DNL Experience Platform].

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 API를 [!DNL Azure File Storage] 사용하기 위해 연결하기 위해 알아야 할 추가 정보를 [!DNL Flow Service] 제공합니다.

### 필요한 자격 증명 수집

연결 [!DNL Flow Service] 을 [!DNL Azure File Storage]하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 액세스하는 [!DNL Azure File Storag]e 인스턴스의 끝점입니다. |
| `userId` | 종단점에 액세스할 수 있는 [!DNL Azure File Storage] 사용자입니다. |
| `password` | 인스턴스의 [!DNL Azure File Storage] 암호 |
| 연결 사양 ID | 연결을 만드는 데 필요한 고유 식별자입니다. 에 대한 연결 사양 ID [!DNL Azure File Storage] 는 다음과 같습니다. `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

시작하는 방법에 대한 자세한 내용은 [이 Azure 파일 저장소 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증:무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 다른 데이터를 가져올 수 있으므로 Azure 파일 저장소 계정당 하나의 연결만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 페이로드에 제공된 속성으로 구성된 새 [!DNL Azure File Storage] 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| --------- | ----------- |
| `auth.params.host` | 액세스하는 인스턴스의 [!DNL Azure File Storage] 끝점입니다. |
| `auth.params.userId` | 종단점에 액세스할 수 있는 [!DNL Azure File Storage] 사용자입니다. |
| `auth.params.password` | 액세스 [!DNL Azure File Storage] 키 |
| `connectionSpec.id` | 연결 [!DNL Azure File Storage] 사양 ID: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 다음 단계

이 튜토리얼을 따라 API를 사용하여 [!DNL Azure File Storage] 연결을 만들고 연결 [!DNL Flow Service] 의 고유 ID 값을 얻게 되었습니다. 다음 자습서에서는 Flow Service API를 사용하여 타사 클라우드 스토리지를 [탐색하는 방법을 학습하면서 이 ID를 사용할 수 있습니다](../../explore/cloud-storage.md).
