---
title: Flow Service API를 사용하여 Azure Blob Base 연결 만들기
description: Flow Service API를 사용하여 Adobe Experience Platform을 Azure Blob에 연결하는 방법을 알아봅니다.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---

# 만들기 [!DNL Azure Blob] 기본 연결 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음에 대한 기본 연결을 만드는 단계를 안내합니다 [!DNL Azure Blob] (이하 &quot;라 한다)[!DNL Blob]&quot;) [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 를 성공적으로 만들기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Blob] 소스 연결 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 와 연결 [!DNL Blob] 저장 영역에서는 다음 연결 속성 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | 인증에 필요한 인증 정보가 들어 있는 문자열입니다 [!DNL Blob] Experience Platform에 연결할 수도 있습니다. 다음 [!DNL Blob] 연결 문자열 패턴은 다음과 같습니다. `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 연결 문자열에 대한 자세한 내용은 다음을 참조하십시오 [!DNL Blob] 문서 [연결 문자열 구성](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | 다른 인증 유형으로 사용하여 연결할 수 있는 공유 액세스 서명 URI [!DNL Blob] 계정이 필요합니다. 다음 [!DNL Blob] SAS URI 패턴: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 자세한 내용은 다음을 참조하십시오 [!DNL Blob] 문서 [공유 액세스 서명 URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | 액세스를 지정할 컨테이너의 이름입니다. 을 사용하여 새 계정을 만들 때 [!DNL Blob] 소스, 사용자가 선택한 하위 폴더에 대한 사용자 액세스를 지정하는 컨테이너 이름을 제공할 수 있습니다. |
| `folderPath` | 액세스를 제공할 폴더의 경로입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL Blob] is: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

다음 [!DNL Blob] 원본은 연결 문자열 및 SAS(공유 액세스 서명) 인증을 모두 지원합니다. SAS(공유 액세스 서명) URI를 사용하면 사용자에게 안전한 위임된 권한 부여가 허용됩니다 [!DNL Blob] 계정이 필요합니다. SAS 기반 인증을 사용하면 권한, 시작 및 만료 날짜 및 특정 리소스에 대한 규정을 설정할 수 있으므로 다양한 액세스 수준을 갖는 인증 자격 증명을 만들 수 있습니다.

이 단계에서는 컨테이너 이름과 하위 폴더의 경로를 정의하여 계정이 액세스할 하위 폴더를 지정할 수도 있습니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL Blob] 요청 매개 변수의 일부로 인증 자격 증명.

**API 형식**

```http
POST /connections
```

**요청**

>[!BEGINTABS]

>[!TAB 연결 문자열]

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Blob] 연결 문자열 기반 인증 사용:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob connection using connectionString",
      "description": "Azure Blob connection using connectionString",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
              "container": "acme-blob-container",
              "folderPath": "/acme/customers/salesData"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.connectionString` | Blob 저장소의 데이터에 액세스하는 데 필요한 연결 문자열입니다. Blob 연결 문자열 패턴은 다음과 같습니다. `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Blob 저장소 연결 사양 ID는 다음과 같습니다. `4c10e202-c428-4796-9208-5f1f5732b1cf` |

>[!TAB SAS URI 인증]

을(를) 만들려면 [!DNL Blob] 공유 액세스 서명 URI를 사용하여 blob 연결, POST 요청 만들기 [!DNL Flow Service] 에 대한 값을 제공하는 동안 API [!DNL Blob] `sasUri`.

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Blob] 공유 액세스 서명 URI 사용:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob source connection using SAS URI",
      "description": "Azure Blob source connection using SAS URI",
      "auth": {
          "specName": "SAS URI Authentication",
          "params": {
              "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
              "container": "acme-blob-container",
              "folderPath": "/acme/customers/salesData"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.connectionString` | SAS URI를 사용하여 [!DNL Blob] 저장. 다음 [!DNL Blob] SAS URI 패턴: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | 다음 [!DNL Blob] 스토리지 연결 사양 ID: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

>[!ENDTABS]

**응답**

성공적인 응답은 고유 식별자(`id`). 이 ID는 소스 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL Blob] api 및 고유 ID를 사용하여 연결을 응답 본문의 일부로 획득했습니다. 이 연결 ID를 사용하여 다음을 수행할 수 있습니다 [흐름 서비스 API를 사용하여 클라우드 스토리지 살펴보기](../../explore/cloud-storage.md).
