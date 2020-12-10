---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: Flow Service API를 사용하여 SFTP 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 Experience Platform을 SFTP(Secure File Transfer Protocol) 서버에 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 7b638f0516804e6a2dbae3982d6284a958230f42
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 2%

---


# API를 사용하여 SFTP 커넥터 [!DNL Flow Service] 만들기

>[!NOTE]
>
>SFTP 커넥터가 베타에 있습니다. 기능 및 설명서는 변경될 수 있습니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../../../home.md#terms-and-conditions) 참조하십시오.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 Experience Platform을 SFTP(Secure File Transfer Protocol) 서버에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 SFTP 서버에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

SFTP에 [!DNL Flow Service] 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | SFTP 서버와 연결된 이름 또는 IP 주소입니다. |
| `username` | SFTP 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | SFTP 서버의 암호입니다. |
| `privateKeyContent` | Base64로 인코딩된 SSH 개인 키 콘텐츠입니다. SSH 개인 키 OpenSSH(RSA/DSA) 형식입니다. |
| `passPhrase` | 키 파일 또는 키 콘텐트가 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 암호 구문 또는 암호입니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수를 PrivateKeyContent 암호와 함께 값으로 사용해야 합니다. |

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증:무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 다른 데이터를 가져올 수 있으므로 SFTP 계정당 하나의 연결만 필요합니다.

### 기본 인증을 사용하여 SFTP 연결 만들기

기본 인증을 사용하여 SFTP 연결을 만들려면 연결 [!DNL Flow Service]`host`, 및 `userName``password`등에 대한 값을 제공하면서 API에 POST을 요청합니다.

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
| `connectionSpec.id` | SFTP 서버 연결 사양 ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**응답**

성공적인 응답은 새로 만든 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 다음 자습서에서 SFTP 서버를 탐색하는 데 필요합니다.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### SSH 공개 키 인증을 사용하여 SFTP 연결 만들기

SSH 공개 키 인증을 사용하여 SFTP 연결을 만들려면 연결 [!DNL Flow Service]`host`, `userName`및 `privateKeyContent``passPhrase`API에 대한 값을 제공하면서 POST을 요청합니다.

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
| `auth.params.privateKeyContent` | base64로 인코딩된 SSH 개인 키 콘텐츠입니다. SSH 개인 키 OpenSSH(RSA/DSA) 형식입니다. |
| `auth.params.passPhrase` | 키 파일 또는 키 콘텐트가 암호 구문으로 보호되는 경우 개인 키를 해독하기 위한 암호 구문 또는 암호입니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수를 PrivateKeyContent 암호와 함께 값으로 사용해야 합니다. |
| `connectionSpec.id` | SFTP 서버 연결 사양 ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**응답**

성공적인 응답은 새로 만든 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 다음 자습서에서 SFTP 서버를 탐색하는 데 필요합니다.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 다음 단계

이 튜토리얼을 따라 API를 사용하여 SFTP 연결을 만들고 연결 고유 ID 값을 [!DNL Flow Service] 얻게 됩니다. 이 연결 ID를 사용하여 Flow Service API를 사용하여 클라우드 스토리지 [를](../../explore/cloud-storage.md) 탐색하거나 Flow Service API를 사용하여 [인제스트 쪽모이 세공 데이터를 생성할 수 있습니다](../../cloud-storage-parquet.md).
