---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 레이블 api;정책 서비스 api;데이터 사용 레이블 개요
solution: Experience Platform
title: 데이터 사용 레이블 개요
description: Adobe Experience Platform에서 데이터 거버넌스 규정 준수를 적용하는 데 데이터 사용 레이블을 사용하는 방법을 알아봅니다.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 16%

---

# 데이터 사용 레이블 개요 {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="중요하고 보호된 데이터에 대한 액세스 제어"
>abstract="<h2>설명</h2><p>특정 데이터 속성 및/또는 세그먼트에 대한 액세스를 제어하여 Experience Platform 사용 사례를 운영하는 다양한 페르소나 및 팀을 위한 유연한 워크플로를 설계할 수 있습니다.</p>"

Adobe Experience Platform을 사용하면 데이터 세트 및 필드에 데이터 사용 레이블을 적용하여 관련 [데이터 거버넌스 정책](../policies/overview.md) 및 [액세스 제어 정책](../../access-control/abac/ui/policies.md)에 따라 각 레이블을 분류할 수 있습니다.

이 문서에서는 [!DNL Experience Platform]의 데이터 사용 레이블에 대한 개요를 제공합니다.

## 데이터 사용 레이블 이해하기

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 거버넌스 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터를 제어하는 방법을 유연하게 선택할 수 있습니다. 모범 사례에서는 데이터를 [!DNL Experience Platform]에 섭취하는 즉시 또는 데이터를 [!DNL Experience Platform]에서 사용할 수 있게 되는 즉시 데이터에 레이블을 지정하는 것을 권장합니다.

데이터 세트 수준에서 적용되는 데이터 사용 레이블은 데이터 세트 내의 모든 필드에 전파됩니다. 레이블은 전달 없이 데이터 세트의 개별 필드(열 헤더)에 직접 적용할 수도 있습니다.

[!DNL Experience Platform]은(는) 데이터 거버넌스에 적용할 수 있는 광범위한 일반적인 제한 사항을 다루는 몇 가지 &quot;핵심&quot; 데이터 사용 레이블을 즉시 제공합니다. 이러한 레이블과 해당 레이블을 나타내는 거버넌스 정책에 대한 자세한 내용은 [핵심 데이터 사용 레이블](reference.md)에 대한 안내서를 참조하십시오.

Adobe에서 제공하는 레이블 외에도 귀사에 대한 사용자 정의 레이블을 정의할 수도 있습니다. 자세한 내용은 [레이블 관리](#manage-labels) 섹션을 참조하십시오.

## 대상 세그먼트에 대한 레이블 상속

[Adobe Experience Platform 세그먼테이션 서비스](../../segmentation/home.md)에서 만든 모든 대상 세그먼트는 해당 데이터 세트의 사용 레이블을 상속합니다. 이렇게 하면 Experience Platform에서 대상에 대한 세그먼트를 활성화할 때 자동 정책 적용을 제공할 수 있습니다.

데이터 세트 수준 레이블을 상속할 뿐만 아니라 세그먼트는 기본적으로 연결된 데이터 세트에서 모든 필드 수준 레이블을 상속합니다. 따라서 세그먼트에서 제외해야 하는 속성을 보다 쉽게 식별하고 제외된 필드의 레이블을 상속하지 못하도록 할 수 있습니다.

Experience Platform에서 자동 적용이 작동하는 방법에 대한 자세한 내용은 [자동 정책 적용](../enforcement/auto-enforcement.md)에 대한 개요를 참조하십시오.

### Adobe Audience Manager 데이터 내보내기 컨트롤의 상속

[!DNL Experience Platform]은(는) Adobe Audience Manager과 세그먼트를 공유할 수 있습니다. Audience Manager 세그먼트에 적용된 모든 데이터 내보내기 컨트롤은 [!DNL Experience Platform] 데이터 거버넌스에서 인식하는 동등한 레이블 및 마케팅 작업으로 변환됩니다.

특정 데이터 내보내기 컨트롤이 [!DNL Experience Platform]의 데이터 사용 레이블에 매핑되는 방법에 대한 참조는 [Audience Manager 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ko#aam-data-export-control-in-aep)를 참조하십시오.

## [!DNL Experience Platform]에서 데이터 사용 레이블 관리 {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="지침"
>abstract="<ul><li>XDM 필드 및 세그먼트에 레이블을 지정하여 액세스를 제한하려는 필드 및/또는 세그먼트를 분류합니다.</li><li>역할에 레이블 지정, 즉 레이블을 역할에 추가하면 해당 역할을 가진 멤버들이 제한할 수 있는 레이블을 정의할 수 있습니다.</li><li>정책 만들기, 즉 정책은 XDM 필드 및 세그먼트와 같은 레이블이 지정된 오브젝트의 레이블과 역할의 레이블 간의 관계를 생성합니다. 레이블이 일치하면 허용 또는 제한 액세스를 정의할 수 있습니다.</li></ul>"

[!DNL Experience Platform] API 또는 사용자 인터페이스를 사용하여 데이터 사용 레이블을 관리할 수 있습니다. 각각에 대한 자세한 내용은 아래 하위 섹션을 참조하십시오.

### UI 사용

[!DNL Experience Platform] UI의 **[!UICONTROL 정책]** 작업 영역에서 조직의 핵심 및 사용자 지정 레이블을 보고 관리할 수 있습니다. **[!UICONTROL 스키마]** 작업 영역을 사용하여 [XDM(Experience Data Model) 스키마에 레이블을 적용](../../xdm/tutorials/labels.md)하거나, 데이터 사용 레이블 사용 안내서를 대신 읽고 [**[!UICONTROL 정책] UI에서 사용자 지정 레이블을 만들고 관리](./user-guide.md)하는 방법을 배울 수 있습니다.

>[!IMPORTANT]
>
>더 이상 데이터 세트 수준의 필드에 레이블을 적용할 수 없습니다. 이 워크플로우는 더 이상 사용되지 않으며, 대신 스키마 수준에서 레이블을 적용합니다. 데이터 세트 오브젝트 수준에서 이전에 적용된 모든 레이블은 2024년 5월 31일까지 Experience Platform UI를 통해 계속 지원됩니다. 모든 스키마에서 레이블이 일관되도록 하려면 데이터 세트 수준의 필드에 이전에 첨부된 모든 레이블을 향후 연도에 따라 스키마 수준으로 마이그레이션해야 합니다. 이 작업을 수행하는 방법에 대한 지침은 [이전에 적용된 레이블 마이그레이션](../e2e.md#migrate-labels)에 대한 섹션을 참조하십시오.

### API 사용

[정책 서비스 API](https://www.adobe.io/experience-platform-apis/references/policy-service/)의 `/labels` 끝점을 사용하면 사용자 지정 레이블 만들기를 포함하여 데이터 사용 레이블을 프로그래밍 방식으로 관리할 수 있습니다. 자세한 내용은 [레이블 끝점 안내서](../api/labels.md)를 참조하십시오.

[데이터 집합 서비스 API](https://www.adobe.io/experience-platform-apis/references/dataset-service/)를 사용하여 데이터 집합 및 필드의 레이블을 관리합니다. 자세한 내용은 [데이터 세트 레이블 관리](./dataset-api.md)에 대한 안내서를 참조하십시오.

## 다음 단계

이 문서에서는 데이터 거버넌스 프레임워크 내에서 데이터 사용 레이블 및 해당 역할에 대해 소개합니다. [!DNL Experience Platform]에서 레이블을 관리하는 방법에 대한 자세한 내용은 이 안내서 전체에 연결된 설명서를 참조하십시오.
