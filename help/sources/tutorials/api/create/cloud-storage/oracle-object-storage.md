---
keywords: Experience Platform;홈;인기 항목;Oracle 개체 저장소;oracle 개체 저장소
solution: Experience Platform
title: Flow Service API를 사용하여 Oracle 개체 스토리지 기본 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 Oracle 개체 저장소에 연결하는 방법을 알아봅니다.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Oracle Object Storage] 기본 연결을 만듭니다

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)를 사용하여 [!DNL Oracle Object Storage]에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Oracle Object Storage]에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이 [!DNL Oracle Object Storage]에 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUrl` | 인증에 필요한 [!DNL Oracle Object Storage] 끝점입니다. 끝점 형식은 다음과 같습니다.`https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 인증에 필요한 [!DNL Oracle Object Storage] 액세스 키 ID입니다. |
| `secretKey` | 인증에 필요한 [!DNL Oracle Object Storage] 암호입니다. |
| `bucketName` | 사용자가 액세스를 제한한 경우 필요한 허용된 버킷 이름입니다. 버킷 이름은 3자에서 63자 사이여야 하며 문자 또는 숫자로 시작하고 끝나야 하며, 소문자, 숫자 또는 하이픈(`-`)만 포함할 수 있습니다. 버킷 이름은 IP 주소처럼 지정할 수 없습니다. |
| `folderPath` | 사용자가 액세스를 제한한 경우 필요한 허용된 폴더 경로입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. [!DNL Oracle Object Storage]에 대한 연결 사양 ID는 다음과 같습니다.`c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

이러한 값을 가져오는 방법에 대한 자세한 내용은 [Oracle 개체 저장소 인증 안내서](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)를 참조하십시오.

### 플랫폼 API 사용

플랫폼 API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 요청 매개 변수의 일부로 [!DNL Oracle Object Storage] 인증 자격 증명을 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 [!DNL Oracle Object Storage]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.serviceUrl` | 인증에 필요한 [!DNL Oracle Object Storage] 끝점입니다. |
| `auth.params.accessKey` | 인증에 필요한 [!DNL Oracle Object Storage] 액세스 키 ID입니다. |
| `auth.params.secretKey` | 인증에 필요한 [!DNL Oracle Object Storage] 암호입니다. |
| `auth.params.bucketName` | 사용자가 액세스를 제한한 경우 필요한 허용된 버킷 이름입니다. |
| `auth.params.folderPath` | 사용자가 액세스를 제한한 경우 필요한 허용된 폴더 경로입니다. |
| `connectionSpec.id` | [!DNL Oracle Object Storage] 연결 사양 ID:`c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**응답**

성공적으로 응답하면 새로 만든 연결의 연결 ID가 반환됩니다. 이 ID는 다음 자습서에서 클라우드 스토리지 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 다음 단계

이 자습서에 따르면 [!DNL Flow Service] API를 사용하여 [!DNL Oracle Object Storage] 연결을 만들고 고유한 연결 ID를 얻습니다. 이 연결 ID를 사용하여 [흐름 서비스 API](../../explore/cloud-storage.md)를 사용하여 클라우드 저장소 탐색에 사용할 수 있습니다.
