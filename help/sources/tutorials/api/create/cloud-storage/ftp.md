---
keywords: Experience Platform;홈;인기 있는 주제 파일 전송 프로토콜 파일 전송 프로토콜
solution: Experience Platform
title: Flow Service API를 사용하여 FTP 기본 연결 만들기
topic-legacy: overview
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 FTP(File Transfer Protocol) 서버에 연결하는 방법을 알아봅니다.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 FTP 기본 연결 만들기

>[!NOTE]
>
>FTP 커넥터는 베타에 있습니다. 기능 및 설명서는 변경될 수 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 를 참조하십시오.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL FTP](파일 전송 프로토콜)에 대한 기본 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md):  [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):  [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL FTP] 서버에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이 [!DNL FTP]에 연결하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | [!DNL FTP] 서버와 연결된 이름 또는 IP 주소입니다. |
| `username` | [!DNL FTP] 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | [!DNL FTP] 서버의 암호입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. [!DNL FTP]에 대한 연결 사양 ID는 다음과 같습니다. `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### 플랫폼 API 사용

플랫폼 API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 현재 연결 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간의 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 요청 매개 변수의 일부로 [!DNL FTP] 인증 자격 증명을 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은 [!DNL FTP]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.host` | FTP 서버의 호스트 이름입니다. |
| `auth.params.username` | FTP 서버와 연결된 사용자 이름입니다. |
| `auth.params.password` | FTP 서버와 연결된 암호입니다. |
| `connectionSpec.id` | FTP 서버 연결 사양 ID: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**응답**

성공적으로 응답하면 새로 만든 연결의 고유 식별자(`id`)가 반환됩니다. 이 ID는 다음 자습서에서 FTP 서버를 탐색하는 데 필요합니다.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 FTP 연결을 만들고 연결의 고유 ID 값을 받았습니다. 이 연결 ID를 사용하여 [Flow Service API](../../explore/cloud-storage.md) 또는 [Flow Service API](../../cloud-storage-parquet.md)를 사용하여 Parquet 데이터를 수집하여 클라우드 저장소를 탐색할 수 있습니다.
