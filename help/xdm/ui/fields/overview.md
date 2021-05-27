---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 공간;필드;
solution: Experience Platform
title: UI에서 XDM 필드 정의
description: Experience Platform 사용자 인터페이스에서 XDM 필드를 정의하는 방법을 알아봅니다.
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 4%

---

# UI에서 XDM 필드 정의

Adobe Experience Platform 사용자 인터페이스의 [!DNL Schema Editor] 에서는 사용자 지정 XDM(Experience Data Model) 클래스 및 스키마 필드 그룹 내에서 고유한 필드를 정의할 수 있습니다. 이 안내서에서는 각 필드 유형에 사용할 수 있는 구성 옵션을 포함하여 UI에서 XDM 필드를 정의하는 단계를 설명합니다.

## 전제 조건

이 안내서에서는 XDM 시스템을 작업해야 합니다. Experience Platform 에코시스템 내에서 XDM의 역할에 대한 소개는 [XDM 개요](../../home.md) 를 참조하고, 클래스 및 필드 그룹이 XDM 스키마에 필드를 기여하는 방법을 알아보려면 스키마 구성](../../schema/composition.md)의 [기본 사항을 참조하십시오.

이 안내서에는 필요하지 않지만 [UI](../../tutorials/create-schema-ui.md)에서 스키마 작성을 위한 튜토리얼도 따라 [!DNL Schema Editor]의 다양한 기능에 익숙해지는 것이 좋습니다.

## 리소스를 선택하여 {#select-resource}에 필드를 추가합니다

UI에서 새 XDM 필드를 정의하려면 먼저 [!DNL Schema Editor] 내에서 스키마를 열어야 합니다. 현재 [!DNL Schema Library]에서 사용할 수 있는 스키마에 따라, [새 스키마](../resources/schemas.md#create) 또는 [편집할 기존 스키마를 선택하도록 선택할 수 있습니다](../resources/schemas.md#edit).

[!DNL Schema Editor] 이 열리면 왼쪽 레일을 사용하여 필드를 정의할 클래스 또는 필드 그룹을 선택합니다. 리소스가 조직에서 정의한 사용자 정의 리소스인 경우 필드를 추가하거나 편집할 수 있는 컨트롤이 캔버스에 나타납니다. 이러한 컨트롤은 스키마 이름 옆에 나타나고 선택한 클래스나 필드 그룹에 정의된 개체 형식 필드도 나타납니다.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>선택하는 클래스나 필드 그룹이 Adobe에서 제공하는 핵심 리소스인 경우 편집할 수 없으므로 위에 표시된 컨트롤이 나타나지 않습니다. 필드를 추가하려는 스키마가 코어 XDM 클래스를 기반으로 하고 사용자 지정 필드 그룹을 포함하지 않는 경우 [새 필드 그룹](../resources/field-groups.md#create)을 만들어 대신 스키마에 추가할 수 있습니다.

리소스에 새 필드를 추가하려면 캔버스에서 스키마 이름 옆에 있는 **더하기(+)** 아이콘을 선택하거나 아래의 필드를 정의할 개체 유형 필드 옆에 있는 아이콘을 선택합니다.

![](../../images/ui/fields/overview/plus-icon.png)

## 리소스 필드 정의 {#define}

**더하기(+)** 아이콘을 선택한 후, **[!UICONTROL 새 필드]**&#x200B;가 고유한 테넌트 ID에 지정된 루트 수준 개체(아래 예에서 `_tenantId`로 표시됨)에 있는 캔버스에 표시됩니다. 사용자 지정 클래스 및 필드 그룹을 통해 스키마에 추가되는 모든 필드는 Adobe 제공 클래스 및 필드 그룹에서 다른 필드와의 충돌을 방지하기 위해 자동으로 이 네임스페이스 내에 배치됩니다.

![](../../images/ui/fields/overview/new-field.png)

**[!UICONTROL 필드 속성]** 아래의 오른쪽 레일에서 새 필드의 세부 사항을 구성할 수 있습니다. 각 필드에 다음 정보가 필요합니다.

| 필드 속성 | 설명 |
| --- | --- |
| [!UICONTROL 필드 이름] | 필드의 고유한 수사적 이름입니다. 스키마를 저장한 후에는 필드 이름을 변경할 수 없습니다.<br><br>그 이름은 camelCase로 작성하면 이상적이다. 영숫자, 대시 또는 밑줄 문자를 포함할 수 있지만 **은 밑줄로 시작할 수 없습니다.**<ul><li>**올바른**:  `fieldName`</li><li>**허용 가능:** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**잘못된**:  `_fieldName`</li></ul> |
| [!UICONTROL 디스플레이 이름] | 그 필드의 이름입니다. |
| [!UICONTROL 유형] | 필드에 포함할 데이터 유형입니다. 이 드롭다운 메뉴에서 XDM에서 지원하는 [표준 스칼라 유형](../../schema/field-constraints.md) 중 하나 또는 [!DNL Schema Registry]에서 이전에 정의한 다중 필드 [데이터 유형](../resources/data-types.md) 중 하나를 선택할 수 있습니다.<br><br>고급 유형  **[!UICONTROL 검색을 선택하여 기존 데이터]** 유형을 검색 및 필터링하고 원하는 유형을 더 쉽게 찾을 수도 있습니다. |

{style=&quot;table-layout:auto&quot;}

필드의 의도한 사용 사례에 대해 더 많은 컨텍스트를 제공하기 위해 사람이 읽을 수 있는 선택적 **[!UICONTROL 설명]**&#x200B;을 필드에 제공할 수도 있습니다.

>[!NOTE]
>
>필드에 대해 선택한 **[!UICONTROL 유형]**&#x200B;에 따라 오른쪽 레일에 추가 구성 컨트롤이 나타날 수 있습니다. 이러한 컨트롤에 대한 자세한 내용은 [유형 특정 필드 속성](#type-specific-properties)의 섹션을 참조하십시오.
>
>오른쪽 레일에는 특수 필드 유형을 지정하는 확인란도 제공됩니다. 자세한 내용은 [특수 필드 유형](#special)의 섹션을 참조하십시오.

필드 구성을 마치면 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![](../../images/ui/fields/overview/field-details.png)

캔버스가 업데이트되어 필드의 이름과 유형을 보여주며, 오른쪽 레일에 이제 다른 속성 외에 필드의 경로가 나열됩니다.

![](../../images/ui/fields/overview/field-added.png)

위의 단계에 따라 스키마에 필드를 더 추가할 수 있습니다. 스키마를 저장하면 기본 클래스와 필드 그룹도 변경 사항이 있을 경우 저장됩니다.

>[!NOTE]
>
>한 스키마의 필드 그룹 또는 클래스에 대한 모든 변경 사항은 해당 필드를 사용하는 다른 모든 스키마에 반영됩니다.

## 유형별 필드 속성 {#type-specific-properties}

새 필드를 정의할 때 필드에 대해 선택한 **[!UICONTROL 유형]**&#x200B;에 따라 오른쪽 레일에 추가 구성 옵션이 나타날 수 있습니다. 다음 표에서는 호환 유형과 함께 이러한 추가 필드 속성에 대해 설명합니다.

| 필드 속성 | 호환 유형 | 설명 |
| --- | --- | --- |
| [!UICONTROL 기본값] | [!UICONTROL 문자열],  [!UICONTROL Double],  [!UICONTROL Long],  [!UICONTROL 정수],  [!UICONTROL Short],  [!UICONTROL Byte],  [!UICONTROL Boolean] | 수집 중에 다른 값이 제공되지 않는 경우 이 필드에 할당되는 기본값입니다. 이 값은 필드에서 선택한 유형을 준수해야 합니다. |
| [!UICONTROL 패턴] | [!UICONTROL 문자열] | 이 필드에 대한 값이 섭취 중에 수락하려면 에 따라야 하는 [정규 표현식](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)입니다. |
| [!UICONTROL 형식] | [!UICONTROL 문자열] | 값이 준수해야 하는 문자열에 대해 미리 정의된 형식 목록에서 선택합니다. 사용 가능한 형식은 다음과 같습니다. <ul><li>[[!UICONTROL 날짜 시간]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 이메일]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 호스트 이름]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri 참조]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json 포인터]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 최소 길이] | [!UICONTROL 문자열] | 섭취 중에 값을 수락하려면 문자열에 포함해야 하는 최소 문자 수입니다. |
| [!UICONTROL 최대 길이] | [!UICONTROL 문자열] | 섭취 중에 값을 수락하려면 문자열에 포함해야 하는 최대 문자 수입니다. |
| [!UICONTROL 최소값] | [!UICONTROL 이중] | 섭취 중 수락되는 Double에 대한 최소 값입니다. 수집된 값이 여기에 입력한 값과 정확히 일치하는 경우 값이 수락됩니다. 이 제약 조건을 사용할 때는 &quot;[!UICONTROL Exclusive 최소값]&quot; 제약 조건을 비워 두어야 합니다. |
| [!UICONTROL 최대값] | [!UICONTROL 이중] | 섭취 중 수락할 Double의 최대 값. 수집된 값이 여기에 입력한 값과 정확히 일치하는 경우 값이 수락됩니다. 이 제약 조건을 사용할 때는 &quot;[!UICONTROL Exclusive 최대값]&quot; 제약 조건을 비워 두어야 합니다. |
| [!UICONTROL 독점적 최소값] | [!UICONTROL 이중] | 섭취 중 수락할 Double의 최대 값. 수집된 값이 여기에 입력한 값과 정확히 일치하는 경우 값이 거부됩니다. 이 제약 조건을 사용하는 경우 &quot;[!UICONTROL 최소값]&quot;(비독점적) 제약 조건을 비워 두어야 합니다. |
| [!UICONTROL 독점 최대값] | [!UICONTROL 이중] | 섭취 중 수락할 Double의 최대 값. 수집된 값이 여기에 입력한 값과 정확히 일치하는 경우 값이 거부됩니다. 이 제약 조건을 사용할 때는 &quot;[!UICONTROL 최대값]&quot;(비독점적) 제약 조건을 비워 두어야 합니다. |

