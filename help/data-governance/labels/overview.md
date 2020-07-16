---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 사용 레이블 개요
topic: labels
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# 데이터 사용 레이블 개요

데이터 사용 표시 및 실행(DULE)은 Adobe Experience Platform의 핵심 메커니즘입니다 [!DNL Data Governance]. DULE 기능을 사용하면 데이터 세트 및 필드에 데이터 사용 레이블을 적용하여 관련 데이터 사용 정책에 따라 각 데이터를 분류할 수 있습니다.

이 문서에서는 데이터 사용 레이블(DULE 레이블이라고도 함)에 대한 개요를 제공합니다 [!DNL Experience Platform]. 이 안내서를 읽기 전에 [데이터 거버넌스 개요를](../home.md) 참조하여 DULE 프레임워크에 대한 보다 강력한 소개를 확인하십시오.

## 데이터 사용 레이블 이해

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터 관리 방식을 유연하게 선택할 수 있습니다. 우수 사례는 데이터를 인제스트되는 즉시 [!DNL Experience Platform]또는 데이터를 사용할 수 있게 되는 즉시 레이블 지정 데이터를 권장합니다 [!DNL Platform].

데이터 집합 수준에서 적용되는 데이터 사용 레이블은 데이터 집합 내의 모든 필드에 전파됩니다. 또한 데이터 세트에 전달하지 않고 개별 필드(열 헤더)에 직접 레이블을 적용할 수 있습니다.

[!DNL Platform] 데이터 거버넌스에 적용되는 다양한 일반적인 제한 사항을 포괄하는 &quot;핵심&quot; 데이터 사용 레이블을 즉시 사용할 수 있습니다. 이러한 레이블 및 해당 레이블이 나타내는 사용 정책에 대한 자세한 내용은 [핵심 데이터 사용 레이블에 대한 안내서를 참조하십시오](reference.md).

Adobe에서 제공하는 레이블 외에도 사용자 지정 레이블을 정의할 수도 있습니다. UI에서 이 작업을 수행하는 방법에 대한 자세한 내용은 [데이터 사용 레이블 사용 안내서를 참조하십시오](./user-guide.md). API 호출을 사용하여 이 작업을 수행하는 방법에 대한 단계는 [데이터 사용 레이블 API 안내서를 참조하십시오](./api.md).

## 대상 세그먼트에 대한 레이블 상속

Adobe Experience Platform [세그멘테이션 서비스를 통해](../../segmentation/home.md) 만들어진 모든 대상 세그먼트는 해당 데이터 세트에 대한 사용 레이블을 상속합니다. 이를 통해 [!DNL Experience Platform] (예: [!DNL Real-time Customer Data Platform]) 위에 구축된 애플리케이션에서 세그먼트를 대상에 활성화할 때 데이터 사용 정책 적용을 자동으로 수행할 수 있습니다.

데이터 세트 수준 레이블을 상속하는 것 외에도 세그먼트는 기본적으로 연결된 데이터 세트에서 모든 필드 수준 레이블을 상속받습니다. 기반 애플리케이션에서 세그먼트를 사용하는 방법에 따라, 사용할 필드를 잠재적으로 지정하여 세그먼트가 제외된 필드에서 레이블을 상속할 수 없게 할 수 있습니다. [!DNL Platform]

실시간 CDP에서 자동 실행이 작동하는 방법에 대한 자세한 내용은 [Adobe 실시간 CDP 데이터 거버넌스 개요를 참조하십시오](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).

### Adobe Audience Manager 데이터 내보내기 컨트롤의 상속

[!DNL Experience Platform] 세그먼트를 Adobe Audience Manager과 공유할 수 있습니다. Audience Manager 세그먼트에 적용된 데이터 내보내기 컨트롤은 상응하는 레이블 및 마케팅 작업으로 [!DNL Experience Platform] [!DNL Data Governance]변환됩니다.

특정 데이터 내보내기 컨트롤이 데이터 사용 레이블에 매핑되는 방법에 대한 참조 [!DNL Platform]는 [Audience Manager 설명서를 참조하십시오](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).


## 다음 단계

데이터 사용 레이블이 도입되었으므로 [사용 안내서를](user-guide.md) 참조하여 UI에서 레이블을 관리하는 방법을 계속 살펴볼 수 [!DNL Experience Platform] 있습니다. API를 사용하여 레이블을 관리하는 방법에 대한 단계는 [사용 레이블 API 안내서를 참조하십시오](./api.md).