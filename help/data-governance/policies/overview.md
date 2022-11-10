---
keywords: Experience Platform;홈;인기 항목;dule;DULE
solution: Experience Platform
title: 데이터 사용 정책 개요
topic-legacy: policies
description: 데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하려면 데이터 사용 정책을 구현해야 합니다. 데이터 사용 정책은 Experience Platform 내에서 데이터 수행을 허용하거나 제한하는 마케팅 작업 종류를 설명하는 규칙입니다.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: c314cba6b822e12aa0367e1377ceb4f6c9d07ac2
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 2%

---

# 데이터 사용 정책 개요 {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="데이터 사용 제한"
>abstract="데이터 사용 정책 유형은 마케팅 활동에 대한 데이터 사용을 제한하기 위해 데이터 거버넌스 레이블에 적용된 특정 마케팅 작업을 평가합니다."

데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하려면 데이터 사용 정책을 구현해야 합니다. 데이터 사용 정책은 내에서 데이터를 수행할 수 있도록 허용되거나 제한된 마케팅 작업 종류를 설명하는 규칙입니다 [!DNL Experience Platform].

사용할 수 있는 정책에는 두 가지 유형이 있습니다.

* **[!UICONTROL 데이터 거버넌스 정책]**: 수행되는 마케팅 작업 및 해당 데이터에 의해 전달된 데이터 사용 레이블을 기반으로 데이터 활성화를 제한합니다.
* **[!UICONTROL 동의 정책]**: 활성화할 수 있는 프로필을 필터링합니다. [대상](../../destinations/home.md) 고객의 동의 또는 환경 설정에 따라

