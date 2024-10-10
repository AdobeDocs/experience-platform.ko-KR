---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 영역;필드;
solution: Experience Platform
title: UI에서 XDM 필드 정의
description: Experience Platform 사용자 인터페이스에서 XDM 필드를 정의하는 방법을 알아봅니다.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 807ce0b0304fd73a455f228529d75cfc68769bf5
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 2%

---

# UI에서 XDM 필드 정의

Adobe Experience Platform 사용자 인터페이스의 [!DNL Schema Editor]을(를) 사용하면 사용자 지정 XDM(경험 데이터 모델) 클래스와 스키마 필드 그룹 내에서 고유한 필드를 정의할 수 있습니다. 이 안내서에서는 각 필드 유형에 사용할 수 있는 구성 옵션을 포함하여 UI에서 XDM 필드를 정의하는 단계를 다룹니다.

## 전제 조건

이 안내서에서는 XDM 시스템에 대한 작업 이해가 필요합니다. 클래스 및 필드 그룹이 XDM 스키마에 필드를 제공하는 방법에 대한 소개는 [XDM 개요](../../home.md) 및 Experience Platform 작성의 [기본 사항](../../schema/composition.md)을 참조하세요.

이 안내서에서는 필요하지 않지만 [UI에서 스키마 작성](../../tutorials/create-schema-ui.md)에 대한 자습서를 따라 [!DNL Schema Editor]의 다양한 기능을 숙지하는 것이 좋습니다.

## 필드를 추가할 리소스 선택 {#select-resource}

