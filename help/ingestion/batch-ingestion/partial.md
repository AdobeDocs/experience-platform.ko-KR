---
keywords: Experience Platform;홈;인기 항목;일괄 처리 수집;일괄 처리 수집;부분 수집;부분 수집;오류 검색;오류 검색;부분 일괄 처리 수집;부분 일괄 처리 수집;부분;수집;수집;수집;
solution: Experience Platform
title: 부분 일괄 처리 수집 개요
description: 이 문서에서는 부분 일괄 처리 수집 관리에 대한 자습서를 제공합니다.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: bc72f77b1b4a48126be9b49c5c663ff11e9054ea
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 9%

---

# 부분 일괄 처리 수집

부분 일괄 처리 수집은 특정 임계값까지 오류가 포함된 데이터를 수집하는 기능입니다. 이 기능을 사용하면 잘못된 데이터가 있는 이유와 함께, 모든 잘못된 데이터가 따로 일괄 처리되는 동안 모든 올바른 데이터를 Adobe Experience Platform에 성공적으로 수집할 수 있습니다.

이 문서에서는 부분 일괄 처리 수집 관리에 대한 자습서를 제공합니다.

## 시작

이 자습서에서는 부분 일괄 처리 수집과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [일괄 처리 수집](./overview.md): [!DNL Experience Platform]에서 CSV 및 Parquet와 같은 데이터 파일에서 데이터를 수집하고 저장하는 메서드입니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

