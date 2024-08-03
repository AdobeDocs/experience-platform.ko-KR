---
title: 일괄 쿼리 라이선스 사용 모니터링
description: Adobe Experience Platform UI는 조직의 Data Distiller 라이선스 사용에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: f3542105e423633e2bdf0f8e8501c1a1dc200f32
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 일괄 쿼리 라이선스 사용 모니터링 {#monitor-license-usage}

라이선스 사용량 대시보드는 구입한 각 제품에 대한 조직의 Query Service 라이선스 사용량 및 사용량 지표에 대한 세분화된 보고서를 제공합니다. 대시보드에 표시된 사용 가능한 지표에 대한 자세한 내용은 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md#available-metrics)를 참조하세요.

대시보드는 구매한 각 제품에 대한 사용 지표, 모든 프로덕션 또는 개발 샌드박스의 통합된 지표 사용 및 특정 샌드박스의 사용 지표를 제공합니다. 여기에 표시되는 정보는 Platform 인스턴스의 일별 스냅샷 중에 캡처됩니다.

>[!NOTE]
>
>라이선스 사용 대시보드는 기본적으로 활성화되어 있지 않습니다. 대시보드를 볼 수 있으려면 사용자에게 &quot;라이선스 사용 대시보드 보기&quot; 권한이 부여되어야 합니다. 라이선스 사용 대시보드를 볼 수 있는 액세스 권한을 부여하는 단계는 [대시보드 사용 권한 안내서](../../dashboards/permissions.md)를 참조하세요.

## 시간 계산 {#compute-hours}

[!UICONTROL 시간 계산] 지표는 일괄 쿼리용 Data Distiller 라이선스가 있는 고객에게만 적용됩니다. [!UICONTROL 계산 시간]은 일괄 처리 쿼리가 실행될 때 쿼리 서비스 엔진에서 데이터를 읽고 처리하고 데이터 레이크에 다시 쓰는 데 걸리는 시간을 측정한 것입니다.

>[!NOTE]
>
>**시간 계산] 데이터는 제한과 함께 사용할 수 있습니다**: 데이터는 2023년 10월 1일부터 트렌드 없이 시작됩니다.[!UICONTROL 

![시간 계산 지표가 강조 표시된 라이선스 사용 대시보드입니다.](../images/data-distiller/compute-hours.png)

조직의 구입한 라이선스를 기반으로 조직에서 사용할 수 있는 지표에 대한 자세한 내용은 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md)를 참조하세요.
