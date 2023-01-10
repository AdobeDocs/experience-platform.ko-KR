---
keywords: Experience Platform;홈;인기 항목;Oracle 개체 저장소;oracle 개체 저장소
solution: Experience Platform
title: Flow Service API를 사용하여 Oracle 개체 스토리지 기본 연결 만들기
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 Oracle 개체 저장소에 연결하는 방법을 알아봅니다.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# 만들기 [!DNL Oracle Object Storage] 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음에 대한 기본 연결을 만드는 단계를 안내합니다 [!DNL Oracle Object Storage] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Oracle Object Storage] 사용 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 에 연결 [!DNL Oracle Object Storage]를 채울 때는 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUrl` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 끝점입니다. 끝점 형식은 다음과 같습니다. `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 액세스 키 ID입니다. |
| `secretKey` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 암호입니다. |
| `bucketName` | 사용자가 액세스를 제한한 경우 필요한 허용된 버킷 이름입니다. 버킷 이름은 3자에서 63자 사이여야 하며 문자 또는 숫자로 시작하고 끝나야 하며, 소문자, 숫자 또는 하이픈만 포함할 수 있습니다(`-`). 버킷 이름은 IP 주소처럼 지정할 수 없습니다. |
| `folderPath` | 사용자가 액세스를 제한한 경우 필요한 허용된 폴더 경로입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL Oracle Object Storage] is: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

이러한 값을 가져오는 방법에 대한 자세한 내용은 [Oracle 개체 저장소 인증 안내서](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL Oracle Object Storage] 요청 매개 변수의 일부로 인증 자격 증명.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Oracle Object Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.serviceUrl` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 끝점입니다. |
| `auth.params.accessKey` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 액세스 키 ID입니다. |
| `auth.params.secretKey` | 다음 [!DNL Oracle Object Storage] 인증에 필요한 암호입니다. |
| `auth.params.bucketName` | 사용자가 액세스를 제한한 경우 필요한 허용된 버킷 이름입니다. |
| `auth.params.folderPath` | 사용자가 액세스를 제한한 경우 필요한 허용된 폴더 경로입니다. |
| `connectionSpec.id` | 다음 [!DNL Oracle Object Storage] 연결 사양 ID: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**응답**

성공적으로 응답하면 새로 만든 연결의 연결 ID가 반환됩니다. 이 ID는 다음 자습서에서 클라우드 스토리지 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Oracle Object Storage] 를 사용하여 연결 [!DNL Flow Service] API이고 고유한 연결 ID를 받았습니다. 이 연결 ID를 사용하여 다음을 수행할 수 있습니다 [흐름 서비스 API를 사용하여 클라우드 스토리지 살펴보기](../../explore/cloud-storage.md).
