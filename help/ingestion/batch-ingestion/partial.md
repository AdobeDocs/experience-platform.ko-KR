---
keywords: Experience Platform;홈;인기 항목;일괄 처리 섭취;부분 수집;부분 수집;오류 검색;오류 검색;부분 배치 수집;부분 배치 수집;부분적;수집;수집;수집
solution: Experience Platform
title: 부분 배치 수집 개요
topic-legacy: overview
description: 이 문서에서는 부분 배치 섭취 관리를 위한 자습서를 제공합니다.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: d380b4d2a75efb1c34010a30c619649a7b99643c
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# 부분 배치 수집

부분 배치 섭취는 특정 임계값까지 오류가 포함된 데이터를 수집하는 기능입니다. 이 기능을 사용하면 사용자가 모든 올바른 데이터를 Adobe Experience Platform에 성공적으로 수집하면서 잘못된 데이터에 대한 세부 정보와 함께 모든 잘못된 데이터를 개별적으로 일괄 처리할 수 있습니다.

이 문서에서는 부분 배치 섭취 관리를 위한 자습서를 제공합니다.

## 시작하기

이 자습서에서는 부분 배치 수집과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 지식이 필요합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [일괄 수집](./overview.md): 다음 메서드를 사용합니다. [!DNL Platform] csv 및 Parquet과 같은 데이터 파일의 데이터를 수집 및 저장합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.

다음 섹션에서는 를 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Platform] API.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- 권한 부여: 베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

## API에서 부분 배치 수집을 위한 배치 활성화 {#enable-api}

>[!NOTE]
>
>이 섹션에서는 API를 사용하여 부분 배치 수집을 위한 배치를 활성화하는 방법에 대해 설명합니다. UI 사용에 대한 지침은 [UI에서 부분 배치 처리를 위한 배치 활성화](#enable-ui) 단계.

부분 수집이 활성화된 새 배치를 생성할 수 있습니다.

새 배치를 생성하려면 [배치 수집 개발자 안내서](./api-overview.md). 에 도달하면 **[!UICONTROL 일괄 처리 만들기]** 단계에서 요청 본문에 다음 필드를 추가합니다.

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 다음을 허용하는 플래그 [!DNL Platform] 일괄 처리에 대한 자세한 오류 메시지를 생성합니다. |
| `partialIngestionPercent` | 전체 배치가 실패하기 전에 허용되는 오류 비율입니다. 따라서 이 예에서 일괄 처리의 최대 5%가 오류일 수 있으며 그 전에 오류가 발생할 수도 있습니다. |


## UI에서 부분 배치 처리를 위한 배치 활성화 {#enable-ui}

>[!NOTE]
>
>이 섹션에서는 UI를 사용하여 부분 배치 처리를 위한 배치를 활성화하는 방법에 대해 설명합니다. API를 사용하여 부분 배치 처리에 대한 배치를 이미 활성화한 경우 다음 섹션으로 건너뛸 수 있습니다.

을 통해 부분 수집을 위한 배치를 활성화하려면 [!DNL Platform] UI를 통해 소스 연결을 통해 새 일괄 처리를 생성하거나 기존 데이터 세트에 새 일괄 처리를 생성하거나 &quot;[!UICONTROL XDM 흐름에 CSV 매핑]&quot;.

### 새 소스 연결 만들기 {#new-source}

새 소스 연결을 만들려면 [소스 개요](../../sources/home.md). 에 도달하면 **[!UICONTROL 데이터 흐름 세부 정보]** 한 단계, 다음 사항을 기록해 두십시오 **[!UICONTROL 부분 수집]** 및 **[!UICONTROL 오류 진단]** 필드.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

다음 **[!UICONTROL 부분 수집]** 토글 기능을 사용하면 부분 배치 수집 기능을 활성화하거나 비활성화할 수 있습니다.

다음 **[!UICONTROL 오류 진단]** 토글은 **[!UICONTROL 부분 수집]** 토글이 꺼져 있습니다. 이 기능을 사용하면 [!DNL Platform] 수집된 일괄 처리에 대한 자세한 오류 메시지를 생성합니다. 만약 **[!UICONTROL 부분 수집]** 토글이 설정되어 있으면 고급 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

다음 **[!UICONTROL 오류 임계값]** 전체 배치가 실패하기 전에 허용 가능한 오류 백분율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

### 기존 데이터 세트 사용 {#existing-dataset}

기존 데이터 세트를 사용하려면 먼저 데이터 세트를 선택합니다. 오른쪽에 있는 사이드바는 데이터 세트에 대한 정보로 채워집니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

다음 **[!UICONTROL 부분 수집]** 토글 기능을 사용하면 부분 배치 수집 기능을 활성화하거나 비활성화할 수 있습니다.

다음 **[!UICONTROL 오류 진단]** 토글은 **[!UICONTROL 부분 수집]** 토글이 꺼져 있습니다. 이 기능을 사용하면 [!DNL Platform] 수집된 일괄 처리에 대한 자세한 오류 메시지를 생성합니다. 만약 **[!UICONTROL 부분 수집]** 토글이 설정되어 있으면 고급 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

다음 **[!UICONTROL 오류 임계값]** 전체 배치가 실패하기 전에 허용 가능한 오류 백분율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

이제 다음을 사용하여 데이터를 업로드할 수 있습니다. **데이터 추가** 단추 및 부분 수집을 사용하여 수집됩니다.

### &quot;[!UICONTROL XDM 스키마에 CSV 매핑]&quot; 흐름 {#map-flow}

를 사용하려면[!UICONTROL XDM 스키마에 CSV 매핑]&quot; 흐름을 수행하려면 [CSV 파일 매핑 자습서](../tutorials/map-csv/overview.md). 에 도달하면 **[!UICONTROL 데이터 추가]** 한 단계, 다음 사항을 기록해 두십시오 **[!UICONTROL 부분 수집]** 및 **[!UICONTROL 오류 진단]** 필드.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

다음 **[!UICONTROL 부분 수집]** 토글 기능을 사용하면 부분 배치 수집 기능을 활성화하거나 비활성화할 수 있습니다.

다음 **[!UICONTROL 오류 진단]** 토글은 **[!UICONTROL 부분 수집]** 토글이 꺼져 있습니다. 이 기능을 사용하면 [!DNL Platform] 수집된 일괄 처리에 대한 자세한 오류 메시지를 생성합니다. 만약 **[!UICONTROL 부분 수집]** 토글이 설정되어 있으면 고급 오류 진단이 자동으로 적용됩니다.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL 오류 임계값]** 전체 배치가 실패하기 전에 허용 가능한 오류 백분율을 설정할 수 있습니다. 기본적으로 이 값은 5%로 설정됩니다.

## 다음 단계 {#next-steps}

이 자습서에서는 부분 배치 수집을 활성화하기 위해 데이터 세트를 생성 또는 수정하는 방법에 대해 설명합니다. 일괄 처리에 대한 자세한 내용은 [배치 수집 개발자 안내서](./api-overview.md).

부분 수집 오류 모니터링에 대한 자세한 내용은 [배치 수집 오류 진단 안내서](../quality/error-diagnostics.md).
