---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 속성 필드를 구성하는 방법
topic-legacy: guide
type: Documentation
description: 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 계산된 속성을 구성하려면 먼저 계산된 속성 값이 있을 필드를 식별해야 합니다. 스키마 필드 그룹을 사용하여 필드를 기존 스키마에 추가하거나 스키마 내에서 이미 정의한 필드를 선택하여 이 필드를 만들 수 있습니다.
translation-type: tm+mt
source-git-commit: 6e0f7578d0818f88e13b963f64cb2de6729f0574
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---


# (알파) UI에서 계산된 속성 필드를 구성합니다.

>[!IMPORTANT]
>
>계산된 속성 기능은 현재 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 구성하려면 먼저 계산된 속성 값이 있을 필드를 식별해야 합니다. 스키마 필드 그룹을 사용하여 필드를 기존 스키마에 추가하거나 스키마 내에서 이미 정의한 필드를 선택하여 이 필드를 만들 수 있습니다.

>[!NOTE]
>
>계산된 속성은 Adobe 정의 필드 그룹 내의 필드에 추가할 수 없습니다. 필드는 `tenant` 네임스페이스 내에 있어야 합니다. 즉, 이 필드는 사용자가 정의하고 스키마에 추가하는 필드여야 합니다.

계산된 속성 필드를 성공적으로 정의하려면 [!DNL Profile]에 대해 스키마를 사용하도록 설정하고 스키마를 기반으로 하는 클래스에 대한 공용 스키마의 일부로 표시되어야 합니다. [!DNL Profile] 사용 가능한 스키마 및 조합에 대한 자세한 내용은 [프로필 및 조합 스키마 보기](../../xdm/api/getting-started.md)의 [!DNL Schema Registry] 개발자 안내서 섹션 섹션을 참조하십시오. 스키마 구성 기본 문서에서 조합](../../xdm/schema/composition.md)의 [섹션을 검토하는 것도 좋습니다.

이 자습서의 워크플로우는 [!DNL Profile] 사용 가능한 스키마를 사용하며 계산된 속성 필드를 포함하는 새 필드 그룹을 정의하고 올바른 네임스페이스인지 확인하는 절차를 따릅니다. 프로필 사용 스키마 내에 올바른 네임스페이스에 있는 필드가 이미 있는 경우 [계산된 특성](#create-a-computed-attribute)을 만들기 위한 단계로 직접 진행할 수 있습니다.

## 스키마 보기

Adobe Experience Platform 사용자 인터페이스를 사용하여 스키마를 찾고, 필드 그룹을 추가하고, 필드를 정의하는 단계입니다. [!DNL Schema Registry] API를 사용하려면 [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md)를 참조하여 필드 그룹을 만들고, 필드 그룹을 스키마에 추가하고, [!DNL Real-time Customer Profile]에 사용할 스키마를 활성화하십시오.

사용자 인터페이스에서 왼쪽 레일에 있는 **[!UICONTROL Schemas]**&#x200B;을 클릭하고 **[!UICONTROL Browse]** 탭의 검색 막대를 사용하여 업데이트할 스키마를 빠르게 찾습니다.

![](../images/computed-attributes/Schemas-Browse.png)

스키마를 찾은 후에는 해당 이름을 클릭하여 [!DNL Schema Editor]을 열고 스키마를 편집할 수 있습니다.

![](../images/computed-attributes/Schema-Editor.png)

## 필드 그룹 만들기

새 필드 그룹을 만들려면 편집기의 왼쪽에 있는 **[!UICONTROL Composition]** 섹션에서 **[!UICONTROL Field groups]** 옆의 **[!UICONTROL Add]**&#x200B;을 클릭합니다. 기존 필드 그룹을 볼 수 있는 **[!UICONTROL Add field group]** 대화 상자가 열립니다. 새 필드 그룹을 정의하려면 **[!UICONTROL Create new field group]**&#x200B;의 라디오 단추를 클릭합니다.

필드 그룹에 이름과 설명을 지정하고 완료되면 **[!UICONTROL Add field group]**&#x200B;을 클릭합니다.

![](../images/computed-attributes/Add-field-group.png)

## 스키마에 계산된 속성 필드 추가

이제 새 필드 그룹이 &quot;[!UICONTROL Composition]&quot;의 &quot;[!UICONTROL Field groups]&quot; 섹션에 표시됩니다. 필드 그룹의 이름을 클릭하면 편집기의 **[!UICONTROL Structure]** 섹션에 여러 개의 **[!UICONTROL Add field]** 단추가 나타납니다.

최상위 수준 필드를 추가하려면 스키마 이름 옆에 있는 **[!UICONTROL Add field]**&#x200B;을 선택하거나 원하는 스키마 내의 아무 곳에나 필드를 추가하도록 선택할 수 있습니다.

**[!UICONTROL Add field]**&#x200B;을 클릭하면 테넌트 ID에 대해 이름이 지정된 새 개체가 열리고 필드가 올바른 네임스페이스에 있음을 보여줍니다. 해당 개체 내에 **[!UICONTROL New field]**&#x200B;이(가) 나타납니다. 계산된 속성을 정의할 필드가 있을 경우 이 값이 필요합니다.

![](../images/computed-attributes/New-field.png)

## 필드 구성

편집기의 오른쪽에 있는 **[!UICONTROL Field properties]** 섹션을 사용하여 이름, 표시 이름, 유형 등 새 필드에 필요한 정보를 제공합니다.

>[!NOTE]
>
>필드의 유형은 계산된 속성 값과 같은 유형이어야 합니다. 예를 들어 계산된 속성 값이 문자열이면 스키마에 정의된 필드가 문자열이어야 합니다.

완료되면 **[!UICONTROL Apply]**&#x200B;을 클릭하고 필드 이름과 해당 유형이 편집기의 **[!UICONTROL Structure]** 섹션에 표시됩니다.

![](../images/computed-attributes/Apply.png)

## [!DNL Profile]에 대한 스키마 사용

계속하기 전에 [!DNL Profile]에 대한 스키마가 활성화되어 있는지 확인하십시오. **[!UICONTROL Schema Properties]** 탭이 나타나도록 편집기의 **[!UICONTROL Structure]** 섹션에서 스키마 이름을 클릭합니다. **[!UICONTROL Profile]** 슬라이더가 파란색이면 [!DNL Profile]에 대해 스키마가 활성화됩니다.

>[!NOTE]
>
>[!DNL Profile]에 대한 스키마 활성화는 실행 취소할 수 없으므로 슬라이더를 활성화한 후 클릭하면 비활성화될 위험이 없습니다.

![](../images/computed-attributes/Profile.png)

이제 **[!UICONTROL Save]**&#x200B;을 클릭하여 업데이트된 스키마를 저장하고 API를 사용하여 나머지 튜토리얼을 계속 진행할 수 있습니다.

## 다음 단계

계산된 특성 값이 저장되는 필드를 만들었으므로 `/computedattributes` API 끝점을 사용하여 계산된 특성을 만들 수 있습니다. API에서 계산된 속성을 만드는 자세한 단계를 보려면 [계산된 특성 API 끝점 안내서](ca-api.md)에서 제공하는 단계를 따르십시오.