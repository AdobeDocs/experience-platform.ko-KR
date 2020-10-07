---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;segmentation service;user guide;ui guide;segmentation ui guide;segment builder;Segment builder;
solution: Experience Platform
title: 세그멘테이션 서비스 세그먼트 빌더 사용 안내서
topic: ui guide
description: '세그먼트 빌더는 프로필 데이터 요소와 상호 작용할 수 있는 풍부한 작업 공간을 제공합니다. 작업 영역에서는 데이터 속성을 나타내는 데 사용되는 드래그 앤 드롭 타일과 같이 규칙을 작성하고 편집하기 위한 직관적인 컨트롤을 제공합니다. '
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '1723'
ht-degree: 0%

---


# [!DNL Segment Builder] 사용 안내서

[!DNL Segment Builder] 은 데이터 요소와 상호 작용할 수 있는 풍부한 작업 공간을 [!DNL Profile] 제공합니다. 작업 영역에서는 데이터 속성을 나타내는 데 사용되는 드래그 앤 드롭 타일과 같이 규칙을 작성하고 편집하기 위한 직관적인 컨트롤을 제공합니다.

![](../images/ui/segment-builder/segment-builder.png)

## 세그먼트 정의 구성 블록

세그먼트 정의의 기본 구성 요소는 속성 및 이벤트입니다. 또한 기존 대상에 포함된 특성과 이벤트를 새 정의에 대한 구성 요소로 사용할 수도 있습니다.

작업 영역의 왼쪽에 있는 **[!UICONTROL 필드]** 섹션에서 이러한 구성 요소를 [!DNL Segment Builder] 볼 수 있습니다. **[!UICONTROL 필드는]** 각 기본 구성 요소에 대한 탭을 포함합니다.&quot;[!UICONTROL 속성][!UICONTROL &quot;, &quot;]이벤트[!UICONTROL &quot; 및 &quot;]대상&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### 속성

