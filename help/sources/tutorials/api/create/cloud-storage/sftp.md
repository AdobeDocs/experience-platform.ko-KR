---
title: 흐름 서비스 API를 사용하여 SFTP 기본 연결 만들기
description: Flow Service API를 사용하여 Adobe Experience Platform을 SFTP(Secure File Transfer Protocol) 서버에 연결하는 방법에 대해 알아봅니다.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 SFTP 기본 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL SFTP]&#x200B;(Secure File Transfer Protocol)에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

>[!IMPORTANT]
>
>[!DNL SFTP] 소스 연결을 사용하여 JSON 개체를 수집할 때 줄바꿈 또는 캐리지 리턴을 피하는 것이 좋습니다. 제한을 해결하려면 라인당 단일 JSON 개체를 사용하고 후속 파일에 여러 라인을 사용합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL SFTP] 서버에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

인증 자격 증명을 검색하는 방법에 대한 자세한 단계는 [[!DNL SFTP] 인증 안내서](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials)를 참조하십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

>[!TIP]
>
>만든 후에는 [!DNL SFTP] 기본 연결의 인증 유형을 변경할 수 없습니다. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

[!DNL SFTP] 원본은 기본 인증과 SSH 공개 키를 통한 인증을 모두 지원합니다. 이 단계에서 액세스 권한을 제공할 하위 폴더의 경로를 지정할 수도 있습니다.

기본 연결 ID를 만들려면 [!DNL SFTP] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

>[!IMPORTANT]
>
>[!DNL SFTP] 커넥터가 `ed25519`, `RSA` 또는 `DSA` 유형의 OpenSSH 키를 지원합니다. 키 파일 내용이 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`(으)로 시작되고 `"-----END [RSA/DSA] PRIVATE KEY-----"`(으)로 끝나는지 확인하십시오. 개인 키 파일이 PPK 형식 파일인 경우 PuTTY 도구를 사용하여 PPK에서 OpenSSH 형식으로 변환합니다.

**API 형식**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 기본 인증]

+++요청

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d  '{
      "name": "SFTP connector with password",
      "description": "SFTP connector password",
      "auth": {
          "specName": "Basic Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.host` | SFTP 서버의 호스트 이름입니다. |
| `auth.params.port` | SFTP 서버의 포트입니다. 이 정수 값은 기본적으로 22입니다. |
| `auth.params.username` | SFTP 서버와 연결된 사용자 이름입니다. |
| `auth.params.password` | SFTP 서버와 연결된 암호입니다. |
| `auth.params.maxConcurrentConnections` | Experience Platform을 SFTP에 연결할 때 지정된 최대 동시 연결 수입니다. 활성화된 경우 이 값을 1 이상으로 설정해야 합니다. |
| `auth.params.folderPath` | 액세스 권한을 제공할 폴더의 경로입니다. |
| `auth.params.disableChunking` | SFTP 서버가 청크를 지원하는지 여부를 확인하는 데 사용되는 부울 값입니다. |
| `connectionSpec.id` | SFTP 서버 연결 사양 ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++응답

성공한 응답은 새로 만든 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 다음 자습서에서 SFTP 서버를 탐색하는 데 필요합니다.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB SSH 공개 키 인증]

+++요청

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SFTP connector with SSH authentication",
      "description": "SFTP connector with SSH authentication",
      "auth": {
          "specName": "SSH PublicKey Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.host` | [!DNL SFTP] 서버의 호스트 이름입니다. |
| `auth.params.port` | SFTP 서버의 포트입니다. 이 정수 값은 기본적으로 22입니다. |
| `auth.params.username` | [!DNL SFTP] 서버와 연결된 사용자 이름입니다. |
| `auth.params.privateKeyContent` | Base64로 인코딩된 SSH 개인 키 콘텐츠입니다. 지원되는 OpenSSH 키 유형은 `ed25519`, `RSA` 및 `DSA`입니다. |
| `auth.params.passPhrase` | 키 파일 또는 키 콘텐츠가 암호로 보호되어 있는 경우 개인 키를 해독하기 위한 암호나 암호입니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수는 PrivateKeyContent의 암호와 함께 값으로 사용해야 합니다. |
| `auth.params.maxConcurrentConnections` | Experience Platform을 SFTP에 연결할 때 지정된 최대 동시 연결 수입니다. 활성화된 경우 이 값을 1 이상으로 설정해야 합니다. |
| `auth.params.folderPath` | 액세스 권한을 제공할 폴더의 경로입니다. |
| `auth.params.disableChunking` | SFTP 서버가 청크를 지원하는지 여부를 확인하는 데 사용되는 부울 값입니다. |
| `connectionSpec.id` | [!DNL SFTP] 서버 연결 사양 ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++응답

성공한 응답은 새로 만든 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 다음 자습서에서 SFTP 서버를 탐색하는 데 필요합니다.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL SFTP] 연결을 만들고 연결의 고유 ID 값을 얻었습니다. 이 연결 ID를 사용하여 [흐름 서비스 API를 사용하여 클라우드 저장소 탐색](../../explore/cloud-storage.md)할 수 있습니다.
