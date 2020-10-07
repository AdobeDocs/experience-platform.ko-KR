---
keywords: Experience Platform;user guide;attribution ai;popular topics;region
solution: Experience Platform
title: Attribution AI 사용 안내서
topic: User guide
description: 이 문서는 Intelligent Services 사용자 인터페이스에서 Attribution AI과 상호 작용하기 위한 가이드 역할을 합니다.
translation-type: tm+mt
source-git-commit: c5e2ea5daf813bf580a11f0182361197e55c6fe8
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 0%

---


# Attribution AI 사용 안내서

Attribution AI은 지능형 서비스의 일부로 고객 상호 작용이 특정 결과에 미치는 영향과 점진적인 영향을 계산하는 다중 채널 알고리즘 속성 서비스입니다. 마케터는 Attribution AI을 통해 고객 여정의 각 단계에서 개별 고객과의 인터랙션이 미치는 영향을 파악하여 마케팅 및 광고 비용을 측정하고 최적화할 수 있습니다.

이 문서는 Intelligent Services 사용자 인터페이스에서 Attribution AI과 상호 작용하기 위한 가이드 역할을 합니다.

## 인스턴스 만들기

UI [!DNL Adobe Experience Platform] 에서 왼쪽 탐색 **[!UICONTROL 영역에서 서비스]** 를 클릭합니다. 서비스 **[!UICONTROL 브라우저가]** 나타나고 사용 가능한 Adobe 지능형 서비스가 표시됩니다. Attribution AI 컨테이너에서 열기를 **[!UICONTROL 클릭합니다]**.

![인스턴스 액세스](./images/user-guide/open_Attribution_ai.png)

Attribution AI 서비스 페이지가 나타납니다. 이 페이지에는 Attribution AI의 서비스 인스턴스가 나열되며 인스턴스 이름, 전환 이벤트, 인스턴스 실행 횟수, 마지막 업데이트 상태 등에 대한 정보가 표시됩니다. 시작하려면 **인스턴스** 만들기를 클릭합니다.

![인스턴스 만들기](./images/user-guide/landing_page.png)

그런 다음 Attribution AI의 설정 페이지가 나타납니다. 이 페이지에서 기본 정보를 제공하고 인스턴스의 데이터 세트를 지정할 수 있습니다.

![설정 페이지](./images/user-guide/setup_attribution.png)

### 인스턴스 이름 지정

[ **[!UICONTROL 기본 정보]**]에서 서비스 인스턴스에 대한 이름과 선택적 설명을 제공합니다.

![인스턴스 이름 지정](./images/user-guide/naming_instance.png)

### 데이터 세트 선택

기본 정보를 채운 후 데이터 세트 선택 **이라는 드롭다운** 드롭다운을 클릭하여 데이터 세트를 선택합니다. 데이터 세트는 모델을 교육하는 데 사용되며, 생성된 후속 데이터에 점수를 매깁니다. 드롭다운 선택기에서 데이터 세트를 선택하면 Attribution AI과 호환되고 XDM(Experience Data Model) 스키마를 준수하는 데이터세트만 나열됩니다. 데이터 세트를 선택하고 **오른쪽** 상단 모서리에서 다음을 클릭하여 이벤트 정의 페이지로 이동합니다.

![설정 페이지](./images/user-guide/initial_creation_attribution.png)

## 이벤트 정의

이벤트를 정의하는 데 사용되는 입력 데이터 유형에는 세 가지가 있습니다.

- **전환 이벤트:** 전자 상거래 주문, 매장 내 구매 및 웹 사이트 방문과 같은 마케팅 활동의 영향을 식별하는 비즈니스 목표
- **조회 창:** 전환 이벤트 터치포인트를 포함하기 전 며칠을 나타내는 기간을 제공합니다.
- **터치포인트:** 전환의 숫자 또는 매출 기반 영향을 평가하는 데 사용되는 수신자, 개인 및 쿠키 수준 마케팅 이벤트.

### 전환 이벤트 정의 {#define-conversion-events}

전환 이벤트를 정의하려면 [필드 이름 **입력] 드롭다운 메뉴를 클릭하여 이벤트에 이름을 지정하고 이벤트 유형을 선택해야** 합니다.

![예 드롭다운](./images/user-guide/conversion_event_2.png)

이벤트를 선택하면 새 드롭다운이 오른쪽에 나타납니다. 두 번째 드롭다운은 작업을 사용하여 이벤트에 추가적인 컨텍스트를 제공하는 데 사용됩니다. 이 전환 이벤트의 경우 기본 작업 *이* 사용됩니다.

>[!NOTE]
>
>이벤트를 정의하면 *전환 이름* 아래의 문자열이 업데이트됩니다.

![드롭다운 없음](./images/user-guide/conversion_event_1.png)

