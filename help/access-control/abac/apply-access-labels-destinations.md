---
title: 액세스 레이블을 사용하여 대상 데이터 흐름에 대한 사용자 액세스 관리
description: 액세스 레이블을 사용하여 대상 데이터 흐름에 대한 사용자 액세스를 관리하여 조직의 일부 사용자만 특정 대상 데이터 흐름에 액세스할 수 있도록 하는 방법을 알아봅니다.
badgePrivateBeta: label="비공개 베타" type="Informative"
hide: true
hidefromtoc: true
role: Developer, Admin, User
source-git-commit: 5e5dc2f755be0f396dec1d3f19c166bae3bc9575
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 1%

---


# 액세스 레이블을 사용하여 대상 데이터 흐름에 대한 사용자 액세스 관리

의 일부로 [!UICONTROL 속성 기반 액세스 제어] 이제 Real-Time CDP의 기능을 사용하여 대상 데이터 흐름에 액세스 레이블을 적용할 수 있습니다. 이렇게 하면 조직의 일부 사용자만 특정 대상 데이터 흐름에 액세스할 수 있습니다.

특정 대상에 액세스 레이블을 추가하면 해당 레이블이 할당된 역할에 액세스할 수 있는 사용자만 해당 대상 데이터 흐름을 보고 편집할 수 있습니다. 대상 데이터 흐름이 레이블로 표시되지 않으면 조직에 속한 모든 사용자가 볼 수 있습니다.

이 기능을 사용할 때 대상 데이터 흐름에 액세스 레이블을 적용할 수 있기 전에 샘플 사용 사례, 사전 요구 사항 및 기타 중요한 콜아웃을 이해하려면 이 페이지를 참조하십시오.

## 전제 조건 {#prerequisites}

이 기능을 사용하기 전에 완료해야 하는 다음 전제 조건을 숙지하십시오. 을 통해 친숙해지기 [!UICONTROL 속성 기반 액세스 제어] Adobe 또한 다음 문서를 읽는 것이 좋습니다.

* [속성 기반 액세스 제어 개요](/help/access-control/abac/overview.md)
* [속성 기반 액세스 제어 엔드투엔드 가이드](/help/access-control/abac/end-to-end-guide.md)

### 권한 UI 액세스 {#access-permissions-ui}

