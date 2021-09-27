---
title: 실시간 고객 데이터 플랫폼 B2B 버전에서 두 스키마 간의 관계 정의
description: 실시간 고객 데이터 플랫폼 B2B Edition에서 두 스키마 간에 일대일 관계를 정의하는 방법을 알아봅니다.
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 0%

---

# 실시간 고객 데이터 플랫폼 B2B 버전에서 두 스키마 간의 관계를 정의합니다

>[!NOTE]
>
>실시간 고객 데이터 플랫폼 B2B Edition을 사용하지 않는 경우 [비B2B 관계 만들기](./relationship-ui.md)에 대한 안내서를 대신 참조하십시오.

실시간 고객 데이터 플랫폼 B2B 에디션은 [계정](../classes/b2b/business-account.md), [기회](../classes/b2b/business-opportunity.md), [캠페인](../classes/b2b/business-campaign.md) 등을 포함하여 기본적인 B2B 데이터 엔터티를 캡처하는 여러 XDM(Experience Data Model) 클래스를 제공합니다. 이러한 클래스를 기반으로 스키마를 구축하고 [실시간 고객 프로필](../../profile/home.md)에서 사용할 수 있도록 함으로써, 서로 다른 소스의 데이터를 결합 스키마라고 하는 통합 표현으로 병합할 수 있습니다.

그러나 결합 스키마에는 동일한 클래스를 공유하는 스키마에서 캡처된 필드만 포함할 수 있습니다. 스키마 관계가 여기에서 시작됩니다. B2B 스키마에서 관계를 구현하면 이러한 비즈니스 엔티티가 어떻게 상호 관련되는지를 설명할 수 있으며 다운스트림 세그먼테이션 사용 사례에 여러 클래스의 속성을 포함할 수 있습니다.

다음 다이어그램은 기본 구현에서 다른 B2B 클래스가 어떻게 서로 관련될 수 있는지에 대한 예를 제공합니다.

![B2B 클래스 관계](../images/tutorials/relationship-b2b/classes.png)

이 자습서에서는 실시간 CDP B2B Edition에서 두 스키마 간에 다대다 관계를 정의하는 단계를 설명합니다.