>[!NOTE]
>
>데이터 사용 정책은 [액세스 제어 정책](../../access-control/abac/end-to-end-guide.md#policy)- 조직의 특정 플랫폼 사용자가 특정 데이터 필드에 액세스할 수 있는지 여부를 확인하고, [!UICONTROL 권한] 탭.

이 문서에서는 데이터 사용 정책에 대한 높은 수준의 개요를 제공하며 UI 또는 API의 정책 작업을 위한 추가 설명서에 대한 링크를 제공합니다.

## 마케팅 작업 {#marketing-actions}

데이터 거버넌스 프레임워크 컨텍스트에서 마케팅 작업(마케팅 사용 사례라고도 함)은 [!DNL Experience Platform] 데이터 소비자는 조직에서 데이터 사용을 제한할 수 있습니다. 따라서 데이터 사용 정책은 다음과 같이 정의됩니다.

1. 특정 마케팅 작업
2. 해당 작업이 수행되는 것을 제한하는 조건

마케팅 작업의 예는 데이터 세트를 타사 서비스로 내보내기를 원하는 것일 수 있습니다. 특정 유형의 데이터(예: PII)를 내보낼 수 없고, &quot;I&quot; 레이블(ID 데이터)이 포함된 데이터 세트를 내보내려고 하면 [!DNL Policy Service] 데이터 사용 정책을 위반했음을 사용자에게 알립니다.

>[!NOTE]
>
>마케팅 작업 자체는 데이터 사용을 제한하지 않습니다. 이러한 작업을 정책 위반에 대해 평가하려면 활성화된 데이터 사용 정책에 포함해야 합니다.

조직의 서비스에서 데이터 사용이 발생하는 경우 정책 위반을 식별할 수 있도록 관련 마케팅 작업을 표시해야 합니다. 그런 다음 [정책 서비스 API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 통합에서 정책 위반을 확인하십시오.

>[!NOTE]
>
>대상에서 마케팅 사용 사례를 설정하여 정책 집행을 자동화할 수 있습니다. 자세한 내용은 [대상 설명서](../../destinations/home.md) 를 참조하십시오.

다음 목록은 이 문서의 부록 을 참조하십시오 [사용 가능한 Adobe 정의 마케팅 작업](#core-actions). 또한 [!DNL Policy Service] API 또는 [!DNL Experience Platform] 사용자 인터페이스. 마케팅 작업 및 정책 작업에 대한 자세한 내용은 다음 섹션에 나와 있습니다.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 데이터 사용 정책 관리 {#manage}

데이터 사용 레이블이 적용되면 데이터 관리자는 [!DNL Policy Service] API 또는 [!DNL Experience Platform] 데이터 사용 레이블이 포함된 데이터에 대해 수행되는 마케팅 작업과 관련된 정책을 관리하고 평가하는 UI입니다. 정책을 만들고 업데이트하며, 정책의 상태를 확인하고, 마케팅 작업을 통해 특정 작업이 데이터 사용 정책을 위반하는지 평가할 수 있습니다.

>[!IMPORTANT]
>
>모든 데이터 사용 정책(Adobe에서 제공하는 핵심 정책 포함)은 기본적으로 비활성화됩니다. 개별 정책을 적용하려면 API 또는 UI를 통해 해당 정책을 수동으로 활성화해야 합니다.

API에서 마케팅 작업 및 데이터 사용 정책 작업에 대한 단계별 지침은 [데이터 사용 정책 생성 및 평가](create.md). 자세한 내용은 [!DNL Policy Service] API인 경우 [정책 서비스 개발자 안내서](../api/getting-started.md).

에서 마케팅 작업 및 정책을 사용하는 방법에 대한 자세한 내용은 [!DNL Platform] UI를 참조하고 [데이터 사용 정책 사용 안내서](./user-guide.md).

## 다음 단계

이 문서에서는 Data Governance 프레임워크 내의 데이터 사용 정책을 소개합니다. 이제 API 및 UI에서 정책을 사용하여 작업하는 방법에 대한 자세한 내용은 이 안내서 전체에서 연결된 프로세스 설명서를 계속 읽을 수 있습니다.

## 부록

다음 섹션에서는 데이터 사용 정책에 대한 추가 정보를 제공합니다.

### Adobe 정의 마케팅 작업 {#core-actions}

아래 표는 Adobe에서 기본적으로 제공하는 핵심 마케팅 작업에 대해 설명합니다.

>[!NOTE]
>
>핵심 마케팅 작업은 위반을 생성하고 확인하기 위한 사용 정책을 식별하는 데 도움이 되는 시작점으로 표시되어야 합니다. 정의 및 해석 방법은 조직의 요구 사항과 정책에 따라 다릅니다.

| 마케팅 작업 | 설명 |
| --- | --- |
| Analytics | 조직의 사이트 또는 앱에서 고객의 사용 측정, 분석 및 보고와 같이 데이터를 분석 목적으로 사용하는 작업입니다. |
| 직접 식별 가능한 데이터와 결합 | PII(개인 식별 정보)를 익명의 데이터와 결합하는 작업입니다. 광고 네트워크, 광고 서버 및 타사 데이터 공급자로부터 가져온 데이터에 대해 계약에는 직접 식별 가능한 데이터로 이러한 데이터를 사용하는 것에 대한 특정 계약 금지가 포함되는 경우가 많습니다. |
| 사이트 간 타깃팅 | 사이트 간 광고 타깃팅에 데이터를 사용하는 작업입니다. 온사이트 데이터와 오프사이트 데이터의 조합 또는 여러 오프사이트 소스의 데이터 조합을 포함하여 여러 사이트의 데이터 조합을 교차 사이트 데이터라고 합니다. 사이트 간 데이터는 일반적으로 수집 및 처리되어 사용자의 관심사에 대한 참조를 만듭니다. |
| Data Science | 데이터 과학 워크플로우에 데이터를 사용하는 작업입니다. 일부 계약에는 데이터 과학을 위한 데이터 사용에 대한 명시적 금지 사항이 포함됩니다. 경우에 따라 AI(인공 지능), ML(기계 학습) 또는 모델링을 위해 데이터를 사용할 수 없다는 용어가 있습니다. |
| 이메일 타겟팅 | 이메일 타겟팅 캠페인에서 데이터를 사용하는 작업입니다. |
| 타사로 내보내기 | 고객과 직접적인 관계가 없는 프로세서 및 엔티티로 데이터를 내보내는 작업입니다. 많은 데이터 제공업체는 원래 수집된 위치에서 데이터를 내보내지 못하도록 하는 계약 조건을 가지고 있습니다. 예를 들어 소셜 네트워크 계약은 종종 그로부터 받는 데이터 전송을 제한합니다. |
| 온사이트 광고 | 조직의 웹 사이트 또는 앱에서 광고를 선택 및 게재하는 등 온사이트 광고에 데이터를 사용하거나 이러한 광고의 게재 및 효과를 측정하는 작업입니다. |
| 온사이트 개인화 | 온사이트 컨텐츠 개인화에 데이터를 사용하는 작업. 온사이트 개인화는 사용자의 관심사에 대해 추론하는 데 사용되는 모든 데이터이며, 이러한 환경 설정을 기반으로 제공되는 콘텐츠 또는 광고를 선택하는 데 사용됩니다. |
| 세그먼트 일치 | 두 명 이상의 Platform 사용자가 세그먼트 데이터를 교환할 수 있는 Adobe Experience Platform 세그먼트 일치에 데이터를 사용하는 작업입니다. 이 작업을 참조하는 정책을 활성화하면 세그먼트 일치에 사용되는 데이터를 제한할 수 있습니다. 예를 들어 핵심 정책 &quot;데이터 공유 제한&quot;이 활성화되어 있으면 [C11 레이블](../labels/reference.md#c11) 세그먼트 일치에 사용할 수 없습니다. |
| 단일 ID 개인화 | 여러 소스의 ID를 결합하는 대신 단일 ID를 개인화 용도로 사용해야 하는 작업입니다. |
