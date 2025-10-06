---
title: 외부 대상 만들기 및 활성화
type: Tutorial
description: Experience Platform API를 사용하여 Adobe Experience Platform에서 외부 대상을 만드는 방법을 알아봅니다.
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 3%

---


# API를 사용하여 외부 대상 만들기 및 활성화

이 튜토리얼에서는 Adobe Experience Platform API를 사용하여 외부 대상자를 만드는 데 필요한 단계를 안내합니다.

## 시작

이 자습서에서는 외부 대상을 만드는 데 관련된 다양한 Experience Platform 서비스에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 읽어 보십시오.

- [소스](../../sources/home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): 외부 데이터에서 대상을 만들 수 있습니다.
- [대상](../../destinations/home.md): 대상은 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 등을 위해 Experience Platform의 데이터를 원활하게 활성화할 수 있도록 일반적으로 사용되는 애플리케이션과의 사전 빌드된 통합입니다.

### 필수 헤더

또한 이 자습서에서는 [개의 API를 성공적으로 호출하려면 &#x200B;](https://www.adobe.com/go/platform-api-authentication-en)인증 자습서[!DNL Experience Platform]를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Experience Platform] API에 대한 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

## 외부 대상 준비 {#prepare}

Experience Platform 내에서 외부 대상을 만들려면 먼저 대상 데이터가 포함된 파일을 준비해야 합니다.

이 예제에서는 CSV 파일을 사용해야 합니다. CSV 파일에 ECID, 전자 메일 ID 또는 CRM ID와 같은 ID 값이 있는 열이 **최소**&#x200B;개 포함되어 있는지 확인하십시오. 또한 세분화 및 활성화에 필요한 모든 데이터 보강 속성을 포함해야 합니다.

또한 파일이 Experience Platform 스키마의 요구 사항을 준수하는지 확인해야 합니다. 스키마 만들기에 대한 자세한 내용은 API를 사용하여 스키마를 만드는 방법에 대한 [자습서](/help/xdm/tutorials/create-schema-api.md) 또는 UI를 사용하여 스키마를 만드는 방법에 대한 [자습서](/help/xdm/tutorials/create-schema-ui.md)를 참조하십시오.

CSV 파일에 필요한 모든 정보가 포함되어 있고 스키마를 준수하는지 확인한 후에는 소스를 사용하여 데이터를 Experience Platform에 수집할 수 있도록 CSV 파일을 클라우드 스토리지 공급자에게 업로드해야 합니다. 클라우드 저장소 원본 사용에 대한 자세한 내용은 [API를 사용한 클라우드 저장소 옵션 탐색에 대한 자습서](/help/sources/tutorials/api/explore/cloud-storage.md) 또는 [원본 개요](/help/sources/home.md#cloud-storage)를 참조하십시오.

## 외부 대상 만들기 {#create}

CSV 파일을 준비한 후 이제 외부 대상을 만드는 프로세스를 시작할 수 있습니다.

`/external-audience/` 끝점에 대한 POST 요청을 수행하여 외부 대상을 만들 수 있습니다.

이 요청을 수행할 때 다음 정보를 지정해야 합니다.

- 대상자의 이름
- 대상자에 대한 설명
- CSV와 스키마 사이의 해당 필드
- 소스 사양 정보
   - 여기에는 수집할 CSV 파일의 파일 경로가 포함됩니다
      - 파일 경로 **에는 공백을 포함할 수 없습니다**. 예를 들어 경로가 `activation/sample-source/Example CSV File.csv`이면 경로를 `activation/sample-source/ExampleCSVFile.csv`(으)로 설정합니다.

이 끝점을 사용하는 방법에 대한 자세한 내용은 [외부 대상 끝점 안내서](/help/segmentation/api/external-audiences.md#create-audience)를 참조하십시오.

+++요청

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

이 요청을 만든 후에는 대상 ID를 검색할 수 있도록 응답에서 받은 `operationId`을(를) 메모해야 합니다.

## 대상자 ID 검색 {#retrieve-audience-id}

이제 외부 대상을 만들었으므로 대상을 Experience Platform에 수집할 수 있도록 대상 ID를 가져와야 합니다.

`/external-audiences/operations` 끝점에 대한 GET 요청을 만들고 외부 대상 만들기 응답에서 이전에 받은 작업의 ID를 제공하여 대상 ID를 검색할 수 있습니다.

이 끝점을 사용하는 방법에 대한 자세한 내용은 [외부 대상 끝점 안내서](/help/segmentation/api/external-audiences.md#retrieve-status)를 참조하십시오.

+++ 요청

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

이 요청을 수행한 후 대상자에 대한 수집 작업을 트리거할 수 있도록 응답에서 받은 `audienceId`을(를) 메모해 두십시오.

## 대상자 수집 시작 {#start-ingestion}

`audienceId`이(가) 있으므로 이제 외부 대상을 Experience Platform으로 수집하도록 트리거할 수 있습니다.

대상 ID를 제공하는 동안 다음 엔드포인트에 POST 요청을 하여 대상 수집을 시작할 수 있습니다. 또한 처리할 파일을 결정할 시작 시간을 지정해야 합니다.

이 끝점을 사용하는 방법에 대한 자세한 내용은 [외부 대상 끝점 안내서](/help/segmentation/api/external-audiences.md#start-audience-ingestion)를 참조하십시오.

+++ 요청

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

이 요청을 수행한 후 수집 상태를 모니터링할 수 있도록 응답에서 받은 `runId`을(를) 메모해 두십시오.

## 수집 상태 모니터링 {#monitor-ingestion}

대상자 수집을 트리거한 후 이제 수집 진행 상황을 모니터링하여 수집의 성공을 확인하고 다운스트림 활성화에 대한 대상자의 가용성을 확인할 수 있습니다.

대상과 실행 ID를 모두 제공하면서 다음 끝점에 GET 요청을 하여 대상 수집 상태를 검색할 수 있습니다.

이 끝점을 사용하는 방법에 대한 자세한 내용은 [외부 대상 끝점 안내서](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status)를 참조하십시오.

+++ 요청

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## 다음 단계 {#next-steps}

>[!IMPORTANT]
>
>외부에서 생성된 대상자를 사용하려면 매일 세분화 작업이 완료될 때까지 **기다려야**&#x200B;합니다.

외부 대상이 성공적으로 수집되었는지 확인했으면 Audience Portal에서 이를 보고 대상과 같은 다운스트림 서비스에서 사용할 수 있습니다.

Audience Portal에 대한 자세한 내용은 [Audience Portal UI 안내서](/help/segmentation/ui/audience-portal.md)를 참조하십시오. 대상에 대한 자세한 내용은 [대상 개요](/help/destinations/home.md)를 참조하세요.

