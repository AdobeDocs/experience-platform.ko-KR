---
keywords: Experience Platform;홈;인기 항목;세그멘테이션 서비스;세그멘테이션 서비스;사용 안내서;세그멘테이션 ui 안내서;세그먼트 빌더;세그먼트 빌더;Segmentation Service;segmentation Service;segmentation-service;segmentation builder;segmentation builder;
solution: Experience Platform
title: 세그먼트 빌더 UI 안내서
topic: ui guide
description: Adobe Experience Platform UI의 세그먼트 빌더는 프로필 데이터 요소와 상호 작용할 수 있는 풍부한 작업 공간을 제공합니다. 작업 영역은 데이터 속성을 나타내는 데 사용되는 드래그 앤 드롭 타일과 같이 규칙을 작성하고 편집하기 위한 직관적인 컨트롤을 제공합니다.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
translation-type: tm+mt
source-git-commit: bad293cf25b955496897d895169ec494416e9787
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 0%

---

# [!DNL Segment Builder] UI 가이드

[!DNL Segment Builder] 는  [!DNL Profile] 데이터 요소와 상호 작용할 수 있는 풍부한 작업 영역을 제공합니다. 작업 영역은 데이터 속성을 나타내는 데 사용되는 드래그 앤 드롭 타일과 같이 규칙을 작성하고 편집하기 위한 직관적인 컨트롤을 제공합니다.

![](../images/ui/segment-builder/segment-builder.png)

## 세그먼트 정의 구성 블록

세그먼트 정의의 기본 구성 요소는 속성 및 이벤트입니다. 또한 기존 대상에 포함된 특성과 이벤트를 새 정의에 대한 구성 요소로 사용할 수도 있습니다.

이러한 구성 블록은 [!DNL Segment Builder] 작업 영역의 왼쪽에 있는 **[!UICONTROL Fields]** 섹션에서 볼 수 있습니다. **[!UICONTROL Fields]** 에는 각 기본 구성 블록에 대한 탭이 포함되어 있습니다.&quot;[!UICONTROL Attributes]&quot;, &quot;[!UICONTROL Events]&quot; 및 &quot;[!UICONTROL Audiences]&quot;

![](../images/ui/segment-builder/segment-fields.png)

### 속성

