---
keywords: Experience Platform;사용자 인터페이스;사용자 인터페이스;사용자 정의;라이센스 사용 대시보드;대시보드;라이센스 사용;자격 부여;소비
title: 라이센스 사용 대시보드
description: Adobe Experience Platform은 조직의 라이선스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
topic: 가이드
type: 설명서
translation-type: tm+mt
source-git-commit: 3908011b31dd24b13a58a2bc5ad5137dd3af5f63
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 3%

---


# (베타) 라이센스 사용 대시보드 {#license-usage-dashboard}

>[!IMPORTANT]
>
>이 문서에 설명된 대시보드 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform 사용자 인터페이스(UI)는 일일 스냅샷 중에 캡처된 조직의 라이센스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 이 안내서에서는 UI에서 라이선스 사용 대시보드에 액세스하고 작업하는 방법에 대해 설명하고 대시보드에 표시되는 시각화에 대한 자세한 정보를 제공합니다.

플랫폼 UI에 대한 일반적인 개요는 [Experience Platform UI 안내서](../../landing/ui-guide.md)를 참조하십시오.

## 라이선스 사용 대시보드 데이터

라이센스 사용 대시보드에는 Experience Platform에 대한 조직의 라이센스 관련 데이터 스냅샷이 표시됩니다. 대시보드의 데이터는 스냅샷을 촬영한 특정 시점에 나타나는 것과 동일하게 표시됩니다. 즉, 스냅숏은 데이터에 대한 근사 또는 샘플이 아니며 대시보드가 실시간으로 업데이트되지 않습니다.

>[!NOTE]
>
>스냅숏을 만든 이후 데이터에 대한 변경 사항이나 업데이트는 다음 스냅샷을 촬영하기 전까지 대시보드에 반영되지 않습니다.

## 라이선스 사용 대시보드 살펴보기

플랫폼 UI 내의 라이센스 사용 대시보드로 이동하려면 왼쪽 레일에서 **[!UICONTROL 라이선스 사용량]**&#x200B;을 선택합니다. 대시보드가 표시되는 **[!UICONTROL 개요]** 탭으로 열립니다.

![](../images/license-usage/dashboard-overview.png)

### 샌드박스 선택

대시보드에서 볼 샌드박스를 선택하려면 [!UICONTROL 프로덕션] 또는 [!UICONTROL 개발]을 선택합니다. 선택한 샌드박스는 샌드박스 이름 옆에 있는 라디오 버튼으로 표시됩니다.

>[!NOTE]
>
>샌드박스에 대한 소비 보고는 동일한 유형의 모든 샌드박스에 대해 누적됩니다. 즉, [!UICONTROL 프로덕션] 또는 [!UICONTROL 개발]을 선택하면 모든 프로덕션 또는 개발 샌드박스에 대한 소비 보고서가 각각 제공됩니다.

![](../images/license-usage/select-sandbox.png)

### 날짜 범위 선택

샌드박스를 선택한 후 날짜 범위 드롭다운을 사용하여 대시보드에 표시할 기간을 선택할 수 있습니다. 다음 3가지 옵션을 사용할 수 있습니다.[!UICONTROL 최근 30일], [!UICONTROL 최근 90일] 및 [!UICONTROL 지난 12개월] 최근 30일은 기본적으로 선택됩니다.

![](../images/license-usage/select-date-range.png)

## 위젯

라이선스 사용량 대시보드는 위젯으로 구성되어 있으며, 조직의 라이선스 사용과 관련된 중요 정보를 제공하는 읽기 전용 지표가 표시됩니다. 표시되는 지표는 조직의 특정 라이선스에 따라 다릅니다(자세한 내용은 [사용 가능한 지표](#available-metrics) 섹션 참조).

각 위젯에는 조직의 실제 번호와 조직의 라이센스에서 사용할 수 있는 총수를 비교하여 라인 그래프가 표시되며 총 사용량의 백분율을 제공합니다.

![](../images/license-usage/widgets.png)

## 사용 가능한 지표

현재 라이선스 사용량 대시보드에는 4개의 지표가 있습니다.

* [!UICONTROL 대응 가능 대상] (프로필 수로 측정됨)
* [!UICONTROL 평균 프로파일 풍부함]
* [!UICONTROL 총 사용량 스토리지]
* [!UICONTROL 세그멘테이션 비율당 스캔한 데이터]

이러한 각 지표의 정의는 조직에서 구입한 라이센스에 따라 다릅니다. 각 지표에 대한 자세한 정의는 다음 제품 설명 설명서를 참조하십시오.

| 라이선스 | 제품 설명 |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>RT 고객 데이터 플랫폼:OD</li><li>RT 고객 데이터 플랫폼: OD PRFL에서 10M까지</li><li>RT 고객 데이터 플랫폼: OD PRFL에서 50M까지</li></ul> | [실시간 고객 데이터 플랫폼](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>AEP:OD 활성화</li><li>AEP:OD 활성화 과정 - 10M</li><li>AEP:최대 50M 활성화 과정</li></ul> | [Adobe Experience Platform 활성화](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD 인텔리전스</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

## 다음 단계

이 문서를 읽고 나면 라이센스 사용 대시보드를 찾아 볼 샌드박스를 선택할 수 있습니다. 조직에서 구입한 라이선스를 기반으로 조직에서 사용할 수 있는 지표에 대한 자세한 정보를 확인할 수도 있습니다.

Experience Platform UI에서 사용 가능한 다른 기능에 대한 자세한 내용은 [플랫폼 UI 안내서](../../landing/ui-guide.md)를 참조하십시오.