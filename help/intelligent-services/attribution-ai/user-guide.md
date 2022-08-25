---
keywords: Experience Platform;사용 안내서;속성 ai;인기 항목;지역
feature: Attribution AI
title: Attribution AI UI 안내서
topic-legacy: User guide
description: 이 문서는 Intelligent Services 사용자 인터페이스의 Attribution AI과 상호 작용하기 위한 안내서의 역할을 합니다.
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: 67b4c49de6ebb9986f735390a0657d908b07e039
workflow-type: tm+mt
source-wordcount: '2705'
ht-degree: 1%

---

# Attribution AI UI 안내서

Attribution AI은 지능형 서비스의 일부로서 멀티 채널, 알고리즘 기반의 어트리뷰션 서비스로, 지정된 결과에 대한 고객 상호 작용의 영향과 점진적 효과를 계산합니다. 마케터는 Attribution AI를 통해 고객 여정의 각 단계에서 개별 고객과의 인터랙션이 미치는 영향을 파악하여 마케팅 및 광고 비용을 측정하고 최적화할 수 있습니다.

이 문서는 Intelligent Services 사용자 인터페이스의 Attribution AI과 상호 작용하기 위한 안내서의 역할을 합니다.

## 인스턴스 만들기

에서 [!DNL Adobe Experience Platform] UI, 선택 **[!UICONTROL 서비스]** 을 클릭합니다. 다음 **[!UICONTROL 서비스]** 브라우저가 나타나고 사용 가능한 Adobe intelligent services가 표시됩니다. Attribution AI 컨테이너에서 **[!UICONTROL 열기]**.

![인스턴스에 액세스](./images/user-guide/open_Attribution_ai.png)

Attribution AI 서비스 페이지가 나타납니다. 이 페이지에는 Attribution AI의 서비스 인스턴스가 나열되며 인스턴스 이름, 전환 이벤트, 인스턴스가 실행되는 빈도 및 마지막 업데이트 상태 등 이러한 인스턴스에 대한 정보가 표시됩니다.

다음 항목이 있습니다. **[!UICONTROL 점수가 지정된 총 전환 이벤트]** 의 오른쪽 하단에 있는 지표 **[!UICONTROL 인스턴스 만들기]** 컨테이너. 이 지표는 모든 샌드박스 환경 및 삭제된 서비스 인스턴스를 포함하여 현재 달력 연도 동안 Attribution AI이 점화한 총 전환 이벤트 수를 추적합니다.

![총 전환](./images/user-guide/total_conversions.png)

UI 오른쪽의 컨트롤을 사용하여 서비스 인스턴스를 편집, 복제 및 삭제할 수 있습니다. 이러한 컨트롤을 표시하려면 기존 컨트롤에서 인스턴스를 선택합니다 **[!UICONTROL 서비스 인스턴스]**. 컨트롤에는 다음 정보가 포함됩니다.

- **[!UICONTROL 편집]**: 선택 **[!UICONTROL 편집]** 기존 서비스 인스턴스를 수정할 수 있습니다. 인스턴스의 이름, 설명, 상태 및 점수 주기를 편집할 수 있습니다.
- **[!UICONTROL 복제]**: 선택 **[!UICONTROL 복제]** 선택한 서비스 인스턴스를 복사합니다. 그런 다음 워크플로우를 수정하여 작은 수정 사항을 만들고 새 인스턴스로 이름을 변경할 수 있습니다.
- **[!UICONTROL 삭제]**: 임의의 기록 실행을 포함하는 서비스 인스턴스를 삭제할 수 있습니다.
- **[!UICONTROL 데이터 소스]**: 사용 중인 데이터 세트에 대한 링크. Attribution AI에서 두 개 이상의 데이터 세트를 사용 중인 경우 &quot;복수&quot; 다음에 데이터 세트 수가 표시됩니다. 하이퍼링크를 선택하면 데이터 세트 미리 보기 팝오버가 표시됩니다.
- **[!UICONTROL 마지막 실행 세부 사항]**: 실행이 실패한 경우에만 표시됩니다. 오류 코드와 같이 실행이 실패한 이유에 대한 정보가 여기에 표시됩니다.

![사이드 창](./images/user-guide/multiple-datasets-pane.png)