UI에서 새 XDM 필드를 정의하려면 먼저 [!DNL Schema Editor] 내에서 스키마를 열어야 합니다. 현재 [!DNL Schema Library]에서 사용할 수 있는 스키마에 따라 [새 스키마를 만들거나](../resources/schemas.md#create) [편집할 기존 스키마를 선택](../resources/schemas.md#edit)할 수 있습니다.

[!DNL Schema Editor]을(를) 열면 필드를 추가할 컨트롤이 캔버스에 나타납니다. 이러한 컨트롤은 선택한 클래스 또는 필드 그룹 아래에 정의된 개체 유형 필드뿐 아니라 스키마 이름 옆에 나타납니다.

![추가 아이콘이 강조 표시된 스키마 편집기입니다.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>표준 필드 그룹에서 제공하는 개체에 필드를 추가하려고 하면 해당 필드 그룹이 사용자 정의 필드 그룹으로 변환되고 원래 필드 그룹은 더 이상 사용할 수 없습니다. 자세한 내용은 스키마 UI 안내서의 [표준 필드 그룹에 필드 추가](../resources/schemas.md#custom-fields-for-standard-groups)에 대한 섹션을 참조하십시오.

리소스에 새 필드를 추가하려면 캔버스에서 스키마 이름 옆에 있는 **더하기(+)** 아이콘을 선택하거나 아래에 필드를 정의할 개체 유형 필드 옆에 있는 아이콘을 선택합니다.

![추가 아이콘이 강조 표시된 스키마 편집기입니다.](../../images/ui/fields/overview/plus-icon.png)

필드를 스키마에 직접 추가하는지 또는 구성 클래스 및 필드 그룹에 추가하는지에 따라 필드를 추가하는 데 필요한 단계가 달라집니다. 이 문서의 나머지 부분에서는 스키마에서 필드가 나타나는 위치에 관계없이 필드의 속성을 구성하는 방법을 중점적으로 다룹니다. 스키마에 필드를 추가할 수 있는 다양한 방법에 대한 자세한 내용은 스키마 UI 안내서의 다음 섹션을 참조하십시오.

* [필드 그룹에 필드 추가](../resources/schemas.md#add-fields)
* [스키마에 직접 필드 추가](../resources/schemas.md#add-individual-fields)

## 필드의 속성 정의 {#define}

**더하기(+)** 아이콘을 선택하면 **[!UICONTROL 제목 없는 필드]** 자리 표시자가 캔버스에 나타납니다.

![제목 없는 새 필드가 강조 표시된 스키마 편집기입니다.](../../images/ui/fields/overview/new-field.png)

**[!UICONTROL 필드 속성]** 아래의 오른쪽 레일에서 새 필드의 세부 정보를 구성할 수 있습니다. 각 필드에 다음 정보가 필요합니다.

| 필드 속성 | 설명 |
| --- | --- |
| [!UICONTROL 필드 이름] | 필드에 대한 고유한 설명적인 이름. 스키마가 저장된 후에는 필드 이름을 변경할 수 없습니다. 이 값은 코드 및 다른 다운스트림 응용 프로그램에서 필드를 식별하고 참조하는 데 사용됩니다<br><br>이름은 camelCase로 작성해야 합니다. 영숫자, 대시 또는 밑줄 문자가 포함될 수 있지만 **밑줄로 시작할 수 없습니다**.<ul><li>**수정**: `fieldName`</li><li>**허용:** `field_name2`, `Field-Name`, `field-name_3`</li><li>**잘못됨**: `_fieldName`</li></ul> |
| [!UICONTROL 표시 이름] | 필드의 표시 이름입니다. 스키마 편집기 캔버스 내의 필드를 나타내는 데 사용할 이름입니다. [표시 이름 전환](../resources/schemas.md#display-name-toggle)을 사용하여 필드 이름을 표시 이름으로 변경할 수 있습니다. |
| [!UICONTROL 유형] | 필드에 포함될 데이터의 유형입니다. 이 드롭다운 메뉴에서 XDM에서 지원하는 [표준 스칼라 유형](../../schema/field-constraints.md) 중 하나 또는 [!DNL Schema Registry]에서 이전에 정의한 다중 필드 [데이터 유형](../resources/data-types.md) 중 하나를 선택할 수 있습니다.<br>참고: 맵 데이터 형식을 선택하면 [!UICONTROL 맵 값 형식] 속성이 나타납니다.<br><br>또한 **[!UICONTROL 고급 형식 검색]**&#x200B;을 선택하여 기존 데이터 형식을 검색 및 필터링하고 원하는 형식을 쉽게 찾을 수 있습니다. |
| [!UICONTROL 맵 값 형식] | 이 값은 필드의 데이터 형식으로 [!UICONTROL 맵]을(를) 선택하는 경우 필요합니다. 맵에 사용할 수 있는 값은 [!UICONTROL 문자열] 및 [!UICONTROL 정수]입니다. 사용 가능한 옵션의 드롭다운 목록에서 값을 선택합니다.<br>[유형별 필드 속성에 대한 자세한 내용](#type-specific-properties)은 필드 정의 개요를 참조하세요. |

{style="table-layout:auto"}

각 필드에 대한 설명 및 메모를 제공하도록 선택할 수도 있습니다. **[!UICONTROL 설명]** 필드를 사용하여 컨텍스트를 추가하고 맵 데이터 형식의 기능을 설명합니다. 이는 구현의 유지 관리 및 가독성에 기여합니다. 초기 설명을 보완하기 위해 메모를 추가할 수도 있습니다. 개발자가 코드 베이스의 컨텍스트 내에서 맵을 효과적으로 이해, 유지 관리 및 활용하는 데 도움이 되는 보다 세분화되고 구체적인 정보를 제공해야 합니다. |


>[!NOTE]
>
>필드에 대해 선택한 **[!UICONTROL 유형]**&#x200B;에 따라 추가 구성 컨트롤이 오른쪽 레일에 나타날 수 있습니다. 이러한 컨트롤에 대한 자세한 내용은 [유형별 필드 속성](#type-specific-properties)의 섹션을 참조하십시오.
>
>오른쪽 레일은 특수 필드 유형을 지정하는 확인란도 제공합니다. 자세한 내용은 [특수 필드 형식](#special)의 섹션을 참조하십시오.

필드 구성을 마치면 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![스키마 편집기의 [!UICONTROL 필드 속성] 섹션이 강조 표시됩니다.](../../images/ui/fields/overview/field-details.png)

캔버스는 고유한 테넌트 ID로 네임스페이스가 지정된 개체 내에 있는 새로 추가된 필드를 표시하도록 업데이트됩니다(아래 예에서 `_tenantId`(으)로 표시됨). 스키마에 추가된 모든 사용자 정의 필드는 Adobe 제공 클래스 및 필드 그룹의 다른 필드와의 충돌을 방지하기 위해 이 네임스페이스 내에 자동으로 배치됩니다. 이제 오른쪽 레일에 다른 속성 외에도 필드의 경로가 나열됩니다.

![스키마 다이어그램의 새 필드와 [!UICONTROL 필드 속성] 섹션의 해당 경로가 강조 표시됩니다.](../../images/ui/fields/overview/field-added.png)

위의 단계에 따라 스키마에 필드를 추가할 수 있습니다. 스키마가 저장되면 해당 기본 클래스와 필드 그룹도 변경된 경우 저장됩니다.

>[!NOTE]
>
>한 스키마의 필드 그룹 또는 클래스에 대한 변경 사항은 해당 변경 사항을 사용하는 다른 모든 스키마에 반영됩니다.

## 유형별 필드 속성 {#type-specific-properties}

새 필드를 정의할 때 필드에 대해 선택한 **[!UICONTROL 유형]**&#x200B;에 따라 오른쪽 레일에 추가 구성 옵션이 나타날 수 있습니다. 다음 표에서는 이러한 추가 필드 속성과 해당 호환 유형을 간략하게 설명합니다.

| 필드 속성 | 호환 가능한 유형 | 설명 |
| --- | --- | --- |
| [!UICONTROL 맵 값 형식] | [!UICONTROL 맵] | [!UICONTROL Type] 드롭다운 옵션에서 맵 값을 선택한 경우에만 [!UICONTROL 맵 값 형식] 속성이 UI에 표시됩니다. 맵의 문자열 및 정수 값 유형 중에서 선택할 수 있습니다.<br>![유형 및 맵 값 유형 필드가 강조 표시된 스키마 편집기.](../../images/ui/fields/overview/map-type.png "유형 및 맵 값 유형 필드가 강조 표시된 스키마 편집기."){width="100" zoomable="yes"}<br>참고: API를 통해 만든 String 또는 Integer 형식이 아닌 맵 데이터 형식은 &#39;[!UICONTROL Complex]&#39; 데이터 형식으로 표시됩니다. UI를 통해 &#39;[!UICONTROL Complex]&#39; 데이터 형식을 만들 수 없습니다. |
| [!UICONTROL 패턴] | [!UICONTROL 문자열] | 수집 중에 수락하려면 이 필드의 값이 준수해야 하는 [정규 표현식](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)입니다. |
| [!UICONTROL 형식] | [!UICONTROL 문자열] | 값이 준수해야 하는 문자열의 사전 정의된 형식 목록에서 선택합니다. 사용 가능한 형식은 다음과 같습니다. <ul><li>[[!UICONTROL 날짜-시간]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL 전자 메일]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL 호스트 이름]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL 최소 길이] | [!UICONTROL 문자열] | 수집 중에 값을 수락하기 위해 문자열에 포함해야 하는 최소 문자 수입니다. |
| [!UICONTROL 최대 길이] | [!UICONTROL 문자열] | 수집 중에 값을 수락하기 위해 문자열에 포함해야 하는 최대 문자 수입니다. |
| [!UICONTROL 최소값] | [!UICONTROL 이중] | 수집 중에 수락될 Double의 최소값입니다. 수집된 값이 여기에 입력한 값과 정확히 일치하는 경우 값이 수락됩니다. 이 제약 조건을 사용할 때는 &quot;[!UICONTROL Exclusive 최소값]&quot; 제약 조건을 비워 두어야 합니다. |
| [!UICONTROL 최대값] | [!UICONTROL 이중] | 수집 중에 수락할 Double의 최대값입니다. 수집된 값이 여기에 입력한 값과 정확히 일치하는 경우 값이 수락됩니다. 이 제약 조건을 사용할 때는 &quot;[!UICONTROL 배타적 최대값]&quot; 제약 조건을 비워 두어야 합니다. |
| [!UICONTROL 전용 최소값] | [!UICONTROL 이중] | 수집 중에 수락할 Double의 최대값입니다. 수집한 값이 여기에 입력한 값과 정확히 일치하는 경우 값이 거부됩니다. 이 제약 조건을 사용할 때는 &quot;[!UICONTROL 최소값]&quot;(비제외) 제약 조건을 비워 두어야 합니다. |
| [!UICONTROL 전용 최대값] | [!UICONTROL 이중] | 수집 중에 수락할 Double의 최대값입니다. 수집한 값이 여기에 입력한 값과 정확히 일치하는 경우 값이 거부됩니다. 이 제약 조건을 사용할 때는 &quot;[!UICONTROL 최대값]&quot;(비제외) 제약 조건을 비워 두어야 합니다. |

{style="table-layout:auto"}

## 특수 필드 유형 {#special}

오른쪽 레일은 선택한 필드에 대해 특수 역할을 지정하는 데 사용할 수 있는 몇 가지 확인란을 제공합니다. 이러한 옵션 중 일부의 사용 사례에는 데이터 모델링 전략과 다운스트림 플랫폼 서비스를 사용하는 방법에 대한 중요한 고려 사항이 포함됩니다.

이러한 특수 유형에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [맵](./map.md)
* [[!UICONTROL 필수]](./required.md)
* [[!UICONTROL 배열]](./array.md)
* [[!UICONTROL 열거형]](./enum.md)
* [[!UICONTROL ID]](./identity.md)(문자열 필드에만 사용 가능)
* [[!UICONTROL 관계]](./relationship.md)(문자열 필드에만 사용 가능)

기술적으로 특별한 필드 유형은 아니지만 스키마 구조가 중첩된 하위 필드를 정의하는 방법에 대해 자세히 알아보려면 [개체 유형 필드 정의](./object.md)에 대한 안내서를 참조하는 것이 좋습니다.

## 다음 단계

이 안내서에서는 UI에서 XDM 필드를 정의하는 방법에 대한 개요를 제공했습니다. 필드는 클래스 및 필드 그룹을 사용하여 스키마에만 추가할 수 있습니다. UI에서 이러한 리소스를 관리하는 방법에 대한 자세한 내용은 [클래스](../resources/classes.md) 및 [필드 그룹](../resources/field-groups.md) 만들기 및 편집에 대한 안내서를 참조하세요.

[!UICONTROL 스키마] 작업 영역의 기능에 대한 자세한 내용은 [[!UICONTROL 스키마] 작업 영역 개요](../overview.md)를 참조하십시오.
