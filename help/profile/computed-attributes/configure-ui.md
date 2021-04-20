---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 속성 필드를 구성하는 방법
topic: guide
type: Documentation
description: 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 계산된 속성을 구성하려면 먼저 계산된 속성 값이 있을 필드를 식별해야 합니다. 이 필드는 믹싱을 사용하여 기존 스키마에 필드를 추가하거나 스키마 내에서 이미 정의한 필드를 선택하여 만들 수 있습니다.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# (알파) UI에서 계산된 속성 필드를 구성합니다.

>[!IMPORTANT]
>
>계산된 속성 기능은 현재 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 구성하려면 먼저 계산된 속성 값이 있을 필드를 식별해야 합니다. 이 필드는 믹싱을 사용하여 기존 스키마에 필드를 추가하거나 스키마 내에서 이미 정의한 필드를 선택하여 만들 수 있습니다.

>[!NOTE]
>
>계산된 속성은 Adobe 정의 믹싱 내의 필드에 추가할 수 없습니다. 필드는 `tenant` 네임스페이스 내에 있어야 합니다. 즉, 이 필드는 사용자가 정의하고 스키마에 추가하는 필드여야 합니다.

계산된 속성 필드를 성공적으로 정의하려면 [!DNL Profile]에 대해 스키마를 사용하도록 설정하고 스키마를 기반으로 하는 클래스에 대한 공용 스키마의 일부로 표시되어야 합니다. [!DNL Profile] 사용 가능한 스키마 및 조합에 대한 자세한 내용은 [프로필 및 조합 스키마 보기](../../xdm/api/getting-started.md)의 [!DNL Schema Registry] 개발자 안내서 섹션 섹션을 참조하십시오. 스키마 구성 기본 문서에서 조합](../../xdm/schema/composition.md)의 [섹션을 검토하는 것도 좋습니다.

이 자습서의 작업 과정은 [!DNL Profile] 사용 가능한 스키마를 사용하며 계산된 속성 필드를 포함하는 새 믹싱을 정의하고 올바른 네임스페이스인지 확인하는 절차를 따릅니다. 프로필 사용 스키마 내에 올바른 네임스페이스에 있는 필드가 이미 있는 경우 [계산된 특성](#create-a-computed-attribute)을 만들기 위한 단계로 직접 진행할 수 있습니다.

## 스키마 보기

Adobe Experience Platform 사용자 인터페이스를 사용하여 스키마를 찾고, 믹싱을 추가하고, 필드를 정의하는 단계입니다. [!DNL Schema Registry] API를 사용하려는 경우 [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md)에서 믹싱을 만들고 스키마에 혼합을 추가하고 [!DNL Real-time Customer Profile]에서 사용할 스키마를 활성화하는 방법을 참조하십시오.

사용자 인터페이스에서 왼쪽 레일에 있는 **[!UICONTROL 스키마]**&#x200B;를 클릭하고 **[!UICONTROL 찾아보기]** 탭의 검색 막대를 사용하여 업데이트할 스키마를 빠르게 찾습니다.

![](../images/computed-attributes/Schemas-Browse.png)

스키마를 찾은 후에는 해당 이름을 클릭하여 [!DNL Schema Editor]을 열고 스키마를 편집할 수 있습니다.

![](../images/computed-attributes/Schema-Editor.png)

## 혼합 만들기

새 믹싱을 만들려면 편집기의 왼쪽에 있는 **[!UICONTROL 컴포지션]** 섹션에서 **[!UICONTROL 믹싱]** 옆에 있는 **[!UICONTROL 추가]**&#x200B;를 클릭합니다. 그러면 기존 믹스를 볼 수 있는 **[!UICONTROL 혼합 추가]** 대화 상자가 열립니다. 새 믹스를 정의하려면 **[!UICONTROL 새 믹신 만들기]**&#x200B;의 라디오 단추를 클릭합니다.

믹싱에 이름과 설명을 지정하고 완료되면 **[!UICONTROL 믹신 추가]**&#x200B;를 클릭합니다.

![](../images/computed-attributes/Add-mixin.png)

## 스키마에 계산된 속성 필드 추가

이제 새 믹싱이 &quot;[!UICONTROL 컴포지션]&quot;의 &quot;[!UICONTROL 혼합]&quot; 섹션에 표시됩니다. 믹스의 이름을 클릭하고 편집기의 **[!UICONTROL 구조]** 섹션에 여러 **[!UICONTROL 필드 추가]** 단추가 나타납니다.

최상위 수준 필드를 추가하려면 스키마 이름 옆에 있는 **[!UICONTROL 필드 추가]**&#x200B;를 선택하거나 원하는 스키마 내의 아무 곳에나 필드를 추가하도록 선택할 수 있습니다.

**[!UICONTROL 필드 추가]**&#x200B;를 클릭하면 해당 필드가 올바른 네임스페이스에 있음을 보여주는 새 개체가 테넌트 ID에 이름이 지정됩니다. 해당 개체 내에 **[!UICONTROL 새 필드]**&#x200B;가 나타납니다. 계산된 속성을 정의할 필드가 있을 경우 이 값이 필요합니다.

![](../images/computed-attributes/New-field.png)

## 필드 구성

편집기의 오른쪽에 있는 **[!UICONTROL 필드 속성]** 섹션을 사용하여 이름, 표시 이름, 유형 등 새 필드에 필요한 정보를 제공합니다.

>[!NOTE]
>
>필드의 유형은 계산된 속성 값과 같은 유형이어야 합니다. 예를 들어 계산된 속성 값이 문자열이면 스키마에 정의된 필드가 문자열이어야 합니다.

완료되면 **[!UICONTROL 적용]**&#x200B;을 클릭하고 필드 이름과 해당 유형이 편집기의 **[!UICONTROL 구조]** 섹션에 표시됩니다.

![](../images/computed-attributes/Apply.png)

## [!DNL Profile]에 대한 스키마 사용

계속하기 전에 [!DNL Profile]에 대한 스키마가 활성화되어 있는지 확인하십시오. **[!UICONTROL 스키마 속성]** 탭이 나타나도록 편집기의 **[!UICONTROL 구조]** 섹션에서 스키마 이름을 클릭합니다. **[!UICONTROL 프로필]** 슬라이더가 파란색이면 [!DNL Profile]에 대해 스키마가 활성화되었습니다.

>[!NOTE]
>
>[!DNL Profile]에 대한 스키마 활성화는 실행 취소할 수 없으므로 슬라이더를 활성화한 후 클릭하면 비활성화될 위험이 없습니다.

![](../images/computed-attributes/Profile.png)

이제 **[!UICONTROL 저장]**&#x200B;을 클릭하여 업데이트된 스키마를 저장하고 API를 사용하여 나머지 자습서를 계속 진행할 수 있습니다.

## 다음 단계

계산된 특성 값이 저장되는 필드를 만들었으므로 `/computedattributes` API 끝점을 사용하여 계산된 특성을 만들 수 있습니다. API에서 계산된 속성을 만드는 자세한 단계를 보려면 [계산된 특성 API 끝점 안내서](ca-api.md)에서 제공하는 단계를 따르십시오.