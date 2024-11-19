---
keywords: Experience Platform;홈;IAB;IAB 2.0;동의;동의
solution: Experience Platform
title: IAB TCF 2.0 동의 데이터 캡처를 위한 데이터 세트 만들기
description: 이 문서에서는 IAB TCF 2.0 동의 데이터를 수집하기 위한 두 개의 필수 데이터 세트를 설정하는 단계를 제공합니다.
role: Developer
feature: Consent, Schemas, Datasets
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: bf651967714745a0b501dcb27373379fe014c9e1
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 0%

---

# IAB TCF 2.0 동의 데이터를 캡처하기 위한 데이터 세트 만들기

Adobe Experience Platform이 IAB [!DNL Transparency & Consent Framework](TCF) 2.0에 따라 고객 동의 데이터를 처리하려면 스키마에 TCF 2.0 동의 필드가 포함된 데이터 세트로 해당 데이터를 보내야 합니다.

특히 TCF 2.0 동의 데이터를 캡처하려면 다음 두 데이터 세트가 필요합니다.

* [!DNL Real-Time Customer Profile]에서 사용할 수 있도록 설정된 [!DNL XDM Individual Profile] 클래스를 기반으로 한 데이터 집합입니다.
* [!DNL XDM ExperienceEvent] 클래스를 기반으로 하는 데이터 집합입니다.

>[!IMPORTANT]
>
>Platform은 개별 프로필 데이터 세트에 수집된 TCF 문자열만 적용합니다. 이 워크플로우의 일부로 데이터 스트림을 만드는 데 ExperienceEvent 데이터 세트가 여전히 필요하지만, 데이터를 프로필 데이터 세트로 수집하기만 하면 됩니다. 시간이 지남에 따라 동의 변경 이벤트를 추적하려는 경우에도 ExperienceEvent 데이터 세트를 사용할 수 있지만, 이러한 값은 세그먼트 활성화를 적용할 때에서 사용되지 않습니다.

이 문서에서는 이러한 두 데이터 세트를 설정하는 단계를 제공합니다. TCF 2.0에 대한 플랫폼 데이터 작업을 구성하는 전체 워크플로에 대한 개요는 [IAB TCF 2.0 준수 개요](./overview.md)를 참조하십시오.

## 전제 조건

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [XDM(경험 데이터 모델)](../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../xdm/schema/composition.md): XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
* [Adobe Experience Platform ID 서비스](../../../../identity-service/home.md): 다양한 데이터 소스에서 장치 및 시스템에 고객 ID를 연결할 수 있습니다.
   * [ID 네임스페이스](../../../../identity-service/features/namespaces.md): 고객 ID 데이터는 Identity Service에서 인식하는 특정 ID 네임스페이스에 제공되어야 합니다.
* [실시간 고객 프로필](../../../../profile/home.md): [!DNL Identity Service]을(를) 활용하여 데이터 세트에서 실시간으로 세부 고객 프로필을 만들 수 있습니다. [!DNL Real-Time Customer Profile]은(는) 데이터 레이크에서 데이터를 가져오고 고객 프로필을 별도의 데이터 저장소에 유지합니다.

## TCF 2.0 필드 그룹 {#field-groups}

[!UICONTROL IAB TCF 2.0 동의 세부 정보] 스키마 필드 그룹은 TCF 2.0 지원에 필요한 고객 동의 필드를 제공합니다. 이 필드 그룹에는 [!DNL XDM Individual Profile] 클래스와 호환되는 버전과 [!DNL XDM ExperienceEvent] 클래스와 호환되는 버전이 있습니다.

아래 섹션에서는 수집 중에 예상되는 데이터를 포함하여 이러한 각 필드 그룹의 구조를 설명합니다.

### 프로필 필드 그룹 {#profile-field-group}

[!DNL XDM Individual Profile]을(를) 기반으로 하는 스키마의 경우 [!UICONTROL IAB TCF 2.0 동의 세부 정보] 필드 그룹은 고객 ID를 TCF 동의 환경 설정에 매핑하는 단일 맵 유형 필드 `identityPrivacyInfo`을(를) 제공합니다. 자동 시행을 수행하려면 실시간 고객 프로필에 대해 활성화된 레코드 기반 스키마에 이 필드 그룹이 포함되어야 합니다.

