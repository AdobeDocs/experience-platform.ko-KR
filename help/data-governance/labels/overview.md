---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 레이블 api;정책 서비스 api;데이터 사용 레이블 개요
solution: Experience Platform
title: 데이터 사용 레이블 개요
description: Adobe Experience Platform에서 데이터 거버넌스 규정 준수를 적용하는 데 데이터 사용 레이블을 사용하는 방법을 알아봅니다.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 15%

---

# 데이터 사용 레이블 개요 {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="중요하고 보호된 데이터에 대한 액세스 제어"
>abstract="<h2>설명</h2><p>특정 데이터 속성 및/또는 세그먼트에 대한 액세스를 제어하여 Experience Platform 사용 사례를 운영하는 다양한 페르소나 및 팀을 위한 유연한 워크플로를 설계할 수 있습니다.</p>"

Adobe Experience Platform을 사용하면 데이터 세트 및 필드에 데이터 사용 레이블을 적용하여 관련 항목에 따라 각 레이블을 분류할 수 있습니다 [데이터 거버넌스 정책](../policies/overview.md) 및 [액세스 제어 정책](../../access-control/abac/ui/policies.md).

이 문서는에서 데이터 사용 레이블에 대한 개요를 제공합니다 [!DNL Experience Platform].

## 데이터 사용 레이블 이해

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 거버넌스 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터를 제어하는 방법을 유연하게 선택할 수 있습니다. 우수 사례는에 데이터가 수집되는 즉시 레이블 지정을 장려합니다. [!DNL Experience Platform]또는 에서 데이터를 사용할 수 있게 되는 즉시 [!DNL Platform].

데이터 세트 수준에서 적용되는 데이터 사용 레이블은 데이터 세트 내의 모든 필드에 전파됩니다. 레이블은 전달 없이 데이터 세트의 개별 필드(열 헤더)에 직접 적용할 수도 있습니다.

[!DNL Platform] 는 데이터 거버넌스에 적용할 수 있는 광범위한 일반적인 제한 사항을 다루는 몇 가지 &quot;핵심&quot; 데이터 사용 레이블을 즉시 제공합니다. 이러한 레이블과 해당 레이블이 나타내는 거버넌스 정책에 대한 자세한 내용은 [핵심 데이터 사용 레이블](reference.md).

Adobe에서 제공하는 레이블 외에도 귀사에 대한 사용자 정의 레이블을 정의할 수도 있습니다. 의 섹션을 참조하십시오. [레이블 관리](#manage-labels) 추가 정보.

## 대상 세그먼트에 대한 레이블 상속

다음에 의해 만들어진 모든 대상 세그먼트 [Adobe Experience Platform 세그멘테이션 서비스](../../segmentation/home.md) 해당 데이터 세트의 사용 레이블을 상속합니다. 이렇게 하면 Experience Platform이 대상에 대한 세그먼트를 활성화할 때 자동으로 정책을 적용할 수 있습니다.

데이터 세트 수준 레이블을 상속할 뿐만 아니라 세그먼트는 기본적으로 연결된 데이터 세트에서 모든 필드 수준 레이블을 상속합니다. 따라서 세그먼트에서 제외해야 하는 속성을 보다 쉽게 식별하고 제외된 필드의 레이블을 상속하지 못하도록 할 수 있습니다.

Platform에서 자동 적용이 작동하는 방법에 대한 자세한 내용은 [자동 정책 시행](../enforcement/auto-enforcement.md).

### Adobe Audience Manager 데이터 내보내기 컨트롤의 상속

[!DNL Experience Platform] 은 Adobe Audience Manager과 세그먼트를 공유할 수 있습니다. Audience Manager 세그먼트에 적용된 모든 데이터 내보내기 컨트롤은 에서 인식하는 동등한 레이블 및 마케팅 작업으로 변환됩니다 [!DNL Experience Platform] 데이터 거버넌스

특정 데이터 내보내기 컨트롤이 의 데이터 사용 레이블에 매핑되는 방식에 대한 참조 [!DNL Platform], 다음을 참조하십시오. [Audience Manager 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## 에서 데이터 사용 레이블 관리 [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="지침"
>abstract="<ul><li>XDM 필드 및 세그먼트에 레이블을 지정하여 액세스를 제한하려는 필드 및/또는 세그먼트를 분류합니다.</li><li>역할에 레이블 지정, 즉 레이블을 역할에 추가하면 해당 역할을 가진 구성원들이 제한할 수 있는 레이블을 정의할 수 있습니다.</li><li>정책 만들기, 즉 정책은 XDM 필드 및 세그먼트와 같은 레이블이 지정된 오브젝트의 레이블과 역할의 레이블 간의 관계를 생성합니다. 레이블이 일치하면 허용 또는 제한 액세스를 정의할 수 있습니다.</li></ul>"

다음을 사용하여 데이터 사용 레이블 관리 [!DNL Experience Platform] API 또는 사용자 인터페이스. 각각에 대한 자세한 내용은 아래 하위 섹션을 참조하십시오.

### UI 사용

다음 **[!UICONTROL 정책]** 의 작업 공간 [!DNL Experience Platform] UI를 통해 조직의 핵심 및 사용자 지정 레이블을 보고 관리할 수 있습니다. 다음을 사용할 수 있습니다. **[!UICONTROL 스키마]** 작업 영역 [XDM(Experience Data Model) 스키마에 레이블 적용](../../xdm/tutorials/labels.md)또는 다음을 사용할 수 있습니다 **[!DNL Datasets]** 작업 영역 [데이터 세트에 레이블 적용](./user-guide.md) 대신,

>[!NOTE]
>
>데이터 세트 수준에서 레이블을 적용하는 것은 데이터 거버넌스 사용 사례에 대해서만 지원됩니다. 데이터에 대한 액세스 정책을 만들려는 경우 데이터 세트가 기반으로 하는 스키마에 레이블을 적용해야 합니다. 의 개요 보기 [속성 기반 액세스 제어](../../access-control/abac/overview.md) 추가 정보.

### API 사용

다음 `/labels` 의 엔드포인트 [정책 서비스 API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 사용자 지정 레이블 만들기를 포함하여 데이터 사용 레이블을 프로그래밍 방식으로 관리할 수 있습니다. 다음을 참조하십시오. [labels endpoint 안내서](../api/labels.md) 추가 정보.

다음 [데이터 세트 서비스 API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 는 데이터 세트 및 필드의 레이블을 관리하는 데 사용됩니다. 다음 안내서를 참조하십시오 [데이터 세트 레이블 관리](./dataset-api.md) 추가 정보.

>[!NOTE]
>
>데이터 세트 수준에서 레이블을 적용하는 것은 데이터 거버넌스 사용 사례에 대해서만 지원됩니다. 데이터에 대한 액세스 정책을 만들려면 다음을 수행해야 합니다 [스키마에 레이블 적용](../../xdm/tutorials/labels.md) 을 참조하십시오. 의 개요 보기 [속성 기반 액세스 제어](../../access-control/abac/overview.md) 추가 정보.

## 다음 단계

이 문서에서는 데이터 거버넌스 프레임워크 내에서 데이터 사용 레이블 및 해당 역할에 대해 소개합니다. 에서 레이블을 관리하는 방법에 대한 자세한 내용은 이 안내서 전체에 연결된 설명서를 참조하십시오. [!DNL Experience Platform].
