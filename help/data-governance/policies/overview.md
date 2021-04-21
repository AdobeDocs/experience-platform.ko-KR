---
keywords: Experience Platform;홈;인기 항목;일정;DULE
solution: Experience Platform
title: 데이터 사용 정책 개요
topic-legacy: policies
description: 데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하기 위해서는 데이터 사용 정책을 구현해야 합니다. 데이터 사용 정책은 Experience Platform 내에서 데이터에 대해 수행하도록 허용되거나 제한된 마케팅 작업의 종류를 설명하는 규칙입니다.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# 데이터 사용 정책 개요

데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하기 위해서는 데이터 사용 정책을 구현해야 합니다. 데이터 사용 정책은 [!DNL Experience Platform] 내의 데이터에 대해 수행하도록 허용되거나 제한된 마케팅 작업의 종류를 설명하는 규칙입니다.

이 문서에서는 데이터 사용 정책에 대한 개요 및 UI 또는 API에서 정책 작업을 위한 추가 설명서에 대한 링크를 제공합니다.

## 마케팅 작업 {#marketing-actions}

데이터 거버넌스 프레임워크 컨텍스트에서 마케팅 작업(마케팅 사용 사례라고도 함)은 데이터 사용을 제한하기 위해 사용자가 [!DNL Experience Platform] 데이터 소비자가 할 수 있는 작업입니다. 따라서 데이터 사용 정책은 다음과 같이 정의됩니다.

1. 특정 마케팅 작업
2. 작업이 제한되는 데이터 사용 레이블

마케팅 작업의 예는 데이터 세트를 제3자 서비스로 내보내려는 것일 수 있습니다. 특정 유형의 데이터(예: PII)를 내보낼 수 없고 &quot;I&quot; 레이블(ID 데이터)이 포함된 데이터 세트를 내보내려고 하면 데이터 사용 정책을 위반했음을 알리는 [!DNL Policy Service]의 응답이 수신됩니다.

>[!NOTE]
>
>마케팅 활동 자체만으로는 데이터 사용을 제한하지 않습니다. 이러한 작업이 정책 위반에 대해 평가되도록 하려면 활성화된 데이터 사용 정책에 포함되어야 합니다.

데이터 사용이 조직의 서비스에서 발생하는 경우 정책 위반을 식별할 수 있도록 관련 마케팅 조치를 표시해야 합니다. 그런 다음 [정책 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)를 사용하여 통합에서 정책 위반을 확인할 수 있습니다.

>[!NOTE]
>
>[!DNL Real-time Customer Data Platform]을(를) 사용하는 경우 대상에 마케팅 사용 사례를 설정하여 정책 적용을 자동화할 수 있습니다. 자세한 내용은 [실시간 CDP](../../rtcdp/privacy/data-governance-overview.md)의 데이터 거버넌스 문서를 참조하십시오.

