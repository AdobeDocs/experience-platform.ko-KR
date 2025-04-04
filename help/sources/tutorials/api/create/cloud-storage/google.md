---
title: 흐름 서비스 API를 사용하여 Google Cloud Storage Base 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Google 클라우드 스토리지 계정에 연결하는 방법을 알아봅니다.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 4%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Google Cloud Storage] 기본 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Google Cloud Storage]에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 Google 클라우드 저장소 계정에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Google Cloud Storage] 계정에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `accessKeyId` | Experience Platform에 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 61자 영숫자 문자열입니다. |
| `secretAccessKey` | Experience Platform에 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 40자의 Base64로 인코딩된 문자열입니다. |
| `bucketName` | [!DNL Google Cloud Storage] 버킷의 이름입니다. 클라우드 저장소의 특정 하위 폴더에 대한 액세스 권한을 제공하려면 버킷 이름을 지정해야 합니다. |
| `folderPath` | 액세스 권한을 제공할 폴더의 경로입니다. |

이러한 값에 대한 자세한 내용은 [Google Cloud Storage HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 안내서를 참조하십시오. 자신의 액세스 키 ID와 비밀 액세스 키를 생성하는 방법에 대한 단계는 [[!DNL Google Cloud Storage] 개요](../../../../connectors/cloud-storage/google-cloud-storage.md)를 참조하세요.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Google Cloud Storage] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

>[!TIP]
>
>이 단계에서는 버킷 이름과 하위 폴더의 경로를 정의하여 계정이 액세스할 하위 폴더를 지정할 수도 있습니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 [!DNL Google Cloud Storage]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
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
| `auth.params.secretAccessKey` | [!DNL Google Cloud Storage] 계정과 연결된 비밀 액세스 키입니다. |
| `auth.params.bucketName` | [!DNL Google Cloud Storage] 버킷의 이름입니다. 클라우드 저장소의 특정 하위 폴더에 대한 액세스를 제공하려면 버킷 이름을 지정해야 합니다. |
| `auth.params.folderPath` | 액세스 권한을 제공할 폴더의 경로입니다. |
| `connectionSpec.id` | [!DNL Google Cloud Storage] 연결 사양 ID: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**응답**

응답이 성공하면 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보가 반환됩니다. 이 ID는 다음 자습서에서 클라우드 스토리지 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 다음 단계

이 자습서에 따라 API를 사용하여 [!DNL Google Cloud Storage] 연결을 만들었고 고유 ID를 응답 본문의 일부로 가져왔습니다. 이 연결 ID를 사용하여 [흐름 서비스 API를 사용하여 클라우드 저장소 탐색](../../explore/cloud-storage.md)할 수 있습니다.
