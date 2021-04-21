---
keywords: Experience Platform;홈;인기 항목;Oracle 개체 저장소;oracle 개체 저장소
solution: Experience Platform
title: Flow Service API를 사용하여 Oracle 개체 저장소 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 Oracle 개체 스토리지에 연결하는 방법을 알아봅니다.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Oracle Object Storage] 소스 연결 만들기

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)를 사용하여 Adobe Experience Platform을 [!DNL Oracle Object Storage]에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Oracle Object Storage]에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Oracle Object Storage]에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUrl` | 인증에 필요한 [!DNL Oracle Object Storage] 끝점입니다. 끝점 형식은 다음과 같습니다.`https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 인증에 필요한 [!DNL Oracle Object Storage] 액세스 키 ID입니다. |
| `secretKey` | 인증에 필요한 [!DNL Oracle Object Storage] 암호입니다. |
| `bucketName` | 사용자가 액세스를 제한한 경우 허용되는 버킷 이름이 필요합니다. 버킷 이름은 3자에서 63자 사이여야 하며 문자 또는 숫자로 시작하고 끝나야 하며 소문자, 숫자 또는 하이픈(`-`)만 포함할 수 있습니다. 버킷 이름은 IP 주소처럼 형식을 지정할 수 없습니다. |
| `folderPath` | 사용자가 제한된 액세스 권한을 가진 경우 허용되는 폴더 경로입니다. |

이러한 값을 얻는 방법에 대한 자세한 내용은 [Oracle 개체 저장소 인증 안내서](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials)를 참조하십시오.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 호출 예](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 만들기

연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 [!DNL Oracle Object Storage] 계정에는 하나의 연결만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

[!DNL Oracle Object Storage] 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. [!DNL Oracle Object Storage]에 대한 연결 사양 ID는 `c85f9425-fb21-426c-ad0b-405e9bd8a46c`입니다.

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
| `auth.params.bucketName` | 사용자가 액세스를 제한한 경우 허용되는 버킷 이름이 필요합니다. |
| `auth.params.folderPath` | 사용자가 제한된 액세스 권한을 가진 경우 허용되는 폴더 경로입니다. |
| `connectionSpec.id` | [!DNL Oracle Object Storage] 연결 사양 ID:`c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**응답**

성공적으로 응답하면 새로 만든 연결의 연결 ID가 반환됩니다. 다음 튜토리얼에서 클라우드 스토리지 데이터를 살펴보려면 이 ID가 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 [!DNL Oracle Object Storage] 연결을 만들고 고유한 연결 ID를 얻었습니다. 이 연결 ID를 Flow Service API](../../explore/cloud-storage.md)를 사용하여 [클라우드 저장소 탐색에 사용할 수 있습니다.
