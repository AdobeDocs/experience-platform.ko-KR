---
keywords: Experience Platform;insights;attribution ai;popular topics;attribution ai insights
solution: Experience Platform
title: Attribution AI에서 인사이트 검색
topic: Attribution AI insights
description: 이 문서는 Adobe Intelligent Services 사용자 인터페이스에서 서비스 인스턴스 인사이트를 상호 작용하는 데 도움이 되는 가이드입니다.
translation-type: tm+mt
source-git-commit: c5e2ea5daf813bf580a11f0182361197e55c6fe8
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 1%

---


# Attribution AI에서 인사이트 검색

Attribution AI 서비스 인스턴스는 마케팅 성과 및 ROI와 관련된 마케팅 결정을 내리고 측정하는 데 도움이 되는 통찰력을 제공합니다. 서비스 인스턴스를 선택하면 고객 경로의 각 단계에서 모든 고객 인터랙션이 미치는 영향을 이해할 수 있도록 시각화와 필터를 제공합니다.

이 문서는 Adobe Intelligent Services 사용자 인터페이스에서 서비스 인스턴스 인사이트를 상호 작용하는 데 도움이 되는 가이드입니다.

## 시작하기

Attribution AI에 대한 인사이트를 활용하려면 성공적인 실행 상태의 서비스 인스턴스를 사용할 수 있어야 합니다. 새 서비스 인스턴스를 만들려면 [Attribution AI 사용자 인터페이스 안내서를 참조하십시오](./user-guide.md). 최근에 서비스 인스턴스를 만들었는데 여전히 트레이닝과 점수 지정 중이라면 24시간 후에 실행을 완료하십시오.

## 서비스 인스턴스 인사이트 개요

UI [!DNL Adobe Experience Platform] 에서 왼쪽 탐색 **[!UICONTROL 영역에서 서비스]** 를 클릭합니다. 서비스 **[!UICONTROL 브라우저가]** 나타나고 사용 가능한 Adobe Intelligent Services가 표시됩니다. Attribution AI 컨테이너에서 열기를 **[!UICONTROL 클릭합니다]**.

![인스턴스 액세스](./images/insights/open_Attribution_ai.png)

Attribution AI 서비스 페이지가 나타납니다. 이 페이지에는 Attribution AI의 서비스 인스턴스가 나열되며 인스턴스 이름, 전환 이벤트, 인스턴스 실행 횟수, 마지막 업데이트 상태 등에 대한 정보가 표시됩니다. 시작하려면 서비스 인스턴스 이름을 클릭합니다.

>[!NOTE]
>
>성공적인 점수 실행을 완료한 서비스 인스턴스만 선택할 수 있습니다.

![인스턴스 만들기](./images/insights/select-service-instance.png)

다음으로, 시각화 및 데이터와 상호 작용할 수 있는 많은 필터와 함께 제공되는 서비스 인스턴스에 대한 인사이트 페이지가 나타납니다. 시각화 및 필터는 이 안내서 전체에서 더 자세히 설명합니다.

![설정 페이지](./images/insights/landing-page.png)

### 서비스 인스턴스 세부 정보

서비스 인스턴스에 대한 추가 세부 사항을 보려면 오른쪽 **[!UICONTROL 상단에 있는 자세히]** 보기를 클릭합니다.

![더 보기](./images/insights/show-more.png)

자세한 목록이 나타납니다. 나열된 속성에 대한 자세한 내용은 [Attribution AI 사용 안내서를 참조하십시오](./user-guide.md).

![세부 정보 표시](./images/insights/advanced-details.png)

### 인스턴스 편집

인스턴스를 편집하려면 오른쪽 **[!UICONTROL 상단]** 탐색에서 편집을 클릭합니다.
![편집 단추 클릭](./images/insights/edit-button.png)

