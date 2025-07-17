---
title: Adobe Analytics을 Experience Platform에 연결
description: Adobe Analytics 보고서 세트 데이터를 Experience Platform으로 가져오는 방법 알아보기
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: d6a290b9891b3507d531a595a5428955c7e9ee90
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---

# Adobe Analytics을 Experience Platform에 연결

Adobe Analytics 소스를 사용하여 Analytics 보고서 세트 데이터를 Adobe Experience Platform으로 수집하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [XDM(경험 데이터 모델) 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [실시간 고객 프로필](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합된 실시간 고객 프로필을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### 주요 용어

이 문서 전체에서 사용되는 다음 주요 용어를 이해하는 것이 중요합니다.

* **표준 특성**: 표준 특성은 Adobe에서 미리 정의한 특성입니다. 모든 고객에 대해 동일한 의미를 포함하며 Analytics 소스 데이터 및 Analytics 스키마 필드 그룹에서 사용할 수 있습니다.
* **사용자 지정 특성**: 사용자 지정 특성은 Analytics의 사용자 지정 변수 계층 구조에 있는 모든 특성입니다. 사용자 지정 속성은 Adobe Analytics 구현 내에서 특정 정보를 보고서 세트에 캡처하는 데 사용되며 보고서 세트마다 용도가 다를 수 있습니다. 사용자 지정 속성에는 eVar, prop 및 목록이 포함됩니다. eVar에 대한 자세한 내용은 다음 [전환 변수에 대한 Analytics 설명서](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=ko)를 참조하십시오.
* **사용자 지정 필드 그룹의 모든 특성**: 고객이 만든 필드 그룹에서 시작된 특성은 모두 사용자 정의이며 표준 특성이나 사용자 지정 특성이 아닙니다.

## 소스 카탈로그 탐색

>[!NOTE]
>
>프로덕션 샌드박스에서 Analytics 소스 데이터 흐름을 만들면 두 개의 데이터 흐름이 만들어집니다.
>
>* 내역 보고서 세트 데이터를 데이터 레이크로 13개월 채우도록 하는 데이터 흐름입니다. 이 데이터 흐름은 채우기가 완료되면 종료됩니다.
>* 라이브 데이터를 데이터 레이크와 [!DNL Real-Time Customer Profile]&#x200B;(으)로 전송하는 데이터 흐름. 이 데이터 흐름은 지속적으로 실행됩니다.

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. *[!UICONTROL Adobe 응용 프로그램]* 범주에서 Adobe Analytics 카드를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![Adobe Analytics 소스 카드가 선택된 소스 카탈로그입니다.](../../../../images/tutorials/create/analytics/catalog.png)

## 데이터 선택

>[!IMPORTANT]
>
>* 화면에 나열된 보고서 세트는 다양한 지역에서 온 것일 수 있습니다. 데이터의 제한 사항 및 의무와 Adobe Experience Platform의 여러 지역에서 해당 데이터를 사용하는 방법을 이해해야 합니다. 귀사에서 이를 허용했는지 확인하십시오.
>* 여러 보고서 세트의 데이터는 의미가 다른 두 개의 사용자 지정 속성(eVar, 목록 및 prop)과 같이 데이터 충돌이 없는 경우에만 실시간 고객 프로필에 대해 활성화할 수 있습니다.

보고서 세트 는 Analytics 보고의 기반을 구성하는 데이터의 컨테이너입니다. 조직에는 서로 다른 데이터 세트를 포함하는 많은 보고서 세트가 있을 수 있습니다.

소스 연결이 생성되는 Experience Platform 샌드박스 인스턴스와 동일한 조직에 매핑되어 있는 한 모든 지역(미국, 영국 또는 싱가포르)에서 보고서 세트를 수집할 수 있습니다. 보고서 세트는 단일 활성 데이터 흐름만 사용하여 수집할 수 있습니다. 보고서 세트가 회색이고 선택할 수 없는 경우 사용 중인 샌드박스 또는 다른 샌드박스에서 이미 수집되었습니다.

여러 보고서 세트를 동일한 샌드박스로 가져오기 위해 바인딩된 연결을 여러 개 만들 수 있습니다. 보고서 세트에 변수(예: eVar 또는 이벤트)에 대한 다른 스키마가 있는 경우 사용자 지정 필드 그룹의 특정 필드에 매핑하여 [데이터 준비](../../../../../data-prep/ui/mapping.md)를 사용하여 데이터 충돌을 방지해야 합니다. 보고서 세트는 단일 샌드박스에만 추가할 수 있습니다.

**[!UICONTROL 보고서 세트]**&#x200B;를 선택한 다음 *[!UICONTROL Analytics 소스 데이터 추가]* 인터페이스를 사용하여 목록을 탐색하고 Experience Platform으로 수집할 Analytics 보고서 세트를 식별합니다. 계속하려면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![수집을 위해 Analytics 보고서 세트가 선택되어 있고 &quot;다음&quot; 단추가 강조 표시됩니다](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Analytics 보고서 세트는 한 번에 하나의 샌드박스에 대해 구성할 수 있습니다. 동일한 보고서 세트를 다른 샌드박스로 가져오려면 다른 샌드박스에 대한 구성을 통해 데이터 세트 흐름을 삭제하고 다시 인스턴스화해야 합니다.—>

## 매핑 {#mapping}

>[!IMPORTANT]
>
>데이터 준비 변환은 전체 데이터 흐름에 지연을 추가할 수 있습니다. 추가되는 지연은 변환 로직의 복잡성에 따라 달라집니다.

Analytics 데이터를 대상 XDM 스키마에 매핑하려면 먼저 기본 스키마를 사용하는지 아니면 사용자 지정 스키마를 사용하는지 확인해야 합니다.

>[!BEGINTABS]

>[!TAB 기본 스키마]

기본 스키마는 사용자를 대신하여 새 스키마를 만듭니다. 새로 만든 이 스키마에 [!DNL Adobe Analytics ExperienceEvent Template] 필드 그룹이 있습니다. 기본 스키마를 사용하려면 **[!UICONTROL 기본 스키마]**&#x200B;를 선택하십시오.

![Analytics 원본 워크플로의 스키마 선택 단계에서 &quot;기본 스키마&quot;를 선택했습니다.](../../../../images/tutorials/create/analytics/default-schema.png)

>[!TAB 사용자 지정 스키마]

사용자 지정 스키마를 사용하면 해당 스키마에 [!DNL Adobe Analytics ExperienceEvent Template] 필드 그룹이 있는 한 Analytics 데이터에 사용 가능한 모든 스키마를 선택할 수 있습니다. 사용자 지정 스키마를 사용하려면 **[!UICONTROL 사용자 지정 스키마]**&#x200B;를 선택하십시오.

![Analytics 원본 워크플로의 스키마 선택 단계에서 &quot;사용자 지정 스키마&quot;를 선택했습니다.](../../../../images/tutorials/create/analytics/custom-schema.png)

>[!ENDTABS]

*[!UICONTROL 매핑]* 인터페이스를 사용하여 소스 필드를 해당 대상 스키마 필드에 매핑하십시오. 사용자 지정 변수를 새 스키마 필드 그룹에 매핑하고 데이터 준비에서 지원하는 대로 계산을 적용할 수 있습니다. 대상 스키마를 선택하여 매핑 프로세스를 시작합니다.

>[!TIP]
>
>[!DNL Adobe Analytics ExperienceEvent Template] 필드 그룹이 있는 스키마만 스키마 선택 메뉴에 표시됩니다. 다른 스키마는 생략됩니다. 보고서 세트 데이터에 사용할 수 있는 적절한 스키마가 없는 경우 새 스키마를 만들어야 합니다. 스키마 만들기에 대한 자세한 단계는 [UI에서 스키마 만들고 편집하는 방법](../../../../../xdm/ui/resources/schemas.md)에 대한 안내서를 참조하십시오.

![매핑 인터페이스의 대상 스키마 선택 패널입니다.](../../../../images/tutorials/create/analytics/select-schema.png)

[!UICONTROL 적용된 표준 매핑]에 대한 지표는 [!UICONTROL 표준 필드 매핑] 패널을 참조할 수 있습니다. [!UICONTROL 설명자 이름 충돌이 있는 표준 매핑] 및 [!DNL Custom mappings].

| 표준 필드 매핑 | 설명 |
| --- | --- |
| [!UICONTROL 표준 매핑 적용됨] | [!UICONTROL 적용된 표준 매핑] 패널에 매핑된 속성의 총 수가 표시됩니다. 표준 매핑은 소스 Analytics 데이터의 모든 속성과 Analytics 필드 그룹의 해당 속성 간의 매핑을 의미합니다. 이는 사전 매핑되며 편집할 수 없습니다. |
| [!UICONTROL 설명자 이름 충돌이 있는 표준 매핑] | 설명자 이름 충돌이 있는 [!UICONTROL 표준 매핑] 패널은 이름 충돌이 있는 매핑된 특성 수를 나타냅니다. 이러한 충돌은 이미 다른 보고서 세트의 필드 설명자 세트가 채워진 스키마를 다시 사용할 때 나타납니다. 이름 충돌이 있더라도 Analytics 데이터 흐름을 진행할 수 있습니다. |
| [!UICONTROL 사용자 지정 매핑] | [!UICONTROL 사용자 지정 매핑] 패널에 eVar, prop 및 목록을 포함하여 매핑된 사용자 지정 특성의 수가 표시됩니다. 사용자 지정 매핑은 소스 Analytics 데이터의 사용자 지정 속성과 선택한 스키마에 포함된 사용자 지정 필드 그룹의 속성 간의 매핑을 의미합니다. |

### 표준 매핑 {#standard-mappings}

Experience Platform은 이름 충돌에 대한 매핑을 자동으로 감지합니다. 매핑과 충돌이 없으면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![이름 충돌 없음을 표시하는 표준 매핑 헤더입니다](../../../../images/tutorials/create/analytics/standard.png)

>[!TIP]
>
>소스 보고서 세트와 선택한 스키마 간에 이름 충돌이 있는 경우 필드 설명자가 변경되지 않음을 확인하면서 Analytics 데이터 흐름을 계속 진행할 수 있습니다. 또는 설명자 세트가 비어 있는 새 스키마를 만들도록 선택할 수 있습니다.

## 사용자 정의 매핑 {#custom-mappings}

데이터 준비 함수를 사용하여 새 사용자 지정 매핑 또는 사용자 지정 특성에 대한 계산된 필드를 추가할 수 있습니다. 사용자 지정 매핑을 추가하려면 **[!UICONTROL 사용자 지정]**&#x200B;을(를) 선택하십시오.

![Analytics 원본 워크플로의 사용자 지정 매핑 탭입니다.](../../../../images/tutorials/create/analytics/custom.png)

* **[!UICONTROL 필드 필터링]**: [!UICONTROL 필드 필터링] 텍스트 입력을 사용하여 매핑에서 특정 매핑 필드를 필터링합니다.
* **[!UICONTROL 새 매핑 추가]**: 새 원본 필드 및 대상 필드 매핑을 추가하려면 **[!UICONTROL 새 매핑 추가]**&#x200B;를 선택하십시오.
* **[!UICONTROL 계산된 필드 추가]**: 필요한 경우 **[!UICONTROL 계산된 필드 추가]**&#x200B;를 선택하여 매핑에 대한 새 계산된 필드를 만들 수 있습니다.
* **[!UICONTROL 매핑 가져오기]**: 데이터 준비의 매핑 가져오기 기능을 사용하여 데이터 수집 프로세스의 수동 구성 시간을 줄이고 오류를 제한할 수 있습니다. 기존 흐름 또는 내보낸 파일에서 매핑을 가져오려면 **[!UICONTROL 매핑 가져오기]**&#x200B;를 선택하십시오. 자세한 내용은 [매핑 가져오기 및 내보내기에 대한 안내서](../../../../../data-prep/ui/mapping.md#import-mapping)를 참조하십시오.
* **[!UICONTROL 템플릿 다운로드]**: 매핑의 CSV 복사본을 다운로드하고 로컬 장치에서 매핑을 구성할 수도 있습니다. **[!UICONTROL 템플릿 다운로드]**&#x200B;를 선택하여 매핑의 CSV 복사본을 다운로드합니다. 소스 파일 및 대상 스키마에 제공된 필드만 사용하고 있는지 확인해야 합니다.

데이터 준비에 대한 자세한 내용은 다음 설명서를 참조하십시오.

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

Analytics 보고서 세트 데이터에 대한 매핑을 완료한 후에는 필터링 규칙 및 조건을 적용하여 수집에서 실시간 고객 프로필로 데이터를 선택적으로 포함하거나 제외할 수 있습니다. 필터링에 대한 지원은 Analytics 데이터에만 사용할 수 있으며 데이터는 [!DNL Profile.] 입력 전에만 필터링됩니다. 모든 데이터는 데이터 레이크로 수집됩니다.

>[!BEGINSHADEBOX]

**실시간 고객 프로필에 대한 데이터 준비 및 Analytics 데이터 필터링에 대한 추가 정보**

* 프로필로 이동하는 데이터에는 필터링 기능을 사용할 수 있지만, 데이터 레이크로 이동하는 데이터에는 사용할 수 없습니다.
* 라이브 데이터에 필터링을 사용할 수 있지만 채우기 데이터는 필터링할 수 없습니다.
   * Analytics 소스는 프로필에 데이터를 채우지 않습니다.
* Analytics 흐름의 초기 설정 동안 데이터 준비 구성을 활용하는 경우 이러한 변경 사항은 자동 13개월 채우기에도 적용됩니다.
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

행 수준 및 열 수준에서 프로필 수집을 위한 데이터를 필터링할 수 있습니다. 행 수준 필터링을 사용하여 문자열 포함, 다음과 같음, 시작 또는 끝과 같은 기준을 정의합니다. 행 수준 필터링을 사용하여 `AND`과(와) `OR`을(를) 사용하여 조건을 조인하고 `NOT`을(를) 사용하여 조건을 무효화할 수도 있습니다.

행 수준에서 Analytics 데이터를 필터링하려면 **[!UICONTROL 행 필터]**&#x200B;를 선택하고 왼쪽 레일을 사용하여 스키마 계층 구조를 탐색하고 선택할 스키마 특성을 식별합니다.

![Analytics 데이터의 행 필터 인터페이스입니다.](../../../../images/tutorials/create/analytics/row-filter.png)

구성할 속성을 식별했으면 왼쪽 레일에서 속성을 선택하고 필터링 패널로 드래그합니다.

![필터링하기 위해 선택한 &quot;제조업체&quot; 특성입니다.](../../../../images/tutorials/create/analytics/filtering-panel.png)

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

![조건 연산자 목록이 있는 조건 드롭다운.](../../../../images/tutorials/create/analytics/conditions.png)

그런 다음 선택한 속성에 따라 포함할 값을 입력합니다. 아래 예에서 [!DNL Apple]제조업체[!DNL Google] 특성의 일부로 수집하기 위해 **[!UICONTROL 및]**&#x200B;을(를) 선택했습니다.

![선택한 특성과 값이 포함된 필터링 패널입니다.](../../../../images/tutorials/create/analytics/include.png)

필터링 조건을 추가로 지정하려면 스키마에서 다른 속성을 추가한 다음 해당 속성을 기반으로 값을 추가합니다. 아래 예제에서는 **[!UICONTROL Model]** 특성이 추가되고 [!DNL iPhone 16] 및 [!DNL Google Pixel 9]과(와) 같은 모델이 수집되도록 필터링됩니다.

![추가 특성 및 값이 컨테이너에 포함되어 있습니다.](../../../../images/tutorials/create/analytics/include-model.png)

새 컨테이너를 추가하려면 필터링 인터페이스의 오른쪽 상단에서 생략 부호(`...`)를 선택한 다음 **[!UICONTROL 컨테이너 추가]**&#x200B;를 선택합니다.

![컨테이너 추가 드롭다운 메뉴를 선택했습니다.](../../../../images/tutorials/create/analytics/add-container.png)

새 컨테이너가 추가되면 **[!UICONTROL 포함]**&#x200B;을 선택한 다음 드롭다운 메뉴에서 **[!UICONTROL 제외]**&#x200B;을(를) 선택하십시오. 제외할 특성과 값을 추가한 다음 완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![제외를 위해 필터링된 특성 및 값입니다.](../../../../images/tutorials/create/analytics/exclude.png)

### 열 수준 필터링

열 수준 필터링을 적용하려면 헤더에서 **[!UICONTROL 열 필터]**&#x200B;를 선택하십시오.

페이지가 대화형 스키마 트리로 업데이트되어 열 수준에서 스키마 속성이 표시됩니다. 여기에서는 프로필 수집에서 제외할 데이터 열을 선택할 수 있습니다. 또는 열을 확장하고 제외할 특정 속성을 선택할 수 있습니다.

기본적으로 모든 Analytics는 프로필로 이동하며 이 프로세스를 사용하면 XDM 데이터 분기를 프로필 수집에서 제외할 수 있습니다.

![스키마 트리가 있는 열 필터 인터페이스입니다.](../../../../images/tutorials/create/analytics/column-filter.png)

### 보조 ID 필터링

열 필터를 사용하여 프로필 수집에서 보조 ID를 제외합니다. 보조 ID를 필터링하려면 **[!UICONTROL 열 필터]**&#x200B;를 선택한 다음 **[!UICONTROL _ID]**&#x200B;을(를) 선택하십시오.

필터는 ID가 보조로 표시된 경우에만 적용됩니다. ID를 선택했지만 이벤트가 기본 ID로 표시된 ID 중 하나와 함께 도착하는 경우 해당 ID는 필터링되지 않습니다.

![열 필터링을 위해 스키마 트리의 보조 ID입니다.](../../../../images/tutorials/create/analytics/secondary-identities.png)

### 데이터 흐름 세부 정보 제공

**[!UICONTROL 데이터 흐름 세부 정보]** 단계가 나타납니다. 여기서 데이터 흐름의 이름과 선택적 설명을 제공해야 합니다. 완료되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![데이터 흐름 세부 정보 인터페이스입니다. 수집 워크플로우의 일부입니다.](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 검토

새 Analytics 데이터 흐름을 만들기 전에 검토할 수 있는 [!UICONTROL 검토] 단계가 나타납니다. 연결의 세부 정보는 다음을 포함하여 범주별로 그룹화됩니다.

* [!UICONTROL 연결]: 연결의 원본 플랫폼을 표시합니다.
* [!UICONTROL 데이터 형식]: 선택한 보고서 세트와 해당 보고서 세트 ID를 표시합니다.

![수집 워크플로의 검토 인터페이스입니다.](../../../../images/tutorials/create/analytics/review.png)

## 데이터 흐름 모니터링 {#monitor-your-dataflow}

데이터 흐름이 완료되면 *[!UICONTROL 데이터 흐름]* 인터페이스를 사용하여 Analytics 데이터 흐름의 상태를 모니터링할 수 있습니다.

Analytics에서 Experience Platform으로 전송되는 데이터의 진행 상황에 대한 정보를 보려면 [!UICONTROL 데이터 집합 활동] 인터페이스를 사용하십시오. 인터페이스에는 이전 달의 총 레코드, 지난 7일 동안의 수집된 총 레코드 및 이전 달의 데이터 크기와 같은 지표가 표시됩니다.

소스는 두 개의 데이터 세트 흐름을 인스턴스화합니다. 한 흐름은 채우기 데이터를 나타내고 다른 흐름은 라이브 데이터에 대한 것입니다. 채우기 데이터는 실시간 고객 프로필로 수집되도록 구성되지 않지만 분석 및 데이터 과학 사용 사례를 위해 데이터 레이크로 전송됩니다.

채우기, 라이브 데이터 및 해당 지연 시간에 대한 자세한 내용은 [Analytics 소스 개요](../../../../connectors/adobe-applications/analytics.md)를 읽어 보십시오.

![Adobe Analytics 데이터에 대한 지정된 대상 데이터 집합에 대한 데이터 집합 활동 페이지입니다.](../../../../images/tutorials/create/analytics/dataset-activity.png)

>[!NOTE]
>
>Analytics 소스 커넥터는 Adobe에서 전체적으로 관리되므로 데이터 세트 활동 페이지에 배치에 대한 정보가 표시되지 않습니다. 수집된 레코드 관련 지표를 보고 데이터가 이동하는지 모니터링할 수 있습니다.

## 데이터 흐름 삭제 {#delete-dataflow}

>[!NOTE]
>
>Analytics 데이터 흐름은 비활성화할 수 없습니다. Analytics 데이터의 흐름을 중지하려면 데이터 흐름을 완전히 **삭제**&#x200B;해야 합니다.

Analytics 데이터 흐름을 삭제하려면 소스 작업 영역의 상단 헤더에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택하십시오. 데이터 흐름 페이지를 사용하여 삭제하려는 Analytics 데이터 흐름을 찾은 다음 그 옆에 있는 생략 부호(`...`)를 선택합니다. 그런 다음 드롭다운 메뉴를 사용하여 **[!UICONTROL 삭제]**&#x200B;를 선택합니다.

* 라이브 Analytics 데이터 흐름을 삭제하면 기본 데이터 세트도 삭제됩니다.
* 채우기 분석 데이터 흐름을 삭제해도 기본 데이터 세트는 삭제되지 않지만, 해당 보고서 세트에 대한 채우기 프로세스는 중지됩니다. 채우기 데이터 흐름을 삭제하는 경우 수집된 데이터는 데이터 세트를 통해 계속 볼 수 있습니다.

## 다음 단계 및 추가 리소스

연결이 만들어지면 들어오는 데이터를 포함하도록 데이터 흐름이 자동으로 만들어지고 데이터 세트를 선택한 스키마로 채웁니다. 또한 데이터 다시 채우기가 발생하고 최대 13개월의 내역 데이터가 수집됩니다. 초기 수집이 완료되면 Analytics 데이터를 사용하고 [!DNL Real-Time Customer Profile] 및 세분화 서비스와 같은 다운스트림 Experience Platform 서비스에서 사용합니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-Time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 개요](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 개요](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 개요](../../../../../query-service/home.md)

다음 비디오는 Adobe Analytics Source 커넥터를 사용하는 데이터 수집에 대한 이해를 지원하기 위한 것입니다.

>[!WARNING]
>
> 다음 비디오에 표시된 [!DNL Experience Platform] UI가 최신 상태가 아닙니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3430256?quality=12&learn=on&captions=kor)