- **[!UICONTROL 전환 이벤트]**: 이 인스턴스에 대해 구성된 전환 이벤트에 대한 빠른 개요입니다.
- **[!UICONTROL 전환 확인 기간]**: 전환 이벤트 터치포인트가 포함되기 전 며칠 수를 나타내는 정의한 기간입니다.
- **[!UICONTROL 터치포인트]**: 이 인스턴스를 만들 때 정의한 모든 터치포인트 목록입니다.

![](./images/user-guide/side_panel_2.png)

선택 **[!UICONTROL 인스턴스 만들기]** 을 가리키도록 업데이트하는 것이 좋습니다.

![인스턴스 만들기](./images/user-guide/landing_page.png)

다음으로, 서비스 인스턴스에 대한 이름 및 선택적 설명을 제공할 수 있는 Attribution AI 설정 페이지가 나타납니다.

![인스턴스 이름 지정](./images/user-guide/naming_instance.png)

## 데이터 선택 {#select-data}

<!-- https://www.adobe.com/go/aai-select-data -->

계획별로, Attribution AI은 Adobe Analytics, 경험 이벤트 및 소비자 경험 이벤트 데이터를 사용하여 속성 점수를 계산할 수 있습니다. 데이터 세트를 선택할 때는 Attribution AI과 호환되는 데이터 세트만 나열됩니다. 데이터 세트를 선택하려면 (**+**) 데이터 세트 이름 옆에 있는 기호를 선택하거나 확인란을 선택하여 여러 데이터 세트를 한 번에 추가합니다. 검색 옵션을 사용하여 관심 있는 데이터 세트를 신속하게 찾을 수도 있습니다.

사용할 데이터 세트를 선택한 후 **[!UICONTROL 추가]** 데이터 세트 미리 보기 창에 데이터 세트를 추가하는 단추.

![데이터 세트 선택](./images/user-guide/select-datasets.png)

정보 아이콘 선택 ![정보 아이콘](./images/user-guide/info-icon.png) 데이터 세트 옆에 데이터 세트 미리 보기 팝오버가 열립니다.

![데이터 세트 선택 및 검색](./images/user-guide/dataset-preview.png)

데이터 집합 미리 보기에는 마지막 업데이트 시간, 소스 스키마 및 처음 10개 열의 미리 보기와 같은 데이터가 포함되어 있습니다.

### 데이터 집합 완결성 {#dataset-completeness}

<!-- https://www.adobe.com/go/aai-dataset-completeness -->

데이터 집합 미리 보기에서 데이터 집합 완결성 비율 값입니다. 이 값은 데이터 세트에 비어 있거나 null인 열 수에 대한 빠른 스냅숏을 제공합니다. 데이터 세트에 누락된 값이 많이 포함되어 있고 이러한 값이 다른 곳에서 캡처되는 경우 누락된 값이 포함된 데이터 세트를 포함하는 것이 좋습니다.

>[!NOTE]
>
>데이터 집합 완전성은 Attribution AI(1년)의 최대 교육 기간을 사용하여 계산됩니다. 즉, 데이터 세트 완결성 값을 표시할 때 1년 이상의 데이터를 고려하지 않습니다.

![데이터 집합 완결성](./images/user-guide/dataset-completeness.png)

### ID 선택 {#identity}

이제 ID 맵(필드)을 기반으로 여러 데이터 세트를 서로 결합할 수 있습니다. ID 유형(&quot;ID 네임스페이스&quot;라고도 함)과 해당 네임스페이스 내의 ID 값을 선택해야 합니다. 동일한 네임스페이스 아래에 두 개 이상의 필드를 스키마 내에 ID로 할당한 경우 네임스페이스가 앞에 추가하는 ID 드롭다운에 할당된 모든 ID 값이 표시됩니다 `EMAIL (personalEmail.address)` 또는 `EMAIL (workEmail.address)`.

>[!IMPORTANT]
>
>선택하는 모든 데이터 세트에 대해 동일한 ID 유형(네임스페이스)을 사용해야 합니다. ID 열 내의 ID 유형 옆에 데이터 세트가 호환되는지를 나타내는 녹색 확인 표시가 나타납니다. 예를 들어 Phone 네임스페이스를 사용하는 경우 `mobilePhone.number` 식별자로 나머지 데이터 세트에 대한 모든 식별자는 Phone 네임스페이스를 사용하여 이 식별자를 포함해야 합니다.

ID를 선택하려면 ID 열에 있는 밑줄이 있는 값을 선택합니다. ID 선택 팝오버가 나타납니다.

![동일한 네임스페이스 선택](./images/user-guide/aai-identity-map.png)