해당 구조 및 사용 사례에 대한 자세한 내용은 이 필드 그룹의 [참조 안내서](../../../../xdm/field-groups/profile/iab.md)를 참조하세요.

### 이벤트 필드 그룹 {#event-field-group}

시간에 따른 동의 변경 이벤트를 추적하려면 [!UICONTROL IAB TCF 2.0 동의 세부 정보] 필드 그룹을 [!UICONTROL XDM ExperienceEvent] 스키마에 추가할 수 있습니다.

시간 경과에 따른 동의 변경 이벤트를 추적할 계획이 없는 경우 이벤트 스키마에 이 필드 그룹을 포함할 필요가 없습니다. TCF 동의 값을 자동으로 적용할 때 Experience Platform은 [프로필 필드 그룹](#profile-field-group)에 수집된 최신 동의 정보만 사용합니다. 이벤트에 의해 캡처된 동의 값은 자동 시행 워크플로우에 참여하지 않습니다.

구조 및 사용 사례에 대한 자세한 내용은 이 필드 그룹의 [참조 안내서](../../../../xdm/field-groups/event/iab.md)를 참조하십시오.

## 고객 동의 스키마 만들기 {#create-schemas}

동의 데이터를 캡처하는 데이터 세트를 만들려면 먼저 해당 데이터 세트를 기반으로 XDM 스키마를 만들어야 합니다.

이전 섹션에서 언급했듯이 다운스트림 플랫폼 워크플로우에서 동의를 적용하려면 [!UICONTROL XDM 개인 프로필] 클래스를 사용하는 스키마가 필요합니다. 시간에 따른 동의 변경을 추적하려는 경우 선택적으로 [!UICONTROL XDM ExperienceEvent]을(를) 기반으로 별도의 스키마를 만들 수도 있습니다. 두 스키마에는 `identityMap` 필드와 적절한 TCF 2.0 필드 그룹이 있어야 합니다.

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 스키마]**&#x200B;을(를) 선택하여 [!UICONTROL 스키마] 작업 영역을 엽니다. 여기에서 아래 섹션의 단계에 따라 각 필수 스키마를 만듭니다.

