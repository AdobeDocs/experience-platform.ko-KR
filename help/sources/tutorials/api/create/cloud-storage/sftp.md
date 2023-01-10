---
keywords: Experience Platform;홈;인기 항목;SFTP;sftp;보안 파일 전송 프로토콜;보안 파일 전송 프로토콜
solution: Experience Platform
title: Flow Service API를 사용하여 SFTP 기본 연결 만들기
type: Tutorial
description: Flow Service API를 사용하여 SFTP(Secure File Transfer Protocol) 서버에 Adobe Experience Platform을 연결하는 방법을 알아봅니다.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---

# 를 사용하여 SFTP 기본 연결 만들기 [!DNL Flow Service] API

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 다음에 대한 기본 연결을 만드는 단계를 안내합니다 [!DNL SFTP] (Secure File Transfer Protocol) [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

>[!IMPORTANT]
>
>를 사용하여 JSON 개체를 수집할 때 줄바꿈 또는 캐리지 리턴 발생을 방지하는 것이 좋습니다 [!DNL SFTP] 소스 연결. 제한 사항을 해결하려면 행당 단일 JSON 개체를 사용하고 후속 파일에 여러 줄을 사용합니다.

다음 섹션에서는 다음에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL SFTP] 서버를 사용하여 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

대상 [!DNL Flow Service] 에 연결 [!DNL SFTP]를 채울 때는 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 와 연결된 이름 또는 IP 주소 [!DNL SFTP] server. |
| `port` | 연결하는 SFTP 서버 포트입니다. 지정하지 않으면 기본값은 입니다 `22`. |
| `username` | 사용자 이름에 액세스할 수 있는 사용자 이름 [!DNL SFTP] server. |
| `password` | 사용자 [!DNL SFTP] server. |
| `privateKeyContent` | Base64로 인코딩된 SSH 개인 키 콘텐츠입니다. OpenSSH 키 유형은 RSA 또는 DSA로 분류해야 합니다. |
| `passPhrase` | 키 파일 또는 키 컨텐츠가 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 암호 구문 또는 암호입니다. 만약 `privateKeyContent` 암호로 보호되어 있는 경우, 이 매개 변수는 개인 키 컨텐츠의 암호를 값으로 사용하여 사용해야 합니다. |
| `maxConcurrentConnections` | 이 매개 변수를 사용하면 SFTP 서버에 연결할 때 플랫폼에서 만드는 동시 연결 수에 대한 최대 제한을 지정할 수 있습니다. 이 값은 SFTP에서 설정한 제한보다 작도록 설정해야 합니다. **참고**: 이 설정이 기존 SFTP 계정에 대해 활성화되면 기존 데이터 흐름에는 영향을 주지 않고 향후 데이터 흐름에만 영향을 줍니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. 에 대한 연결 사양 ID [!DNL SFTP] is: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

다음 [!DNL SFTP] 소스는 SSH 공개 키를 통해 기본 인증 및 인증을 모두 지원합니다.

기본 연결 ID를 만들려면 `/connections` 제공하는 동안 엔드포인트 [!DNL SFTP] 요청 매개 변수의 일부로 인증 자격 증명.

>[!IMPORTANT]
>
>다음 [!DNL SFTP] 커넥터는 RSA 또는 DSA 유형인 OpenSSH 키를 지원합니다. 주요 파일 내용이 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 다음으로 끝남 `"-----END [RSA/DSA] PRIVATE KEY-----"`. 개인 키 파일이 PPK 형식 파일인 경우 PuTTY 도구를 사용하여 PPK에서 OpenSSH 형식으로 변환합니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL SFTP]:

>[!BEGINTABS]

>[!TAB 기본 인증]

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
              "maxConcurrentConnections": 1
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
| `auth.params.port` | SFTP 서버의 포트입니다. 이 정수 값은 기본적으로 22로 설정됩니다. |
| `auth.params.username` | SFTP 서버와 연결된 사용자 이름입니다. |
| `auth.params.password` | SFTP 서버와 연결된 암호입니다. |
| `auth.params.maxConcurrentConnections` | Platform을 SFTP에 연결할 때 지정된 최대 동시 연결 수입니다. 활성화되면 이 값을 최소 1로 설정해야 합니다. |
| `connectionSpec.id` | SFTP 서버 연결 사양 ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!TAB SSH 공개 키 인증]

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
              "maxConcurrentConnections": 1

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
| `auth.params.host` | 의 호스트 이름 [!DNL SFTP] server. |
| `auth.params.port` | SFTP 서버의 포트입니다. 이 정수 값은 기본적으로 22로 설정됩니다. |
| `auth.params.username` | 사용자 이름과 연결된 사용자 이름 [!DNL SFTP] server. |
| `auth.params.privateKeyContent` | Base64로 인코딩된 SSH 개인 키 콘텐츠입니다. OpenSSH 키 유형은 RSA 또는 DSA로 분류해야 합니다. |
| `auth.params.passPhrase` | 키 파일 또는 키 컨텐츠가 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 암호 구문 또는 암호입니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수는 PrivateKeyContent의 암호와 함께 값으로 사용해야 합니다. |
| `auth.params.maxConcurrentConnections` | Platform을 SFTP에 연결할 때 지정된 최대 동시 연결 수입니다. 활성화되면 이 값을 최소 1로 설정해야 합니다. |
| `connectionSpec.id` | 다음 [!DNL SFTP] 서버 연결 사양 ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!ENDTABS]

**응답**

성공적인 응답은 고유 식별자(`id`) 내의 아무 곳에나 삽입할 수 있습니다. 이 ID는 다음 자습서에서 SFTP 서버를 탐색하는 데 필요합니다.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 다음 단계

이 자습서에 따라 다음을 만들었습니다 [!DNL SFTP] 를 사용하여 연결 [!DNL Flow Service] API이고, 연결의 고유 ID 값을 받았습니다. 이 연결 ID를 사용하여 다음을 수행할 수 있습니다 [흐름 서비스 API를 사용하여 클라우드 스토리지 살펴보기](../../explore/cloud-storage.md).