네임스페이스 내에서 두 개 이상의 ID를 사용할 수 있는 경우 사용 사례에 대한 올바른 ID 필드를 선택해야 합니다. 예를 들어 이메일 네임스페이스, 작업 및 개인 이메일 내에 두 개의 이메일 ID를 사용할 수 있습니다. 사용 사례에 따라 개인 이메일은 보다 많이 채워질 가능성이 높고 개별 예측에 더 유용합니다. 즉, `EMAIL (personalEmail.address)` ID로 사용

![데이터 집합 키를 선택하지 않았습니다.](./images/user-guide/aai-identity-namespace.png)

>[!NOTE]
>
> 데이터 세트에 유효한 ID 유형(네임스페이스)이 없는 경우 기본 ID를 설정하고 을(를) 사용하여 ID 네임스페이스에 할당해야 합니다 [스키마 편집기](../../xdm/schema/composition.md#identity). 네임스페이스와 ID에 대해 자세히 알아보려면 [ID 서비스 네임스페이스](../../identity-service/namespaces.md) 설명서.

## 미디어 채널 및 캠페인 필드 매핑 {#aai-mapping}

<!-- https://www.adobe.com/go/aai-mapping -->

데이터 세트 선택 및 추가를 완료하면 **맵** 구성 단계가 나타납니다. Attribution AI을 사용하려면 이전 단계에서 선택한 각 데이터 세트에 대한 미디어 채널 필드를 매핑해야 합니다. 데이터 세트 간 미디어 채널 매핑이 없으면 Attribution AI에서 파생된 인사이트가 제대로 표시되지 않아 인사이트 페이지를 해석하기 어렵습니다. 미디어 채널만 필요하지만 미디어 작업, 캠페인 이름, 캠페인 그룹 및 캠페인 태그와 같은 일부 선택적 필드를 매핑하는 것이 좋습니다. 이렇게 하면 Attribution AI이 보다 명확한 통찰력과 최적의 결과를 제공할 수 있습니다.

![매핑](./images/user-guide/mapping.png)

## 이벤트 정의 {#define-events}

<!-- https://www.adobe.com/go/aai-define-events -->

이벤트를 정의하는 데 사용되는 입력 데이터 유형에는 세 가지가 있습니다.

- **전환 이벤트:** 전자 상거래 주문, 매장 내 구매 및 웹 사이트 방문과 같은 마케팅 활동의 영향을 식별하는 비즈니스 목표입니다.
- **전환 확인 기간:** 전환 이벤트 터치포인트를 포함하기 전 며칠 수를 나타내는 시간대를 제공합니다.
- **터치포인트:** 전환의 숫자 또는 매출 기반 영향을 평가하는 데 사용되는 수신자, 개인 및 쿠키 수준 마케팅 이벤트.

### 전환 이벤트 정의 {#define-conversion-events}

전환 이벤트를 정의하려면 이벤트에 이름을 지정하고 **데이터 세트 및 필드 선택** 드롭다운 메뉴 아래의 제품에서 사용할 수 있습니다.

![yes 드롭다운](./images/user-guide/define-conversion-events.png)

이벤트를 선택하면 해당 오른쪽에 새 드롭다운이 나타납니다. 두 번째 드롭다운은 작업을 사용하여 이벤트에 추가 컨텍스트를 제공하는 데 사용됩니다. 이 전환 이벤트의 경우 기본 작업입니다 *존재* 이 사용됩니다.

>[!NOTE]
>
>다음 아래의 문자열 *전환 이름* 은 이벤트를 정의할 때 업데이트됩니다.

![드롭다운 없음](./images/user-guide/conversion_event_1.png)

그런 다음 이전 단계에서 모든 입력 데이터 세트를 결합하여 생성되는 결합된 데이터 세트를 선택할 수 있습니다. 또는 **데이터 세트 및 필드 선택** 드롭다운 메뉴 아래의 제품에서 사용할 수 있습니다.

다음 **[!UICONTROL 이벤트 추가]** 및 **[!UICONTROL 그룹 추가]** 전환을 더 정의하는 데 버튼이 사용됩니다. 정의하는 변환에 따라 다음을 사용해야 할 수 있습니다 **[!UICONTROL 이벤트 추가]** 및 **[!UICONTROL 그룹 추가]** 추가 컨텍스트를 제공하는 단추입니다.

![이벤트 추가](./images/user-guide/add_event.png)

선택 **[!UICONTROL 이벤트 추가]** 위에서 설명한 것과 동일한 방법을 사용하여 채울 수 있는 추가 필드를 만듭니다. 이렇게 하면 변환 이름 아래의 문자열 정의에 AND 문이 추가됩니다. 을(를) 선택합니다 **x** 를 클릭하여 추가된 이벤트를 제거합니다.

![이벤트 메뉴 추가](./images/user-guide/add_event_result.png)

선택 **[!UICONTROL 그룹 추가]** 은 원본과 별도로 추가 필드를 만드는 옵션을 제공합니다. 그룹이 추가되면 파란색 *및* 버튼이 나타납니다. 선택 **및** &quot;Or&quot;를 포함할 매개 변수를 변경하는 옵션을 제공합니다. 또는 는 여러 개의 성공적인 전환 경로를 정의하는 데 사용됩니다. &quot;및&quot;은 추가 조건을 포함하도록 전환 경로를 확장합니다.

![및 또는](./images/user-guide/and_or.png)

둘 이상의 전환이 필요한 경우 **전환 추가** 새 변환 카드를 만들려면 위의 프로세스를 반복하여 전환을 여러 개 정의할 수 있습니다.

![전환 추가](./images/user-guide/add_conversion.png)

### 전환 확인 기간 정의 {#lookback-window}

전환 정의를 완료한 후 전환 확인 기간을 확인해야 합니다. 화살표 키를 사용하거나 기본값(56)을 선택하여 터치포인트를 포함할 전환 이벤트까지 남은 일 수를 지정합니다. 터치포인트는 다음 단계에서 정의됩니다.

![전환 확인](./images/user-guide/lookback_window.png)

### 터치포인트 정의

터치포인트를 정의하는 작업은 다음과 유사한 워크플로우를 따릅니다 [전환 정의](#define-conversion-events). 처음에는 터치 포인트에 이름을 지정하고 *필드 이름 입력* 드롭다운 메뉴 아래의 제품에서 사용할 수 있습니다. 선택하면 기본값 &quot;exists&quot;가 있는 연산자 드롭다운이 나타납니다. 드롭다운을 선택하여 연산자 목록을 표시합니다.

![연산자](./images/user-guide/operators.png)

이 터치포인트의 목적에 대해 을(를) 선택합니다. **다음과 같음**.

![1단계](./images/user-guide/touchpoint_step1.png)

터치 포인트에 대한 연산자가 선택되면, *필드 값 입력* 을 사용할 수 있습니다. 에 대한 드롭다운 값 *필드 값 입력* 이전에 선택한 연산자 및 터치 포인트 값을 기준으로 채웁니다. 드롭다운에서 값이 채워지지 않으면 해당 값을에 수동으로 입력할 수 있습니다. 드롭다운을 선택하고 을(를) 선택합니다 **클릭**.

>[!NOTE]
>
>연산자 &quot;존재함&quot; 및 &quot;존재하지 않음&quot;에는 연산자와 연결된 필드 값이 없습니다.

![터치 포인트 드롭다운](./images/user-guide/touchpoint_dropdown.png)

다음 **이벤트 추가** 및 **그룹 추가** 버튼은 터치포인트를 추가로 정의하는 데 사용됩니다. 터치포인트를 둘러싼 복잡한 특성 때문에 단일 터치포인트에 대한 여러 이벤트 및 그룹이 있는 것은 일반적이지 않습니다.

선택한 경우, **이벤트 추가** 을(를) 통해 추가 필드를 추가할 수 있습니다. 선택 **x** 를 클릭하여 추가된 이벤트를 제거합니다.

![이벤트 추가](./images/user-guide/touchpoint_add_event.png)

선택 **그룹 추가** 원본과 별도로 추가 필드를 만드는 선택 사항을 제공합니다. 그룹이 추가되면 파란색 *및* 버튼이 나타납니다. 선택 **및** 매개 변수를 변경하려면 새 매개 변수 &quot;Or&quot;를 사용하여 여러 개의 성공적인 경로를 정의합니다. 이 특정 터치 포인트에는 하나의 성공적인 경로만 있으므로 &quot;Or&quot;가 필요하지 않습니다.

![터치 포인트 개요](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>아래의 문자열 사용 *터치 포인트 이름* 터치 포인트에 대한 간단한 개요를 살펴보십시오. 문자열이 터치 포인트의 이름과 일치하는지 확인합니다.

![](./images/user-guide/touchpoint_string.png)

을(를) 선택하여 추가 터치포인트를 추가할 수 있습니다 **터치 포인트 추가** 위의 프로세스를 반복합니다.

![터치 포인트 추가](./images/user-guide/add_touchpoint.png)

필요한 모든 터치포인트를 정의했으면 위로 스크롤하여 선택합니다 **다음** 오른쪽 상단 모서리에서 최종 단계로 진행합니다.

![완성된 정의](./images/user-guide/define_event_next.png)

## 고급 교육 및 점수 설정

Attribution AI의 마지막 페이지는 **[!UICONTROL 고급]** 교육 및 점수 설정에 사용되는 페이지입니다.

![새 페이지 고급](./images/user-guide/advanced_settings.png)

### 교육 일정 예약

사용 *예약*&#x200B;를 채울 요일과 시간을 선택할 수 있습니다.

아래에서 드롭다운을 선택합니다. *점수 주기* 일별, 주별 및 월별 점수 중에서 선택합니다. 다음으로, 점수를 받을 요일을 선택합니다. 여러 일을 선택할 수 있습니다. 같은 날을 다시 선택하면 선택 취소됩니다.

![교육 일정 예약](./images/user-guide/schedule_training.png)

점수를 매길 시간을 변경하려면 시계 아이콘을 선택합니다. 표시되는 새 오버레이에서 점수부여 작업을 수행할 시간을 입력합니다. 오버레이 외부를 선택하여 닫습니다.

>[!NOTE]
>
>각 점수 프로세스를 완료하는 데 최대 24시간이 걸릴 수 있습니다.

![시계 아이콘](./images/user-guide/time_of_day.png)

### 추가 점수 데이터 세트 열(선택 사항)

기본적으로 표준 스키마의 각 서비스 인스턴스에 대해 점수 데이터 세트가 만들어집니다. 전환 이벤트 및 터치포인트 구성을 기반으로 추가 열을 점수 데이터 세트 출력에 추가할 수 있습니다. 먼저 입력 데이터 세트에서 열을 선택하면 해당 열을 드래그하여 놓아 햄버거 아이콘 위에 마우스 왼쪽 버튼을 눌러 순서를 변경할 수 있습니다.

![점수 데이터 집합 열 추가](./images/user-guide/Add-score-dataset.png)

### 지역 기반 모델링(선택 사항) {#region-based-modeling-optional}

고객의 행동이 국가 및 지역에 따라 크게 다를 수 있습니다. 글로벌 기업의 경우 국가 기반 또는 지역 기반 모델을 사용하면 속성 정확도를 높일 수 있습니다. 추가된 각 영역은 해당 지역의 데이터를 사용하여 새 모델을 생성합니다.

새 영역을 정의하려면 먼저 **[!UICONTROL 영역 추가]**. 나타나는 컨테이너에서 영역의 이름을 입력합니다. 한 값(&quot;placeContext.geo.countryCode&quot;)만 **[!UICONTROL 필드 이름 입력]** 드롭다운. 이 값을 선택합니다.

![지역 선택](./images/user-guide/select_region_att.png)

다음으로 연산자를 선택합니다.

![지역 연산자](./images/user-guide/region_operators.png)

끝으로, 에서 국가 코드를 입력합니다. **[!UICONTROL 필드 값 입력]** 드롭다운.

>[!NOTE]
>
>국가 코드는 두 자 길이입니다. 전체 목록은 여기에서 찾을 수 있습니다 [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![지역](./images/user-guide/region-based.png)

### 교육 창 {#training-window}

가장 정확한 모델을 얻을 수 있도록 비즈니스를 나타내는 이전 데이터로 모델을 교육하는 것이 중요합니다. 기본적으로 모델은 전환 이벤트 데이터의 2/4분기(6개월)를 사용하여 교육을 받습니다. 드롭다운을 선택하여 기본값을 변경합니다. 1~4분기(3~12개월)의 데이터를 사용하여 교육을 실시하도록 선택할 수 있습니다.

>[!NOTE]
>
>더 짧은 교육 기간은 최근 트렌드에 더 민감하지만, 더 긴 교육 기간은 더 강력한 모델을 만들고 최신 트렌드에 덜 민감합니다.

![교육 창](./images/user-guide/training_window.png)

교육 창을 선택하면 **[!UICONTROL 완료]** 오른쪽 상단 모서리에서 데이터를 처리할 시간을 허용합니다. 완료되면 인스턴스 설정이 완료되었음을 확인하는 팝업 대화 상자가 나타납니다. 선택 **[!UICONTROL 확인]** 으로 리디렉션됩니다. **[!UICONTROL 서비스 인스턴스]** 서비스 인스턴스를 볼 수 있는 페이지입니다.

![설치 완료](./images/user-guide/instance_setup_complete.png)

## 속성 기반 액세스 제어

>[!IMPORTANT]
>
>속성 기반 액세스 제어는 현재 제한된 릴리스에서만 사용할 수 있습니다.

[속성 기반 액세스 제어](../../../help/access-control/abac/overview.md) 는 관리자가 속성을 기반으로 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있도록 해주는 Adobe Experience Platform의 기능입니다. 속성은 스키마 필드나 세그먼트에 추가된 레이블과 같이 객체에 추가된 메타데이터일 수 있습니다. 관리자는 사용자 액세스 권한을 관리하기 위한 속성을 포함하는 액세스 정책을 정의합니다.

이 기능을 사용하면 조직 또는 데이터 사용 범위를 정의하는 레이블을 사용하여 XDM(Experience Data Model) 스키마 필드에 레이블을 지정할 수 있습니다. 동시에 관리자는 사용자 및 역할 관리 인터페이스를 사용하여 XDM 스키마 필드를 둘러싼 액세스 정책을 정의하고 사용자 또는 사용자 그룹(내부, 외부 또는 타사 사용자)에 부여된 액세스를 더 잘 관리할 수 있습니다. 또한 속성 기반 액세스 제어를 사용하여 관리자가 특정 세그먼트에 대한 액세스를 관리할 수 있습니다.

속성 기반 액세스 제어를 통해 관리자는 모든 플랫폼 워크플로우 및 리소스에서 중요한 SPD(개인 데이터)와 PII(개인 식별 정보)에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 해당 필드에 해당하는 특정 필드 및 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.

특성 기반 액세스 제어로 인해 일부 필드 및 기능에는 액세스가 제한되어 특정 Attribution AI 서비스 인스턴스에 사용할 수 없을 수 있습니다. 예를 들면 &quot;Identity&quot;, &quot;Score Definition&quot; 및 &quot;Clone&quot;이 있습니다.

Attribution AI 작업 공간 상단에서 **통찰력 페이지**&#x200B;로 지정하는 경우, 사이드바에 표시되는 세부 정보는 액세스가 제한되었습니다.

![제한된 스키마 필드가 강조 표시된 Attribution AI 작업 영역입니다.](./images/user-guide/access-restricted.png)

에서 제한된 스키마가 있는 데이터 세트를 선택하는 경우 **[!UICONTROL 인스턴스 만들기 워크플로우]** 페이지가 표시되면 메시지가 있는 데이터 세트 이름 옆에 경고 기호가 나타납니다. [!UICONTROL 제한된 정보는 제외됩니다].

![제한된 데이터 세트 필드가 강조 표시된 Attribution AI 작업 공간입니다.](./images/user-guide/restricted-info-excluded.png)

에서 제한된 스키마가 있는 데이터 세트를 미리 볼 때 **[!UICONTROL 인스턴스 만들기 워크플로우]** 페이지를 보면 [!UICONTROL 액세스 제한 사항으로 인해 데이터 집합 미리 보기에 특정 정보가 표시되지 않습니다.]

![제한된 미리 보기 스키마 필드가 있는 Attribution AI 작업 공간 결과가 강조 표시됩니다.](./images/user-guide/restricted-dataset-preview.png)

제한된 정보로 인스턴스를 만든 후 **[!UICONTROL 목표 정의]** 단계에서 경고가 맨 위에 표시됩니다. [!UICONTROL 액세스 제한 사항으로 인해 구성에 특정 정보가 표시되지 않습니다.]

![인스턴스의 제한된 필드가 있는 Attribution AI 작업 영역은 강조 표시됩니다.](./images/user-guide/information-not-displayed.png)

## 다음 단계

이 자습서를 따라 Attribution AI에 서비스 인스턴스를 만들었습니다. 인스턴스가 점수가 끝나면(최대 24시간 허용) 다음 작업을 수행할 수 있습니다 [Attribution AI 인사이트 살펴보기](./discover-insights.md). 또한 점수 결과를 다운로드하려면 다음을 방문하십시오. [점수 다운로드](./download-scores.md) 설명서.

## 추가 리소스

다음 비디오에서는 Attribution AI에서 새 인스턴스를 만들기 위한 종단 간 워크플로우를 간략하게 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
