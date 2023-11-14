---
title: 일괄 쿼리 라이선스 사용 모니터링
description: Adobe Experience Platform UI는 조직의 Data Distiller 라이선스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: f33629d73e9bc7273e6ee5170294618f3e9731a8
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 일괄 쿼리 라이선스 사용 모니터링 {#monitor-license-usage}

라이선스 사용량 대시보드는 구입한 각 제품에 대한 조직의 Query Service 라이선스 사용량 및 사용량 지표에 대한 세분화된 보고서를 제공합니다. 대시보드에 표시된 사용 가능한 지표에 대한 자세한 내용은 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md#available-metrics).

대시보드는 구매한 각 제품에 대한 사용 지표, 모든 프로덕션 또는 개발 샌드박스의 통합된 지표 사용 및 특정 샌드박스의 사용 지표를 제공합니다. 여기에 표시되는 정보는 Platform 인스턴스의 일별 스냅샷 중에 캡처됩니다.

>[!NOTE]
>
>라이선스 사용 대시보드는 기본적으로 활성화되어 있지 않습니다. 대시보드를 볼 수 있으려면 사용자에게 &quot;라이선스 사용 대시보드 보기&quot; 권한이 부여되어야 합니다. 라이선스 사용 대시보드를 볼 수 있는 액세스 권한을 부여하는 단계에 대해서는 [대시보드 권한 안내서](../../dashboards/permissions.md).

## 시간 계산 {#compute-hours}

다음 [!UICONTROL 시간 계산] 지표는 일괄 쿼리에 Data Distiller 라이선스가 있는 고객에게만 적용됩니다. [!UICONTROL 시간 계산] 일괄 처리 쿼리가 실행될 때 데이터를 다시 데이터 레이크에 읽고, 처리하고, 쓰는 데 쿼리 서비스 엔진이 사용한 시간 측정입니다.

>[!NOTE]
>
>**다음 [!UICONTROL 시간 계산] 제한 사항이 있는 데이터 사용 가능**: 데이터는 2023년 10월 1일부터 트렌드 없이 시작됩니다.<br>다음 **채우기** 계약 시작 일자의 데이터가 진행 중인 작업입니다. 해당 연도 말까지 사용할 수 있을 것으로 예상됩니다.

![컴퓨팅 시간 지표가 강조 표시된 라이선스 사용 대시보드입니다.](../images/data-distiller/compute-hours.png)

조직의 구입한 라이선스를 기반으로 조직에서 사용할 수 있는 지표에 대한 자세한 내용은 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md).
