---
title: UI에서 Adobe Analytics Source 연결 만들기
description: UI에서 Adobe Analytics 소스 연결을 만들어 소비자 데이터를 Adobe Experience Platform으로 가져오는 방법을 알아봅니다.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2676'
ht-degree: 3%

---

# UI에서 Adobe Analytics 소스 연결 만들기

이 자습서에서는 UI에서 Adobe Analytics 소스 연결을 만들어 Adobe Analytics 보고서 세트 데이터를 Adobe Experience Platform으로 가져오는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [XDM(경험 데이터 모델) 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [실시간 고객 프로필](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합된 실시간 고객 프로필을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### 주요 용어

이 문서 전체에서 사용되는 다음 주요 용어를 이해하는 것이 중요합니다.

* **표준 특성**: 표준 특성은 Adobe에서 미리 정의한 특성입니다. 모든 고객에 대해 동일한 의미를 포함하고 [!DNL Analytics] 원본 데이터 및 [!DNL Analytics] 스키마 필드 그룹에서 사용할 수 있습니다.
* **사용자 지정 특성**: 사용자 지정 특성은 [!DNL Analytics]의 사용자 지정 변수 계층 구조에 있는 모든 특성입니다. 사용자 지정 속성은 Adobe Analytics 구현 내에서 특정 정보를 보고서 세트에 캡처하는 데 사용되며 보고서 세트마다 용도가 다를 수 있습니다. 사용자 지정 속성에는 eVar, prop 및 목록이 포함됩니다. eVar에 대한 자세한 내용은 다음 [[!DNL Analytics] 전환 변수에 대한 설명서](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=ko)를 참조하십시오.
* **사용자 지정 필드 그룹의 모든 특성**: 고객이 만든 필드 그룹에서 시작된 특성은 모두 사용자 정의이며 표준 특성이나 사용자 지정 특성이 아닙니다.
* **친숙한 이름**: 친숙한 이름은 [!DNL Analytics] 구현에서 사용자 지정 변수에 대해 사용자가 제공한 레이블입니다. 알기 쉬운 이름에 대한 자세한 내용은 다음 [[!DNL Analytics] 전환 변수에 대한 설명서](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=ko)를 참조하십시오.

## Adobe Analytics과의 소스 연결 만들기

>[!NOTE]
>
>프로덕션 샌드박스에서 Analytics 소스 데이터 흐름을 만들면 두 개의 데이터 흐름이 만들어집니다.
>
>* 내역 보고서 세트 데이터를 데이터 레이크로 13개월 채우도록 하는 데이터 흐름입니다. 이 데이터 흐름은 채우기가 완료되면 종료됩니다.
>* 라이브 데이터를 데이터 레이크와 [!DNL Real-Time Customer Profile]&#x200B;(으)로 전송하는 데이터 흐름. 이 데이터 흐름은 지속적으로 실행됩니다.

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 검색 창을 사용하여 표시되는 소스의 범위를 좁힐 수도 있습니다.

**[!UICONTROL Adobe 응용 프로그램]** 범주에서 **[!UICONTROL Adobe Analytics]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/analytics/catalog.png)

### 데이터 선택

>[!IMPORTANT]
>
>화면에 나열된 보고서 세트는 다양한 지역에서 온 것일 수 있습니다. 데이터의 제한 사항 및 의무와 Adobe Experience Platform의 여러 지역에서 해당 데이터를 사용하는 방법을 이해해야 합니다. 귀사에서 이를 허용했는지 확인하십시오.

**[!UICONTROL Analytics 원본 데이터 추가]** 단계에서는 원본 연결을 만들 수 있는 [!DNL Analytics] 보고서 세트 데이터 목록을 제공합니다.

보고서 세트는 [!DNL Analytics] 보고의 기초가 되는 데이터의 컨테이너입니다. 조직에는 서로 다른 데이터 세트를 포함하는 많은 보고서 세트가 있을 수 있습니다.

소스 연결이 생성되는 Experience Platform 샌드박스 인스턴스와 동일한 조직에 매핑되어 있는 한 모든 지역(미국, 영국 또는 싱가포르)에서 보고서 세트를 수집할 수 있습니다. 보고서 세트는 단일 활성 데이터 흐름만 사용하여 수집할 수 있습니다. 선택할 수 없는 보고서 세트는 사용 중인 샌드박스 또는 다른 샌드박스에서 이미 수집되었습니다.

여러 보고서 세트를 동일한 샌드박스로 가져오기 위해 바인딩된 연결을 여러 개 만들 수 있습니다. 보고서 세트에 변수(예: eVar 또는 이벤트)에 대한 다른 스키마가 있는 경우 사용자 지정 필드 그룹의 특정 필드에 매핑하여 [데이터 준비](../../../../../data-prep/ui/mapping.md)를 사용하여 데이터 충돌을 방지해야 합니다. 보고서 세트는 단일 샌드박스에만 추가할 수 있습니다.

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>여러 보고서 세트의 데이터는 의미가 다른 두 개의 사용자 지정 속성(eVar, 목록 및 prop)과 같이 데이터 충돌이 없는 경우에만 실시간 고객 프로필에 대해 활성화할 수 있습니다.

[!DNL Analytics] 원본 연결을 만들려면 보고서 세트를 선택한 다음 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Analytics 보고서 세트는 한 번에 하나의 샌드박스에 대해 구성할 수 있습니다. 동일한 보고서 세트를 다른 샌드박스로 가져오려면 다른 샌드박스에 대한 구성을 통해 데이터 세트 흐름을 삭제하고 다시 인스턴스화해야 합니다.—>

### 매핑

>[!IMPORTANT]
>
>데이터 준비 변환은 전체 데이터 흐름에 지연을 추가할 수 있습니다. 추가되는 지연은 변환 로직의 복잡성에 따라 달라집니다.

[!DNL Analytics] 데이터를 대상 XDM 스키마에 매핑하려면 먼저 기본 스키마를 사용할지 사용자 지정 스키마를 사용할지 선택해야 합니다.

기본 스키마는 사용자를 대신하여 [!DNL Adobe Analytics ExperienceEvent Template] 필드 그룹을 포함하는 새 스키마를 만듭니다. 기본 스키마를 사용하려면 **[!UICONTROL 기본 스키마]**&#x200B;를 선택하십시오.

![기본 스키마](../../../../images/tutorials/create/analytics/default-schema.png)

사용자 지정 스키마를 사용하면 해당 스키마에 [!DNL Adobe Analytics ExperienceEvent Template] 필드 그룹이 있는 한 [!DNL Analytics] 데이터에 사용 가능한 모든 스키마를 선택할 수 있습니다. 사용자 지정 스키마를 사용하려면 **[!UICONTROL 사용자 지정 스키마]**&#x200B;를 선택하십시오.

![사용자 지정 스키마](../../../../images/tutorials/create/analytics/custom-schema.png)

[!UICONTROL 매핑] 페이지에서는 소스 필드를 해당 대상 스키마 필드에 매핑하는 인터페이스를 제공합니다. 여기에서 사용자 지정 변수를 새 스키마 필드 그룹에 매핑하고 데이터 준비에서 지원하는 대로 계산을 적용할 수 있습니다. 대상 스키마를 선택하여 매핑 프로세스를 시작합니다.

>[!TIP]
>
>[!DNL Adobe Analytics ExperienceEvent Template] 필드 그룹이 있는 스키마만 스키마 선택 메뉴에 표시됩니다. 다른 스키마는 생략됩니다. 보고서 세트 데이터에 사용할 수 있는 적절한 스키마가 없는 경우 새 스키마를 만들어야 합니다. 스키마 만들기에 대한 자세한 단계는 [UI에서 스키마 만들고 편집하는 방법](../../../../../xdm/ui/resources/schemas.md)에 대한 안내서를 참조하십시오.

![스키마 선택](../../../../images/tutorials/create/analytics/select-schema.png)

[!UICONTROL 표준 필드 매핑] 섹션에는 [!UICONTROL 적용된 표준 매핑], [!UICONTROL 일치하지 않는 표준 매핑] 및 [!UICONTROL 사용자 지정 매핑]에 대한 패널이 표시됩니다. 각 카테고리에 대한 특정 정보는 다음 표를 참조하십시오.

| 표준 필드 매핑 | 설명 |
| --- | --- |
| [!UICONTROL 표준 매핑 적용됨] | [!UICONTROL 적용된 표준 매핑] 패널에 매핑된 속성의 총 수가 표시됩니다. 표준 매핑은 원본 [!DNL Analytics] 데이터의 모든 특성과 [!DNL Analytics] 필드 그룹의 해당 특성 간의 매핑 집합을 나타냅니다. 이는 사전 매핑되며 편집할 수 없습니다. |
| [!UICONTROL 일치하지 않는 표준 매핑] | [!UICONTROL 일치하지 않는 표준 매핑] 패널은 이름 충돌이 있는 매핑된 특성 수를 나타냅니다. 이러한 충돌은 이미 다른 보고서 세트의 필드 설명자 세트가 채워진 스키마를 다시 사용할 때 나타납니다. 알기 쉬운 이름 충돌이 있어도 [!DNL Analytics] 데이터 흐름을 진행할 수 있습니다. |
| [!UICONTROL 사용자 지정 매핑] | [!UICONTROL 사용자 지정 매핑] 패널에 eVar, prop 및 목록을 포함하여 매핑된 사용자 지정 특성의 수가 표시됩니다. 사용자 지정 매핑은 원본 [!DNL Analytics] 데이터의 사용자 지정 특성과 선택한 스키마에 포함된 사용자 지정 필드 그룹의 특성 간의 매핑 집합을 나타냅니다. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

[!DNL Analytics] ExperienceEvent 템플릿 스키마 필드 그룹을 미리 보려면 [!UICONTROL 적용된 표준 매핑] 패널에서 **[!UICONTROL 보기]**&#x200B;를 선택합니다.

![보기](../../../../images/tutorials/create/analytics/view.png)

[!UICONTROL Adobe Analytics ExperienceEvent 템플릿 스키마 필드 그룹] 페이지에서는 스키마 구조를 검사하는 데 사용할 인터페이스를 제공합니다. 완료되면 **[!UICONTROL 닫기]**&#x200B;를 선택합니다.

![필드 그룹 미리 보기](../../../../images/tutorials/create/analytics/field-group-preview.png)

Experience Platform은 모든 친숙한 이름 충돌에 대해 매핑 세트를 자동으로 감지합니다. 매핑 집합과 충돌이 없으면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![매핑](../../../../images/tutorials/create/analytics/mapping.png)

>[!TIP]
>
>소스 보고서 세트와 선택한 스키마 간에 알기 쉬운 이름 충돌이 있는 경우 [!DNL Analytics] 데이터 흐름을 계속 사용할 수 있으며 필드 설명자는 변경되지 않습니다. 또는 설명자 세트가 비어 있는 새 스키마를 만들도록 선택할 수 있습니다.

#### 사용자 정의 매핑

데이터 준비 함수를 사용하여 새 사용자 지정 매핑 또는 사용자 지정 특성에 대한 계산된 필드를 추가할 수 있습니다. 사용자 지정 매핑을 추가하려면 **[!UICONTROL 사용자 지정]**&#x200B;을(를) 선택하십시오.

![사용자 지정](../../../../images/tutorials/create/analytics/custom.png)

필요에 따라 **[!UICONTROL 새 매핑 추가]** 또는 **[!UICONTROL 계산된 필드 추가]**&#x200B;를 선택하고 사용자 지정 특성에 대한 사용자 지정 매핑을 만들 수 있습니다. 데이터 준비 기능을 사용하는 방법에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md)를 참조하십시오.

다음 설명서는 데이터 준비, 계산된 필드 및 매핑 함수 이해에 대한 추가 리소스를 제공합니다.

* [데이터 준비 개요](../../../../../data-prep/home.md)
* [데이터 준비 매핑 함수](../../../../../data-prep/functions.md)
* [계산된 필드 추가](../../../../../data-prep/ui/mapping.md#calculated-fields)

<!-- 
To use Data Prep functions and add new mapping or calculated fields for custom attributes, select **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Next, select **[!UICONTROL Add new mapping]**.

Depending on your needs, you can select either **[!UICONTROL Add new mapping]** or **[!UICONTROL Add calculated field]** from the options that appear. 

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

An empty mapping set appears. Select the mapping icon to add a source field.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

You can use the interface to navigate through the source schema structure and identify the new source field that you want to use. Once you have selected the source field that you want to map, select **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Next, select the mapping icon under [!UICONTROL Target Field] to map your selected source field to its appropriate target field.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Similar to the source schema, you can use the interface to navigate through the target schema structure and select the target field you want to map to. Once you have selected the appropriate target field, select **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

With your custom mapping set completed, select **[!UICONTROL Next]** to proceed.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png) -->

## 실시간 고객 프로필에 대한 필터링 {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="필터 규칙 만들기"
>abstract="데이터를 실시간 고객 프로필로 전송할 때 행 및 열 수준 필터링 규칙을 정의합니다. 행 수준 필터링을 사용하여 조건을 적용하고 **프로필 수집에 포함**&#x200B;할 데이터를 보여 줍니다. 열 수준 필터링을 사용하여 **프로필 수집에서 제외**&#x200B;할 데이터 열을 선택합니다. 필터링 규칙은 데이터 레이크로 전송된 데이터에 적용되지 않습니다."

[!DNL Analytics] 보고서 세트 데이터에 대한 매핑을 완료한 후에는 필터링 규칙과 조건을 적용하여 수집에서 실시간 고객 프로필로 데이터를 선택적으로 포함하거나 제외할 수 있습니다. 필터링에 대한 지원은 [!DNL Analytics] 데이터에만 사용할 수 있으며 데이터는 [!DNL Profile.] 입력 전에만 필터링됩니다. 모든 데이터는 데이터 레이크로 수집됩니다.

>[!BEGINSHADEBOX]

**실시간 고객 프로필에 대한 데이터 준비 및 Analytics 데이터 필터링에 대한 추가 정보**

* 프로필로 이동하는 데이터에는 필터링 기능을 사용할 수 있지만, 데이터 레이크로 이동하는 데이터에는 사용할 수 없습니다.
* 라이브 데이터에 필터링을 사용할 수 있지만 채우기 데이터는 필터링할 수 없습니다.
   * [!DNL Analytics] 원본이 프로필에 데이터를 채우지 않습니다.
* [!DNL Analytics] 흐름의 초기 설정 중에 데이터 준비 구성을 활용하는 경우 이러한 변경 내용은 자동 13개월 채우기에도 적용됩니다.
   * 단, 필터링은 라이브 데이터에만 예약되어 있으므로 필터링에 대해서는 해당되지 않습니다.
* 데이터 준비는 스트리밍 및 일괄 처리 수집 경로 모두에 적용됩니다. 기존 데이터 준비 구성을 수정하는 경우 이러한 변경 사항은 스트리밍 및 배치 수집 경로 모두에서 새 수신 데이터에 적용됩니다.
   * 그러나 스트리밍 데이터인지 배치 데이터인지에 관계없이, Experience Platform에 이미 수집된 데이터에는 데이터 준비 구성이 적용되지 않습니다.
* Analytics의 표준 속성은 항상 자동으로 매핑됩니다. 따라서 표준 속성에는 변환을 적용할 수 없습니다.
   * 그러나 ID 서비스 또는 프로필에서 필요하지 않은 표준 속성은 필터링할 수 있습니다.
* 열 수준 필터링을 사용하여 필수 필드 및 ID 필드를 필터링할 수 없습니다.
* 보조 ID, 특히 AAID 및 AACustomID를 필터링할 수 있지만 ECID는 필터링할 수 없습니다.
* 변환 오류가 발생하면 해당 열이 NULL이 됩니다.

>[!ENDSHADEBOX]

### 행 수준 필터링

>[!IMPORTANT]
>
>행 수준 필터링을 사용하여 조건을 적용하고 **프로필 수집에 포함**&#x200B;할 데이터를 보여 줍니다. 열 수준 필터링을 사용하여 **프로필 수집을 위해 제외**&#x200B;할 데이터 열을 선택합니다.

행 수준 및 열 수준에서 [!DNL Profile] 수집에 대한 데이터를 필터링할 수 있습니다. 행 수준 필터링을 사용하면 문자열 포함, 다음과 같음, 시작 또는 끝과 같은 기준을 정의할 수 있습니다. 행 수준 필터링을 사용하여 `AND`과(와) `OR`을(를) 사용하여 조건을 조인하고 `NOT`을(를) 사용하여 조건을 무효화할 수도 있습니다.

행 수준에서 [!DNL Analytics] 데이터를 필터링하려면 **[!UICONTROL 행 필터]**&#x200B;를 선택하세요.

![행 필터](../../../../images/tutorials/create/analytics/row-filter.png)

왼쪽 레일을 사용하여 스키마 계층을 탐색하고 선택한 스키마 속성을 선택하여 특정 스키마를 추가로 드릴다운합니다.

![왼쪽 레일](../../../../images/tutorials/create/analytics/left-rail.png)

구성할 속성을 식별했으면 왼쪽 레일에서 속성을 선택하고 필터링 패널로 드래그합니다.

![필터링 패널](../../../../images/tutorials/create/analytics/filtering-panel.png)

다른 조건을 구성하려면 **[!UICONTROL 같음]**&#x200B;을 선택한 다음 나타나는 드롭다운 창에서 조건을 선택하십시오.

구성 가능한 조건 목록은 다음과 같습니다.

* [!UICONTROL 같음]
* [!UICONTROL 같지 않음]
* [!UICONTROL 다음으로 시작]
* [!UICONTROL 다음으로 끝남]
* [!UICONTROL 다음으로 끝나지 않음]
* [!UICONTROL 포함]
* [!UICONTROL 포함하지 않음]
* [!UICONTROL 존재함]
* [!UICONTROL 존재하지 않음]

![조건](../../../../images/tutorials/create/analytics/conditions.png)

그런 다음 선택한 속성에 따라 포함할 값을 입력합니다. 아래 예에서 **[!UICONTROL 제조업체]** 특성의 일부로 수집하기 위해 [!DNL Apple] 및 [!DNL Google]을(를) 선택했습니다.

![include-manufacturer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

필터링 조건을 추가로 지정하려면 스키마에서 다른 속성을 추가한 다음 해당 속성을 기반으로 값을 추가합니다. 아래 예제에서는 **[!UICONTROL Model]** 특성이 추가되고 [!DNL iPhone 13] 및 [!DNL Google Pixel 6]과(와) 같은 모델이 수집되도록 필터링됩니다.

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

새 컨테이너를 추가하려면 필터링 인터페이스의 오른쪽 상단에서 생략 부호(`...`)를 선택한 다음 **[!UICONTROL 컨테이너 추가]**&#x200B;를 선택합니다.

![컨테이너 추가](../../../../images/tutorials/create/analytics/add-container.png)

새 컨테이너가 추가되면 표시되는 드롭다운 창에서 **[!UICONTROL 포함]**&#x200B;을 선택한 다음 **[!UICONTROL 제외]**&#x200B;를 선택하십시오.

![제외](../../../../images/tutorials/create/analytics/exclude.png)

그런 다음 스키마 속성을 드래그하고 필터링에서 제외할 해당 값을 추가하여 동일한 프로세스를 완료합니다. 아래 예에서 [!DNL iPhone 12], [!DNL iPhone 12 mini] 및 [!DNL Google Pixel 5]은(는) 모두 **[!UICONTROL Model]** 특성에서 제외에서 필터링되고, 가로가 **[!UICONTROL 화면 방향]**&#x200B;에서 제외되며, 모델 번호 [!DNL A1633]은(는) **[!UICONTROL 모델 번호]**&#x200B;에서 제외됩니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![exclude-examples](../../../../images/tutorials/create/analytics/exclude-examples.png)

### 열 수준 필터링

열 수준 필터링을 적용하려면 헤더에서 **[!UICONTROL 열 필터]**&#x200B;를 선택하십시오.

![열 필터](../../../../images/tutorials/create/analytics/column-filter.png)

페이지가 대화형 스키마 트리로 업데이트되어 열 수준에서 스키마 속성이 표시됩니다. 여기에서 [!DNL Profile] 수집에서 제외하려는 데이터 열을 선택할 수 있습니다. 또는 열을 확장하고 제외할 특정 속성을 선택할 수 있습니다.

기본적으로 모든 [!DNL Analytics]은(는) [!DNL Profile]&#x200B;(으)로 이동하며 이 프로세스를 통해 XDM 데이터 분기를 [!DNL Profile] 수집에서 제외할 수 있습니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![열 선택](../../../../images/tutorials/create/analytics/columns-selected.png)

### 보조 ID 필터링

열 필터를 사용하여 프로필 수집에서 보조 ID를 제외합니다. 보조 ID를 필터링하려면 **[!UICONTROL 열 필터]**&#x200B;를 선택한 다음 **[!UICONTROL _ID]**&#x200B;을(를) 선택하십시오.

필터는 ID가 보조로 표시된 경우에만 적용됩니다. ID를 선택했지만 이벤트가 기본 ID로 표시된 ID 중 하나와 함께 도착하는 경우 해당 ID는 필터링되지 않습니다.

![보조 ID](../../../../images/tutorials/create/analytics/secondary-identities.png)

### 데이터 흐름 세부 정보 제공

**[!UICONTROL 데이터 흐름 세부 정보]** 단계가 나타납니다. 여기서 데이터 흐름의 이름과 선택적 설명을 제공해야 합니다. 완료되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![데이터 흐름-세부 정보](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 검토

새 Analytics 데이터 흐름을 만들기 전에 검토할 수 있는 [!UICONTROL 검토] 단계가 나타납니다. 연결의 세부 정보는 다음을 포함하여 범주별로 그룹화됩니다.

* [!UICONTROL 연결]: 연결의 원본 플랫폼을 표시합니다.
* [!UICONTROL 데이터 형식]: 선택한 보고서 세트와 해당 보고서 세트 ID를 표시합니다.

![검토](../../../../images/tutorials/create/analytics/review.png)

## 데이터 흐름 모니터링 {#monitor-your-dataflow}

데이터 흐름이 완료되면 소스 카탈로그에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택하여 데이터의 활동 및 상태를 모니터링합니다.

![데이터 흐름 탭이 선택된 소스 카탈로그입니다.](../../../../images/tutorials/create/analytics/select-dataflows.png)

조직의 기존 Analytics 데이터 흐름 목록이 나타납니다. 여기에서 타겟 데이터 세트를 선택하여 해당 수집 활동을 확인합니다.

![조직의 기존 Adobe Analytics 데이터 흐름 목록입니다.](../../../../images/tutorials/create/analytics/select-target-dataset.png)

[!UICONTROL 데이터 집합 활동] 페이지에서는 Analytics에서 Experience Platform으로 전송되는 데이터의 진행 상황에 대한 정보를 제공합니다. 인터페이스에는 이전 달의 총 레코드, 지난 7일 동안의 수집된 총 레코드 및 이전 달의 데이터 크기와 같은 지표가 표시됩니다.

소스는 두 개의 데이터 세트 흐름을 인스턴스화합니다. 한 흐름은 채우기 데이터를 나타내고 다른 흐름은 라이브 데이터에 대한 것입니다. 채우기 데이터는 실시간 고객 프로필로 수집되도록 구성되지 않지만 분석 및 데이터 과학 사용 사례를 위해 데이터 레이크로 전송됩니다.

채우기, 라이브 데이터 및 해당 지연 시간에 대한 자세한 내용은 [Analytics 소스 개요](../../../../connectors/adobe-applications/analytics.md)를 읽어 보십시오.

![Adobe Analytics 데이터에 대한 지정된 대상 데이터 집합에 대한 데이터 집합 활동 페이지입니다.](../../../../images/tutorials/create/analytics/dataset-activity.png)

>[!NOTE]
>
>Analytics 소스 커넥터는 Adobe에서 전체적으로 관리되므로 데이터 세트 활동 페이지에 배치에 대한 정보가 표시되지 않습니다. 수집된 레코드 관련 지표를 보고 데이터가 이동하는지 모니터링할 수 있습니다.

## 데이터 흐름 삭제 {#delete-dataflow}

Analytics 데이터 흐름을 삭제하려면 소스 작업 영역의 상단 헤더에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택하십시오. 데이터 흐름 페이지를 사용하여 삭제하려는 Analytics 데이터 흐름을 찾은 다음 그 옆에 있는 생략 부호(`...`)를 선택합니다. 그런 다음 드롭다운 메뉴를 사용하여 **[!UICONTROL 삭제]**&#x200B;를 선택합니다.

* 라이브 Analytics 데이터 흐름을 삭제하면 기본 데이터 세트도 삭제됩니다.
* 채우기 분석 데이터 흐름을 삭제해도 기본 데이터 세트는 삭제되지 않지만, 해당 보고서 세트에 대한 채우기 프로세스는 중지됩니다. 채우기 데이터 흐름을 삭제하는 경우 수집된 데이터는 데이터 세트를 통해 계속 볼 수 있습니다.

## 다음 단계 및 추가 리소스

연결이 만들어지면 들어오는 데이터를 포함하도록 데이터 흐름이 자동으로 만들어지고 데이터 세트를 선택한 스키마로 채웁니다. 또한 데이터 다시 채우기가 발생하고 최대 13개월의 내역 데이터가 수집됩니다. 초기 수집이 완료되면 [!DNL Analytics] 데이터를 [!DNL Real-Time Customer Profile] 및 세분화 서비스와 같은 다운스트림 Experience Platform 서비스에서 사용합니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-Time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 개요](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 개요](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 개요](../../../../../query-service/home.md)

다음 비디오는 Adobe Analytics Source 커넥터를 사용하는 데이터 수집에 대한 이해를 지원하기 위한 것입니다.

>[!WARNING]
>
> 다음 비디오에 표시된 [!DNL Experience Platform] UI가 최신 상태가 아닙니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
