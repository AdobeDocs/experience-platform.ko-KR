---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 데이터 거버넌스 및 개인 정보 보호 자습서
topic-legacy: tutorial
type: Tutorial
description: 이 문서에서는 Adobe Experience Platform 데이터 거버넌스 및 Adobe Experience Platform Privacy Service과 관련하여 사용할 수 있는 다양한 자습서에 대한 개요를 제공합니다.
exl-id: c3cef447-b343-445b-a3ed-54f873f6dfb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# [!DNL Data Governance] 및  [!DNL Privacy] Tutorials

Adobe Experience Platform 데이터 거버넌스를 사용하면 데이터 세트 및 필드에 데이터 사용 레이블을 적용하고, 관련 데이터 사용 정책에 따라 각 항목을 분류하고, 데이터 세트 및/또는 필드에 대해 특정 작업이 수행될 때 정책 위반을 평가할 수 있습니다. 이 문서에 나와 있는 자습서를 시작하기 전에 프레임워크에 대한 보다 강력한 소개를 보려면 [[!DNL Data Governance] 개요](../data-governance/home.md)를 참조하십시오.

Adobe Experience Platform [!DNL Privacy Service]은 다양한 솔루션에서 개인 정보 보호 및 규정 준수 요청을 조정할 수 있는 RESTful API 및 사용자 인터페이스를 제공합니다. 자세한 내용은 [Privacy Service 개요](../privacy-service/home.md)를 읽으십시오.

## 데이터 사용 레이블 추가

데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터 관리 방식을 유연하게 선택할 수 있습니다. 우수 사례는 [!DNL Experience Platform]으로 인제스트되거나 [!DNL Platform]에서 데이터를 사용할 수 있게 되는 즉시 레이블 지정 데이터를 권장합니다. 데이터 집합 수준에서 적용되는 데이터 사용 레이블은 데이터 집합 내의 모든 필드에 전파됩니다. 또한 데이터 세트의 개별 필드(열 헤더)에 전달하지 않고 레이블을 직접 적용할 수도 있습니다. 데이터에 데이터 사용 레이블을 적용하는 방법에 대한 자세한 내용은 [데이터 사용 레이블 개요](../data-governance/labels/overview.md)를 참조하십시오.

## 데이터 사용 정책 만들기

[!DNL Policy Service] API를 사용하면 데이터 사용 정책을 만들고 관리하여 특정 사용 레이블이 포함된 데이터에 대해 수행할 수 있는 마케팅 작업을 결정할 수 있습니다. 시작하려면 [데이터 사용 정책 개요](../data-governance/policies/overview.md)를 읽으십시오.

## 데이터 사용 정책 적용

데이터에 대한 사용 레이블을 추가하고 해당 레이블에 대한 마케팅 조치를 위한 정책을 만들었으면 [!DNL Policy Service API]을(를) 사용하여 데이터 세트 또는 임의 사용 레이블 그룹에서 수행하는 마케팅 작업이 정책 위반인지 여부를 평가할 수 있습니다. 그런 다음 API 응답을 기반으로 정책 위반을 처리하도록 자체 내부 프로토콜을 설정할 수 있습니다. 시작하려면 [정책 적용 개요](../data-governance/enforcement/overview.md)를 방문하십시오.

## 고객 세그먼트에 대한 데이터 사용 규정 준수

[!DNL Real-time Customer Profile]에서 사용할 수 있는 세그먼트에는 해당 세그먼트 정의 내에 병합 정책 ID가 들어 있습니다. 이 병합 정책에는 세그먼트에 포함할 데이터 집합에 대한 정보가 포함되며, 이 정보에는 적용 가능한 데이터 사용 레이블이 포함됩니다. 대상 세그먼트에 대한 데이터 사용 규정 준수를 적용하는 특정 단계에 대해서는 세그먼트](../segmentation/tutorials/governance.md)에 대해 [데이터 사용 준수 적용 자습서를 따르십시오.

## [!DNL Privacy Service]  시작하기

[!DNL Privacy Service] 는 Adobe Experience Cloud 애플리케이션에서 데이터 주체(고객)의 개인 데이터를 관리할 수 있도록 해주는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service] 또한 애플리케이션과 관련된 작업의 상태 및 결과에 액세스할 수 있는 중앙 감사 및 로깅 메커니즘을  [!DNL Experience Cloud] 제공합니다. [!DNL Privacy Service] 작업을 만들고 모니터링하는 방법을 보여주는 지침은 [Privacy Service 개발자 안내서](../privacy-service/api/getting-started.md) 또는 [Privacy Service 사용자 안내서](../privacy-service/ui/overview.md)에 제공된 단계를 따르십시오.
