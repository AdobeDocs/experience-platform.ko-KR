---
keywords: Experience Platform;홈;인기 항목;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 PostgreSQL 기본 연결 만들기
type: Tutorial
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 PostgreSQL에 연결하는 방법을 알아봅니다.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 5%

---

# [!DNL Flow Service] API를 사용하여 [!DNL PostgreSQL] 기본 연결 만들기

기본 연결은 소스와 Adobe Experience Platform 간의 인증된 연결을 나타냅니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL PostgreSQL]에 대한 기본 연결을 만드는 단계를 안내합니다.


## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL PostgreSQL]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL PostgreSQL]과(와) 연결하려면 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | [!DNL PostgreSQL] 계정과 연결된 연결 문자열입니다. [!DNL PostgreSQL] 연결 문자열 패턴은 `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL PostgreSQL]의 연결 사양 ID는 `74a1c565-4e59-48d7-9d67-7c03b8a13137`입니다. |

연결 문자열을 가져오는 방법에 대한 자세한 내용은 이 [[!DNL PostgreSQL] 문서](https://www.postgresql.org/docs/9.2/app-psql.html)를 참조하세요.

#### 연결 문자열에 SSL 암호화 사용

다음 속성을 사용하여 연결 문자열을 추가하여 [!DNL PostgreSQL] 연결 문자열에 SSL 암호화를 사용하도록 설정할 수 있습니다.

| 속성 | 설명 | 예 |
| --- | --- | --- |
| `EncryptionMethod` | [!DNL PostgreSQL] 데이터에 대해 SSL 암호화를 사용하도록 설정할 수 있습니다. | <uL><li>`EncryptionMethod=0`(사용 안 함)</li><li>`EncryptionMethod=1`(활성화됨)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | `EncryptionMethod`이(가) 적용되면 [!DNL PostgreSQL] 데이터베이스에서 보낸 인증서의 유효성을 검사합니다. | <uL><li>`ValidationServerCertificate=0`(사용 안 함)</li><li>`ValidationServerCertificate=1`(활성화됨)</li></ul> |

다음은 SSL 암호화가 추가된 [!DNL PostgreSQL] 연결 문자열의 예입니다. `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL PostgreSQL] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL PostgreSQL]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| ------------- | --------------- |
| `auth.params.connectionString` | [!DNL PostgreSQL] 계정과 연결된 연결 문자열입니다. [!DNL PostgreSQL] 연결 문자열 패턴은 `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`입니다. |
| `connectionSpec.id` | [!DNL PostgreSQL] 연결 사양 ID: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**응답**

성공한 응답은 새로 만든 기본 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 다음 자습서에서 [!DNL PostgreSQL] 데이터베이스를 탐색하는 데 필요합니다.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL PostgreSQL] 연결 기본 연결을 만들었습니다. 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다.

* [ [!DNL Flow Service] API를 사용하여 데이터 표의 구조와 내용을 살펴봅니다.](../../explore/tabular.md)
* [ [!DNL Flow Service] API를 사용하여 데이터베이스 데이터를 플랫폼으로 가져올 데이터 흐름을 만드십시오.](../../collect/database-nosql.md)
