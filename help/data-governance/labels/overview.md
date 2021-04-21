---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 레이블 api;정책 서비스 api;데이터 사용 레이블 개요
solution: Experience Platform
title: 데이터 사용 레이블 개요
topic-legacy: labels
description: Adobe Experience Platform 데이터 거버넌스를 사용하면 데이터 세트 및 필드에 데이터 사용 레이블을 적용하여 관련 데이터 사용 정책에 따라 각 데이터를 분류할 수 있습니다. 이 문서에서는 Experience Platform의 데이터 사용 레이블에 대한 개요를 제공합니다.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 데이터 사용 레이블 개요

Adobe Experience Platform [!DNL Data Governance]에서는 데이터 세트 및 필드에 데이터 사용 레이블을 적용하여 관련 데이터 사용 정책에 따라 각 데이터를 분류할 수 있습니다.

이 문서에서는 [!DNL Experience Platform]의 데이터 사용 레이블에 대한 개요를 제공합니다. 이 안내서를 읽기 전에 데이터 거버넌스 프레임워크에 대한 보다 강력한 소개를 보려면 [데이터 거버넌스 개요](../home.md)를 참조하십시오.

## 데이터 사용 레이블 이해

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터 관리 방식을 유연하게 선택할 수 있습니다. 우수 사례는 [!DNL Experience Platform]으로 인제스트되거나 [!DNL Platform]에서 데이터를 사용할 수 있게 되는 즉시 레이블 지정 데이터를 권장합니다.

데이터 집합 수준에서 적용되는 데이터 사용 레이블은 데이터 집합 내의 모든 필드에 전파됩니다. 또한 데이터 세트의 개별 필드(열 헤더)에 전달하지 않고 레이블을 직접 적용할 수도 있습니다.

[!DNL Platform] 데이터 거버넌스에 적용되는 다양한 일반적인 제한 사항을 포괄하는 &quot;핵심&quot; 데이터 사용 레이블을 즉시 사용할 수 있습니다. 이러한 레이블 및 해당 레이블이 나타내는 사용 정책에 대한 자세한 내용은 [핵심 데이터 사용 레이블](reference.md)에 대한 안내서를 참조하십시오.

Adobe에서 제공하는 레이블 외에도 조직에 대해 고유한 사용자 지정 레이블을 정의할 수도 있습니다. 자세한 내용은 [레이블 관리](#manage-labels)의 섹션을 참조하십시오.

## 대상 세그먼트에 대한 레이블 상속

[Adobe Experience Platform 세그멘테이션 서비스](../../segmentation/home.md)에서 만든 모든 대상 세그먼트는 해당 데이터 세트의 사용 레이블을 상속합니다. 이를 통해 Experience Platform은 세그먼트를 대상에 활성화할 때 자동 데이터 사용 정책 적용을 제공할 수 있습니다.

데이터 세트 수준 레이블을 상속하는 것 외에도 세그먼트는 기본적으로 연결된 데이터 세트에서 모든 필드 수준 레이블을 상속합니다. 따라서 세그먼트에서 제외해야 하는 속성을 보다 쉽게 식별하고 제외된 필드에서 레이블을 상속하지 못하도록 할 수 있습니다.

플랫폼에서 자동 실행이 작동하는 방법에 대한 자세한 내용은 [자동 정책 적용](../enforcement/auto-enforcement.md)에 대한 개요를 참조하십시오.

### Adobe Audience Manager 데이터 내보내기 컨트롤에서 상속

[!DNL Experience Platform] Adobe Audience Manager과 세그먼트를 공유할 수 있습니다. Audience Manager 세그먼트에 적용된 모든 데이터 내보내기 컨트롤은 [!DNL Experience Platform] [!DNL Data Governance]에서 인식하는 동일한 레이블 및 마케팅 작업으로 변환됩니다.

특정 데이터 내보내기 컨트롤이 [!DNL Platform]의 데이터 사용 레이블에 매핑되는 방법에 대한 참조를 보려면 [Audience Manager 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)를 참조하십시오.

## [!DNL Experience Platform] {#manage-labels}에서 데이터 사용 레이블 관리

[!DNL Experience Platform] API 또는 사용자 인터페이스를 사용하여 데이터 사용 레이블을 관리할 수 있습니다. 각 항목에 대한 자세한 내용은 아래 하위 섹션을 참조하십시오.

### UI 사용

[!DNL Experience Platform] UI의 **[!UICONTROL Policies]** 작업 영역에서 조직의 핵심 및 사용자 지정 레이블을 보고 관리할 수 있습니다. **[!DNL Datasets]** 작업 영역에서 데이터 세트 및 필드에 레이블을 적용할 수 있습니다. 자세한 내용은 [레이블 사용자 안내서](user-guide.md)를 참조하십시오.

### API 사용

[정책 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)의 `/labels` 종단점을 사용하면 사용자 지정 레이블 만들기를 포함하여 데이터 사용 레이블을 프로그래밍 방식으로 관리할 수 있습니다. 자세한 내용은 [레이블 끝점 안내서](../api/labels.md)를 참조하십시오.

[데이터 집합 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml)는 데이터 집합 및 필드에 대한 레이블을 관리하는 데 사용됩니다. 자세한 내용은 [데이터 세트 레이블 관리](./dataset-api.md)의 안내서를 참조하십시오.

## 다음 단계

이 문서에서는 데이터 거버넌스 프레임워크 내의 데이터 사용 레이블 및 역할에 대해 소개합니다. [!DNL Experience Platform]에서 레이블을 관리하는 방법에 대한 자세한 내용은 이 안내서 전체에 연결된 설명서를 참조하십시오.
