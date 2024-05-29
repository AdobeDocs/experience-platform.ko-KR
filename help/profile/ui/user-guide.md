---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;통합 프로필;통합 프로필;통합;프로필;rtcp;프로필 활성화;프로필 활성화;결합 스키마;결합 프로필;결합 프로필
title: 실시간 고객 프로필 UI 안내서
description: 실시간 고객 프로파일은 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 다양한 채널의 데이터를 취합하여 각 개별 고객을 전체적으로 파악할 수 있도록 합니다. 이 문서는 Adobe Experience Platform 사용자 인터페이스에서 실시간 고객 프로필과 상호 작용하기 위한 안내서 역할을 합니다.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] UI 안내서

[!DNL Real-Time Customer Profile] 은 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 취합하여 각 개별 고객을 전체적으로 파악할 수 있도록 합니다. 이 문서는 상호 작용을 위한 안내서 역할을 합니다 [!DNL Real-Time Customer Profile] Adobe Experience Platform UI(사용자 인터페이스)의 데이터입니다.

## 시작하기

이 UI 안내서를 사용하려면 다양한 내용을 이해해야 합니다 [!DNL Experience Platform] 관리와 관련된 서비스 [!DNL Real-Time Customer Profiles]. 이 안내서를 읽거나 UI에서 작업하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL Real-Time Customer Profile] 개요](../home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.
* [[!DNL Identity Service]](../../identity-service/home.md): 사용 [!DNL Real-Time Customer Profile] 서로 다른 데이터 소스의 id를 로 수집할 때 [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.

## [!UICONTROL 개요]

Experience Platform UI에서 **[!UICONTROL 프로필]** 을(를) 왼쪽 탐색에서 **[!UICONTROL 개요]** 프로필 대시보드를 표시하는 탭입니다.

>[!NOTE]
>
>Platform을 처음 사용하는 조직에 아직 활성 프로필 데이터 세트 또는 병합 정책을 만들지 않은 경우 [!UICONTROL 프로필] 대시보드가 표시되지 않습니다. 대신, [!UICONTROL 개요] 탭에는 실시간 고객 프로필을 시작하는 데 도움이 되는 링크 및 설명서가 표시됩니다.

### 프로필 대시보드 {#profile-dashboard}

프로필 대시보드는 조직의 프로필 데이터와 관련된 주요 지표에 대해 간략하게 설명합니다.

자세한 내용은 [프로필 대시보드 안내서](../../dashboards/guides/profiles.md).

![프로필 대시보드가 표시됩니다.](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL 찾아보기] 탭 지표

다음 항목 선택 **[!UICONTROL 찾아보기]** 조직의 프로필 데이터와 관련된 몇 가지 지표를 표시하는 탭입니다. 이 안내서의 다음 섹션에 설명된 대로 이 탭을 사용하여 병합 정책 또는 ID를 사용하여 프로필 저장소를 검색할 수도 있습니다.

의 오른쪽 **[!UICONTROL 찾아보기]** 탭은 입니다. [프로필 개수](#profile-count) 및 목록 [네임스페이스별 프로필](#profiles-by-namespace).

>[!NOTE]
>
>이러한 프로필 지표는 다음에 표시되는 지표와 다를 수 있습니다. [프로필 대시보드](#profile-dashboard) 조직의 기본 병합 정책을 사용하여 평가되기 때문입니다. 기본 병합 정책을 정의하는 방법을 포함하여 병합 정책 작업에 대한 자세한 내용은 다음을 참조하십시오. [병합 정책 개요](../merge-policies/overview.md).

이 섹션에는 이러한 지표 외에도 지표가 마지막으로 평가된 시간을 보여 주는 마지막으로 업데이트된 날짜 및 시간이 있습니다.

![프로필 지표가 표시되고 강조 표시됩니다.](../images/user-guide/browse-metrics.png)

### 프로필 개수 {#profile-count}

조직의 기본 병합 정책이 프로필 조각을 병합하여 각 개별 고객에 대한 단일 프로필을 형성한 후 프로필 수에 조직이 Experience Platform 내에 보유한 총 프로필 수가 표시됩니다. 즉, 조직에는 서로 다른 채널에서 브랜드와 상호 작용하는 단일 고객과 관련된 여러 프로필 조각이 있을 수 있지만, 이러한 조각은 기본 병합 정책에 따라 함께 병합되고 모두 동일한 개인과 관련되어 있으므로 &quot;1&quot; 프로필 수를 반환합니다.

프로필 카운트에는 속성이 있는 프로필(레코드 데이터)과 Adobe Analytics 프로필과 같이 시계열(이벤트) 데이터만 포함된 프로필이 모두 포함됩니다. 프로필 수는 Platform 내에서 최신 총 프로필 수를 제공하기 위해 정기적으로 새로 고쳐집니다.

#### 프로필 수 지표 업데이트

레코드를 로 수집할 때 [!DNL Profile] 저장소가 카운트를 5% 이상 늘리거나 줄이면 카운트를 업데이트하기 위해 작업이 트리거됩니다. 스트리밍 데이터 워크플로의 경우 5% 증가 또는 감소 임계값이 충족되었는지 확인하기 위해 시간별로 검사가 수행됩니다. 이 경우 프로필 수를 업데이트하기 위해 작업이 자동으로 트리거됩니다. 일괄 처리 수집의 경우, 프로필 스토어에 일괄 처리를 성공적으로 수집한 후 15분 이내에 5% 증가 또는 감소 임계값이 충족되면 프로필 수를 업데이트하는 작업이 실행됩니다.

### [!UICONTROL 네임스페이스별 프로필] {#profiles-by-namespace}

다음 **[!UICONTROL 네임스페이스별 프로필]** 지표는 프로필 스토어에 있는 병합된 모든 프로필의 총 네임스페이스 수 및 분류를 표시합니다. 네임스페이스별 총 프로필 수(즉, 각 네임스페이스에 대해 표시된 값을 함께 추가)는 하나의 프로필에 연결된 여러 네임스페이스가 있을 수 있으므로 항상 프로필 수 지표보다 높습니다. 예를 들어 고객이 둘 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다.

#### 업데이트 중 [!UICONTROL 네임스페이스별 프로필] 지표

와 유사 [프로필 개수](#profile-count) 지표, 레코드를 로 수집할 때 [!DNL Profile] 저장소가 카운트를 5% 이상 늘리거나 줄이면 네임스페이스 지표를 업데이트하는 작업이 트리거됩니다. 스트리밍 데이터 워크플로의 경우 5% 증가 또는 감소 임계값이 충족되었는지 확인하기 위해 시간별로 검사가 수행됩니다. 이 경우 프로필 수를 업데이트하기 위해 작업이 자동으로 트리거됩니다. 일괄 처리 수집의 경우, 일괄 처리를 성공적으로 수집한 후 15분 이내에 [!DNL Profile] 저장, 5% 증가 또는 감소 임계값이 충족되면 지표를 업데이트하는 작업이 실행됩니다.

## 사용 [!UICONTROL 찾아보기] 프로필을 보기 위한 탭

다음에서 **[!UICONTROL 찾아보기]** 탭에서는 병합 정책을 사용하여 샘플 프로필을 보거나 id 네임스페이스 및 값을 사용하여 특정 프로필을 조회할 수 있습니다.

![조직에 속한 프로필이 표시됩니다.](../images/user-guide/none-selected.png)

### 찾아보기 [!UICONTROL 병합 정책]

다음 **[!UICONTROL 찾아보기]** 탭은 기본적으로 조직의 기본 병합 정책으로 설정됩니다. 다른 병합 정책을 선택하려면 `X` 병합 정책 이름 옆에 있는 선택기를 사용하여 **[!UICONTROL 병합 정책 선택]** 대화 상자.

>[!NOTE]
>
>선택한 병합 정책이 없으면 다음 옆에 있는 선택기 버튼을 사용합니다. **[!UICONTROL 병합 정책]** 선택 대화 상자를 여는 필드입니다.

![병합 정책 선택기가 강조 표시됩니다.](../images/user-guide/browse-by-merge-policy.png)

에서 병합 정책을 선택하려면 다음을 수행하십시오. **[!UICONTROL 병합 정책 선택]** 대화 상자에서 정책 이름 옆에 있는 라디오 버튼을 선택한 다음 다음을 사용합니다. **[!UICONTROL 선택]** (으)로 돌아가기 [!UICONTROL 찾아보기] 탭. 그런 다음 을(를) 선택할 수 있습니다 **[!UICONTROL 보기]** 샘플 프로필을 새로 고치고 새 병합 정책이 적용된 프로필 샘플링을 확인합니다.

![필터링 기준으로 사용할 병합 정책을 선택할 수 있는 대화 상자가 표시됩니다.](../images/user-guide/select-merge-policy.png)

표시되는 프로필은 선택한 병합 정책이 적용된 후 조직의 프로필 저장소에서 최대 20개의 프로필 샘플을 나타냅니다. 선택한 병합 정책에 대한 샘플 프로필은 새 데이터가 조직의 프로필 저장소에 추가되면 새로 고쳐집니다.

샘플 프로필 중 하나의 세부 정보를 보려면 **[!UICONTROL 프로필 ID]**. 자세한 내용은 이 안내서의 뒷부분에 있는 섹션을 참조하십시오. [프로필 세부 정보 보기](#profile-detail).

![병합 정책과 일치하는 샘플 프로필이 표시됩니다.](../images/user-guide/sample-profiles.png)

플랫폼 내에서 병합 정책 및 해당 역할에 대한 자세한 내용은 다음을 참조하십시오. [병합 정책 개요](../merge-policies/overview.md).

### 찾아보기 [!UICONTROL 신원] {#browse-identity}

다음에서 **[!UICONTROL 찾아보기]** 탭에서 id 네임스페이스를 사용하여 id 값으로 특정 프로필을 조회할 수 있습니다. ID별로 탐색하려면 병합 정책, ID 네임스페이스 및 ID 값을 제공해야 합니다.

![병합 정책 선택기가 강조 표시됩니다.](../images/user-guide/browse-by-merge-policy.png)

필요한 경우 **[!UICONTROL 병합 정책]** 선택기: **[!UICONTROL 병합 정책 선택]** 대화 상자를 열고 사용할 병합 정책을 선택합니다.

![필터링 기준으로 사용할 병합 정책을 선택할 수 있는 대화 상자가 표시됩니다.](../images/user-guide/select-merge-policy.png)

그런 다음 **[!UICONTROL ID 네임스페이스]** 선택기: **[!UICONTROL ID 네임스페이스 선택]** 대화 상자를 열고 검색할 네임스페이스를 선택합니다. 조직에 네임스페이스가 많은 경우 대화 상자의 검색 창을 사용하여 네임스페이스 이름을 입력할 수 있습니다.

네임스페이스를 선택하여 추가 세부 정보를 보거나 라디오 단추를 선택하여 네임스페이스를 선택할 수 있습니다. 그런 다음 을 사용할 수 있습니다. **[!UICONTROL 선택]** 계속합니다.

![필터링 기준으로 사용할 ID 네임스페이스를 선택할 수 있는 대화 상자가 표시됩니다.](../images/user-guide/select-identity-namespace.png)

을(를) 선택한 후 [!UICONTROL ID 네임스페이스] 및 (으)로 돌아가기 [!UICONTROL 찾아보기] 탭에서 다음을 입력할 수 있습니다 **[!UICONTROL ID 값]** 을(를) 선택한 네임스페이스와 관련이 있습니다.

>[!NOTE]
>
>이 값은 개별 고객 프로필에 한정되며 제공된 네임스페이스에 유효한 항목이어야 합니다. 예를 들어 ID 네임스페이스 &quot;Email&quot;을 선택하려면 유효한 이메일 주소 형식의 ID 값이 필요합니다.

![필터링할 ID 값이 강조 표시됩니다.](../images/user-guide/filter-identity-value.png)

값을 입력한 후 다음을 선택합니다. **[!UICONTROL 보기]** 값과 일치하는 단일 프로필이 반환됩니다. 다음 항목 선택 **[!UICONTROL 프로필 ID]** 프로필 세부 사항을 보려면 다음을 수행하십시오.

![ID 값과 일치하는 프로필이 강조 표시됩니다.](../images/user-guide/filtered-identity-value.png)

## 프로필 세부 정보 보기 {#profile-detail}

선택 후 **[!UICONTROL 프로필 ID]**, **[!UICONTROL 세부 사항]** 탭이 열립니다. 다음에 표시되는 프로필 정보 **[!UICONTROL 세부 사항]** 탭이 여러 프로필 조각에서 함께 병합되어 개별 고객에 대한 단일 뷰를 형성했습니다. 여기에는 기본 속성, 연결된 ID 및 채널 환경 설정 등 고객 세부 정보가 포함됩니다.

표시되는 기본 필드를 조직 수준에서 변경하여 기본 프로필 속성을 표시할 수도 있습니다. 속성 추가 및 제거, 대시보드 패널 크기 조정을 위한 단계별 지침을 포함하여 이러한 필드를 사용자 지정하는 방법에 대해 자세히 알아보려면 [프로필 세부 사항 사용자 정의 안내서](profile-customization.md).

![세부 정보 탭이 강조 표시됩니다. 프로필 세부 사항이 표시됩니다.](../images/user-guide/profile-detail.png)

사용 가능한 탭 중 하나를 선택하여 개별 고객 프로필과 관련된 추가 정보를 볼 수 있습니다. 이러한 탭에는 속성, 이벤트 및 현재 프로필이 자격을 갖춘 대상자를 보여 주는 대상자 멤버십 탭이 포함됩니다.

### 속성 탭

다음 **[!UICONTROL 속성]** 지정된 병합 정책이 적용된 후 탭에서는 단일 프로필과 관련된 모든 속성을 요약하는 목록 보기가 제공됩니다.

다음 속성을 선택하여 JSON 개체로 볼 수도 있습니다. **[!UICONTROL JSON 보기]**. 이 기능은 프로필 속성이 Platform에 수집되는 방식을 더 잘 이해하고자 하는 사용자에게 유용합니다.

![[속성] 탭이 강조 표시됩니다. 프로필 속성이 표시됩니다.](../images/user-guide/attributes.png)

에지에서 사용할 수 있는 속성을 보려면 **[!UICONTROL Edge]** 를 클릭합니다.

![속성 탭 내의 데이터 위치 선택기가 강조 표시됩니다.](../images/user-guide/attributes-select.png)

에지 프로필에 대한 자세한 내용은 [edge 프로필 설명서](../edge-profiles.md).

### 이벤트 탭

다음 **[!UICONTROL 이벤트]** 탭에는 고객과 연관된 100개의 최신 ExperienceEvents의 데이터가 포함되어 있습니다. 이 데이터에는 이메일 열림, 장바구니 활동 및 페이지 보기가 포함될 수 있습니다. 선택 **[!UICONTROL 모두 보기]** 개별 이벤트에 대해 추가 필드 및 값을 이벤트의 일부로 캡처합니다.

을 선택하여 이벤트를 JSON 개체로 볼 수도 있습니다. **[!UICONTROL JSON 보기]**. 이 메서드는 Platform에서 이벤트를 캡처하는 방법을 이해하는 데 유용합니다.

![이벤트 탭이 강조 표시됩니다. 프로필 이벤트가 표시됩니다.](../images/user-guide/events.png)

### 대상자 멤버십 탭

다음 **[!UICONTROL 대상자 멤버십]** 탭에는 현재 개별 고객 프로필이 속한 대상자의 이름과 설명이 포함된 목록이 표시됩니다. 이 목록은 프로필이 대상에서 정규화되거나 만료될 때 자동으로 업데이트됩니다. 프로필이 현재 자격이 있는 총 대상자 수가 탭 오른쪽에 표시됩니다.

Experience Platform의 세그멘테이션에 대한 자세한 내용은 [Adobe Experience Platform 세그멘테이션 서비스 설명서](../../segmentation/home.md).

![대상자 멤버십 탭이 강조 표시됩니다. 프로필의 대상자 멤버십 세부 정보가 표시됩니다.](../images/user-guide/audience-membership.png)

Edge에서 사용할 수 있는 프로필의 대상 멤버십을 보려면 을 선택합니다. **[!UICONTROL Edge]** 를 입력합니다. 에지 세분화에 대한 자세한 내용은 [edge segmentation 안내서](../../segmentation/ui/edge-segmentation.md).

![대상자 멤버십 탭 내의 데이터 위치 선택기가 강조 표시됩니다.](../images/user-guide/audience-membership-select.png)

## 병합 정책

메인에서 **[!UICONTROL 프로필]** 메뉴에서 **[!UICONTROL 병합 정책]** 탭으로 조직에 속한 병합 정책 목록을 볼 수 있습니다. 나열된 각 정책의 이름, 기본 병합 정책인지 여부 및 해당 정책이 적용되는 스키마 클래스가 표시됩니다.

병합 정책에 대한 자세한 내용은 [병합 정책 개요](../merge-policies/overview.md).

![병합 정책 탭이 강조 표시됩니다. 조직에 속한 병합 정책이 표시됩니다.](../images/user-guide/merge-policies.png)

## 유니온 스키마 {#union-schema}

메인에서 **[!UICONTROL 프로필]** 메뉴에서 **[!UICONTROL 유니온 스키마]** 탭에서는 수집된 데이터에 사용 가능한 유니온 스키마를 볼 수 있습니다. 유니온 스키마는 모든 의 조합입니다. [!DNL Experience Data Model] 스키마가에서 사용할 수 있도록 설정된 동일한 클래스의 XDM(필드) [!DNL Real-Time Customer Profile].

유니온 스키마에 대한 자세한 내용은 [유니온 스키마 UI 안내서](union-schema.md).

![유니온 스키마 탭이 강조 표시됩니다. 조직에 속한 결합 스키마가 표시됩니다.](../images/user-guide/union-schema.png)

## 계산된 속성 {#computed-attributes}

메인에서 **[!UICONTROL 프로필]** 메뉴에서 **[!UICONTROL 계산된 속성]** 조직 내에 속한 계산된 속성 목록을 보려면 탭을 사용하십시오.

![계산된 속성 탭이 강조 표시됩니다.](../images/user-guide/computed-attributes.png)

계산된 속성에 대한 자세한 내용은 [계산된 속성 개요](../computed-attributes/overview.md). Platform UI 내에서 계산된 속성을 사용하는 방법에 대한 자세한 내용은 [계산된 속성 UI 안내서](../computed-attributes/ui.md).

## 다음 단계

이 안내서를 읽으면 Experience Platform UI를 사용하여 조직의 프로필 데이터를 보고 관리하는 방법을 알 수 있습니다. Experience Platform API를 사용하여 프로필 데이터로 작업하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [실시간 고객 프로필 API 안내서](../api/overview.md).
