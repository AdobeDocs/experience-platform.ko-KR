---
title: 확장 앱 보고를 위한 사용자 정의 가능한 통찰력
description: SQL 쿼리를 사용하여 사용자 지정 대시보드에 대한 인사이트를 생성하는 방법에 대해 알아봅니다.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 확장 앱 보고를 위한 사용자 지정 가능한 통찰력

사용자 지정 SQL 쿼리를 사용하여 다양한 구조화된 데이터 세트에서 통찰력을 효과적으로 추출하십시오. 기술 전문가는 query pro 모드를 사용하여 SQL로 복잡한 분석을 수행한 다음 사용자 지정 대시보드의 차트를 통해 기술 전문가가 아닌 사용자와 이 분석을 공유하거나 CSV 파일로 내보낼 수 있습니다. 이 인사이트 생성 방법은 관계가 명확한 표에 적합하며, 인사이트 및 필터 내에서 틈새 사용 사례에 맞는 맞춤화를 강화할 수 있습니다.

>[!IMPORTANT]
>
>Query pro 모드는 를 구입한 사용자만 사용할 수 있습니다. [데이터 Distiller SKU](../../../query-service/data-distiller/overview.md).

SQL에서 인사이트를 생성하려면 먼저 대시보드를 만들어야 합니다.

## 사용자 지정 대시보드 만들기 {#create-custom-dashboard}

사용자 지정 대시보드를 만들려면 다음을 선택합니다. **[!UICONTROL 대시보드]** 왼쪽 탐색 패널에서 대시보드 작업 영역을 열 수 있습니다. 그런 다음 을 선택합니다. **[!UICONTROL 대시보드 만들기]**.

![[대시보드 만들기]가 강조 표시된 대시보드 인벤토리.](../../images/customizable-insights/create-dashboard.png)

다음 **[!UICONTROL 대시보드 만들기]** 대화 상자가 나타납니다. 대시보드 만들기 방법을 선택할 수 있는 두 가지 옵션이 있습니다. 인사이트를 만들려면 기존 데이터 모델을 [[!UICONTROL 안내식 디자인 모드]](../../user-defined-dashboards.md) 또는 를 사용하여 직접 SQL을 [!UICONTROL Query pro 모드].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

기존 데이터 모델을 사용하면 특정 비즈니스 요구 사항에 맞게 체계적이고 효율적이며 확장 가능한 프레임워크를 제공할 수 있습니다. 방법 알아보기 [기존 데이터 모델에서 인사이트 만들기](../../user-defined-dashboards.md#create-widget), 사용자 지정 대시보드 안내서를 참조하십시오.

SQL 쿼리에서 생성된 통찰력은 훨씬 뛰어난 유연성과 사용자 정의를 제공합니다. 기술 전문가는 query pro 모드를 사용하여 SQL에 대해 복잡한 분석을 수행한 다음 이 대시보드 기능을 통해 기술 전문가가 아닌 사용자와 이 분석을 공유할 수 있습니다. 선택 **[!UICONTROL Query pro 모드]** 뒤에 오는 **[!UICONTROL 저장]**.

>[!NOTE]
>
>선택한 후에는 해당 대시보드 내에서 이 선택을 변경할 수 없습니다. 대신 다른 대시보드 만들기 메서드를 사용하여 새 대시보드를 만들어야 합니다.

![다음 [!UICONTROL 대시보드 만들기] 쿼리 프로 모드 및 저장 이 강조 표시된 대화 상자.](../../images/customizable-insights/query-pro-mode.png)

## 차트 만들기 {#create-a-chart}

다음을 참조하십시오. [query pro 모드 안내서](./query-pro-mode.md) SQL을 사용하여 차트를 만드는 방법에 대한 단계별 지침입니다.
