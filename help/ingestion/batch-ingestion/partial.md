---
keywords: Experience Platform;home;popular topics;batch ingestion;batch ingestion;partial ingestion;Retrieve error;부분 일괄 처리 통합;부분 일괄 처리 통합;일부분;통합;통합;통합
solution: Experience Platform
title: 부분 일괄 처리 통합 개요
topic-legacy: overview
description: 이 문서에서는 부분 일괄 처리를 관리하는 자습서를 제공합니다.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# 부분 일괄 처리

부분 일괄 처리란 오류가 포함된 데이터를 특정 임계값까지 인제스트하는 기능입니다. 이 기능을 사용하면 모든 정확한 데이터를 Adobe Experience Platform으로 성공적으로 인제스트할 수 있으며 모든 잘못된 데이터가 잘못된 이유에 대한 세부 정보와 함께 별도로 일괄적으로 묶을 수 있습니다.

이 문서에서는 부분 일괄 처리를 관리하는 자습서를 제공합니다.

## 시작하기

이 자습서에서는 부분 일괄 처리에 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [일괄 처리](./overview.md):CSV 및  [!DNL Platform] Portable과 같은 데이터 파일의 데이터를 인제스트하고 저장하는 방법입니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크

다음 섹션에서는 [!DNL Platform] API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:Bearer `{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

## API {#enable-api}에서 부분 일괄 처리를 활성화합니다.

>[!NOTE]
>
>이 섹션에서는 API를 사용하여 부분 일괄 처리를 위한 일괄 처리를 활성화하는 방법에 대해 설명합니다. UI 사용에 대한 지침은 UI](#enable-ui) 단계에서 부분 일괄 처리를 위한 일괄 처리 활성화를 참조하십시오.[

부분 처리가 활성화된 새 배치를 만들 수 있습니다.

새 배치를 만들려면 [일괄 처리 통합 개발자 안내서](./api-overview.md)의 단계를 따릅니다. **[!UICONTROL Create batch]** 단계에 도달하면 요청 본문 내에 다음 필드를 추가합니다.

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `enableErrorDiagnostics` | [!DNL Platform]이(가) 일괄 처리에 대한 자세한 오류 메시지를 생성할 수 있도록 하는 플래그. |
| `partialIngestionPercentage` | 전체 배치가 실패하기 전에 허용되는 오류 비율. 따라서 이 예에서는 일괄 처리가 실패하기 전에 최대 5%의 일괄 처리가 오류일 수 있습니다. |


## UI {#enable-ui}에서 부분 일괄 처리를 활성화합니다.

>[!NOTE]
>
>이 섹션에서는 UI를 사용하여 부분 일괄 처리를 활성화하는 방법에 대해 설명합니다. API를 사용하여 부분 일괄 처리를 이미 활성화한 경우 다음 섹션으로 건너뛸 수 있습니다.

[!DNL Platform] UI를 통해 부분 소집에 대한 일괄 처리를 활성화하려면 소스 연결을 통해 새 일괄 처리를 만들거나 기존 데이터 세트에 새 일괄 처리를 만들거나 &quot;[!UICONTROL Map CSV to XDM flow]&quot;을(를) 통해 새 일괄 처리를 만들 수 있습니다.

### 새 소스 연결 {#new-source} 만들기

새 소스 연결을 만들려면 [소스 개요](../../sources/home.md)에 나열된 단계를 수행합니다. **[!UICONTROL Dataflow detail]** 단계에 도달하면 **[!UICONTROL Partial ingestion]** 및 **[!UICONTROL Error diagnostics]** 필드를 기록해 두십시오.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

**[!UICONTROL Partial ingestion]** 토글을 사용하면 부분 일괄 처리 통합 사용을 활성화 또는 비활성화할 수 있습니다.

**[!UICONTROL Error diagnostics]** 토글은 **[!UICONTROL Partial ingestion]** 토글이 꺼져 있을 때만 표시됩니다. 이 기능을 사용하면 [!DNL Platform]에서 인제스트된 배치에 대한 자세한 오류 메시지를 생성할 수 있습니다. **[!UICONTROL Partial ingestion]** 토글이 켜져 있으면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;을 사용하면 전체 배치가 실패하기 전에 허용되는 오류 백분율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

### 기존 데이터 집합 {#existing-dataset} 사용

기존 데이터 세트를 사용하려면 먼저 데이터 세트를 선택합니다. 오른쪽의 세로 막대는 데이터 세트에 대한 정보를 채웁니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

**[!UICONTROL Partial ingestion]** 토글을 사용하면 부분 일괄 처리 통합 사용을 활성화 또는 비활성화할 수 있습니다.

**[!UICONTROL Error diagnostics]** 토글은 **[!UICONTROL Partial ingestion]** 토글이 꺼져 있을 때만 표시됩니다. 이 기능을 사용하면 [!DNL Platform]에서 인제스트된 배치에 대한 자세한 오류 메시지를 생성할 수 있습니다. **[!UICONTROL Partial ingestion]** 토글이 켜져 있으면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]**&#x200B;을 사용하면 전체 배치가 실패하기 전에 허용되는 오류 백분율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

이제 **데이터 추가** 단추를 사용하여 데이터를 업로드할 수 있으며 부분 섭취를 사용하여 인제스트됩니다.

### &quot;[!UICONTROL Map CSV to XDM schema]&quot; 흐름 {#map-flow} 사용

&quot;[!UICONTROL Map CSV to XDM schema]&quot; 흐름을 사용하려면 [CSV 파일 매핑 자습서](../tutorials/map-a-csv-file.md)에 나열된 단계를 따르십시오. **[!UICONTROL Add data]** 단계에 도달하면 **[!UICONTROL Partial ingestion]** 및 **[!UICONTROL Error diagnostics]** 필드를 기록해 두십시오.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

**[!UICONTROL Partial ingestion]** 토글을 사용하면 부분 일괄 처리 통합 사용을 활성화 또는 비활성화할 수 있습니다.

**[!UICONTROL Error diagnostics]** 토글은 **[!UICONTROL Partial ingestion]** 토글이 꺼져 있을 때만 표시됩니다. 이 기능을 사용하면 [!DNL Platform]에서 인제스트된 배치에 대한 자세한 오류 메시지를 생성할 수 있습니다. **[!UICONTROL Partial ingestion]** 토글이 켜져 있으면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** 전체 배치가 실패하기 전에 허용되는 오류 백분율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

## 다음 단계 {#next-steps}

이 자습서에서는 데이터 세트를 만들거나 수정하여 부분 일괄 처리를 활성화하는 방법에 대해 다룹니다. 일괄 처리에 대한 자세한 내용은 [일괄 처리 통합 개발자 가이드](./api-overview.md)를 참조하십시오.

부분 통합 오류 모니터링에 대한 자세한 내용은 [일괄 처리 통합 오류 진단 안내서](../quality/error-diagnostics.md)를 참조하십시오.
