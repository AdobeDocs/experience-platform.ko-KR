---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 거버넌스 및 개인 정보 보호 자습서
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# [!DNL Data Governance] 및 [!DNL Privacy] Tutorials

[!DNL Data Usage Labeling and Enforcement] (DULE)는 Adobe Experience Platform [!DNL Data Governanc]e의 핵심 메커니즘입니다. DULE 기능을 사용하면 데이터 세트 및 필드에 데이터 사용 레이블을 적용하여 관련 데이터 사용 정책에 따라 각 데이터를 분류할 수 있습니다. 레이블을 시작하기 전에 [데이터 거버넌스 개요](../data-governance/home.md) 를 참조하여 Within DULE 프레임워크에 대한 보다 강력한 소개를 [!DNL Platform]확인하십시오.

Adobe Experience Platform [!DNL Privacy Service] 는 다양한 솔루션에서 개인 정보 및 규정 준수 요청을 조정할 수 있는 RESTful API 및 사용자 인터페이스를 제공합니다. 자세한 내용은 [Privacy Service 개요를 읽어 보십시오](../privacy-service/home.md).

## 데이터 사용 레이블 추가

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터 관리 방식을 유연하게 선택할 수 있습니다. 우수 사례는 데이터를 인제스트되는 즉시 [!DNL Experience Platform]또는 데이터를 사용할 수 있게 되는 즉시 레이블 지정 데이터를 권장합니다 [!DNL Platform]. 데이터 집합 수준에서 적용되는 데이터 사용 레이블은 데이터 집합 내의 모든 필드에 전파됩니다. 또한 데이터 세트에 전달하지 않고 개별 필드(열 헤더)에 직접 레이블을 적용할 수 있습니다. 데이터에 데이터 사용 레이블을 적용하는 방법에 대한 자세한 내용은 [데이터 사용 레이블 개요를 참조하십시오](../data-governance/labels/overview.md).

## 데이터 사용 정책 만들기

DULE [!DNL Policy Service] API를 사용하면 DULE 정책을 만들고 관리하여 특정 DULE 레이블이 포함된 데이터에 대해 수행할 수 있는 마케팅 작업을 결정할 수 있습니다. 시작하려면 [데이터 사용 정책 개요를 참조하십시오](../data-governance/policies/overview.md).

## 데이터 사용 정책 적용

데이터에 대한 데이터 사용 레이블 지정 및 실행(DULE) 레이블을 만들고 이러한 레이블에 대한 마케팅 작업을 위한 일정 정책을 만들었다면 DULE [!DNL Policy Service] API를 사용하여 데이터 세트에 대해 수행된 마케팅 작업 또는 임의 DULE 레이블 그룹이 정책 위반인지 여부를 평가할 수 있습니다. 그런 다음 API 응답을 기반으로 정책 위반을 처리하도록 자체 내부 프로토콜을 설정할 수 있습니다. 시작하려면 [정책 실행 개요를 참조하십시오](../data-governance/enforcement/overview.md).

## 고객 세그먼트에 대한 데이터 사용 규정 준수

에서 사용할 수 있는 세그먼트에는 세그먼트 정의 내에 [!DNL Real-time Customer Profile] 병합 정책 ID가 포함됩니다. 이 병합 정책에는 세그먼트에 포함할 데이터 집합에 대한 정보가 포함되며, 이 정보에는 적용 가능한 데이터 사용 레이블이 포함됩니다. 대상 세그먼트에 대한 데이터 사용 규정 준수를 적용하는 특정 단계에 대해서는 세그먼트에 대한 [데이터 사용 규정 준수 시행 자습서를 따르십시오](../segmentation/tutorials/governance.md).

## Get started with [!DNL Privacy Service]

[!DNL Privacy Service] 는 Adobe Experience Cloud 애플리케이션에서 데이터 주체(고객)의 개인 데이터를 관리할 수 있도록 해주는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service] 또한 [!DNL Experience Cloud] 응용 프로그램과 관련된 작업의 상태 및 결과에 액세스할 수 있는 중앙 감사 및 로깅 메커니즘을 제공합니다. 작업을 만들고 모니터링하는 방법에 대한 지침을 보려면 [!DNL Privacy Service] Privacy Service 개발자 가이드 [또는](../privacy-service/api/getting-started.md) Privacy Service 사용자 안내서에 설명된 단계를 따르십시오 [](../privacy-service/ui/overview.md).