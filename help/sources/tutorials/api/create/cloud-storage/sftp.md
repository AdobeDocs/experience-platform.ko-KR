---
keywords: Experience Platform;홈;인기 항목;SFTP;SFTP;보안 파일 전송 프로토콜;보안 파일 전송 프로토콜
solution: Experience Platform
title: Flow Service API를 사용하여 SFTP 소스 연결 만들기
topic: overview
type: Tutorial
description: Flow Service API를 사용하여 SFTP(Secure File Transfer Protocol) 서버에 Adobe Experience Platform을 연결하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 0e11acc4a599d360cb3048445003f61848ad23d3
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 2%

---


# [!DNL Flow Service] API를 사용하여 SFTP 소스 연결 만들기

이 자습서에서는 [!DNL Flow Service] API를 사용하여 Experience Platform을 SFTP(Secure File Transfer Protocol) 서버에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

>[!IMPORTANT]
>
>SFTP 소스 연결을 사용하여 JSON 개체를 인제스트할 때 뉴라인 또는 캐리지 리턴이 발생하지 않는 것이 좋습니다. 제한 사항을 해결하려면 라인당 단일 JSON 개체를 사용하고 이후 파일에 대해 여러 행을 사용하십시오.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 SFTP 서버에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) SFTP에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | SFTP 서버와 연결된 이름 또는 IP 주소입니다. |
| `username` | SFTP 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | SFTP 서버의 암호입니다. |
| `privateKeyContent` | Base64 인코딩된 SSH 개인 키 콘텐츠입니다. OpenSSH 키 유형은 RSA 또는 DSA로 분류되어야 합니다. |
| `passPhrase` | 키 파일 또는 키 내용이 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 암호 구문 또는 암호입니다. PrivateKeyContent가 암호로 보호되는 경우 이 매개 변수를 PrivateKeyContent 암호와 함께 값으로 사용해야 합니다. |

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

연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 여러 데이터 흐름을 만들어 서로 다른 데이터를 가져오는 데 사용할 수 있으므로 하나의 연결만 필요합니다.

### 기본 인증을 사용하여 SFTP 연결 만들기

기본 인증을 사용하여 SFTP 연결을 만들려면 연결의 `host`, `userName` 및 `password`에 대한 값을 제공하면서 [!DNL Flow Service] API에 POST 요청을 하십시오.

**API 형식**

```http
POST /connections
```

**요청**

SFTP 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. SFTP에 대한 연결 사양 ID는 `b7bf2577-4520-42c9-bae9-cad01560f7bc`입니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "SFTP connector with password",
        "description": "SFTP connector password",
        "auth": {
            "specName": "Basic Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
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
| `auth.params.username` | SFTP 서버와 연결된 사용자 이름입니다. |
| `auth.params.password` | SFTP 서버와 연결된 암호입니다. |
| `connectionSpec.id` | SFTP 서버 연결 사양 ID:`b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**응답**

성공적인 응답은 새로 만든 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 다음 자습서에서 SFTP 서버를 탐색하는 데 필요합니다.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### SSH 공개 키 인증을 사용하여 SFTP 연결 만들기

SSH 공개 키 인증을 사용하여 SFTP 연결을 만들려면 `host`, `userName`, `privateKeyContent` 및 `passPhrase`에 대한 값을 제공하는 동안 [!DNL Flow Service] API에 POST 요청을 하십시오.

>[!IMPORTANT]
>
>SFTP 커넥터는 RSA 또는 DSA 유형 OpenSSH 키를 지원합니다. 키 파일 내용이 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`으로 시작하고 `"-----END [RSA/DSA] PRIVATE KEY-----"`로 끝나야 합니다. 개인 키 파일이 PPK 형식 파일인 경우 PuTTY 도구를 사용하여 PPK에서 OpenSSH 형식으로 변환합니다.

**API 형식**

```http
POST /connections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "SFTP connector with SSH authentication",
        "description": "SFTP connector with SSH authentication",
        "auth": {
            "specName": "SSH PublicKey Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
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
| `auth.params.username` | SFTP 서버와 연결된 사용자 이름입니다. |
| `auth.params.privateKeyContent` | Base64 인코딩된 SSH 개인 키 콘텐츠입니다. OpenSSH 키 유형은 RSA 또는 DSA로 분류되어야 합니다. |
| `auth.params.passPhrase` | 키 파일 또는 키 내용이 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 암호 구문 또는 암호입니다. PrivateKeyContent가 암호로 보호되는 경우 이 매개 변수를 PrivateKeyContent 암호와 함께 값으로 사용해야 합니다. |
| `connectionSpec.id` | SFTP 서버 연결 사양 ID:`b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**응답**

성공적인 응답은 새로 만든 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 다음 자습서에서 SFTP 서버를 탐색하는 데 필요합니다.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 SFTP 연결을 만들고 연결의 고유 ID 값을 받았습니다. 이 연결 ID를 Flow Service API](../../explore/cloud-storage.md) 또는 [인제스트 Portable 데이터를 사용하여 [클라우드 스토리지 탐색에 사용할 수 있습니다. Flow Service API](../../cloud-storage-parquet.md)
