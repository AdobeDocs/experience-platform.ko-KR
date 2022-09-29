---
title: 배치 질의 라이선스 사용량 모니터링
description: Adobe Experience Platform UI는 조직의 Data Distiller 라이선스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
source-git-commit: 74175e5e2ce31427ef6ea8d93055d6ca3a8406f4
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 배치 쿼리 라이선스 사용 모니터링 {#monitor-license-usage}

Adobe Experience Platform UI(사용자 인터페이스)는 조직의 Query Service 라이선스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.

UI에서 라이선스 사용 대시보드에 액세스 및 상호 작용하는 방법과 대시보드에 표시된 사용 가능한 지표에 대한 자세한 내용을 보려면 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md).

자세한 내용은 [대시보드 개요](../../dashboards/home.md) 를 참조하십시오.

## 위젯 {#widgets}

라이선스 사용량 대시보드는 위젯으로 구성되며, 조직의 라이선스 사용과 관련된 중요한 정보를 제공하는 읽기 전용 지표를 표시합니다. 표시되는 지표는 조직의 특정 라이센스에 따라 다릅니다.

라디오 단추를 선택하여 분석할 샌드박스를 선택하고 드롭다운을 사용하여 분석에 대한 기간을 선택합니다. 사용 가능한 옵션은 30일, 90일, 12개월 기간, 마지막 년, 전체 계약 기간 또는 사용자 지정 날짜입니다.

## 계산 시간 {#compute-hours}

다음 [!UICONTROL 계산 시간] 위젯은 선 그래프를 사용하여 조직의 일괄 처리 쿼리 처리 시간을 매일 시각화합니다. 위젯은 위젯의 왼쪽 상단에 숫자로 표시된 세 개의 지표를 표시합니다. 이것들은

- [!UICONTROL 실제]: 개요 드롭다운에서 선택한 기간에 대한 총 계산 시간 수입니다. 이 지표는 그래프에도 실선이 표시됩니다.
- [!UICONTROL 라이센스]: 조직의 라이선스 계약에 의해 허용되는 총 계산 시간 수입니다. 이 지표는 그래프에도 점선으로 표시됩니다.
- [!UICONTROL 사용]: 이는 라이선스에서 동의한 최대 계산 시간에 대한 사용자의 사용 비율입니다.

>[!IMPORTANT]
>
>다음 [!UICONTROL 계산 시간] 위젯은 배치 쿼리에 대한 Data Distiller 라이선스가 있는 고객에게만 적용됩니다.

![컴퓨팅 시간 위젯이 강조 표시된 라이선스 사용 대시보드.](../images/data-distiller/compute-hours.png)