**[!UICONTROL Attributes]** 탭에서는 [!DNL XDM Individual Profile] 클래스에 속하는 [!DNL Profile] 속성을 검색할 수 있습니다. 각 폴더를 확장하여 추가 속성을 표시할 수 있습니다. 여기서 각 속성은 작업 영역의 중앙에 있는 규칙 빌더 캔버스로 드래그할 수 있는 타일입니다. [규칙 빌더 캔버스](#rule-builder-canvas)에 대한 자세한 내용은 이 안내서의 뒷부분에서 설명합니다.

![](../images/ui/segment-builder/attributes.png)

### 이벤트

**[!UICONTROL Events]** 탭에서는 [!DNL XDM ExperienceEvent] 데이터 요소를 사용하여 발생한 이벤트 또는 작업을 기반으로 대상을 만들 수 있습니다. 또한 **[!UICONTROL Events]** 탭에서 이벤트 유형을 찾을 수 있습니다. 이 탭은 세그먼트를 보다 신속하게 만들 수 있도록 일반적으로 사용되는 이벤트 컬렉션입니다.

[!DNL ExperienceEvent] 요소를 검색할 수 있을 뿐만 아니라 이벤트 유형도 검색할 수 있습니다. 이벤트 유형은 [!DNL ExperienceEvents]과 동일한 코딩 로직을 사용하므로, 올바른 이벤트를 찾는 [!DNL XDM ExperienceEvent] 클래스를 검색하지 않아도 됩니다. 예를 들어 검색 막대를 사용하여 &quot;cart&quot;를 검색하면 세그먼트 정의를 작성할 때 매우 일반적으로 사용되는 두 개의 장바구니 동작인 이벤트 유형 &quot;[!UICONTROL AddCart]&quot; 및 &quot;[!UICONTROL RemoveCart]&quot;이 반환됩니다.

모든 유형의 구성 요소는 [Lucene의 검색 구문](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)을 사용하는 검색 막대에 이름을 입력하여 검색할 수 있습니다. 전체 단어를 입력하면 검색 결과가 입력되기 시작합니다. 예를 들어 XDM 필드 `ExperienceEvent.commerce.productViews`에 따라 규칙을 작성하려면 검색 필드에 &quot;제품 보기&quot;를 입력하기 시작합니다. 단어 &quot;product&quot;를 입력하면 검색 결과가 표시됩니다. 각 결과에는 해당 결과가 속하는 개체 계층 구조가 포함됩니다.

>[!NOTE]
>
>조직에서 정의한 사용자 정의 스키마 필드를 표시하고 규칙을 만드는 데 최대 24시간이 걸릴 수 있습니다.

그런 다음 [!DNL ExperienceEvents] 및 &quot;[!UICONTROL Event Types]&quot;을(를) 세그먼트 정의로 쉽게 드래그하여 놓을 수 있습니다.

![](../images/ui/segment-builder/events-eventTypes.png)

기본적으로 데이터 저장소에서 채워진 스키마 필드만 표시됩니다. 여기에는 &quot;[!UICONTROL Event Types]&quot;이 포함됩니다. &quot;[!UICONTROL Event Types]&quot; 목록이 표시되지 않거나 &quot;[!UICONTROL Any]&quot;을 &quot;[!UICONTROL Event Type]&quot;로만 선택할 수 있는 경우 **[!UICONTROL Fields]** 옆의 **톱니바퀴 아이콘**&#x200B;을 선택한 다음 **[!UICONTROL Available Fields]** 아래에서 **[!UICONTROL Show full XDM schema]**&#x200B;을 선택합니다. **톱니바퀴 아이콘**&#x200B;을 다시 선택하여 **[!UICONTROL Fields]** 탭으로 돌아가십시오. 이제 데이터 포함 여부에 상관없이 여러 개의 &quot;[!UICONTROL Event Types]&quot; 및 스키마 필드를 볼 수 있습니다.

![](../images/ui/segment-builder/show-populated.png)

### 대상자

**[!UICONTROL Audiences]** 탭에는 Adobe Audience Manager과 같은 외부 소스에서 가져온 모든 대상뿐만 아니라 [!DNL Experience Platform] 내에 만든 대상이 나열됩니다.

**[!UICONTROL Audiences]** 탭에서 사용 가능한 모든 소스를 폴더 그룹으로 볼 수 있습니다. 폴더를 선택하면 사용 가능한 하위 폴더와 대상을 볼 수 있습니다. 또한 폴더 구조(확인 표시는 현재 있는 폴더를 의미함)를 보기 위해 폴더 아이콘(맨 오른쪽 이미지에 표시)을 선택하고 트리의 폴더 이름을 선택하여 폴더를 다시 쉽게 탐색할 수 있습니다.

대상자 옆ⓘ에 마우스를 올려 놓으면 해당 ID, 설명 및 폴더 계층 구조를 포함하여 대상에 대한 정보를 볼 수 있습니다.

![](../images/ui/segment-builder/audience-folder-structure.png)

[Lucene의 검색 구문](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)을 활용하는 검색 막대를 사용하여 대상을 검색할 수도 있습니다. **[!UICONTROL Audiences]** 탭에서 최상위 폴더를 선택하면 검색 막대가 표시되므로 해당 폴더 내에서 검색할 수 있습니다. 전체 단어를 입력하면 검색 결과가 채워지기 시작합니다. 예를 들어 `Online Shoppers`이라는 대상자를 찾으려면 검색 표시줄에 &quot;온라인&quot;을 입력합니다. &quot;Online&quot;이라는 단어를 모두 입력하면 &quot;Online&quot;이라는 단어가 포함된 검색 결과가 표시됩니다.

## 규칙 빌더 캔버스 {#rule-builder-canvas}

세그먼트 정의는 대상 대상의 주요 특성이나 행동을 설명하는 데 사용되는 규칙 모음입니다. 이러한 규칙은 [!DNL Segment Builder]의 중앙에 있는 규칙 빌더 캔버스를 사용하여 만듭니다.

세그먼트 정의에 새 규칙을 추가하려면 **[!UICONTROL Fields]** 탭에서 타일을 드래그하여 규칙 빌더 캔버스에 놓습니다. 추가되는 데이터 유형에 따라 컨텍스트별 옵션이 표시됩니다. 사용 가능한 데이터 유형은 다음과 같습니다.문자열, 날짜, [!DNL ExperienceEvents], &quot;[!UICONTROL Event Types]&quot; 및 대상.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Adobe Experience Platform에 대한 최신 변경 사항으로 이벤트 간 `OR` 및 `AND` 논리 연산자의 사용이 업데이트되었습니다. 이 업데이트는 기존 세그먼트에 영향을 주지 않습니다. 하지만 기존 세그먼트 및 새 세그먼트 만들기에 대한 모든 후속 업데이트는 이러한 변경 사항에 영향을 받습니다. 자세한 내용은 [시간 상수 업데이트](./segment-refactoring.md)를 참조하십시오.

### 대상자 추가

**[!UICONTROL Audience]** 탭의 대상을 규칙 빌더 캔버스로 드래그하여 놓아 새 세그먼트 정의에서 대상 멤버십을 참조할 수 있습니다. 이렇게 하면 대상 멤버십을 새 세그먼트 규칙에 속성으로 포함하거나 제외할 수 있습니다.

[!DNL Segment Builder]을(를) 사용하여 만든 [!DNL Platform] 대상의 경우 대상을 해당 대상에 대한 세그먼트 정의에 사용된 규칙 세트로 전환할 수 있는 옵션이 제공됩니다. 이 변환은 규칙 로직의 사본을 만들며, 이렇게 만든 다음 원래 세그먼트 정의에 영향을 주지 않고 수정할 수 있습니다. 세그먼트 정의를 규칙 논리로 변환하기 전에 최근에 변경한 내용을 저장했는지 확인합니다.

>[!NOTE]
>
>외부 소스에서 대상을 추가하면 대상 멤버십만 참조됩니다. 대상을 규칙으로 변환할 수 없으므로 원래 대상을 만드는 데 사용된 규칙을 새 세그먼트 정의에서 수정할 수 없습니다.

![](../images/ui/segment-builder/add-audience-to-segment.png)

대상을 규칙으로 변환할 때 충돌이 발생하는 경우 [!DNL Segment Builder]은(는) 기존 옵션을 최대한 유지하려고 합니다.

### 코드 보기

또는 [!DNL Segment Builder]에서 만든 규칙의 코드 기반 버전을 볼 수도 있습니다. 규칙 빌더 캔버스 내에 규칙을 만든 후 **[!UICONTROL Code view]**&#x200B;을 선택하여 세그먼트를 PQL로 볼 수 있습니다.

![](../images/ui/segment-builder/code-view.png)

코드 보기는 API 호출에 사용할 세그먼트 값을 복사할 수 있는 단추를 제공합니다. 최신 버전의 세그먼트를 가져오려면 세그먼트에 최신 변경 사항을 저장했는지 확인하십시오.

![](../images/ui/segment-builder/copy-code.png)

### 집계 함수

[!DNL Segment Builder]의 집계는 데이터 유형이 숫자(이중 또는 정수)인 XDM 속성 그룹의 계산입니다. 세그먼트 빌더 내에서 지원되는 4개의 집계 함수는 SUM, AVERAGE, MIN 및 MAX입니다.

집계 함수를 만들려면 왼쪽 레일에서 이벤트를 선택하고 [!UICONTROL Events] 컨테이너에 삽입합니다.

![](../images/ui/segment-builder/select-event.png)

이벤트 컨테이너 내에 이벤트를 배치한 후, 줄임표 아이콘(...)을 선택하고 **[!UICONTROL Aggregate]** 순으로 선택합니다.

![](../images/ui/segment-builder/add-aggregation.png)

이제 집계가 추가됩니다. 이제 합계 함수를 선택하고, 합산할 속성, 항등 함수 및 값을 선택할 수 있습니다. 아래 예에서 이 세그먼트는 각 개별 구입이 $100 미만인 경우에도 $100보다 큰 구매 값의 합계를 가진 모든 프로파일을 검증합니다.

![](../images/ui/segment-builder/filled-aggregation.png)

### 카운트 함수

세그먼트 빌더의 카운트 함수는 지정된 이벤트를 찾고 완료한 횟수를 계산하는 데 사용됩니다. 세그먼트 빌더에서 지원되는 개수 함수는 &quot;최소&quot;, &quot;최대&quot;, &quot;정확히&quot;, &quot;사이&quot; 및 &quot;모두&quot;입니다.

카운트 함수를 만들려면 왼쪽 레일에서 이벤트를 선택하고 [!UICONTROL Events] 컨테이너에 삽입합니다.

![](../images/ui/segment-builder/add-event.png)

이벤트 컨테이너 내에 이벤트를 배치한 후 [!UICONTROL At least 1] 단추를 선택합니다.

![](../images/ui/segment-builder/add-count.png)

이제 count 함수가 추가됩니다. 이제 카운트 함수와 함수 값을 선택할 수 있습니다. 아래 예제는 한 번 이상의 클릭이 있는 이벤트를 포함하는 것입니다.

![](../images/ui/segment-builder/select-count.png)

## 컨테이너

세그먼트 규칙은 나열된 순서대로 평가됩니다. 컨테이너는 중첩된 쿼리를 사용하여 실행 순서를 제어할 수 있습니다.

규칙 빌더 캔버스에 타일을 하나 이상 추가하면 컨테이너를 추가할 수 있습니다. 새 컨테이너를 만들려면 타일의 오른쪽 위 모서리에서 줄임표(...)를 선택한 다음 **[!UICONTROL Add container]**&#x200B;을 선택합니다.

![](../images/ui/segment-builder/add-container.png)

새 컨테이너는 첫 번째 컨테이너의 자식으로 표시되지만 컨테이너를 드래그하여 이동하여 계층을 조정할 수 있습니다. 컨테이너의 기본 동작은 제공된 특성, 이벤트 또는 대상을 &quot;[!UICONTROL Include]&quot;으로 하는 것입니다. 타일 맨 위 왼쪽 모서리에서 **[!UICONTROL Include]**&#x200B;을 선택하고 &quot;[!UICONTROL Exclude]&quot;을 선택하여 컨테이너 기준과 일치하는 &quot;[!UICONTROL Exclude]&quot; 프로필로 규칙을 설정할 수 있습니다.

하위 컨테이너에서 &quot;컨테이너 감싸기 해제&quot;를 선택하여 하위 컨테이너를 추출하고 상위 컨테이너에 인라인을 추가할 수도 있습니다. 이 옵션에 액세스하려면 하위 컨테이너의 오른쪽 위 모서리에서 줄임표(...)를 선택합니다.

![](../images/ui/segment-builder/include-exclude.png)

**[!UICONTROL Unwrap container]**&#x200B;을 선택하면 하위 컨테이너가 제거되고 기준이 인라인으로 표시됩니다.

>[!NOTE]
>
>컨테이너를 래핑할 때는 논리가 원하는 세그먼트 정의를 계속 충족하도록 주의하십시오.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## 정책 병합

[!DNL Experience Platform] 여러 소스에서 데이터를 취합하여 각 개별 고객에 대한 전체 보기를 확인할 수 있습니다. 이 데이터를 함께 가져올 때 병합 정책은 데이터의 우선 순위를 지정하는 방법과 프로필을 만들기 위해 결합할 데이터를 결정하는 데 사용하는 규칙입니다.[!DNL Platform]

이 대상에 대한 마케팅 목적과 일치하는 병합 정책을 선택하거나 [!DNL Platform]에서 제공하는 기본 병합 정책을 사용할 수 있습니다. 고유한 기본 병합 정책을 만드는 것을 비롯하여 조직에 고유한 여러 병합 정책을 만들 수 있습니다. 조직에 대한 병합 정책을 만드는 방법에 대한 단계별 지침은 UI](../../profile/ui/merge-policies.md)을 사용하여 병합 정책을 사용하는 [의 자습서를 참조하십시오.

세그먼트 정의에 대한 병합 정책을 선택하려면 **[!UICONTROL Fields]** 탭에서 톱니바퀴 아이콘을 선택한 다음 **[!UICONTROL Merge Policy]** 드롭다운 메뉴를 사용하여 사용할 병합 정책을 선택합니다.

![](../images/ui/segment-builder/merge-policy-selector.png)

## 세그먼트 속성

세그먼트 정의를 작성할 때 작업 공간의 오른쪽에 있는 **[!UICONTROL Segment Properties]** 섹션에는 결과 세그먼트의 예상 크기가 표시되므로 대상 자체를 작성하기 전에 필요에 따라 세그먼트 정의를 조정할 수 있습니다.

**[!UICONTROL Segment Properties]** 섹션에서는 세그먼트 정의의 이름 및 설명을 포함하여 세그먼트 정의에 대한 중요한 정보를 지정할 수도 있습니다. 세그먼트 정의 이름은 조직에서 정의한 세그먼트 중에서 세그먼트를 식별하는 데 사용되므로 설명적이고 간결하며 고유해야 합니다.

세그먼트 정의를 계속 작성하면 **[!UICONTROL View Profiles]**&#x200B;을 선택하여 페이지의 대상이 아닌 미리 보기를 볼 수 있습니다.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>대상 추정은 해당 일의 샘플 데이터의 샘플 크기를 사용하여 생성됩니다. 프로필 스토어에 1백만 개 미만의 엔티티가 있는 경우 전체 데이터 세트가 사용됩니다.1백만~2천만 개의 개체 중 100만 개의 개체가 사용됩니다.2천만 개 이상의 개체에 대해 전체 엔티티의 5%가 사용됩니다. 세그먼트 예상 생성에 대한 자세한 내용은 세그먼트 작성 자습서의 [예측 생성 섹션](../tutorials/create-a-segment.md#estimate-and-preview-an-audience)에서 확인할 수 있습니다.

## 다음 단계 {#next-steps}

세그먼트 빌더는 [!DNL Real-time Customer Profile] 데이터에서 마케팅 가능한 대상을 분리할 수 있는 풍부한 워크플로우를 제공합니다. 이 안내서를 본 후 다음을 수행할 수 있습니다.

- 특성, 이벤트 및 기존 대상을 구성 요소로 조합하여 세그먼트 정의를 만듭니다.
- 규칙 빌더 캔버스 및 컨테이너를 사용하여 세그먼트 규칙이 실행되는 순서를 제어할 수 있습니다.
- 필요에 따라 세그먼트 정의를 조정할 수 있는 잠재 고객의 견적을 볼 수 있습니다.
- 예약된 세그먼테이션에 대해 모든 세그먼트 정의를 활성화합니다.
- 스트리밍 세그먼테이션에 지정된 세그먼트 정의를 활성화합니다.

[!DNL Segmentation Service]에 대한 자세한 내용을 보려면 설명서를 계속 읽고 관련 비디오를 시청하여 학습 내용을 보완하십시오. [!DNL Segmentation Service] UI의 다른 부분에 대한 자세한 내용은 [[!DNL Segmentation Service] 사용자 안내서](./overview.md)를 참조하십시오.
