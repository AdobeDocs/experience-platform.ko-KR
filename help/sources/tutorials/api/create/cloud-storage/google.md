---
title: 흐름 서비스 API를 사용하여 Google Cloud Storage Base 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Google 클라우드 스토리지 계정에 연결하는 방법을 알아봅니다.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 만들기 [!DNL Google Cloud Storage] 를 사용한 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL Google Cloud Storage] 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 를 사용하여 Google 클라우드 스토리지 계정에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 을(를) 사용하여 [!DNL Google Cloud Storage] 계정, 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `accessKeyId` | 인증을 위해 사용되는 61자의 영숫자 문자열 [!DNL Google Cloud Storage] 계정을 플랫폼에 추가합니다. |
| `secretAccessKey` | 인증을 위해 사용되는 40자의 base64로 인코딩된 문자열 [!DNL Google Cloud Storage] 계정을 플랫폼에 추가합니다. |
| `bucketName` | 의 이름 [!DNL Google Cloud Storage] 버킷. 클라우드 저장소의 특정 하위 폴더에 대한 액세스 권한을 제공하려면 버킷 이름을 지정해야 합니다. |
| `folderPath` | 액세스 권한을 제공할 폴더의 경로입니다. |

이러한 값에 대한 자세한 내용은 [Google 클라우드 스토리지 HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 가이드. 자신의 액세스 키 ID 및 비밀 액세스 키를 생성하는 방법에 대한 단계는 [[!DNL Google Cloud Storage] 개요](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Google Cloud Storage] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

>[!TIP]
>
>이 단계에서는 버킷 이름과 하위 폴더의 경로를 정의하여 계정이 액세스할 하위 폴더를 지정할 수도 있습니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Google Cloud Storage]:

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
| `auth.params.accessKeyId` | 와 연결된 액세스 키 ID [!DNL Google Cloud Storage] 계정입니다. |
| `auth.params.secretAccessKey` | 와(과) 연결된 비밀 액세스 키 [!DNL Google Cloud Storage] 계정입니다. |
| `auth.params.bucketName` | 의 이름 [!DNL Google Cloud Storage] 버킷. 클라우드 저장소의 특정 하위 폴더에 대한 액세스를 제공하려면 버킷 이름을 지정해야 합니다. |
| `auth.params.folderPath` | 액세스 권한을 제공할 폴더의 경로입니다. |
| `connectionSpec.id` | 다음 [!DNL Google Cloud Storage] 연결 사양 ID: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 연결의 세부 정보를 반환합니다(`id`). 이 ID는 다음 자습서에서 클라우드 스토리지 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Google Cloud Storage] api 및 고유 ID를 사용한 연결은 응답 본문의 일부로 가져왔습니다. 이 연결 ID를 사용하여 다음을 수행할 수 있습니다. [흐름 서비스 API를 사용하여 클라우드 저장소 살펴보기](../../explore/cloud-storage.md).