[!UICONTROL 권한] 는 관리자가 사용자 역할과 정책을 정의하여 제품 애플리케이션 내의 기능 및 개체에 대한 권한을 관리할 수 있는 Experience Cloud 영역입니다. 읽기 [권한 섹션](/help/access-control/abac/end-to-end-guide.md#permissions) 시작합니다.

### 역할, 레이블 만들기 및 사용자 할당 {#create-roles-labels-assign-users}

다음에 대한 액세스 권한을 받은 후 [!UICONTROL 권한] UI, 사용자 또는 팀원은 역할을 설정하고 해당 역할에 필요한 레이블을 추가해야 합니다. 마지막으로 특정 레이블이 지정된 리소스에 액세스해야 하는 사용자를 역할에 추가해야 합니다. 다음 설명서 섹션을 참조하십시오.

* [새 역할 만들기](/help/access-control/abac/ui/roles.md)
* [역할에 레이블 추가](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [역할에 사용자 추가](/help/access-control/ui/users.md)

### 대상 데이터 흐름 만들기 {#create-dataflow}

데이터 흐름에 액세스 레이블을 적용하려면 먼저 원하는 대상에 연결하고 데이터 흐름을 만들어 데이터를 내보내야 합니다.

에 대한 안내서 읽기 [대상에 연결하는 중](/help/destinations/ui/connect-destination.md) 및 [대상에 대한 데이터 활성화](/help/destinations/ui/activation-overview.md). 그런 다음 목록에서 원하는 대상을 선택합니다. [사용 가능한 커넥터 카탈로그](/help/destinations/catalog/overview.md).

## 이미 사용 가능: 다른 Experience Platform 리소스에 액세스 레이블 적용 {#apply-labels-other-resources}

이 릴리스를 통해 사용자에게 특정 대상 데이터 흐름에 대한 객체 수준 액세스 권한을 부여할 수 있지만, 다음과 같은 다른 Experience Platform 리소스에서는 이미 객체 수준에 대한 액세스 권한을 부여하는 기능을 사용할 수 있습니다. [대상](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## 사용 사례 예 {#use-case-example}

대상에 대한 개체 수준 액세스 제어를 사용하면 마케터의 특정 팀이 특정 대상에만 액세스하도록 제한할 수 있습니다. 예를 들어 조직에 미국 및 영국과 같은 여러 지리적 위치에 고객 데이터가 있는 경우 마케팅 팀이 미국 위치에 대해서만 데이터 흐름을 보고 편집하고, 다른 마케팅 팀이 영국 위치에 대한 데이터 흐름을 보고 편집하도록 제한할 수 있습니다.

## 대상 데이터 흐름에 액세스 레이블 적용 {#apply-labels-to-destination-dataflow}

특정 데이터 흐름에 액세스 레이블을 적용하려면 다음을 수행하십시오.

1. 다음으로 이동 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 사용자의 액세스를 제한하려는 대상 데이터 흐름을 찾습니다.
1. 줄임표(`...`)에 있는 [!UICONTROL 이름] 열 및 사용 ![세부 정보 컨트롤 편집](/help/access-control/images/olac/key-icon.svg) **[!UICONTROL 액세스 레이블 적용]** 새 레이블을 추가하고 데이터 흐름의 기존 레이블을 관리하도록 제어합니다.
   ![대상 작업 영역의 찾아보기 보기에서 액세스 레이블 적용을 선택합니다.](/help/access-control/images/olac/apply-access-labels.png)
1. 대상 데이터 흐름에 추가할 레이블을 선택하고 **[!UICONTROL 저장]**.
   ![대상 데이터 흐름에 적용할 액세스 레이블을 선택합니다.](/help/access-control/images/olac/view-access-labels.png)
1. 이제 데이터 흐름에 액세스 레이블이 UI에 어떻게 표시되는지 확인합니다.
   ![선택한 데이터 흐름이 있는 여러 대상 데이터 흐름을 보고 액세스 레이블을 표시합니다.](/help/access-control/images/olac/dataflow-with-access-label.png)

대상 데이터 흐름이 레이블로 표시되지 않으면 모든 사용자에 대해 표시됩니다. 데이터 흐름이 하나 이상의 액세스 레이블로 표시된 경우 레이블 또는 레이블 조합이 동일한 역할에 속하는 사용자에 대해서만 표시됩니다.

대상 데이터 흐름에 표준 및 사용자 지정 레이블을 추가할 수 있습니다. 대상 데이터 흐름에 레이블을 추가한 후:

* 동일한 레이블에 대한 액세스 권한이 있는 역할에 할당된 사용자는 UI에서 새 레이블이 있는 데이터 흐름을 볼 수 있습니다. 사용자 인터페이스 또는 API를 통해 대상 데이터 흐름을 보고 편집할 수 있습니다.

* 다음의 사용자 *아님* 동일한 레이블에 대한 액세스 권한이 있는 역할에 할당된 대상 데이터 흐름에는 사용자 인터페이스 또는 API를 통해 보거나 편집할 수 있는 액세스 권한이 없습니다.

## 중요 설명선 및 알아 두어야 할 항목 {#important-callouts}

현재 액세스 레이블은 기존 데이터 흐름에만 적용할 수 있습니다. 즉, 액세스 레이블을 적용하려면 먼저 누군가가 대상에 대한 데이터 흐름을 만들어야 합니다.

해당 레이블에 대한 액세스 권한이 없는 경우 대상 데이터 흐름에 액세스 레이블을 적용할 수 없습니다.

대상 데이터 흐름에 여러 레이블을 추가할 때 데이터 흐름을 보고 편집할 수 있어야 하는 사용자를 레이블 조합이 적어도 동일한 역할에 추가해야 합니다. 예를 들어 레이블 C1, I2 및 다른 사용자 지정 레이블을 대상 데이터 흐름에 적용하는 경우 이 세 레이블의 조합에 대한 액세스 권한이 있는 역할에 추가된 사용자만 이 특정 대상 데이터 흐름을 보고 편집할 수 있습니다.

![특정 사용자만 여러 레이블이 적용된 대상에 액세스할 수 있는 방법을 보여 주는 벤 다이어그램입니다.](/help/access-control/images/olac/multiple-labels-venn.png)

## 다음 단계 {#next-steps}

이 문서의 단계에 따라 이제 조직의 일부 사용자만 특정 대상 데이터 흐름에 액세스할 수 있도록 액세스 레이블을 대상 데이터 흐름에 적용하는 방법을 이해할 수 있습니다.

다음으로,에서 지원하는 다른 기능에 대해 자세히 알아볼 수 있습니다. [!UICONTROL 속성 기반 액세스 제어] 데이터를 대상으로 활성화할 때. 예를 들어 사용자의 액세스를 다음으로 제한할 수 있습니다 [특정 필드만 보기 및 활성화](/help/access-control/abac/overview.md#destinations).