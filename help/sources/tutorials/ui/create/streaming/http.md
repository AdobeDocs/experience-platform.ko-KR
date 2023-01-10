---
keywords: Experience Platform;홈;인기 항목;스트리밍 연결;스트리밍 연결 만들기;ui 안내서;자습서;스트리밍 연결 만들기;스트리밍 수집;섭취;
solution: Experience Platform
title: UI를 사용하여 HTTP API 스트리밍 연결 만들기
type: Tutorial
description: 이 UI 안내서는 Adobe Experience Platform을 사용하여 스트리밍 연결을 만드는 데 도움이 됩니다.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---


# 만들기 [!DNL HTTP API] ui를 사용한 스트리밍 연결

이 자습서에서는 다음을 사용하여 스트리밍 소스 연결을 만드는 단계를 제공합니다 [!UICONTROL 소스] 작업 공간.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   - [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 스트리밍 연결 만들기

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 **[!UICONTROL 스트리밍]** 카테고리, 선택 **[!UICONTROL HTTP API]** 그런 다음 **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/http/catalog.png)

다음 **[!UICONTROL HTTP API 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 로 새 데이터 흐름을 만들 HTTP API 계정을 선택한 다음 을 선택합니다 **[!UICONTROL 다음]** 계속 진행합니다.

![기존 계정](../../../../images/tutorials/create/http/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 계정 이름과 선택적 설명을 제공합니다. 다음 구성 속성을 제공하는 옵션도 제공됩니다.

- **[!UICONTROL 인증]:** 이 속성은 스트리밍 연결에 인증이 필요한지 여부를 결정합니다. 인증은 신뢰할 수 있는 소스에서 데이터를 수집할 수 있도록 합니다. PII(개인 식별 정보)를 처리하는 경우 이 속성을 켜야 합니다. 기본적으로 이 속성은 꺼져 있습니다.
- **[!UICONTROL XDM 호환 가능]:** 이 속성은 이 스트리밍 연결이 XDM 스키마와 호환되는 이벤트를 전송하는지 여부를 나타냅니다. 기본적으로 이 속성은 꺼져 있습니다.

완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![신규 계정](../../../../images/tutorials/create/http/new.png)

## 데이터 선택

HTTP API 연결을 만든 후 **[!UICONTROL 데이터 선택]** 데이터가 업로드되고 미리 볼 수 있는 인터페이스를 제공하는 단계가 나타납니다.

선택 **[!UICONTROL 파일 업로드]** 를 눌러 데이터를 업로드합니다. 또는 데이터를 로 끌어다 놓을 수 있습니다 [!UICONTROL 파일 드래그 앤 드롭] 인터페이스 섹션을 참조하십시오.

![add-data](../../../../images/tutorials/create/http/add-data.png)

데이터가 업로드된 상태에서 인터페이스 오른쪽을 사용하여 파일 계층 구조를 미리 볼 수 있습니다. 선택 **[!UICONTROL 다음]** 계속 진행합니다.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## XDM 스키마에 데이터 필드 매핑

다음 [!UICONTROL 매핑] 소스 데이터를 Platform 데이터 세트에 매핑할 인터페이스를 제공하는 단계가 나타납니다.

Parquet 파일은 XDM 규격 파일이어야 하며 수동으로 매핑을 구성할 필요가 없습니다. CSV 파일을 사용하려면 명시적으로 매핑을 구성해야 하지만 매핑할 소스 데이터 필드를 선택할 수 있도록 하십시오. XDM 불만 사항으로 표시된 JSON 파일은 수동 구성이 필요하지 않습니다. 그러나 XDM 규격으로 표시되지 않으면 매핑을 명시적으로 구성해야 합니다.

수집할 인바운드 데이터에 대한 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

### 새 데이터 세트 만들기

새 데이터 세트를 만들려면 **[!UICONTROL 새 데이터 세트]**. 표시되는 양식에서 이름, 선택적 설명 및 데이터 세트에 대한 대상 스키마를 제공합니다. 을(를) 선택하는 경우 [!DNL Profile]-활성화된 스키마에서는 데이터 세트가 [!DNL Profile]-enabled.

![새로운 데이터 세트](../../../../images/tutorials/create/http/new-dataset.png)

### 기존 데이터 세트 사용

기존 데이터 세트를 사용하려면 **[!UICONTROL 기존 데이터 세트]**. 표시되는 양식에서 사용할 데이터 세트를 선택합니다. 데이터 세트를 선택하고 나면 데이터 세트를 선택할지 여부를 선택할 수 있습니다 [!DNL Profile]-enabled.

![기존 데이터 세트](../../../../images/tutorials/create/http/existing-dataset.png)

### 표준 필드 매핑


필요에 따라 필드를 직접 매핑하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산 또는 계산된 값을 도출할 수 있습니다. 매퍼 인터페이스 및 계산된 필드를 사용하는 방법에 대한 포괄적인 단계는 다음을 참조하십시오 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md).

새 소스 필드를 추가하려면 **[!UICONTROL 새 매핑 추가]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

새 소스 필드 및 대상 필드 쌍이 나타납니다. 새 소스 필드를 추가하려면 [!UICONTROL 소스 필드 선택] 입력 막대.

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

다음 [!UICONTROL 속성 선택] 패널 을 사용하면 파일 계층 구조를 탐색하고 대상 XDM 필드에 매핑할 특정 소스 필드를 선택할 수 있습니다. 매핑할 소스 필드를 선택하면 **[!UICONTROL 선택]** 계속 진행합니다.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

소스 필드를 선택하면 매핑할 적절한 대상 XDM 필드를 식별할 수 있습니다. 대상 필드 섹션 아래에서 스키마 아이콘을 선택합니다.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

다음 [!UICONTROL 대상 필드에 소스 필드 매핑] 대상 데이터 집합의 스키마를 탐색할 수 있는 인터페이스를 제공하는 창이 나타납니다. 소스 필드와 일치하는 타겟 필드를 선택한 다음 을 선택합니다 **[!UICONTROL 선택]** 계속 진행합니다.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

소스 필드가 모두 적절한 대상 XDM 필드에 매핑되면 을 선택합니다 **[!UICONTROL 다음]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## 데이터 흐름 세부 정보

다음 **[!UICONTROL 데이터 흐름 세부 정보]** 단계가 나타납니다. 이 페이지에서 이름과 선택적 설명을 지정하여 만든 데이터 집합에 대한 세부 정보를 제공할 수 있습니다.

데이터 집합에 대한 세부 정보를 제공한 후 다음을 선택합니다 **[!UICONTROL 다음]**.

![데이터 흐름 세부 정보](../../../../images/tutorials/create/http/dataflow-detail.png)

## 검토

다음 **[!UICONTROL 검토]** 데이터 흐름을 만들기 전에 데이터 흐름 세부 사항을 검토할 수 있는 단계가 나타납니다. 세부 사항은 다음 범주 내에 있습니다.

- **[!UICONTROL 연결]**: 계정 이름, 소스 플랫폼 및 소스 이름을 표시합니다.
- **[!UICONTROL 데이터 세트 및 맵 필드 할당]**: 대상 데이터 세트와 데이터 세트가 준수하는 스키마를 표시합니다.

세부 정보가 정확한지 확인한 후 **[!UICONTROL 완료]**.

![검토](../../../../images/tutorials/create/http/review.png)

## 스트리밍 끝점 URL 가져오기

연결이 생성되면 소스 세부 정보 페이지가 나타납니다. 이 페이지에는 이전에 실행한 데이터 흐름, ID 및 스트리밍 끝점 URL을 포함하여 새로 만든 연결에 대한 세부 사항이 표시됩니다.

![엔드포인트](../../../../images/tutorials/create/http/endpoint.png)

## 다음 단계

이 자습서에 따라 스트리밍 HTTP 연결을 만들어 스트리밍 끝점을 사용하여 다양한 항목에 액세스할 수 있습니다 [!DNL Data Ingestion] API. API에서 스트리밍 연결을 만드는 지침은 다음을 참조하십시오. [스트리밍 연결 만들기 자습서](../../../api/create/streaming/http.md).

데이터를 Platform으로 스트리밍하는 방법에 대해 알아보려면 다음 자습서를 참조하십시오. [스트리밍 시계열 데이터](../../../../../ingestion/tutorials/streaming-time-series-data.md) 또는 [스트리밍 레코드 데이터](../../../../../ingestion/tutorials/streaming-record-data.md).
