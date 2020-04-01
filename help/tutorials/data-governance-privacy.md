---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 거버넌스 및 개인 정보 보호 자습서
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# 데이터 거버넌스 및 개인 정보 보호 자습서

DULE(Data Usage Lawring and Enforcement)는 Adobe Experience Platform 데이터 거버넌스의 핵심 메커니즘입니다. DULE 기능을 사용하면 데이터 세트 및 필드에 데이터 사용 레이블을 적용하여 관련 데이터 사용 정책에 따라 각 세그먼트를 분류할 수 있습니다. 레이블을 시작하기 전에 플랫폼 내의 DULE [프레임워크에 대한 보다 강력한 소개를](../data-governance/home.md) 보려면 데이터 거버넌스 개요를 참조하십시오.

Adobe Experience Platform 개인 정보 보호 서비스는 다양한 솔루션에서 개인 정보 보호 및 규정 준수 요청을 조정할 수 있는 RESTful API와 사용자 인터페이스를 제공합니다. 자세한 내용은 개인정보 보호 서비스 개요를 [읽어 보시기](../privacy-service/home.md)바랍니다.

## 데이터 사용 레이블 추가

데이터 사용 레이블을 사용하면 데이터 세트에 적용되는 사용 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터 관리 방식을 유연하게 선택할 수 있습니다. 모범 사례는 Adobe Experience Platform에서 인제스트되는 즉시 또는 플랫폼에서 사용할 수 있는 데이터가 확보되는 즉시 레이블 지정 데이터를 권장합니다. 데이터 집합 수준에서 적용되는 데이터 사용 레이블은 데이터 집합 내의 모든 필드에 전파됩니다. 또한 데이터 세트에서 전달하지 않고 개별 필드(열 헤더)에 직접 레이블을 적용할 수 있습니다. 데이터에 데이터 사용 레이블을 적용하는 방법에 대한 자세한 내용은 [데이터 사용 레이블 개요를](../data-governance/labels/overview.md)참조하십시오.

## 데이터 사용 정책 만들기

DULE 정책 서비스 API를 사용하면 DULE 정책을 만들고 관리하여 특정 DULE 레이블이 포함된 데이터에 대해 수행할 수 있는 마케팅 작업을 결정할 수 있습니다. 시작하려면 [데이터 사용 정책 개요를](../data-governance/policies/overview.md)참조하십시오.

## 데이터 사용 정책 적용

데이터에 대한 데이터 사용 레이블 지정 및 적용(DULE 파섹) 레이블을 만들고 이러한 레이블에 대한 마케팅 작업에 대한 DULE 정책을 만들었으면 DULE 정책 서비스 API를 사용하여 데이터 세트에 대해 수행된 마케팅 작업 또는 임의 DULE 레이블 그룹이 정책 위반을 구성하는지 평가할 수 있습니다. 그런 다음 자체 내부 프로토콜을 설정하여 API 응답을 기반으로 정책 위반을 처리할 수 있습니다. 시작하려면 [정책 적용 개요를](../data-governance/enforcement/overview.md)참조하십시오.

## 고객 세그먼트에 대한 데이터 사용 규정 준수 적용

실시간 고객 프로필에서 사용할 수 있는 세그먼트에는 세그먼트 정의 내에 병합 정책 ID가 포함되어 있습니다. 이 병합 정책에는 세그먼트에 포함할 데이터 집합에 대한 정보가 포함되며, 여기에는 적용 가능한 데이터 사용 레이블이 포함됩니다. 대상 세그먼트에 대한 데이터 사용 규정 준수를 적용하는 방법에 대한 자세한 내용은 세그먼트에 [대한](../segmentation/tutorials/governance.md)데이터 사용 규정 준수 시행 자습서를 따르십시오.

## 개인정보 보호 서비스 시작하기

개인정보 보호 서비스는 Adobe Experience Cloud 응용 프로그램에서 데이터 주체(고객)의 개인 데이터를 관리할 수 있도록 해주는 RESTful API 및 사용자 인터페이스를 제공합니다. 또한 개인 정보 보호 서비스는 Experience Cloud 응용 프로그램과 관련된 작업의 상태 및 결과에 액세스할 수 있는 중앙 감사 및 로깅 메커니즘을 제공합니다. 개인정보 보호 서비스 작업을 만들고 모니터링하는 방법에 대한 지침은 개인정보 보호 서비스 개발자 안내서 [또는 개인정보](../privacy-service/api/getting-started.md) 보호 서비스 사용 안내서에 [설명된](../privacy-service/ui/overview.md)단계를 따르십시오.