>[!NOTE]
>
>동의 데이터를 대신 캡처하는 데 사용할 기존 XDM 스키마가 있는 경우 새 스키마를 만드는 대신 해당 스키마를 편집할 수 있습니다. 그러나 기존 스키마가 실시간 고객 프로필에서 사용할 수 있도록 설정된 경우 기본 ID는 이메일 주소와 같이 관심 기반 광고에서 사용할 수 없는 직접 식별 가능한 필드일 수 없습니다. 제한된 필드가 확실하지 않은 경우 법률 자문을 구하십시오.
>
>또한 기존 스키마를 편집할 때는 추가(끊김 없이)만 변경할 수 있습니다. 자세한 내용은 [스키마 진화의 원칙](../../../../xdm/schema/composition.md#evolution) 섹션을 참조하십시오.

### 프로필 동의 스키마 만들기 {#profile-schema}

**[!UICONTROL 스키마 만들기]**&#x200B;를 선택한 다음 드롭다운 메뉴에서 **[!UICONTROL XDM 개인 프로필]**&#x200B;을 선택합니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

**[!UICONTROL 필드 그룹 추가]** 대화 상자가 표시되어 스키마에 필드 그룹을 바로 추가할 수 있습니다. 목록에서 **[!UICONTROL IAB TCF 2.0 동의 세부 정보]**&#x200B;를 선택합니다. 선택적으로 검색 창을 사용하여 결과 범위를 좁혀 필드 그룹을 더 쉽게 찾을 수 있습니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

그런 다음 목록에서 **[!UICONTROL IdentityMap]** 필드 그룹을 찾아 선택합니다. 두 필드 그룹이 오른쪽 레일에 나열되면 **[!UICONTROL 필드 그룹 추가]**&#x200B;를 선택합니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

`identityPrivacyInfo` 및 `identityMap` 필드가 스키마 구조에 추가되었음을 보여주는 캔버스가 다시 나타납니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

스키마에 필드를 추가하기 전에 루트 필드를 선택하여 오른쪽 레일에 **[!UICONTROL 스키마 속성]**&#x200B;을 표시하십시오. 여기서 스키마의 이름과 설명을 입력할 수 있습니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

이름과 설명을 제공한 후 필요에 따라 캔버스 왼쪽의 **[!UICONTROL 필드 그룹]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 선택하여 스키마에 필드를 더 추가할 수 있습니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

[!DNL Real-Time Customer Profile]에서 이미 사용할 수 있도록 설정된 기존 스키마를 편집하는 경우 [동의 스키마를 기반으로 데이터 세트 만들기](#dataset)의 섹션을 건너뛰기 전에 **[!UICONTROL 저장]**&#x200B;을 선택하여 변경 내용을 확인하십시오. 새 스키마를 만드는 경우 아래 하위 섹션에 설명된 단계를 계속 수행합니다.

#### [!DNL Real-Time Customer Profile]에서 사용할 스키마 활성화

플랫폼이 수신한 동의 데이터를 특정 고객 프로필에 연결하려면 [!DNL Real-Time Customer Profile]에서 동의 스키마를 사용할 수 있도록 설정해야 합니다.

>[!NOTE]
>
>이 섹션에 표시된 예제 스키마는 해당 `identityMap` 필드를 기본 ID로 사용합니다. 다른 필드를 기본 ID로 설정하려면 이메일 주소와 같이 관심 기반 광고에서 사용할 수 없는 직접 식별 가능한 필드가 아니라 쿠키 ID와 같은 간접 식별자를 사용해야 합니다. 제한된 필드가 확실하지 않은 경우 법률 자문을 구하십시오.
>
>스키마에 대한 기본 ID 필드를 설정하는 방법에 대한 단계는 [[!UICONTROL 스키마] UI 안내서](../../../../xdm/ui/fields/identity.md)에서 찾을 수 있습니다.

[!DNL Profile]에 대한 스키마를 활성화하려면 왼쪽 레일에서 스키마 이름을 선택하여 **[!UICONTROL 스키마 속성]** 섹션을 엽니다. 여기에서 **[!UICONTROL 프로필]** 전환 단추를 선택합니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

기본 ID가 누락되었음을 나타내는 팝오버가 나타납니다. 기본 ID가 `identityMap` 필드에 포함되므로 대체 기본 ID를 사용하기 위한 확인란을 선택하십시오.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

마지막으로 **[!UICONTROL 저장]**&#x200B;을 선택하여 변경 내용을 확인합니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### 이벤트 동의 스키마 만들기 {#event-schema}

>[!NOTE]
>
>이벤트 동의 스키마는 시간 경과에 따른 동의 변경 이벤트를 추적하는 데만 사용되며 다운스트림 시행 워크플로우에는 참여하지 않습니다. 시간이 지남에 따라 동의 변경 사항을 추적하지 않으려면 [동의 데이터 세트 만들기](#datasets)의 다음 섹션으로 건너뛸 수 있습니다.

**[!UICONTROL 스키마]** 작업 영역에서 **[!UICONTROL 스키마 만들기]**&#x200B;를 선택한 다음 드롭다운에서 **[!UICONTROL XDM ExperienceEvent]**&#x200B;을(를) 선택합니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

**[!UICONTROL 필드 그룹 추가]** 대화 상자가 나타납니다. 목록에서 **[!UICONTROL IAB TCF 2.0 동의 세부 정보]**&#x200B;를 선택합니다. 선택적으로 검색 창을 사용하여 결과 범위를 좁혀 필드 그룹을 더 쉽게 찾을 수 있습니다.


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

그런 다음 목록에서 **[!UICONTROL IdentityMap]** 필드 그룹을 찾아 선택합니다. 두 필드 그룹이 오른쪽 레일에 나열되면 **[!UICONTROL 필드 그룹 추가]**&#x200B;를 선택합니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

`consentStrings` 및 `identityMap` 필드가 스키마 구조에 추가되었음을 보여주는 캔버스가 다시 나타납니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

스키마에 필드를 추가하기 전에 루트 필드를 선택하여 오른쪽 레일에 **[!UICONTROL 스키마 속성]**&#x200B;을 표시하십시오. 여기서 스키마의 이름과 설명을 입력할 수 있습니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

이름과 설명을 제공한 후 필요에 따라 캔버스 왼쪽의 **[!UICONTROL 필드 그룹]** 섹션에서 **[!UICONTROL 추가]**&#x200B;를 선택하여 스키마에 필드를 더 추가할 수 있습니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

필요한 필드 그룹을 추가한 후에는 **[!UICONTROL 저장]**&#x200B;을 선택하여 완료하십시오.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## 동의 스키마를 기반으로 데이터 세트 만들기 {#datasets}

위에서 설명한 각 필수 스키마에 대해 궁극적으로 고객의 동의 데이터를 수집하는 데이터 세트를 만들어야 합니다. 레코드 스키마를 기반으로 하는 데이터 세트는 [!DNL Real-Time Customer Profile]에 대해 활성화되어야 하지만 시계열 스키마 **을(를) 기반으로 하는 데이터 세트는 [!DNL Profile]을(를) 사용할 수**&#x200B;이어서는 안 됩니다.

시작하려면 왼쪽 탐색에서 **[!UICONTROL 데이터 세트]**&#x200B;를 선택한 다음 오른쪽 상단 모서리에서 **[!UICONTROL 데이터 세트 만들기]**&#x200B;를 선택하십시오.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

다음 페이지에서 **[!UICONTROL 스키마에서 데이터 집합 만들기]**&#x200B;를 선택합니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

**[!UICONTROL 스키마 선택]** 단계부터 **[!UICONTROL 스키마에서 데이터 집합 만들기]** 워크플로가 나타납니다. 제공된 목록에서 이전에 생성한 동의 스키마 중 하나를 찾습니다. 선택적으로 검색 창을 사용하여 결과의 범위를 좁히고 스키마를 더 쉽게 찾을 수 있습니다. 원하는 스키마 옆에 있는 라디오 단추를 선택한 후 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속합니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

**[!UICONTROL 데이터 집합 구성]** 단계가 나타납니다. **[!UICONTROL 완료]**&#x200B;를 선택하기 전에 데이터 집합에 대해 쉽게 식별할 수 있는 고유한 이름과 설명을 제공하십시오.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

새로 생성된 데이터 세트에 대한 세부 정보 페이지가 나타납니다. 데이터 세트가 시계열 스키마를 기반으로 하는 경우 프로세스가 완료됩니다. 데이터 집합이 레코드 스키마를 기반으로 하는 경우 프로세스의 마지막 단계는 [!DNL Real-Time Customer Profile]에서 사용할 데이터 집합을 활성화하는 것입니다.

오른쪽 레일에서 **[!UICONTROL 프로필]** 토글을 선택한 다음 확인 팝오버에서 **[!UICONTROL 활성화]**&#x200B;를 선택하여 [!DNL Profile]에 대한 스키마를 활성화합니다.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

스키마를 만든 경우 위의 단계에 따라 이벤트 기반 데이터 세트를 다시 만드십시오.

## 다음 단계

이 자습서에 따라 이제 고객 동의 데이터를 수집하는 데 사용할 수 있는 데이터 세트를 하나 이상 만들었습니다.

* 실시간 고객 프로필에서 사용할 수 있도록 설정된 레코드 기반 데이터 세트입니다. **(필수)**
* [!DNL Profile]에 사용할 수 없는 시계열 기반 데이터 집합입니다. (선택 사항)

이제 [IAB TCF 2.0 개요](./overview.md#merge-policies)(으)로 돌아가서 TCF 2.0 규정 준수를 위한 플랫폼 구성 프로세스를 계속할 수 있습니다.
