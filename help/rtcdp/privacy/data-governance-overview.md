---
title: 데이터 거버넌스 개요
seo-title: 실시간 고객 데이터 플랫폼의 데이터 거버넌스
description: '데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수할 수 있습니다. '
seo-description: '데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수할 수 있습니다. '
translation-type: tm+mt
source-git-commit: f5fbb1434b7154dcdbef12de7882ecd3d2f18d52

---


# 실시간 CDP의 데이터 거버넌스

실시간 고객 데이터 플랫폼(실시간 CDP)은 여러 엔터프라이즈 시스템의 데이터를 통합하여 마케터가 고객을 보다 효과적으로 식별, 이해 및 참여시킬 수 있도록 합니다. 이 데이터는 조직 또는 법률 규정에 의해 정의된 사용 제한을 받을 수 있습니다. 따라서 데이터를 처리할 때 실시간 CDP가 사용 정책을 준수하도록 하는 것이 중요합니다.

Adobe Experience Platform 데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수할 수 있습니다. 실시간 CDP에서 중요한 역할을 하는 Adobe Marketing Cloud를 사용하면 사용 정책을 정의하고, 해당 정책을 기반으로 데이터를 분류하고, 특정 마케팅 활동을 수행할 때 정책 위반을 확인할 수 있습니다.

실시간 CDP는 Adobe Experience Platform을 기반으로 구축되므로 대부분의 데이터 거버넌스 기능은 Experience Platform 문서에서 다룹니다. 본 문서는 경험 플랫폼의 데이터 거버넌스 [개요를](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) 보완하기 위해 작성되었으며 실시간 CDP에서 사용할 수 있는 거버넌스 기능에 대해 간략히 설명합니다. 다음 주제에 대해 다룹니다.

* [데이터에 사용 레이블 적용](#apply-usage-labels-to-your-data)
* [데이터 사용 정책 관리](#manage-data-usage-policies)
* [데이터 사용 규정 준수](#enforce-data-usage-compliance)

## 데이터에 사용 레이블 적용

데이터 거버넌스를 사용하면 데이터 세트 또는 데이터 세트 필드 수준에서 데이터에 사용 레이블을 적용할 수 있습니다. 데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터를 분류할 수 있습니다.

데이터 사용 레이블 작업에 대한 자세한 내용은 Adobe Experience Platform용 [데이터 사용 레이블 사용 안내서를](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/tutorials/dule/dule_working_with_labels.md) 참조하십시오.

## 대상에 대한 제한 설정

대상에 대한 마케팅 사용 사례를 정의하여 대상에 대한 데이터 사용 제한을 설정할 수 있습니다. 대상에 대한 사용 사례를 정의하면 사용 정책 위반을 확인하고 해당 대상으로 전송된 프로필 또는 세그먼트가 데이터 거버넌스 규칙과 호환되는지 확인할 수 있습니다.

마케팅 사용 사례는 설정 단계에서 _대상 편집_ 워크플로우에 대해 _정의할 수_ 있습니다. 자세한 내용은 대상 설명서를 참조하십시오.


## 데이터 사용 정책 관리

데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하려면 데이터 사용 정책을 정의하고 활성화해야 합니다. 데이터 사용 정책은 실시간 CDP 내에서 데이터에 대해 수행할 수 있거나 제한된 마케팅 작업의 종류를 설명하는 규칙입니다. 자세한 내용은 경험 플랫폼 데이터 거버넌스 개요의 [&quot;데이터 사용 정책&quot; 섹션을](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) 참조하십시오.

Adobe Experience Platform은 일반적인 고객 경험 사용 사례를 위한 몇 가지 **핵심 정책을** 제공합니다. 이러한 정책은 정책 서비스 개발자 안내서의 &quot;모든 정책 [목록](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)&quot; 섹션에 나와 있는 것처럼 DULE Policy Service API에 요청하여 [볼 수 있습니다](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_policy_service_developer_guide.md). 개발자 안내서의 &quot;정책 만들기&quot; 섹션에 나와 있는 것처럼 사용자 지정 사용 제한을 모델링하기 위한 사용자 **지정 정책을** 만들 수도 있습니다.

## (베타) 데이터 사용 규정 준수 강화 {#enforce-data-usage-compliance}

>[!IMPORTANT]
>이 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 요청 시 활성화할 수 있습니다. 설명서 및 기능은 변경될 수 있습니다.

데이터가 레이블이 지정되고 사용 정책이 정의되면, 정책을 통해 데이터 사용 규정을 적용할 수 있습니다. 실시간 CDP의 대상에 고객 세그먼트를 활성화할 때 데이터 거버넌스는 위반이 발생하는 경우 사용 정책을 자동으로 적용합니다.

다음 다이어그램에서는 정책 적용이 세그먼트 활성화의 데이터 흐름에 어떻게 통합되는지를 보여 줍니다.

![](assets/enforcement-flow.png)

세그먼트가 처음 활성화되면 DULE 정책 서비스는 다음 요소를 기반으로 정책 위반을 확인합니다.

* 활성화할 세그먼트 내의 필드 및 데이터 세트에 적용되는 데이터 사용 레이블입니다.
* 대상의 마케팅 목적입니다.

### 정책 위반 메시지

정책 위반이 세그먼트를 활성화하려고 시도하지 않거나 이미 활성화된 세그먼트를 [](#policy-enforcement-for-activated-segments)편집하지 않으면 작업이 금지되고 하나 이상의 정책이 위반되었음을 나타내는 팝업이 나타납니다. 팝업 왼쪽 열에서 정책 위반을 선택하여 해당 위반에 대한 세부 정보를 표시합니다.

![](assets/violation-popover.png)

[팝업의 세부 *정보* ] 탭에는 위반을 트리거한 동작이 위반 발생 이유를 나타내며 문제를 잠재적으로 해결하는 방법에 대한 제안이 있습니다.

데이터 **계보를** 클릭하여 데이터 레이블을 통해 위반이 발생한 대상, 세그먼트, 병합 정책 또는 데이터 세트를 추적합니다.

![](assets/data-lineage.png)

위반이 트리거되면 해당 **구성 요소가** 데이터 사용 정책을 준수하도록 업데이트될 때까지 활성화 시 저장 단추가 비활성화됩니다.

### 활성화된 세그먼트에 대한 정책 적용

정책 적용은 활성화된 후에도 세그먼트에 적용되므로, 정책 위반의 결과로 세그먼트나 대상에 대한 변경 사항을 제한할 수 있습니다. 대상으로 세그먼트를 활성화하는 것과 관련된 많은 구성 요소로 인해 다음 작업 중 하나가 잠재적으로 위반을 유발할 수 있습니다.

* 데이터 사용 레이블 업데이트
* 세그먼트에 대한 데이터 집합 변경
* 세그먼트 설명 변경
* 대상 구성 변경

위의 작업 중 하나라도 위반이 발생하면 해당 작업을 저장할 수 없으며 정책 위반 메시지가 표시되므로 활성화된 세그먼트가 수정 시 데이터 사용 정책을 계속 준수할 수 있습니다.

## 다음 단계

실시간 CDP의 주요 데이터 거버넌스 기능과 경험 플랫폼을 통해 데이터 거버넌스 기능을 어떻게 활용하는지 소개합니다. Adobe Experience Platform의 데이터 거버넌스 [설명서를 계속 읽어 보시기 바랍니다](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html). 이 설명서에서는 데이터 사용 레이블 및 정책 관리를 위한 단계별 워크플로우뿐만 아니라 필수 데이터 거버넌스 개념에 대한 개요를 제공합니다.