인스턴스의 설명 및 점수 지정 빈도를 편집할 수 있는 편집 대화 상자가 나타납니다. 변경 사항을 확인하고 대화 상자를 닫으려면 오른쪽 **[!UICONTROL 아래 모서리에서 편집을]** 클릭합니다.

![팝업 편집](./images/insights/edit-popover.png)

### 추가 작업 {#more-actions}

추가 **[!UICONTROL 작업]** 단추는 *편집*&#x200B;옆에 있는 오른쪽 위 탐색에 있습니다. 추가 작업 **[!UICONTROL 을]** 클릭하면 다음 작업 중 하나를 선택할 수 있는 드롭다운이 열립니다.

- **삭제**:인스턴스를 삭제합니다.
- **요약 데이터 다운로드**:요약 데이터가 포함된 CSV 파일을 다운로드합니다.
- **액세스 점수**:[ **액세스 점수** ]를 클릭하면 Attribution AI 자습서의 [액세스 스코어로 리디렉션됩니다](./download-scores.md).
- **실행 내역 보기**:서비스 인스턴스와 연관된 모든 점수 실행 목록이 포함된 팝업이 나타납니다.

![추가 작업](./images/insights/more-actions.png)

## 데이터 필터링

Attribution AI 인사이트를 통해 데이터를 필터링하고 선택한 필터를 기반으로 UI 시각적 효과를 자동으로 업데이트할 수 있습니다.

>[!NOTE]
>
>기본적으로 모든 필터는 &quot;증분 및 영향[!UICONTROL 의 기여도 전환&quot;으로 설정된 &quot;기여도 모델]&quot; 필터를 제외한 &quot;모두&quot;로 설정됩니다.

### 전환 이벤트

Attribution AI에서 새 인스턴스를 만들 때 필수 필드 중 하나는 &quot;전환 이벤트&quot;입니다. 전환 이벤트는 전자 상거래 주문, 매장 내 구매 및 웹 사이트 방문과 같은 마케팅 활동의 영향을 식별하는 비즈니스 목표입니다.

인스턴스 내에서 **[!UICONTROL 전환 이벤트]** 드롭다운을 사용하면 데이터를 필터링하기 위해 인스턴스에 대해 정의된 이벤트를 선택할 수 있습니다. 특정 이벤트를 선택하면 UI 시각화가 변경되어 해당 이벤트에 속하는 전환만 채웁니다.

![전환 이벤트](./images/insights/conversion-event.png)

### 속성 모델

기여도 **[!UICONTROL 모델을]** 클릭하면 다양한 속성 모델을 모두 사용할 수 있는 드롭다운이 열립니다. 여러 모델을 선택하여 결과를 비교할 수 있습니다. 서로 다른 기여도 모델과 작동 방법에 대한 자세한 내용은 각 모델에 대한 정보가 포함된 표가 포함된 [Attribution AI](./overview.md) 개요를 참조하십시오.

![어트리뷰션 모델](./images/insights/attribution-model.png)

### 제품

제품 **** 필터를 사용하면 인스턴스를 만들 때 처음에 인제스트한 모든 제품에서 선택할 수 있습니다. 드롭다운을 클릭하고 검색 기능을 사용하여 비교할 모든 제품을 빠르게 선택합니다.

![제품 필터](./images/insights/product-filter.png)

### Geography

지역 **[!UICONTROL 위치]** 필터는 지역 기반 모델을 기반으로 국가 코드를 채웁니다. 데이터에 따라 이 필터가 없거나 없을 수 있습니다.