이벤트 **[!UICONTROL 추가]** 및 **[!UICONTROL 그룹]** 추가 단추를 사용하여 변환을 추가로 정의합니다. 정의하는 변환에 따라 추가 컨텍스트를 제공하기 위해 이벤트 **[!UICONTROL 추가]** 및 그룹 **** 추가 단추를 사용해야 할 수 있습니다.

![이벤트 추가](./images/user-guide/add_event.png)

이벤트 **[!UICONTROL 추가를 클릭하면]** 위에 설명한 것과 동일한 방법으로 입력할 수 있는 추가 필드가 만들어집니다. 이렇게 하면 전환 이름 아래의 문자열 정의에 AND 문이 추가됩니다. 추가된 이벤트를 **제거하려면** x를 클릭합니다.

![이벤트 메뉴 추가](./images/user-guide/add_event_result.png)

그룹 **[!UICONTROL 추가를]** 클릭하면 원본과 별도로 추가 필드를 만들 수 있는 옵션이 제공됩니다. 그룹이 추가되면 파란색 *및* 단추가 나타납니다. And **를** 클릭하면 매개 변수를 &quot;Or&quot;로 변경하는 옵션이 제공됩니다. &quot;Or&quot;은 여러 개의 성공적인 전환 경로를 정의하는 데 사용됩니다. &quot;And&quot;는 추가 조건을 포함하도록 전환 경로를 확장합니다.

![and 또는](./images/user-guide/and_or.png)

두 개 이상의 전환이 필요한 경우 **전환** 추가를 클릭하여 새 전환 카드를 만듭니다. 위의 프로세스를 반복하여 전환을 여러 개 정의할 수 있습니다.

![전환 추가](./images/user-guide/add_conversion.png)

### 룩백 창 정의 {#lookback-window}

전환 정의를 완료한 후에는 조회 창을 확인해야 합니다. 화살표 키를 사용하거나 기본값(56)을 클릭하여 터치포인트를 포함할 전환 이벤트까지 남은 일 수를 지정합니다. 터치포인트는 다음 단계에서 정의됩니다.

![lookback](./images/user-guide/lookback_window.png)

### 터치포인트 정의