>[!NOTE]
>
>이 자습서에서는 플랫폼 UI에서 B2B 스키마 간의 관계를 수동으로 설정하는 방법에 중점을 둡니다. B2B 소스 연결에서 데이터를 가져오는 경우 자동 생성 유틸리티를 사용하여 필요한 스키마, ID 및 관계를 대신 생성할 수 있습니다. 자동 생성 유틸리티](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)를 사용하는 [에 대한 자세한 내용은 B2B 네임스페이스 및 스키마에 대한 소스 설명서를 참조하십시오.

## 시작하기

이 자습서에서는 [!DNL XDM System] UI의 [!DNL Experience Platform] 스키마 편집기에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

* [Experience Platform의 XDM 시스템](../home.md): XDM 및 의 구현에 대한 개요입니다 [!DNL Experience Platform].
* [스키마 작성 기본 사항](../schema/composition.md): XDM 스키마의 기본 구성 요소 소개.
* [ [!DNL Schema Editor]](create-schema-ui.md)를 사용하여 스키마 만들기: UI에서 스키마를 작성 및 편집하는 방법에 대한 기본 사항을 다루는 자습서입니다.

## 소스 및 대상 스키마 정의

이미 관계에 정의될 두 개의 스키마를 생성한 것으로 예상됩니다. 데모 목적으로 이 자습서에서는 비즈니스 기회(&quot;[!DNL Opportunities]&quot; 스키마에 정의됨)와 관련 비즈니스 계정(&quot;[!DNL Accounts]&quot; 스키마에 정의됨) 간의 관계를 만듭니다.

스키마 관계는 **대상 스키마**&#x200B;의 기본 ID 필드를 참조하는 **소스 스키마** 내의 전용 필드로 표시됩니다. 다음에 오는 단계에서 &quot;[!DNL Opportunities]&quot;은 소스 스키마 역할을 하지만 &quot;[!DNL Accounts]&quot;은 대상 스키마 역할을 합니다.

### B2B 관계에서의 ID 이해

관계를 설정하려면 두 스키마에 기본 ID가 정의되어 있어야 하며 [!DNL Real-time Customer Profile]에 대해 활성화되어 있어야 합니다. B2B 엔티티에 대한 기본 ID를 설정할 때는 문자열 기반 엔티티 ID가 서로 다른 시스템 또는 위치에서 수집하는 경우 겹칠 수 있으므로 Platform에서 데이터 충돌이 발생할 수 있습니다.

이를 설명하기 위해 모든 표준 B2B 클래스에는 [[!UICONTROL B2B 소스] 데이터 유형](../data-types/b2b-source.md)을 준수하는 &quot;key&quot; 필드가 포함됩니다. 이 데이터 유형은 식별자의 소스에 대한 다른 컨텍스트 정보와 함께 B2B 엔티티에 대한 문자열 식별자에 대한 필드를 제공합니다. 이 필드 중 하나인 `sourceKey` 은 데이터 유형의 다른 필드의 값을 연결하여 엔터티에 대한 완전 고유 식별자를 생성합니다. 이 필드는 항상 B2B 엔티티 스키마의 기본 ID로 사용해야 합니다.

![sourceKey 필드](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>[XDM 필드를 identity](../ui/fields/identity.md)로 설정할 때 ID를 정의하려면 ID 네임스페이스를 제공해야 합니다. Adobe이 제공하는 표준 네임스페이스 또는 조직에서 정의한 사용자 정의 네임스페이스일 수 있습니다. 실제로 네임스페이스는 단순한 컨텍스트 문자열이며 ID 유형을 분류하는 데 조직에 의미 있는 경우 원하는 값으로 설정할 수 있습니다. 자세한 내용은 [ID 네임스페이스](../../identity-service/namespaces.md)의 개요를 참조하십시오.

참조용으로 다음 섹션에서는 관계가 정의되기 전에 이 자습서에서 사용되는 각 스키마의 구조를 설명합니다. 스키마 구조와 사용 중인 사용자 지정 네임스페이스에서 기본 ID가 정의된 위치를 주목하십시오.

### [!DNL Opportunities] 스키마

소스 스키마 &quot;[!DNL Opportunities]&quot;은 [!UICONTROL XDM Business Opportunity] 클래스를 기반으로 합니다. 클래스에서 제공하는 필드 중 하나인 `opportunityKey` 은 스키마의 식별자 역할을 합니다. 특히 `opportunityKey` 개체 아래의 `sourceKey` 필드는 [!DNL B2B Opportunity] 라는 사용자 지정 네임스페이스 아래에 스키마의 기본 ID로 설정됩니다.
**[!UICONTROL 스키마 속성]**&#x200B;에 표시되는 대로 이 스키마는 [!DNL Real-time Customer Profile]에서 사용하도록 설정되었습니다.

![기회 스키마](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] 스키마

대상 스키마 &quot;[!DNL Accounts]&quot;은 [!UICONTROL XDM 계정] 클래스를 기반으로 합니다. 루트 수준 `accountKey` 필드에는 [!DNL B2B Account]라는 사용자 지정 네임스페이스 아래의 기본 ID 역할을 하는 `sourceKey`이 포함되어 있습니다. 이 스키마는 프로필에서도 사용할 수 있도록 활성화되었습니다.

![계정 스키마](../images/tutorials/relationship-b2b/accounts.png)

## 소스 스키마에 대한 관계 필드 정의 {#relationship-field}

두 스키마 간의 관계를 정의하려면 소스 스키마에 대상 스키마의 기본 ID를 참조하는 전용 필드가 있어야 합니다. 표준 B2B 클래스에는 일반적으로 관련된 비즈니스 엔터티에 대한 전용 소스 키 필드가 포함됩니다. 예를 들어 [!UICONTROL XDM Business Opportunity] 클래스에는 관련 계정(`accountKey`)과 관련 캠페인(`campaignKey`)에 대한 소스 키 필드가 포함되어 있습니다. 그러나 기본 구성 요소 이상이 필요한 경우 사용자 지정 필드 그룹을 사용하여 다른 [!UICONTROL B2B 소스] 필드를 스키마에 추가할 수도 있습니다.

>[!NOTE]
>
>현재 소스 스키마에서 대상 스키마로 일대일 관계만 정의할 수 있습니다. 일대다 관계의 경우 스키마에 &quot;다&quot;를 나타내는 관계 필드를 정의해야 합니다.

관계 필드를 설정하려면 캔버스 내의 해당 필드 옆에 있는 화살표 아이콘(![화살표 아이콘](../images/tutorials/relationship-b2b/arrow.png))을 선택합니다. [!DNL Opportunities] 스키마의 경우, 이것은 계정과 다대다 관계를 설정하는 것이 목표이므로 `accountKey.sourceKey` 필드입니다.

![관계 단추](../images/tutorials/relationship-b2b/relationship-button.png)

관계에 대한 세부 사항을 지정할 수 있는 대화 상자가 나타납니다. 관계 유형은 자동으로 **[!UICONTROL 다대다]**&#x200B;로 설정됩니다.

![관계 대화 상자](../images/tutorials/relationship-b2b/relationship-dialog.png)

**[!UICONTROL 참조 스키마]**&#x200B;에서 검색 막대를 사용하여 대상 스키마의 이름을 찾습니다. 대상 스키마의 이름을 강조 표시하면 **[!UICONTROL 참조 ID 네임스페이스]** 필드가 자동으로 스키마 기본 ID의 네임스페이스로 업데이트됩니다.

![참조 스키마](../images/tutorials/relationship-b2b/reference-schema.png)

**[!UICONTROL 현재 스키마에서 관계 이름]** 및 **[!UICONTROL 참조 스키마에서 관계 이름]** 아래에서 각각 소스 및 대상 스키마 컨텍스트에서 관계에 대한 친숙한 이름을 제공합니다. 완료되면 **[!UICONTROL 저장]** 을 선택하여 변경 사항을 적용하고 스키마를 저장합니다.

![관계 이름](../images/tutorials/relationship-b2b/relationship-name.png)

이제 관계 필드가 이전에 제공한 친숙한 이름으로 표시되어 캔버스가 다시 나타납니다. 쉽게 참조할 수 있도록 왼쪽 레일 아래에도 관계 이름이 나열되어 있습니다.

![적용된 관계](../images/tutorials/relationship-b2b/relationship-applied.png)

대상 스키마의 구조를 볼 경우, 관계 마커는 스키마의 기본 ID 필드 옆에, 왼쪽 레일에 나타납니다.

![대상 스키마 관계 마커](../images/tutorials/relationship-b2b/destination-relationship.png)

## 다음 단계

이 자습서를 따라 [!DNL Schema Editor] 을 사용하여 두 스키마 간에 다대다 관계를 만들었습니다. 이러한 스키마를 기반으로 하는 데이터 세트를 사용하여 데이터를 수집하여 프로필 데이터 저장소에서 데이터가 활성화되면 두 스키마의 속성을 여러 클래스 세그먼테이션 사용 사례에 사용할 수 있습니다. 자세한 내용은 실시간 CDP B2B Edition에 대한 설명서를 참조하십시오.
