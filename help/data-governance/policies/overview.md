---
keywords: Experience Platform;홈;인기 항목;dule;DULE
solution: Experience Platform
title: 데이터 사용 정책 개요
description: 데이터 사용 정책은 Adobe Experience Platform 내에서 데이터 수행을 허용하거나 제한하는 마케팅 작업 종류를 설명하는 규칙입니다.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 17%

---

# 데이터 사용 정책 개요 {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="데이터 사용 제한"
>abstract="데이터 사용 정책 유형은 마케팅 활동 데이터 사용을 제한하기 위해 데이터 거버넌스 레이블에 적용되는 특정 마케팅 작업을 평가합니다."

데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하려면 데이터 사용 정책을 구현해야 합니다. 데이터 사용 정책은 [!DNL Experience Platform] 내의 데이터 수행을 허용하거나 제한하는 마케팅 작업의 종류를 설명하는 규칙입니다.

두 가지 유형의 정책을 사용할 수 있습니다.

* **[!UICONTROL 데이터 거버넌스 정책]**: 수행되는 마케팅 작업과 해당 데이터가 전달하는 데이터 사용 레이블을 기반으로 데이터 활성화를 제한합니다.
* **[!UICONTROL 동의 정책]**: 고객의 동의 또는 환경 설정에 따라 [대상](../../destinations/home.md)에 대해 활성화할 수 있는 프로필을 필터링합니다.

