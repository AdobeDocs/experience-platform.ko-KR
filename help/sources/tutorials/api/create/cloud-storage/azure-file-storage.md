---
keywords: Experience Platform;홈;인기 항목;Azure;Azure 파일 저장소;Azure 파일 저장소
solution: Experience Platform
title: Flow Service API를 사용하여 Azure 파일 저장소 기본 연결 만들기
type: Tutorial
description: Flow Service API를 사용하여 Azure 파일 저장소를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 만들기 [!DNL Azure File Storage] 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음에 대한 기본 연결을 만드는 단계를 안내합니다 [!DNL Azure File Storage] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Azure File Storage] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 연결 [!DNL Azure File Storage]를 채울 때는 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 의 끝점입니다 [!DNL Azure File Storag]액세스 중인 인스턴스입니다. |
| `userId` | 에 대한 충분한 액세스 권한이 있는 사용자 [!DNL Azure File Storage] 엔드포인트. |
| `password` | 사용자 [!DNL Azure File Storage] 인스턴스 |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL Azure File Storage] is: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

시작하는 방법에 대한 자세한 내용은 [이 Azure 파일 저장소 문서](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL Azure File Storage] 요청 매개 변수의 일부로 인증 자격 증명.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Azure File Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | 의 끝점입니다 [!DNL Azure File Storage] 액세스 중인 인스턴스.. |
| `auth.params.userId` | 에 대한 충분한 액세스 권한이 있는 사용자 [!DNL Azure File Storage] 엔드포인트. |
| `auth.params.password` | 다음 [!DNL Azure File Storage] 액세스 키. |
| `connectionSpec.id` | 다음 [!DNL Azure File Storage] 연결 사양 ID: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**응답**

성공적인 응답은 고유 식별자(`id`). 이 ID는 소스 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Azure File Storage] 를 사용하여 연결 [!DNL Flow Service] API를 사용하고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 다음 ID를 사용하여 방법을 배울 수 있습니다 [흐름 서비스 API를 사용하여 타사 클라우드 스토리지 살펴보기](../../explore/cloud-storage.md).