{style=&quot;table-layout:auto&quot;}

## 특수 필드 유형 {#special}

오른쪽 레일에는 선택한 필드에 대한 특수 역할을 지정하는 몇 가지 확인란이 있습니다. 이러한 옵션 중 일부에 대한 사용 사례에는 데이터 모델링 전략 및 다운스트림 Platform 서비스를 사용하는 방법과 관련된 중요한 고려 사항이 포함되어 있습니다.

이러한 특수 유형에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [[!UICONTROL 필수 여부]](./required.md)
* [[!UICONTROL 어레이]](./array.md)
* [[!UICONTROL 열거형]](./enum.md)
* [[!UICONTROL ID]](./identity.md) (문자열 필드에만 사용 가능)
* [[!UICONTROL 관계]](./relationship.md) (문자열 필드에만 사용 가능)

기술적으로 특수 필드 유형은 아니지만, 스키마 구조인 경우 중첩된 하위 필드 정의에 대한 자세한 내용을 보려면 [개체 유형 필드 정의](./object.md)의 안내서를 방문하는 것이 좋습니다.

## 다음 단계

이 안내서에서는 UI에서 XDM 필드를 정의하는 방법에 대한 개요를 제공합니다. 클래스 및 필드 그룹을 사용하여 스키마에만 필드를 추가할 수 있습니다. UI에서 이러한 리소스를 관리하는 방법에 대한 자세한 내용은 [클래스](../resources/classes.md) 및 [필드 그룹](../resources/field-groups.md)을 만들고 편집하는 방법에 대한 안내서를 참조하십시오.

[!UICONTROL 스키마] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL 스키마] 작업 공간 개요](../overview.md)를 참조하십시오.