[ **[!UICONTROL 속성]** ] 탭에서는 [!DNL Profile] [!DNL XDM Individual Profile] 클래스에 속한 속성을 검색할 수 있습니다. 각 폴더를 확장하여 추가 속성을 표시할 수 있습니다. 여기서 각 속성은 작업 영역의 가운데에 있는 규칙 빌더 캔버스로 드래그할 수 있는 타일입니다. 규칙 [빌더 캔버스에](#rule-builder-canvas) 대한 자세한 내용은 이 안내서 후반부에서 설명합니다.

![](../images/ui/segment-builder/attributes.png)

### 이벤트

[ **[!UICONTROL 이벤트]** ] 탭에서는 [!DNL XDM ExperienceEvent] 데이터 요소를 사용하여 발생한 이벤트 또는 작업을 기반으로 대상을 만들 수 있습니다. 또한 이벤트 탭에서 이벤트 유형을 **[!UICONTROL 찾을]** 수 있습니다. 이 탭은 세그먼트를 보다 신속하게 만들 수 있도록 일반적으로 사용되는 이벤트 컬렉션입니다.

요소를 검색할 수 있을 뿐만 아니라 이벤트 유형을 검색할 수도 [!DNL ExperienceEvent] 있습니다. 이벤트 유형에서는 올바른 이벤트를 찾는 [!DNL ExperienceEvents][!DNL XDM ExperienceEvent] 클래스를 검색하지 않고도 동일한 코딩 로직을 사용합니다. 예를 들어, 검색 막대를 사용하여 &quot;장바구니&quot;를 검색하면 세그먼트 정의를 작성할 때[!UICONTROL 매우 일반적으로 사용되는 두]가지 장바구니 작업인 &quot;AddCart[!UICONTROL &quot; 및 &quot;]RemoveCart&quot;가 반환됩니다.

Lucene의 검색 구문을 사용하는 검색 막대에 구성 요소의 이름을 입력하여 [모든 유형의 구성 요소를 검색할 수 있습니다](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 전체 단어가 입력되면 검색 결과가 채워지기 시작합니다. 예를 들어 XDM 필드를 기반으로 규칙을 만들려면 검색 필드 `ExperienceEvent.commerce.productViews`에 &quot;제품 보기&quot;를 입력하십시오. 단어 &quot;product&quot;를 입력하면 검색 결과가 표시됩니다. 각 결과에는 해당 개체가 속하는 개체 계층 구조가 포함됩니다.

>[!NOTE]
>
>조직에서 정의한 사용자 정의 스키마 필드는 표시되는 데 최대 24시간이 걸릴 수 있으며 빌드 규칙에 사용할 수 있습니다.

그런 다음 세그먼트 정의 [!DNL ExperienceEvents] 에 &quot;[!UICONTROL 이벤트 유형]&quot;을 드래그하여 놓을 수 있습니다.

![](../images/ui/segment-builder/events-eventTypes.png)

기본적으로 데이터 저장소에서 채워진 스키마 필드만 표시됩니다. 여기에는 &quot;[!UICONTROL 이벤트 유형&quot;이 포함됩니다]. &quot;이벤트 유형[!UICONTROL &quot; 목록이 보이지 않거나 &quot;]이벤트 유형[!UICONTROL &quot;으로 &quot;]임의의[!UICONTROL &quot;만]선택할 수 있는 경우, &quot;이벤트 유형 **&quot;으로** 선택할 **[!UICONTROL 수 있는 경우에만 &quot;]**&#x200B;임의의 **[!UICONTROL &quot;을]** 다음 **[!UICONTROL 아이콘을 선택하고 다음]**&#x200B;으로Twitter를 선택한 다음TwitterTwitter필드를 선택한 다음TwithoutCumfCuseCuseCuseXdm을 선택한 다음Cuse사용 가능한XfXfXpxPuts사용 가능한PdpXpspXpspPutsPutsPutsFPutsF사용 가능한FPuts사용 가능한FPutsPutsPutsPutsPutsPutsP 톱니바퀴 아이콘 **을 다시 선택하여** 필드 **[!UICONTROL 탭으로]** 돌아갈 수 있으며 이제 데이터가 포함되어 있는지 여부와 관계없이 여러 개의 &quot;[!UICONTROL 이벤트 유형]&quot;과 스키마 필드를 볼 수있습니다.

![](../images/ui/segment-builder/show-populated.png)

### 대상자

대상자 **[!UICONTROL 탭]** 은 Adobe Audience Manager과 같은 외부 소스에서 가져온 모든 대상뿐만 아니라 내부에서 만든 대상도 [!DNL Experience Platform]나열합니다.

대상 **[!UICONTROL 탭에서]** 사용 가능한 모든 소스를 폴더 그룹으로 볼 수 있습니다. 폴더를 선택하면 사용 가능한 하위 폴더와 대상을 볼 수 있습니다. 또한 폴더 구조를 보기 위해(오른쪽 이미지에 표시됨) 폴더 아이콘을 선택할 수 있으며(확인 표시는 현재 사용 중인 폴더를 의미함), 트리에서 폴더 이름을 선택하여 폴더를 다시 쉽게 탐색할 수 있습니다.

대상자 ⓘ 옆에 마우스를 두면 해당 ID, 설명 및 폴더 계층 구조 등 대상에 대한 정보를 보고 대상을 찾을 수 있습니다.

![](../images/ui/segment-builder/audience-folder-structure.png)

Lucene의 검색 구문을 활용하는 검색 막대를 사용하여 [대상을 검색할 수도 있습니다](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 대상 **** 탭에서 최상위 폴더를 선택하면 검색 막대가 나타나므로 해당 폴더 내에서 검색할 수 있습니다. 전체 단어를 입력하면 검색 결과가 채워지기 시작합니다. 예를 들어 이름이 지정된 대상을 찾으려면 검색 막대 `Online Shoppers`에 &quot;Online&quot;을 입력합니다. 단어 &quot;Online&quot;을 모두 입력하면 단어 &quot;Online&quot;이 포함된 검색 결과가 나타납니다.

## 규칙 빌더 캔버스 {#rule-builder-canvas}

세그먼트 정의는 대상 대상의 주요 특성이나 행동을 설명하는 데 사용되는 규칙 모음입니다. 이러한 규칙은 의 가운데에 있는 규칙 빌더 캔버스를 사용하여 만듭니다 [!DNL Segment Builder].

세그먼트 정의에 새 규칙을 추가하려면 필드 탭에서 **[!UICONTROL 타일을]** 드래그하여 규칙 빌더 캔버스에 놓습니다. 그런 다음 추가되는 데이터의 유형에 따라 컨텍스트별 옵션이 제공됩니다. 사용 가능한 데이터 유형은 다음과 같습니다.문자열, 날짜, [!DNL ExperienceEvents]&quot;[!UICONTROL 이벤트 유형]&quot; 및 대상

![](../images/ui/segment-builder/rule-builder-canvas.png)

### 대상자 추가

대상을 **[!UICONTROL 대상]** 탭에서 규칙 빌더 캔버스로 드래그하여 놓아 새 세그먼트 정의에서 대상 멤버십을 참조할 수 있습니다. 이렇게 하면 대상 멤버십을 새 세그먼트 규칙에 속성으로 포함 또는 제외할 수 있습니다.

를 사용하여 만든 [!DNL Platform] 대상의 경우 대상을 해당 대상의 세그먼트 정의에서 사용된 규칙 세트로 변환할 수 [!DNL Segment Builder]있는 옵션이 제공됩니다. 이 변환은 규칙 로직의 복사본을 만들며, 그런 다음 원래 세그먼트 정의에 영향을 주지 않고 수정할 수 있습니다. 세그먼트 정의를 규칙 논리로 변환하기 전에 최근에 변경한 내용을 저장했는지 확인하십시오.

>[!NOTE]
>
>외부 소스에서 대상을 추가하는 경우 대상 멤버십만 참조됩니다. 대상을 규칙으로 변환할 수 없으므로 원래 대상을 만드는 데 사용되는 규칙은 새 세그먼트 정의에서 수정할 수 없습니다.

![](../images/ui/segment-builder/add-audience-to-segment.png)

대상을 규칙으로 전환할 때 충돌이 발생하는 경우 기존 옵션을 최대한 그대로 유지하려 [!DNL Segment Builder] 합니다.

### 코드 보기

또는 에서 만든 규칙의 코드 기반 버전을 볼 수 있습니다 [!DNL Segment Builder]. 규칙 빌더 캔버스 내에서 규칙을 만들면 **[!UICONTROL 코드 보기를 선택하여]** 세그먼트를 PQL으로 볼 수 있습니다.

![](../images/ui/segment-builder/code-view.png)

코드 보기는 API 호출에 사용할 세그먼트 값을 복사할 수 있는 단추를 제공합니다. 최신 버전의 세그먼트를 가져오려면 세그먼트에 최신 변경 사항을 저장했는지 확인하십시오.

![](../images/ui/segment-builder/copy-code.png)

## 컨테이너

세그먼트 규칙은 나열된 순서대로 평가됩니다. 컨테이너는 중첩된 쿼리를 사용하여 실행 순서를 제어할 수 있습니다.

규칙 빌더 캔버스에 타일을 하나 이상 추가하면 컨테이너를 추가할 수 있습니다. 새 컨테이너를 만들려면 타일의 오른쪽 위 모서리에서 줄임표(...)를 선택한 다음 컨테이너 **[!UICONTROL 추가를 선택합니다]**.

![](../images/ui/segment-builder/add-container.png)

새 컨테이너는 첫 번째 컨테이너의 자식으로 표시되지만 컨테이너를 드래그하여 이동하여 계층을 조정할 수 있습니다. 컨테이너의 기본 동작은 제공된 특성, 이벤트 또는 대상을 &quot;[!UICONTROL 포함]&quot;하는 것입니다. 타일 맨 위 왼쪽 모서리에서 [포함]을 선택하고 &quot;[!UICONTROL 제외]&quot; **[!UICONTROL 를 선택하여]** 컨테이너 기준과 일치하는 &quot;[!UICONTROL 제외]&quot;프로필로 규칙을 설정할 수있습니다.

하위 컨테이너에서 &quot;컨테이너 감싸기 해제&quot;를 선택하여 하위 컨테이너를 추출하여 상위 컨테이너에 인라인을 추가할 수도 있습니다. 이 옵션에 액세스하려면 하위 컨테이너의 오른쪽 위 모서리에서 줄임표(...)를 선택합니다.

![](../images/ui/segment-builder/include-exclude.png)

컨테이너 **[!UICONTROL 의]** 감싸기 해제를 선택하면 하위 컨테이너가 제거되고 기준이 인라인으로 표시됩니다.

>[!NOTE]
>
>컨테이너 래핑 해제 시 로직이 원하는 세그먼트 정의를 계속 충족하는지 주의하십시오.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## 정책 병합

[!DNL Experience Platform] 여러 소스에서 데이터를 취합하여 각 개별 고객의 전체 상황을 파악할 수 있습니다. 이 데이터를 함께 가져올 때 병합 정책은 데이터의 우선 순위를 지정하는 방법과 프로필을 만들기 위해 결합할 데이터를 결정하는 데 [!DNL Platform] 사용하는 규칙입니다.

이 대상에 대한 마케팅 목적과 일치하는 병합 정책을 선택하거나 에서 제공하는 기본 병합 정책을 사용할 수 있습니다 [!DNL Platform]. 고유한 기본 병합 정책을 만드는 것을 비롯하여 조직에 고유한 여러 병합 정책을 만들 수 있습니다. 조직의 병합 정책을 만드는 방법에 대한 단계별 지침은 UI를 사용하여 병합 정책을 [사용하는 방법에 대한 자습서를 참조하십시오](../../profile/ui/merge-policies.md).

세그먼트 정의에 대한 병합 정책을 선택하려면 **[!UICONTROL 필드]** 탭에서 톱니바퀴 아이콘을 선택한 다음 정책 **[!UICONTROL 병합]** 드롭다운 메뉴를 사용하여 사용할 병합 정책을 선택합니다.

![](../images/ui/segment-builder/merge-policy-selector.png)

## 세그먼트 속성

세그먼트 정의를 작성할 때 작업 공간의 오른쪽에 있는 **[!UICONTROL 세그먼트 속성]** 섹션에 결과 세그먼트의 예상 크기가 표시되므로, 대상을 스스로 작성하기 전에 필요에 따라 세그먼트 정의를 조정할 수 있습니다.

세그먼트 **[!UICONTROL 속성]** 섹션에서는 세그먼트 정의에 대한 이름 및 설명을 포함하여 중요한 정보를 지정할 수도 있습니다. 세그먼트 정의 이름은 조직에서 정의한 세그먼트 중에서 세그먼트를 식별하는 데 사용되므로 설명적이고 간결하며 고유해야 합니다.

세그먼트 정의를 계속 작성하면 프로필 보기를 선택하여 페이지의 대상 미리 보기를 볼 **[!UICONTROL 수 있습니다]**.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>대상 추정은 해당 일의 샘플 데이터의 샘플 크기를 사용하여 생성됩니다. 프로필 스토어에 1백만 개 미만의 개체가 있는 경우 전체 데이터 세트가 사용됩니다.100만개에서 2000만개가 사용됩니다.2천만 개 이상의 개체에 대해 전체 개체의 5%가 사용됩니다. 세그먼트 예측 생성에 대한 자세한 내용은 세그먼트 작성 자습서의 [예측 생성 섹션](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 에서 확인할 수 있습니다.

## 다음 단계 및 추가 리소스 {#next-steps}

세그먼트 빌더는 마케팅 가능한 대상을 [!DNL Real-time Customer Profile] 데이터에서 분리할 수 있는 풍부한 워크플로우를 제공합니다. 이 가이드를 읽고 나면 다음을 수행할 수 있습니다.

- 속성, 이벤트 및 기존 대상을 구성 요소로 조합하여 세그먼트 정의를 만듭니다.
- 규칙 빌더 캔버스 및 컨테이너를 사용하여 세그먼트 규칙이 실행되는 순서를 제어할 수 있습니다.
- 필요에 따라 세그먼트 정의를 조정할 수 있는 잠재 고객에 대한 견적을 볼 수 있습니다.
- 예약된 세그먼테이션에 대해 모든 세그먼트 정의를 활성화합니다.
- 스트리밍 세그먼테이션에 지정된 세그먼트 정의를 활성화합니다.

자세한 내용 [!DNL Segmentation Service]을 살펴보려면 설명서를 계속 읽고 아래 비디오를 시청하여 학습 내용을 보완해 주십시오. UI의 다른 부분에 대한 자세한 내용은 [!DNL Segmentation Service] [[!DNL Segmentation Service] 사용 안내서를 참조하십시오.](./overview.md)

>[!WARNING]
>
> 다음 비디오에 표시된 [!DNL Platform] UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

**세그먼트 만들기:**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**동적 세그먼트 만들기:**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)