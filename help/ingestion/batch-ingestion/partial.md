---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;
solution: Experience Platform
title: 부분 일괄 처리 처리 개요
topic: overview
description: 이 문서에서는 부분 일괄 처리 처리를 관리하는 자습서를 제공합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 0%

---


# 부분 일괄 처리

부분 일괄 처리란 오류가 포함된 데이터를 특정 임계값까지 인제스트하는 기능입니다. 이 기능을 사용하면 사용자가 모든 올바른 데이터를 Adobe Experience Platform으로 성공적으로 인제스트할 수 있으며 모든 잘못된 데이터가 잘못된 이유에 대한 세부 정보와 함께 별도로 일괄적으로 묶을 수 있습니다.

이 문서에서는 부분 일괄 처리 처리를 관리하는 자습서를 제공합니다.

## 시작하기

이 자습서에서는 부분 일괄 처리에 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [일괄 처리](./overview.md):CSV 및 [!DNL Platform] Portable과 같은 데이터 파일의 데이터를 인제하고 저장하는 방법입니다.
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

다음 섹션에서는 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 [!DNL Platform] 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

## API에서 부분 일괄 처리를 활성화합니다. {#enable-api}

>[!NOTE]
>
>이 섹션에서는 API를 사용하여 부분 일괄 처리를 활성화하는 방법에 대해 설명합니다. UI 사용에 대한 지침은 UI [단계에서 부분 일괄 처리를 위한 일괄 처리](#enable-ui) 활성화를 참조하십시오.

부분 처리가 활성화된 새 배치를 만들 수 있습니다.

새 배치를 만들려면 일괄 처리 통합 개발자 안내서의 [단계를 따릅니다](./api-overview.md). 배치 **[!UICONTROL 생성]** 단계에 도달하면 요청 본문 내에 다음 필드를 추가합니다.

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 일괄 처리에 대한 자세한 오류 메시지 [!DNL Platform] 를 생성할 수 있는 플래그. |
| `partialIngestionPercentage` | 전체 배치가 실패하기 전에 허용되는 오류 비율. 따라서 이 예에서는 일괄 처리가 실패하기 전에 최대 5%의 일괄 처리를 오류가 발생할 수 있습니다. |


## UI에서 부분 일괄 처리를 위한 일괄 처리 활성화 {#enable-ui}

>[!NOTE]
>
>이 섹션에서는 UI를 사용하여 부분 일괄 처리를 활성화하는 방법에 대해 설명합니다. API를 사용하여 부분 일괄 처리를 이미 활성화한 경우 다음 섹션으로 건너뛸 수 있습니다.

UI를 통해 부분 섭취에 대한 배치를 활성화하려면 소스 연결을 통해 새 배치를 만들거나 기존 데이터 세트에 새 배치를 만들거나 &quot;CSV를 [!DNL Platform] XDM 플로우에 매핑&quot;을 통해 새 배치를 만들 수 있습니다.

### 새 소스 연결 만들기 {#new-source}

새 소스 연결을 만들려면 소스 [개요에 나열된 단계를 따릅니다](../../sources/home.md). 데이터 흐름 세부 **[!UICONTROL 정보]** 단계에 도달하면 **[!UICONTROL 부분 섭취]** 및 **[!UICONTROL 오류 진단]** 필드를참고합니다.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

부분 **[!UICONTROL 통합]** 토글을 사용하면 부분 일괄 처리를 사용하거나 사용하지 않을 수 있습니다.

오류 **[!UICONTROL 진단]** 토글은 부분 통합 토글이 꺼진 경우에만 **[!UICONTROL 나타납니다]** . 이 기능을 사용하면 인제스트된 배치에 대한 자세한 오류 메시지 [!DNL Platform] 를 생성할 수 있습니다. 부분 **[!UICONTROL 통합]** 전환이 켜지면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

오류 임계값 **[!UICONTROL 을 사용하면]** 전체 배치가 실패하기 전에 허용되는 오류 비율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

### 기존 데이터 세트 사용 {#existing-dataset}

기존 데이터 세트를 사용하려면 먼저 데이터 세트를 선택합니다. 오른쪽의 세로 막대는 데이터 세트에 대한 정보를 채웁니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

부분 **[!UICONTROL 통합]** 토글을 사용하면 부분 일괄 처리를 사용하거나 사용하지 않을 수 있습니다.

오류 **[!UICONTROL 진단]** 토글은 부분 통합 토글이 꺼진 경우에만 **[!UICONTROL 나타납니다]** . 이 기능을 사용하면 인제스트된 배치에 대한 자세한 오류 메시지 [!DNL Platform] 를 생성할 수 있습니다. 부분 **[!UICONTROL 통합]** 전환이 켜지면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

오류 임계값 **[!UICONTROL 을 사용하면]** 전체 배치가 실패하기 전에 허용되는 오류 비율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

이제 데이터 **추가** 단추를 사용하여 데이터를 업로드할 수 있으며 부분 섭싱을 사용하여 인제스트됩니다.

### &quot;XDM 스키마에[!UICONTROL CSV 매핑&quot; 흐름을]사용하십시오 {#map-flow}

&quot;[!UICONTROL CSV를 XDM 스키마에]매핑&quot; 흐름을 사용하려면 CSV 파일 [매핑 자습서에 나열된 단계를 따르십시오](../tutorials/map-a-csv-file.md). 데이터 **[!UICONTROL 추가]** 단계에 도달하면 **[!UICONTROL 부분 섭취]** 및 **[!UICONTROL 오류 진단]** 필드를참고하십시오.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

부분 **[!UICONTROL 통합]** 토글을 사용하면 부분 일괄 처리를 사용하거나 사용하지 않을 수 있습니다.

오류 **[!UICONTROL 진단]** 토글은 부분 통합 토글이 꺼진 경우에만 **[!UICONTROL 나타납니다]** . 이 기능을 사용하면 인제스트된 배치에 대한 자세한 오류 메시지 [!DNL Platform] 를 생성할 수 있습니다. 부분 **[!UICONTROL 통합]** 전환이 켜지면 향상된 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

오류 임계값 **[!UICONTROL 을 사용하면]** 전체 배치가 실패하기 전에 허용되는 오류 비율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

## 다음 단계 {#next-steps}

이 자습서에서는 데이터 세트를 만들거나 수정하여 부분 일괄 처리를 활성화하는 방법에 대해 설명합니다. 일괄 처리에 대한 자세한 내용은 [일괄 처리 통합 개발자 안내서를 참조하십시오](./api-overview.md).

부분 섭취 오류 모니터링에 대한 자세한 내용은 [배치 처리 오류 진단 안내서를 참조하십시오](../quality/error-diagnostics.md).
