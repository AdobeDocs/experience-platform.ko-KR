---
title: 흐름 서비스 API를 사용하여 Amazon Kinesis Source 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Amazon Kinesis 소스에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 3%

---

# 흐름 서비스 API를 사용하여 [!DNL Amazon Kinesis] 소스 연결 만들기

>[!IMPORTANT]
>
>[!DNL Amazon Kinesis] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Amazon Kinesis]&#x200B;(이하 &quot;[!DNL Kinesis]&quot;)을(를) Experience Platform에 연결하는 단계를 안내합니다.

## 시작

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Kinesis]을(를) Experience Platform에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Amazon Kinesis] 계정에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `accessKeyId` | 액세스 키 ID는 Experience Platform에 대한 [!DNL Kinesis] 계정을 인증하는 데 사용되는 액세스 키 쌍의 절반입니다. |
| `secretKey` | 비밀 액세스 키는 Experience Platform에 대한 [!DNL Kinesis] 계정을 인증하는 데 사용되는 액세스 키 쌍의 나머지 절반입니다. |
| `region` | [!DNL Kinesis] 계정의 지역입니다. 지역에 대한 자세한 내용은 [허용 목록에 IP 주소 추가](../../../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Kinesis] 연결 사양 ID: `86043421-563b-46ec-8e6c-e23184711bf6`. |

[!DNL Kinesis] 액세스 키 및 생성 방법에 대한 자세한 내용은 이 [[!DNL AWS] IAM 사용자에 대한 액세스 키 관리 가이드](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)를 참조하십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

원본 연결을 만드는 첫 번째 단계는 [!DNL Kinesis] 원본을 인증하고 기본 연결 ID를 생성하는 것입니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Kinesis] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.accessKeyId` | [!DNL Kinesis] 계정의 액세스 키 ID입니다. |
| `auth.params.secretKey` | [!DNL Kinesis] 계정의 비밀 액세스 키입니다. |
| `auth.params.region` | [!DNL Kinesis] 계정의 지역입니다. |
| `connectionSpec.id` | [!DNL Kinesis] 연결 사양 ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 다음 단계에서 소스 연결을 만들려면 이 ID가 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 소스 연결 만들기 {#source}

소스 연결은 데이터가 수집되는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 소스, 데이터 형식 및 데이터 흐름을 만드는 데 필요한 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 조직에만 해당됩니다.

소스 연결을 만들려면 [!DNL Flow Service] API의 `/sourceConnections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```http
POST /sourceConnections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 포함하도록 제공할 수 있는 선택적 값입니다. |
| `baseConnectionId` | 이전 단계에서 생성된 [!DNL Kinesis] 소스의 기본 연결 ID입니다. |
| `connectionSpec.id` | [!DNL Kinesis]에 대한 고정 연결 사양 ID입니다. 이 ID: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | 수집할 [!DNL Kinesis] 데이터의 형식입니다. 현재 지원되는 데이터 형식은 `json`뿐입니다. |
| `params.stream` | 레코드를 가져올 데이터 스트림의 이름입니다. |
| `params.dataType` | 이 매개 변수는 수집되는 데이터의 유형을 정의합니다. 지원되는 데이터 형식은 `raw` 및 `xdm`입니다. |
| `params.reset` | 이 매개 변수는 데이터를 읽는 방법을 정의합니다. `latest`을(를) 사용하여 가장 최근 데이터에서 읽기를 시작하고 `earliest`을(를) 사용하여 스트림에서 사용 가능한 첫 번째 데이터에서 읽기를 시작합니다. |

**응답**

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 데이터 흐름을 만들려면 다음 자습서에서 이 ID가 필요합니다.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>스트리밍 데이터 흐름을 만들거나 업데이트한 후 데이터 손실 또는 데이터 감소의 잠재적 인스턴스를 방지하기 위해 데이터 수집에서 5분 정도의 짧은 일시 중지가 필요합니다.

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Kinesis] 소스 연결을 만들었습니다. 다음 자습서에서 이 원본 연결 ID를 사용하여 [API를 사용하여 스트리밍 데이터 흐름을 만들 [!DNL Flow Service] 수 있습니다](../../collect/streaming.md).