터치포인트를 정의하는 작업은 전환 [을 정의하는 비슷한 워크플로우를 따릅니다](#define-conversion-events). 처음에는 터치포인트의 이름을 지정하고 [필드 이름 입력] 드롭다운 메뉴에서 *터치포인트 값을* 선택해야 합니다. 선택하면 연산자 드롭다운에 기본값 &quot;exists&quot;가 표시됩니다. 드롭다운을 클릭하여 연산자 목록을 표시합니다.

![연산자](./images/user-guide/operators.png)

이 터치포인트의 경우 **같음**&#x200B;을 선택합니다.

![단계 1](./images/user-guide/touchpoint_step1.png)

터치포인트의 연산자를 선택하면 필드 값 *입력* 기능을 사용할 수 있습니다. 필드 값 *입력* 드롭다운 값은 이전에 선택한 연산자 및 터치포인트 값을 기반으로 채워집니다. 드롭다운에 값이 채워지지 않으면 해당 값을 수동으로 입력할 수 있습니다. 드롭다운을 클릭하고 **클릭을 선택합니다**.

>[!NOTE]
>
>&quot;exists&quot; 및 &quot;not exists&quot; 연산자에게는 필드 값이 연결되어 있지 않습니다.

![터치포인트 드롭다운](./images/user-guide/touchpoint_dropdown.png)

이벤트 *추가* 및 *그룹* 추가 단추를 사용하여 터치포인트를 추가로 정의합니다. 터치포인트를 둘러싼 복잡한 특성 때문에 하나의 터치포인트에 대해 여러 이벤트와 그룹이 있는 것이 일반적입니다.

클릭하면 **이벤트** 추가를 통해 추가 필드를 추가할 수 있습니다. 추가된 이벤트를 **제거하려면** x를 클릭합니다.

![이벤트 추가](./images/user-guide/touchpoint_add_event.png)

그룹 **추가를 클릭하면** 원본과 별도로 추가 필드를 만들 수 있는 옵션이 제공됩니다. 그룹이 추가되면 파란색 *및* 단추가 나타납니다. And **를** 클릭하여 매개 변수를 변경하면 새 매개 변수 &quot;Or&quot;가 여러 개의 성공한 경로를 정의하는 데 사용됩니다. 이 특정 터치포인트는 하나의 성공한 경로만 있으므로 &quot;Or&quot;이 필요하지 않습니다.

![터치포인트 개요](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>터치포인트 이름 *에 있는* 문자열을 사용하여 터치포인트를 신속하게 살펴봅니다. 문자열이 터치포인트 이름과 일치하는지 확인합니다.

![](./images/user-guide/touchpoint_string.png)

터치포인트 **추가를 클릭하고 위 프로세스를 반복하여 터치포인트를** 추가할 수 있습니다.

![터치포인트 추가](./images/user-guide/add_touchpoint.png)

필요한 모든 터치포인트 정의가 완료되면 위로 스크롤하여 오른쪽 위 **의** 모서리에서 [다음]을 클릭하여 마지막 단계로 진행합니다.

![완성된 정의](./images/user-guide/define_event_next.png)

## 고급 트레이닝 및 점수 설정

Attribution AI의 마지막 페이지는 *교육 및 점수 설정에* 사용되는 고급 페이지입니다.

![새 페이지 고급](./images/user-guide/advanced_settings.png)

### 교육 일정

[ *일정*]을 사용하여 점수를 매길 요일과 시간을 선택할 수 있습니다.

점수 *주기* 아래의 드롭다운을 클릭하여 일별, 주별 및 월별 점수 중에서 선택합니다. 다음으로, 점수를 매길 요일을 선택합니다. 여러 날을 선택할 수 있습니다. 하루 중 한 번 클릭하여 선택 취소합니다.

![교육 일정](./images/user-guide/schedule_training.png)

점수 매김이 발생하는 시간을 변경하려면 시계 아이콘을 클릭합니다. 표시되는 새 오버레이에서 채점할 시간을 입력합니다. 오버레이 외부를 클릭하여 닫습니다.

>[!NOTE]
>
>각 점수 지정 프로세스를 완료하는 데 최대 24시간이 걸릴 수 있습니다.

![시계 아이콘](./images/user-guide/time_of_day.png)

### 지역 기반 모델링(선택 사항) {#region-based-modeling-optional}

고객의 행동은 국가와 지역에 따라 크게 다를 수 있습니다. 글로벌 비즈니스의 경우 국가 기반 또는 지역 기반 모델을 사용하면 기여도 정확도를 높일 수 있습니다. 추가된 각 영역은 해당 지역의 데이터를 사용하여 새 모델을 생성합니다.

새 영역을 정의하려면 먼저 영역 **[!UICONTROL 추가를 클릭합니다]**. 표시되는 컨테이너에서 영역 이름을 입력합니다. 필드 이름 입력 드롭다운에서 하나의 값(&quot;placeContext.geo.countryCode&quot;) **[!UICONTROL 만]** 채워집니다. 이 값을 선택합니다.

![지역 선택](./images/user-guide/select_region_att.png)

그런 다음 연산자를 선택합니다.

![지역 연산자](./images/user-guide/region_operators.png)

마지막으로, 필드 값 입력 드롭다운에 국가 **[!UICONTROL 코드를]** 입력합니다.

>[!NOTE]
>
>국가 번호는 2자입니다. 전체 목록은 [ISO 3166-1 alpha-2에서 확인할 수 있습니다](https://datahub.io/core/country-list).

![region](./images/user-guide/region-based.png)

### 교육 창 {#training-window}

가장 정확한 모델을 얻으려면 비즈니스를 나타내는 내역 데이터로 모델을 교육하는 것이 중요합니다. 기본적으로 모델은 2분기(6개월) 전환 이벤트 데이터를 사용하여 교육됩니다. 드롭다운을 선택하여 기본값을 변경합니다. 1~4개 데이터(3-12개월)로 트레이닝을 선택할 수 있습니다.

>[!NOTE]
>
>트레이닝 기간이 짧을수록 최근 트렌드에 더 민감하지만, 트레이닝 기간이 길수록 모델이 더욱 견고해지고 최신 트렌드에 덜 민감합니다.

![교육 창](./images/user-guide/training_window.png)

교육 창을 선택한 후 오른쪽 위 **[!UICONTROL 의 [마침]** ]을 클릭합니다. 데이터를 처리하는 데 약간의 시간이 소요됩니다. 완료되면 인스턴스 설정이 완료되었음을 확인하는 팝업 대화 상자가 나타납니다. 서비스 인스턴스를 볼 수 있는 **[!UICONTROL 서비스 인스턴스]** **** 페이지로 리디렉션하려면 확인을 클릭합니다.

![설치 완료](./images/user-guide/instance_setup_complete.png)

## 다음 단계

이 튜토리얼을 따라 Attribution AI에서 서비스 인스턴스를 만들었습니다. 인스턴스 점수가 끝나면(최대 24시간 허용) Attribution AI 통찰력을 [발견할 수 있습니다](./discover-insights.md). 또한 점수 결과를 다운로드하려면 원시 점수 [다운로드 설명서를](./download-scores.md) 참조하십시오.

## Journey Orchestration용

다음 비디오에서는 Attribution AI에서 새 인스턴스를 만드는 엔드 투 엔드 워크플로우에 대해 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)