>[!NOTE]
>
>데이터 사용 정책은 조직의 특정 Experience Platform 사용자가 특정 데이터 필드에 액세스할 수 있는지 여부를 결정하는 [액세스 제어 정책](../../access-control/abac/end-to-end-guide.md#policy)과 혼동하지 않으며 [!UICONTROL 권한] 탭을 통해 구성됩니다.

이 문서에서는 데이터 사용 정책에 대한 높은 수준의 개요를 제공하며 UI 또는 API에서 정책 작업을 수행하기 위한 추가 설명서에 대한 링크를 제공합니다.

## 마케팅 액션 {#marketing-actions}

데이터 거버넌스 프레임워크의 컨텍스트에서 마케팅 작업(마케팅 사용 사례라고도 함)은 [!DNL Experience Platform] 데이터 소비자가 수행할 수 있는 작업이며, 조직에서 데이터 사용을 제한하려고 합니다. 따라서 데이터 사용 정책은 다음과 같이 정의됩니다.

1. 특정 마케팅 액션
2. 해당 작업이 수행되는 것이 제한되는 조건

마케팅 액션의 예로는 데이터 세트를 서드파티 서비스로 내보내는 작업이 있을 수 있습니다. 특정 유형의 데이터(예: PII(개인 식별 정보))를 내보낼 수 없다는 정책이 있는 경우 &quot;I&quot; 레이블(ID 데이터)이 포함된 데이터 세트를 내보내려고 하면 [!DNL Policy Service]에서 데이터 사용 정책을 위반했다는 응답을 받게 됩니다.

>[!NOTE]
>
>마케팅 액션 자체는 데이터 사용을 제한하지 않습니다. 이러한 작업을 정책 위반에 대해 평가하려면 활성화된 데이터 사용 정책에 포함되어야 합니다.

조직의 서비스에서 데이터 사용이 발생할 때 정책 위반을 식별할 수 있도록 관련 마케팅 작업을 표시해야 합니다. 그런 다음 [정책 서비스 API](https://www.adobe.io/experience-platform-apis/references/policy-service/)를 사용하여 통합에서 정책 위반을 확인할 수 있습니다.

>[!NOTE]
>
>대상에 대한 마케팅 사용 사례를 설정하여 정책 시행을 자동화할 수 있습니다. 특정 대상의 구성 옵션에 대한 자세한 내용은 [대상 설명서](../../destinations/home.md)를 참조하십시오.

[사용 가능한 Adobe 정의 마케팅 작업](#core-actions) 목록은 이 문서의 부록을 참조하십시오. [!DNL Policy Service] API 또는 [!DNL Experience Platform] 사용자 인터페이스를 사용하여 사용자 지정 마케팅 작업을 정의할 수도 있습니다. 마케팅 작업 및 정책 작업에 대한 자세한 내용은 다음 섹션에 나와 있습니다.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share audiences with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager audiences are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Experience Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 데이터 사용 정책 관리 {#manage}

데이터 사용 레이블이 적용되면 데이터 관리자는 [!DNL Policy Service] API 또는 [!DNL Experience Platform] UI를 사용하여 데이터 사용 레이블이 포함된 데이터에 대해 수행되는 마케팅 작업과 관련된 정책을 관리하고 평가할 수 있습니다. 정책을 만들고 업데이트하며, 정책의 상태를 결정하고, 마케팅 작업을 통해 특정 작업이 데이터 사용 정책을 위반하는지 여부를 평가할 수 있습니다.

>[!IMPORTANT]
>
>모든 데이터 사용 정책(Adobe에서 제공하는 핵심 정책 포함)은 기본적으로 비활성화되어 있습니다. 개별 정책을 적용하여 시행하려면 API 또는 UI를 통해 해당 정책을 수동으로 활성화해야 합니다.

API에서 마케팅 작업 및 데이터 사용 정책을 사용하는 방법에 대한 단계별 지침은 [데이터 사용 정책 만들기 및 평가](create.md)에 대한 자습서를 참조하십시오. [!DNL Policy Service] API에서 제공하는 주요 작업에 대한 자세한 내용은 [정책 서비스 개발자 안내서](../api/getting-started.md)를 참조하십시오.

[!DNL Experience Platform] UI에서 마케팅 작업 및 정책으로 작업하는 방법에 대한 자세한 내용은 [데이터 사용 정책 사용 안내서](./user-guide.md)를 참조하십시오.

## 다음 단계

이 문서에서는 데이터 거버넌스 프레임워크 내의 데이터 사용 정책에 대해 소개합니다. 이제 이 안내서 전체에 연결된 프로세스 설명서를 계속 읽어서 API 및 UI에서 정책으로 작업하는 방법에 대해 자세히 알아볼 수 있습니다.

## 부록

다음 섹션에서는 데이터 사용 정책에 대한 추가 정보를 제공합니다.

### Adobe 정의 마케팅 작업 {#core-actions}

아래 표는 Adobe에서 즉시 사용할 수 있도록 제공하는 핵심 마케팅 작업에 대해 설명합니다.

>[!NOTE]
>
>핵심 마케팅 작업은 생성할 사용 정책을 식별하고 위반 여부를 확인하는 데 도움이 되는 시작점으로 간주되어야 합니다. 정의 및 해석 방법은 조직의 요구 사항 및 정책에 따라 다릅니다.

| 마케팅 액션 | 설명 |
| --- | --- |
| Analytics | 조직의 사이트 또는 앱에 대한 고객의 사용을 측정, 분석 및 보고하는 것과 같은 분석 목적으로 데이터를 사용하는 작업입니다. |
| 직접 식별 가능한 데이터와 결합 | PII(개인 식별 가능 정보)를 익명 데이터와 결합하는 작업입니다. 광고 네트워크, 광고 서버 및 서드파티 데이터 공급자가 제공한 데이터에 대한 계약은 종종 직접 식별 가능한 데이터와 함께 이러한 데이터의 사용에 대한 특정 계약상의 금지를 포함합니다. |
| 크로스 사이트 타겟팅 | 사이트 간 광고 타겟팅에 데이터를 사용하는 작업입니다. 온사이트 데이터와 오프사이트 데이터의 조합 또는 여러 오프사이트 소스의 데이터 조합을 포함하는 여러 사이트의 데이터 조합을 크로스 사이트 데이터라고 합니다. 크로스 사이트 데이터는 일반적으로 사용자의 관심 분야를 추론하기 위해 수집 및 처리됩니다. |
| 데이터 과학 | 데이터 과학 워크플로에 데이터를 사용하는 작업입니다. 일부 계약에는 데이터 과학을 위한 데이터 사용에 대한 명시적 금지가 포함되어 있습니다. 이는 인공 지능(AI), 머신 러닝(ML) 또는 모델링을 위한 데이터 사용을 금지하는 용어로 표현됩니다. |
| 데이터 내보내기 | Adobe 제품 및 서비스 외부의 모든 위치 또는 대상으로 데이터를 내보내는 작업입니다. 예를 들어, 데이터를 로컬 시스템으로 다운로드하고, 화면에서 데이터를 복사하고, Adobe, Customer Journey Analytics 예약된 프로젝트, 보고서 다운로드, 보고 API 등의 외부에 데이터 전달을 예약합니다. |
| 이메일 타겟팅 | 이메일 타겟팅 캠페인에서 데이터를 사용하는 액션입니다. |
| 서드파티로 내보내기 | 고객과 직접적인 관계가 없는 프로세서 및 엔티티에 데이터를 내보내는 작업입니다. 많은 데이터 공급자는 원래 데이터가 수집되었던 곳에서 데이터를 내보내는 것을 금지하는 조건을 계약서에 포함합니다. 예를 들어, 소셜 네트워크 계약은 종종 수신된 데이터의 전송을 제한합니다. |
| 온사이트 Advertising | 조직의 웹 사이트 또는 앱에서 광고를 선택하고 게재하는 작업을 포함하여 온사이트 광고에 대한 데이터를 사용하거나 이러한 광고의 전달 및 효과를 측정하는 작업입니다. |
| 온사이트 Personalization | 온사이트 콘텐츠 개인화에 데이터를 사용하는 작업입니다. 온사이트 개인화는 사용자의 관심 분야를 추론하는 데 사용되는 모든 데이터이며 이러한 추론을 기반으로 어떤 콘텐츠 또는 광고를 제공할지 선택하는 데 사용됩니다. |
| 세그먼트 일치 | 두 명 이상의 Adobe Experience Platform 사용자가 대상 데이터를 교환할 수 있도록 Experience Platform 세그먼트 일치에 데이터를 사용하는 작업입니다. 이 작업을 참조하는 정책을 활성화하여 세그먼트 일치에 사용되는 데이터를 제한할 수 있습니다. 예를 들어 핵심 정책 &quot;데이터 공유 제한&quot;을 사용하도록 설정한 경우 [C11 레이블이](../labels/reference.md#c11)인 데이터는 세그먼트 일치에 사용할 수 없습니다. |
| 단일 ID Personalization | 여러 소스의 ID를 연결하는 대신 개인화 목적으로 단일 ID를 사용해야 하는 작업입니다. |