다음 섹션에서는 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 문서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Experience Platform] API를 호출하려면 먼저 [인증 튜토리얼](https://www.adobe.com/go/platform-api-authentication-en)을 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Experience Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

## API에서 부분 일괄 처리 수집에 대한 일괄 처리 활성화 {#enable-api}

>[!NOTE]
>
>이 섹션에서는 API를 사용하여 부분 일괄 처리 수집에 대한 일괄 처리를 활성화하는 방법에 대해 설명합니다. UI 사용에 대한 지침은 [UI에서 부분 일괄 처리 수집에 대한 일괄 처리 활성화](#enable-ui) 단계를 참조하십시오.

부분 수집이 활성화된 새 배치를 생성할 수 있습니다.

새 일괄 처리를 만들려면 [일괄 처리 수집 개발자 안내서](./api-overview.md)의 단계를 따릅니다. **[!UICONTROL Create batch]** 단계에 도달하면 다음 필드를 요청 본문에 추가합니다.

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `enableErrorDiagnostics` | [!DNL Experience Platform]에서 일괄 처리에 대한 자세한 오류 메시지를 생성할 수 있는 플래그입니다. |
| `partialIngestionPercent` | 전체 일괄 처리 전에 허용되는 오류의 백분율입니다. 따라서 이 예에서 최대 5%의 배치가 오류일 수 있지만 실패하게 됩니다. |


## UI에서 부분 일괄 처리 수집에 대한 일괄 처리 활성화 {#enable-ui}

>[!NOTE]
>
>이 섹션에서는 UI를 사용하여 부분 일괄 처리 수집에 대한 일괄 처리를 활성화하는 방법에 대해 설명합니다. API를 사용하여 부분 일괄 처리 수집에 대한 일괄 처리를 이미 활성화한 경우 다음 섹션으로 건너뛸 수 있습니다.

[!DNL Experience Platform] UI를 통해 부분 수집을 위한 일괄 처리를 활성화하려면 소스 연결을 통해 새 일괄 처리를 만들거나 기존 데이터 세트에서 새 일괄 처리를 만들거나 &quot;[!UICONTROL Map CSV to XDM flow]&quot;을(를) 통해 새 일괄 처리를 만들 수 있습니다.

### 새 소스 연결 만들기 {#new-source}

새 원본 연결을 만들려면 [원본 개요](../../sources/home.md)에 나열된 단계를 따릅니다. **[!UICONTROL Dataflow detail]** 단계에 도달하면 **[!UICONTROL Partial ingestion]** 및 **[!UICONTROL Error diagnostics]** 필드를 메모해 두십시오.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

**[!UICONTROL Partial ingestion]** 토글을 사용하면 부분 일괄 처리 수집의 사용을 활성화하거나 비활성화할 수 있습니다.

**[!UICONTROL Error diagnostics]** 전환은 **[!UICONTROL Partial ingestion]** 전환이 꺼진 경우에만 나타납니다. 이 기능을 사용하면 [!DNL Experience Platform]에서 수집된 일괄 처리에 대한 자세한 오류 메시지를 생성할 수 있습니다. **[!UICONTROL Partial ingestion]** 토글이 켜져 있으면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;을(를) 사용하면 전체 일괄 처리가 실패하기 전에 허용되는 오류의 백분율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

### 기존 데이터 세트 사용 {#existing-dataset}

기존 데이터 세트를 사용하려면 데이터 세트를 선택하여 시작합니다. 오른쪽의 사이드바는 데이터 세트에 대한 정보로 채워집니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

**[!UICONTROL Partial ingestion]** 토글을 사용하면 부분 일괄 처리 수집의 사용을 활성화하거나 비활성화할 수 있습니다.

**[!UICONTROL Error diagnostics]** 전환은 **[!UICONTROL Partial ingestion]** 전환이 꺼진 경우에만 나타납니다. 이 기능을 사용하면 [!DNL Experience Platform]에서 수집된 일괄 처리에 대한 자세한 오류 메시지를 생성할 수 있습니다. **[!UICONTROL Partial ingestion]** 토글이 켜져 있으면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;을(를) 사용하면 전체 일괄 처리가 실패하기 전에 허용되는 오류의 백분율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

이제 **데이터 추가** 단추를 사용하여 데이터를 업로드할 수 있으며 부분 수집을 사용하여 수집됩니다.

### &quot;[!UICONTROL Map CSV to XDM schema]&quot; 흐름 사용 {#map-flow}

&quot;[!UICONTROL Map CSV to XDM schema]&quot; 흐름을 사용하려면 [CSV 파일 매핑 자습서](../tutorials/map-csv/overview.md)의 나열된 단계를 따르십시오. **[!UICONTROL Add data]** 단계에 도달하면 **[!UICONTROL Partial ingestion]** 및 **[!UICONTROL Error diagnostics]** 필드를 메모해 두십시오.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

**[!UICONTROL Partial ingestion]** 토글을 사용하면 부분 일괄 처리 수집의 사용을 활성화하거나 비활성화할 수 있습니다.

**[!UICONTROL Error diagnostics]** 전환은 **[!UICONTROL Partial ingestion]** 전환이 꺼진 경우에만 나타납니다. 이 기능을 사용하면 [!DNL Experience Platform]에서 수집된 일괄 처리에 대한 자세한 오류 메시지를 생성할 수 있습니다. **[!UICONTROL Partial ingestion]** 토글이 켜져 있으면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;을(를) 사용하면 전체 일괄 처리가 실패하기 전에 허용되는 오류의 백분율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

## 기존 데이터 흐름에 대한 부분 수집 및 오류 진단 활성화

부분 수집 또는 오류 진단을 활성화하지 않고 Experience Platform의 데이터 흐름이 생성된 경우 흐름을 다시 생성하지 않고 이러한 기능을 활성화할 수 있습니다. 부분 수집 및 강력한 오류 진단을 활성화하여 데이터 수집 워크플로우의 안정성과 문제 해결 편의성을 크게 향상시킬 수 있습니다. [!DNL Flow Service] API를 사용하여 기존 데이터 흐름에 대한 부분 수집 및 오류 진단을 활성화하는 방법에 대해 알아보려면 아래 섹션을 읽어 보십시오.

기본적으로 데이터 흐름에는 부분 수집 또는 오류 진단이 활성화되어 있지 않을 수 있습니다. 이러한 기능은 데이터 수집 중 문제를 식별하고 격리하는 데 유용합니다. [!DNL Flow Service] API를 사용하면 현재 데이터 흐름 구성을 검색하고 PATCH 요청을 사용하여 필요한 변경 내용을 적용할 수 있습니다.

기존 데이터 흐름에 대해 부분 수집 및 오류 진단을 활성화하려면 아래 단계를 따르십시오.

### 플로우 세부 정보 검색

데이터 흐름 구성을 검색하려면 `/flows/{FLOW_ID}` 끝점에 GET 요청을 만들고 데이터 흐름의 ID를 제공하십시오. 데이터 흐름 세부 정보 검색에 대한 자세한 내용은 [API를 사용하여 데이터 흐름 업데이트 [!DNL Flow Service]  안내서를 참조하십시오.](../../sources/tutorials/api/update-dataflows.md)

응답에서 반환된 `etag` 필드의 값을 저장하십시오. 버전 일관성을 유지하기 위해 업데이트 요청에 필요합니다.

### 흐름 구성 업데이트

그런 다음 `/flows/` 끝점에 PATCH 요청을 수행하고 부분 수집 및 오류 진단을 활성화할 데이터 흐름의 ID를 제공합니다.

>[!IMPORTANT]
>
>- If-Match 키를 사용하여 이전에 저장한 `etag` 값을 요청 헤더에 포함합니다.
>- 특정 요구 사항에 맞게 `partialIngestionPercent` 값을 수정할 수 있습니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
        {
            "op": "add",
            "path": "/options",
            "value": {
                "partialIngestionPercent": "10"
            }
        },
        {
            "op": "add",
            "path": "/options/errorDiagnosticsEnabled",
            "value": true
        }
    ]'
```

**응답**

응답이 성공하면 데이터 흐름의 `id`과(와) 업데이트된 `etag`이(가) 반환됩니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

### 업데이트 확인

PATCH이 완료되면 GET 요청을 만들고 데이터 흐름을 검색하여 변경 사항이 성공적으로 완료되었는지 확인합니다.

**API 형식**

```http
GET /flows/{FLOW_ID}
```

**요청**

다음 요청은 플로우 ID에 대한 업데이트된 정보를 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답이 데이터 흐름 세부 정보를 반환하여 이제 `options` 섹션에서 부분 수집 및 오류 진단이 활성화되었는지 확인합니다.

```json
"options": {
    "partialIngestionPercent": 10,
    "errorDiagnosticsEnabled": true
}
```

## 다음 단계 {#next-steps}

이 튜토리얼에서는 부분 일괄 처리 수집을 활성화하기 위해 데이터 세트를 만들거나 수정하는 방법을 다룹니다. 일괄 처리 수집에 대한 자세한 내용은 [일괄 처리 수집 개발자 안내서](./api-overview.md)를 참조하십시오.

부분 수집 오류 모니터링에 대한 자세한 내용은 [일괄 처리 수집 오류 진단 안내서](../quality/error-diagnostics.md)를 참조하십시오.
