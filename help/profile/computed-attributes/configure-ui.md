---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 속성 필드를 구성하는 방법
type: Documentation
description: 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 계산된 속성을 구성하려면 먼저 계산된 속성 값을 가질 필드를 식별해야 합니다. 스키마 필드 그룹을 사용하여 필드를 만들어 기존 스키마에 필드를 추가하거나 스키마 내에 이미 정의한 필드를 선택하여 생성할 수 있습니다.
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (알파) UI에서 계산된 속성 필드를 구성합니다

>[!IMPORTANT]
>
>계산된 특성 기능은 현재 알파에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 구성하려면 먼저 계산된 속성 값을 가질 필드를 식별해야 합니다. 스키마 필드 그룹을 사용하여 필드를 만들어 기존 스키마에 필드를 추가하거나 스키마 내에 이미 정의한 필드를 선택하여 생성할 수 있습니다.

>[!NOTE]
>
>계산된 특성을 Adobe 정의 필드 그룹 내의 필드에 추가할 수 없습니다. 필드는 `tenant` 네임스페이스, 즉 사용자가 정의하고 스키마에 추가하는 필드여야 합니다.

계산된 속성 필드를 성공적으로 정의하려면 [!DNL Profile] 및 는 스키마를 기반으로 하는 클래스에 대한 결합 스키마의 일부로 나타납니다. 자세한 내용은 [!DNL Profile]-사용할 수 있는 스키마 및 결합을 참조하십시오. [!DNL Schema Registry] 개발자 안내서 섹션 [프로필 및 결합 스키마 보기 스키마 활성화](../../xdm/api/getting-started.md). 또한 을 검토하는 것이 좋습니다 [조합 섹션](../../xdm/schema/composition.md) 스키마 작성 기본 사항 설명서에서 를 참조하십시오.

이 자습서의 워크플로우는 [!DNL Profile]-enabled 스키마에서 계산된 속성 필드를 포함하는 새 필드 그룹을 정의하고 올바른 네임스페이스인지 확인하는 단계를 따릅니다. 이미 프로필 사용 스키마 내에 올바른 네임스페이스에 있는 필드가 있는 경우 다음 단계로 직접 진행할 수 있습니다 [계산된 속성 만들기](#create-a-computed-attribute).

## 스키마 보기

다음에 이어지는 단계는 Adobe Experience Platform 사용자 인터페이스를 사용하여 스키마를 찾고, 필드 그룹을 추가하고, 필드를 정의하는 것입니다. 를 사용하려면 [!DNL Schema Registry] API는 [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md) 필드 그룹을 만들고, 필드 그룹을 스키마에 추가하고, 과 함께 사용할 스키마를 활성화하는 방법에 대한 절차 [!DNL Real-Time Customer Profile].

사용자 인터페이스에서 를 클릭합니다. **[!UICONTROL 스키마]** 왼쪽 레일에서 를 클릭하고 **[!UICONTROL 찾아보기]** 업데이트할 스키마를 빠르게 찾으려면 탭을 클릭하십시오.

![](../images/computed-attributes/Schemas-Browse.png)

스키마를 찾으면 해당 이름을 클릭하여 를 엽니다 [!DNL Schema Editor] 스키마를 편집할 수 있는 위치입니다.

![](../images/computed-attributes/Schema-Editor.png)

## 필드 그룹 만들기

새 필드 그룹을 만들려면 **[!UICONTROL 추가]** 다음 **[!UICONTROL 필드 그룹]** 에서 **[!UICONTROL 조성물]** 편집기의 왼쪽에 있는 섹션을 참조하십시오. 이렇게 하면 **[!UICONTROL 필드 그룹 추가]** 기존 필드 그룹을 볼 수 있는 대화 상자입니다. 에 대한 라디오 단추를 클릭합니다. **[!UICONTROL 새 필드 그룹 만들기]** 를 눌러 새 필드 그룹을 정의합니다.

필드 그룹에 이름과 설명을 지정하고 **[!UICONTROL 필드 그룹 추가]** 완료 시.

![](../images/computed-attributes/Add-field-group.png)

## 스키마에 계산된 속성 필드 추가

이제 새 필드 그룹이 &quot;[!UICONTROL 필드 그룹]&quot; 섹션 아래의 &quot;[!UICONTROL 조성물]&quot;. 필드 그룹 및 여러 개의 이름을 클릭합니다 **[!UICONTROL 필드 추가]** 버튼이 **[!UICONTROL 구조]** 편집기의 섹션.

선택 **[!UICONTROL 필드 추가]** 최상위 필드를 추가하기 위해 스키마 이름 옆에 를 추가하거나 원하는 스키마 내의 아무 곳에나 필드를 추가하도록 선택할 수 있습니다.

클릭 후 **[!UICONTROL 필드 추가]** 테넌트 ID에 대해 이름이 인 새 개체가 열리고 필드가 올바른 네임스페이스에 있음을 나타냅니다. 해당 개체 내에서 **[!UICONTROL 새 필드]** 이 나타납니다. 계산된 속성을 정의할 필드가 이 경우입니다.

![](../images/computed-attributes/New-field.png)

## 필드 구성

사용 **[!UICONTROL 필드 속성]** 편집기 오른쪽의 섹션에서 이름, 표시 이름 및 유형 등 새 필드에 필요한 정보를 제공합니다.

>[!NOTE]
>
>필드의 유형은 계산된 속성 값과 같은 유형이어야 합니다. 예를 들어 계산된 속성 값이 문자열이면 스키마에 정의되어 있는 필드가 문자열이어야 합니다.

완료되면 를 클릭합니다 **[!UICONTROL 적용]** 필드의 이름과 필드의 유형이 **[!UICONTROL 구조]** 편집기의 섹션.

![](../images/computed-attributes/Apply.png)

## 스키마 활성화 [!DNL Profile]

계속하기 전에 스키마가 [!DNL Profile]. 에서 스키마 이름을 클릭합니다 **[!UICONTROL 구조]** 편집기의 섹션 및 **[!UICONTROL 스키마 속성]** 탭이 나타납니다. 만약 **[!UICONTROL 프로필]** 슬라이더가 파란색이고 스키마가 [!DNL Profile].

>[!NOTE]
>
>스키마 활성화 [!DNL Profile] 실행 취소할 수 없으므로 이 슬라이더를 활성화한 후 클릭하면 비활성화될 위험이 없습니다.

![](../images/computed-attributes/Profile.png)

이제 을(를) 클릭합니다. **[!UICONTROL 저장]** 업데이트된 스키마를 저장하고 API를 사용하여 나머지 자습서를 계속 진행하려면 다음을 수행하십시오.

## 다음 단계

이제 계산된 속성 값이 저장되는 필드를 만들었으므로 `/computedattributes` API 엔드포인트. API에서 계산된 속성을 만드는 자세한 단계는 [계산된 특성 API 끝점 안내서](ca-api.md).