---
title: UI를 사용하여 HTTP API 스트리밍 연결 만들기
description: 이 UI 안내서는 Adobe Experience Platform을 사용하여 스트리밍 연결을 만드는 데 도움이 됩니다.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---


# UI를 사용하여 [!DNL HTTP API] 스트리밍 연결 만들기

이 자습서에서는 [!UICONTROL 소스] 작업 영역을 사용하여 스트리밍 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 스트리밍 연결 만들기

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**[!UICONTROL 스트리밍]** 범주에서 **[!UICONTROL HTTP API]**&#x200B;를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/http/catalog.png)

**[!UICONTROL HTTP API 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 HTTP API 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속합니다.

![기존 계정](../../../../images/tutorials/create/http/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을 선택하세요. 표시되는 입력 양식에서 계정 이름과 설명(선택 사항)을 입력합니다. 다음 구성 속성을 제공하는 옵션도 제공됩니다.

- **[!UICONTROL 인증]:** 이 속성은 스트리밍 연결에 인증이 필요한지 여부를 결정합니다. 인증은 신뢰할 수 있는 소스에서 데이터를 수집하도록 보장합니다. PII(개인 식별 정보)를 처리하는 경우 이 속성을 설정해야 합니다. 기본적으로 이 속성은 꺼져 있습니다.
- **[!UICONTROL XDM 호환]:** 이 속성은 이 스트리밍 연결에서 XDM 스키마와 호환되는 이벤트를 전송할지 여부를 나타냅니다. 기본적으로 이 속성은 꺼져 있습니다.

완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 후 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속하십시오.

![새 계정](../../../../images/tutorials/create/http/new.png)

## 데이터 선택

HTTP API 연결을 만든 후 데이터를 업로드하고 미리 볼 수 있는 인터페이스를 제공하는 **[!UICONTROL 데이터 선택]** 단계가 나타납니다.

데이터를 업로드하려면 **[!UICONTROL 파일 업로드]**&#x200B;를 선택하십시오. 또는 데이터를 인터페이스의 [!UICONTROL 파일 드래그 앤 드롭] 섹션으로 드래그 앤 드롭할 수 있습니다.

![데이터 추가](../../../../images/tutorials/create/http/add-data.png)

데이터가 업로드된 상태에서 인터페이스의 오른쪽을 사용하여 파일 계층 구조를 미리 볼 수 있습니다. 계속하려면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## 데이터 필드를 XDM 스키마에 매핑

소스 데이터를 Experience Platform 데이터 집합에 매핑하는 인터페이스를 제공하는 [!UICONTROL 매핑] 단계가 나타납니다.

[!DNL HTTP API] 원본은 JSON 파일 수집을 지원합니다. JSON 파일이 XDM 컴플레인으로 표시된 경우 수동 구성이 필요하지 않습니다. 그렇지 않은 경우 매핑을 명시적으로 구성해야 합니다.

수집할 인바운드 데이터에 대한 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

### 새 데이터 세트 만들기

새 데이터 집합을 만들려면 **[!UICONTROL 새 데이터 집합]**&#x200B;을(를) 선택하십시오. 표시되는 양식에 데이터 세트의 대상 스키마뿐만 아니라 이름, 선택적 설명을 입력합니다. [!DNL Profile]이(가) 활성화된 스키마를 선택하는 경우 데이터 세트가 [!DNL Profile]도 활성화되어야 하는지 여부를 선택할 수 있습니다.

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### 기존 데이터 세트 사용

기존 데이터 집합을 사용하려면 **[!UICONTROL 기존 데이터 집합]**&#x200B;을(를) 선택하십시오. 표시되는 양식에서 사용할 데이터 세트를 선택합니다. 데이터 세트를 선택하면 데이터 세트가 [!DNL Profile] 활성화되어야 하는지 여부를 선택할 수 있습니다.

![기존 데이터 세트](../../../../images/tutorials/create/http/existing-dataset.png)

### 표준 필드 매핑

필요에 따라 필드를 직접 매핑하도록 선택하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 파생할 수 있습니다. 매퍼 인터페이스 및 계산된 필드 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md)를 참조하십시오.

새 소스 필드를 추가하려면 **[!UICONTROL 새 매핑 추가]**&#x200B;를 선택하십시오.

![새 매핑 추가](../../../../images/tutorials/create/http/add-new-mapping.png)

새 소스 필드와 대상 필드 쌍이 나타납니다. 새 소스 필드를 추가하려면 [!UICONTROL 소스 필드 선택] 입력 막대 옆의 화살표 아이콘을 선택합니다.

![소스 필드 선택](../../../../images/tutorials/create/http/select-source-field.png)

[!UICONTROL 특성 선택] 패널을 사용하면 파일 계층 구조를 살펴보고 대상 XDM 필드에 매핑할 특정 소스 필드를 선택할 수 있습니다. 매핑할 소스 필드를 선택한 후 **[!UICONTROL 선택]**&#x200B;을(를) 선택하여 계속합니다.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

소스 필드를 선택하면 이제 매핑할 적절한 타겟 XDM 필드를 식별할 수 있습니다. 대상 필드 섹션 아래에서 스키마 아이콘을 선택합니다.

![타겟 필드 선택](../../../../images/tutorials/create/http/select-target-field.png)

[!UICONTROL 소스 필드를 대상 필드에 매핑] 창이 나타나고 대상 데이터 집합의 스키마를 탐색할 수 있는 인터페이스를 제공합니다. 원본 필드와 일치하는 대상 필드를 선택한 다음 **[!UICONTROL Select]**&#x200B;을(를) 선택하여 계속하십시오.

![대상 필드에 매핑](../../../../images/tutorials/create/http/map-to-target-field.png)

소스 필드가 모두 해당 대상 XDM 필드에 매핑되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## 데이터 흐름 세부 정보

**[!UICONTROL 데이터 흐름 세부 정보]** 단계가 나타납니다. 이 페이지에서는 이름과 설명(선택 사항)을 지정하여 생성된 데이터 흐름에 대한 세부 정보를 제공할 수 있습니다.

데이터 흐름에 대한 세부 정보를 제공한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![데이터 흐름-세부 정보](../../../../images/tutorials/create/http/dataflow-detail.png)

## 검토

**[!UICONTROL 검토]** 단계가 표시되어 데이터 흐름을 만들기 전에 세부 사항을 검토할 수 있습니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

- **[!UICONTROL 연결]**: 계정 이름, 원본 플랫폼 및 원본 이름을 표시합니다.
- **[!UICONTROL 데이터 집합 및 맵 필드 할당]**: 대상 데이터 집합과 데이터 집합이 준수하는 스키마를 표시합니다.

세부 정보가 올바른지 확인한 후 **[!UICONTROL 마침]**&#x200B;을 선택합니다.

![검토](../../../../images/tutorials/create/http/review.png)

## 스트리밍 끝점 URL 가져오기

연결이 생성되면 소스 세부 정보 페이지가 나타납니다. 이 페이지에는 이전에 실행한 데이터 흐름, ID 및 스트리밍 끝점 URL을 포함하여 새로 생성된 연결의 세부 정보가 표시됩니다.

![끝점](../../../../images/tutorials/create/http/endpoint.png)

## 다음 단계

이 자습서에 따라 스트리밍 HTTP 연결을 만들어 스트리밍 끝점을 사용하여 다양한 [!DNL Data Ingestion] API에 액세스할 수 있습니다. API에서 스트리밍 연결을 만드는 방법에 대한 지침은 [스트리밍 연결 만들기 자습서](../../../api/create/streaming/http.md)를 참조하십시오.

Experience Platform으로 데이터를 스트리밍하는 방법에 대해 알아보려면 [시계열 데이터 스트리밍](../../../../../ingestion/tutorials/streaming-time-series-data.md)에 대한 자습서 또는 [레코드 데이터 스트리밍](../../../../../ingestion/tutorials/streaming-record-data.md)에 대한 자습서를 참조하십시오.