[사용 가능한 Adobe 정의 마케팅 작업](#core-actions)의 목록은 이 문서의 부록을 참조하십시오. [!DNL Policy Service] API 또는 [!DNL Experience Platform ] 사용자 인터페이스를 사용하여 고유한 사용자 지정 마케팅 작업을 정의할 수도 있습니다. 마케팅 작업 및 정책 작업에 대한 자세한 내용은 다음 섹션을 참조하십시오.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## 데이터 사용 정책 관리 {#manage}

데이터 사용 레이블이 적용되면 데이터 관리자는 [!DNL Policy Service] API 또는 [!DNL Experience Platform] UI를 사용하여 데이터 사용 레이블이 포함된 데이터에 대해 수행되는 마케팅 작업과 관련된 정책을 관리하고 평가할 수 있습니다. 정책을 생성 및 업데이트하고, 정책의 상태를 결정하고, 마케팅 작업을 통해 특정 작업이 데이터 사용 정책을 위반하는지 평가할 수 있습니다.

>[!IMPORTANT]
>
>모든 데이터 사용 정책(Adobe에서 제공하는 핵심 정책 포함)은 기본적으로 비활성화됩니다. 개별 정책을 적용하려면 API 또는 UI를 통해 해당 정책을 수동으로 활성화해야 합니다.

API에서 마케팅 작업 및 데이터 사용 정책을 사용한 작업에 대한 단계별 지침은 [데이터 사용 정책 만들기 및 평가](create.md)에 대한 자습서를 참조하십시오. [!DNL Policy Service] API에서 제공하는 키 작업에 대한 자세한 내용은 [정책 서비스 개발자 안내서](../api/getting-started.md)를 참조하십시오.

[!DNL Platform] UI에서 마케팅 작업 및 정책으로 작업하는 방법에 대한 자세한 내용은 [데이터 사용 정책 사용 사용자 안내서](./user-guide.md)를 참조하십시오.

## 다음 단계

이 문서에서는 [!DNL Data Governance] 프레임워크 내의 데이터 사용 정책을 소개합니다. 이제 API 및 UI에서 정책을 사용하여 작업하는 방법에 대한 자세한 내용은 이 안내서 전체에서 연결된 프로세스 설명서를 계속 참조할 수 있습니다.

## 부록

다음 섹션에서는 데이터 사용 정책에 대한 추가 정보를 제공합니다.

### Adobe 정의 마케팅 작업 {#core-actions}

아래 표는 Adobe에서 기본적으로 제공하는 핵심 마케팅 작업에 대해 설명합니다.

>[!NOTE]
>
>핵심 마케팅 작업은 위반을 만들고 확인할 사용 정책을 식별하는 데 도움이 되는 시작점으로 보아야 합니다. 정의 및 해석 방법은 조직의 요구 사항과 정책에 따라 다릅니다.

| 마케팅 활동 | 설명 |
| --- | --- |
| Analytics | 조직의 사이트 또는 앱 사용을 측정, 분석 및 보고하는 등 분석 목적으로 데이터를 사용하는 작업입니다. |
| PII와 결합 | PII(개인 식별 정보)와 익명 데이터를 결합하는 작업입니다. 광고 네트워크, 광고 서버 및 제3자 데이터 공급자로부터 제공되는 데이터에 대한 계약에는 이러한 데이터를 직접 식별할 수 있는 데이터와 함께 사용하는 것에 대한 특정 계약 금지 규정이 포함되어 있습니다. |
| 사이트 간 타깃팅 | 사이트 간 광고 타깃팅에 데이터를 사용하는 작업입니다. 사이트 내 데이터와 오프사이트 데이터의 조합 또는 여러 오프라인 소스의 데이터 조합을 포함하여 여러 사이트의 데이터 조합을 사이트 간 데이터라고 합니다. 사이트 간 데이터는 일반적으로 사용자 관심사에 대한 참조를 위해 수집 및 처리됩니다. |
| Data Science | 데이터 과학 워크플로우에 데이터를 사용하는 작업입니다. 일부 계약에는 데이터 과학을 위한 데이터 사용에 대한 명시적 금지 사항이 포함되어 있습니다. 경우에 따라 AI(인위적 Intelligence), 머신 러닝(ML) 또는 모델링에 대한 데이터 사용을 금지하는 용어로 표현됩니다. |
| 이메일 타깃팅 | 이메일 타깃팅 캠페인의 데이터를 사용하는 작업입니다. |
| 제3자로 내보내기 | 고객과 직접적인 관계가 없는 프로세서 및 엔티티로 데이터를 내보내는 작업입니다. 많은 데이터 제공업체는 원래 데이터가 수집된 위치에서 내보내기를 금지하는 계약서에 조건을 가지고 있습니다. 예를 들어, 소셜 네트워크 계약에서는 종종 해당 계약으로부터 받는 데이터의 전송을 제한합니다. |
| 온사이트 광고 | 조직의 웹사이트 또는 앱에서 광고를 선택 및 배달하거나 이러한 광고의 전달 및 효과를 측정하기 위해 온사이트 광고에 데이터를 사용하는 행위 |
| 온사이트 개인화 | 온사이트 컨텐츠 개인화에 데이터를 사용하는 작업입니다. 온사이트 개인화는 사용자의 관심사에 대한 참조를 만드는 데 사용되는 모든 데이터로 이러한 참조를 기반으로 제공되는 컨텐트 또는 광고를 선택하는 데 사용됩니다. |
| 단일 ID 개인화 | 여러 소스에서 ID를 결합하는 대신 개인화를 위해 단일 ID를 사용해야 하는 작업입니다. |