>[!NOTE]
>
>국가 번호는 2자입니다. 전체 목록은 [ISO 3166-1 alpha-2에서 확인할 수 있습니다](https://datahub.io/core/country-list).

### 지역

>[!NOTE]
>
>이 필터는 서비스 인스턴스를 만들 때 Attribution AI 사용자 인터페이스 안내서에서 선택적 단계 [영역 기반 모델링을](./user-guide.md#region-based-modeling-optional) 수행한 경우에만 제공됩니다.

이 필터를 사용하면 인스턴스 생성 프로세스에서 설정한 모든 영역을 선택할 수 있습니다.

### Channel

채널 **** 필터를 클릭하면 사용 가능한 모든 마케팅 채널이 포함된 드롭다운이 표시됩니다. 여러 채널을 선택하여 비교할 수 있습니다.

![Channel](./images/insights/channel.png)

### 날짜 범위

달력 아이콘을 클릭하여 날짜 범위 팝업을 엽니다. 시작 및 종료 전환 이벤트 날짜는 UI에 채워진 데이터의 양을 결정합니다. 채워진 데이터의 양을 늘리거나 집중하기 위해 날짜 범위를 좁히거나 넓히도록 선택할 수 있습니다.

![날짜 범위](./images/insights/display-date-range.png)

## 데이터 개요

개요 **[!UICONTROL 카드는]** 속성 모델별 총 전환 수를 보여줍니다. 이 문서에서 앞에서 설명한 필터를 사용하여 검색을 구체화하는 방법에 따라 총 개수가 변경됩니다. 모델을 더 선택하면 해당 범례에 해당하는 고유한 색상이 있는 추가 서클이 개요에 추가됩니다.

![개요](./images/insights/Overview.png)

## 주간 트렌드

주별 **[!UICONTROL 트렌드]** 카드에서는 필터링 프로세스 동안 설정한 날짜 범위로 총 전환을 분석합니다.

![트렌드](./images/insights/weekly-trends.png)

주별 트렌드 ** 카드의 오른쪽 상단에 있는 줄임표를 클릭하면 일별, 주별 또는 월별 트렌드를 선택할 수 있는 드롭다운이 표시됩니다.

특정 속성 모델의 데이터 라인 위로 마우스를 가져가면 해당 날짜에 대한 총 전환 수가 표시되는 팝업이 만들어집니다.

![호구 트렌드](./images/insights/weekly-trend-hover.png)

## 채널별 분류

채널 **[!UICONTROL 카드별]** 분류는 각 채널과 관련된 총 전환 수를 결정하는 데 사용됩니다. 이 카드를 사용하면 각 채널의 효과성과 ROI를 결정하는 데 도움이 됩니다.

![분류 채널](./images/insights/channel-breakdown.png)

채널별 분류 카드 **[!UICONTROL 의 오른쪽 상단에서 줄임표를 클릭하면 터치포인트를 기준으로 데이터를 채울 수 있는 드롭다운이]** 열립니다.

![터치포인트](./images/insights/breakdown-by-touchpoints.png)

## 주요 캠페인

상위 **[!UICONTROL 캠페인]** 카드에는 캠페인의 개요와 각 채널에서 캠페인이 수행되는 방법이 표시됩니다. 이 카드를 사용하면 특정 채널에 대한 특정 캠페인의 효과를 팀에 알리며 향후 투자 대상에 대한 통찰력을 제공할 수 있습니다.

![상위 캠페인](./images/insights/top-campaigns.png)

## 다음 단계

데이터 필터링을 완료하고 적절한 정보를 표시할 수 있게 되면 점수에 액세스할 수 있는 옵션이 있습니다. 스코어에 액세스하는 방법에 대한 자세한 설명은 Attribution AI [자습서에서](./download-scores.md) 액세스 점수를 참조하십시오. 또한 [더 많은 작업에 명시된 요약 데이터를 다운로드할 수도 있습니다](#more-actions). &quot;요약 데이터 다운로드&quot;를 선택하면 날짜별로 집계된 요약 데이터가 다운로드됩니다.

## Journey Orchestration용

다음 비디오는 Attribution AI 인사이트 페이지를 사용하여 마케팅 채널 및 캠페인의 ROI를 이해하는 방법을 학습하는 데 도움이 되도록 만들어졌습니다.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)