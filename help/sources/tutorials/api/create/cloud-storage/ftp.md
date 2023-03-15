---
keywords: Experience Platform;홈;인기 항목; 파일 전송 프로토콜; 파일 전송 프로토콜
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 FTP 기본 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 FTP(File Transfer Protocol) 서버에 연결하는 방법을 알아봅니다.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 를 사용하여 FTP 기본 연결 만들기 [!DNL Flow Service] API

>[!NOTE]
>
>FTP 커넥터는 Beta 버전입니다. 기능 및 설명서는 변경될 수 있습니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블이 지정된 커넥터 사용에 대한 자세한 정보를 제공합니다.

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 기본 연결을 만드는 단계를 안내합니다. [!DNL FTP] (파일 전송 프로토콜) [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL FTP] 를 사용하는 서버 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 에 연결하려면 [!DNL FTP], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 와(과) 연계된 이름 또는 IP 주소 [!DNL FTP] 서버입니다. |
| `username` | 에 대한 액세스 권한이 있는 사용자 이름 [!DNL FTP] 서버입니다. |
| `password` | 에 대한 암호 [!DNL FTP] 서버입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL FTP] 은(는) `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL FTP] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```http
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL FTP]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공적인 응답은 고유 식별자()를 반환합니다.`id`)을 참조하십시오. 이 ID는 다음 자습서에서 FTP 서버를 탐색하는 데 필요합니다.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API이며, 연결의 고유 ID 값을 가져왔습니다. 이 연결 ID를 사용하여 다음을 수행할 수 있습니다. [흐름 서비스 API를 사용하여 클라우드 저장소 살펴보기](../../explore/cloud-storage.md).
