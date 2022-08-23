---
keywords: Experience Platform;홈;인기 항목;Analytics 소스 커넥터;Analytics 커넥터;Analytics 소스;Analytics
solution: Experience Platform
title: UI에서 Adobe Analytics 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: UI에서 Adobe Analytics 소스 연결을 만들어 소비자 데이터를 Adobe Experience Platform으로 가져오는 방법을 알아봅니다.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 1d77ad44c7123f32301257c238299b7c16e2c92b
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 2%

---

# UI에서 Adobe Analytics 소스 연결 만들기

이 자습서에서는 가져올 UI에서 Adobe Analytics 소스 연결을 만드는 단계를 제공합니다 [!DNL Analytics] 보고서 세트 데이터를 Adobe Experience Platform에 가져옵니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [XDM(경험 데이터 모델) 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [실시간 고객 프로필](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 주요 용어

이 문서 전체에서 사용되는 다음과 같은 주요 용어를 이해하는 것이 중요합니다.

* **표준 속성**: 표준 속성은 Adobe에 의해 사전 정의된 모든 속성입니다. 모든 고객에 대해 동일한 의미를 포함하며, [!DNL Analytics] 소스 데이터 및 [!DNL Analytics] 스키마 필드 그룹.
* **사용자 지정 속성**: 사용자 지정 속성은 다음 의 사용자 지정 변수 계층 구조에 있는 모든 속성입니다. [!DNL Analytics]. 사용자 지정 속성은 Adobe Analytics 구현 내에서 특정 정보를 보고서 세트에 캡처하는 데 사용되며 보고서 세트와 보고서 세트의 사용에 따라 다를 수 있습니다. 사용자 지정 속성에는 eVar, prop 및 목록이 포함됩니다. 다음을 참조하십시오 [[!DNL Analytics] 전환 변수에 대한 설명서](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 를 참조하십시오.
* **사용자 지정 필드 그룹의 모든 속성**: 고객이 생성한 필드 그룹에서 생성된 속성은 모두 사용자가 정의하며 표준 또는 사용자 지정 속성이 아닌 것으로 간주됩니다.
* **친숙한 이름**: 친숙한 이름은 에서 사용자 지정 변수에 대해 사용자가 제공하는 레이블입니다 [!DNL Analytics] 구현 을 참조하십시오. 다음을 참조하십시오 [[!DNL Analytics] 전환 변수에 대한 설명서](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 친숙한 이름에 대한 자세한 정보.

## Adobe Analytics과 소스 연결 만들기

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 검색 창을 사용하여 표시된 소스 범위를 좁힐 수도 있습니다.

아래에 **[!UICONTROL Adobe 애플리케이션]** 카테고리, 선택 **[!UICONTROL Adobe Analytics]** 그런 다음 **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/analytics/catalog.png)

### 데이터 선택

다음 **[!UICONTROL Analytics 소스 데이터 추가]** 단계는 [!DNL Analytics] 보고서 세트 데이터를 사용하여 소스 연결을 만들 수 있습니다.

하나의 활성 데이터 흐름만 사용하여 보고서 세트를 수집할 수 있습니다. 여러 데이터 흐름에서는 사용할 수 없습니다. 또한 보고서 세트는 소스 연결이 만들어지는 Platform Sandbox 인스턴스와 동일한 영역에 속해야 합니다. 선택할 수 없는 보고서 세트는 이 샌드박스 또는 다른 샌드박스에서 이미 섭취되었습니다.

여러 개의 인바운드 연결을 만들어 여러 보고서 세트를 동일한 샌드박스로 가져올 수 있습니다. 보고서 세트에 변수(예: eVar 또는 이벤트)에 대한 스키마가 다른 경우 이러한 보고서 세트를 사용자 지정 필드 그룹의 특정 필드에 매핑해야 하며 [데이터 준비](../../../../../data-prep/ui/mapping.md). 보고서 세트는 단일 샌드박스에만 추가할 수 있습니다.

>[!NOTE]
>
>의미가 다른 두 사용자 지정 속성(eVar, 목록 및 prop)과 같은 데이터 충돌이 없으면 여러 보고서 세트의 데이터를 XDM의 동일한 속성에 매핑할 수 없는 경우에만 실시간 고객 데이터 프로필에 대해 활성화할 수 있습니다.

을(를) 만들려면 [!DNL Analytics] 소스 연결에서 보고서 세트를 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### 매핑

>[!IMPORTANT]
>
>데이터 준비 변환은 전체 데이터 플로우에 지연을 추가할 수 있습니다. 추가된 추가적인 지연은 변환 로직의 복잡성에 따라 달라집니다.

매핑하기 전에 [!DNL Analytics] 데이터를 XDM 스키마를 타겟팅하려면 먼저 기본 스키마를 사용하는지 또는 사용자 지정 스키마를 사용하는지를 선택해야 합니다.

기본 스키마는 를 포함하여 사용자를 대신하여 새 스키마를 만듭니다 [!DNL Adobe Analytics ExperienceEvent Template] 필드 그룹. 기본 스키마를 사용하려면 **[!UICONTROL 기본 스키마]**.

![기본 스키마](../../../../images/tutorials/create/analytics/default-schema.png)

사용자 지정 스키마를 사용하여 사용 가능한 스키마를 선택할 수 있습니다 [!DNL Analytics] 스키마에 가 있는 한 데이터 [!DNL Adobe Analytics ExperienceEvent Template] 필드 그룹. 사용자 지정 스키마를 사용하려면 **[!UICONTROL 사용자 지정 스키마]**.

![사용자 정의 스키마](../../../../images/tutorials/create/analytics/custom-schema.png)

다음 [!UICONTROL 매핑] 페이지는 소스 필드를 적절한 대상 스키마 필드에 매핑하는 인터페이스를 제공합니다. 여기에서 사용자 지정 변수를 새 스키마 필드 그룹에 매핑하고 데이터 준비에 지원되는 대로 계산을 적용할 수 있습니다. 대상 스키마를 선택하여 매핑 프로세스를 시작합니다.

>[!TIP]
>
>가 있는 스키마만 [!DNL Adobe Analytics ExperienceEvent Template] 필드 그룹이 스키마 선택 메뉴에 표시됩니다. 다른 스키마는 생략됩니다. 보고서 세트 데이터에 사용할 수 있는 적절한 스키마가 없으면 새 스키마를 만들어야 합니다. 스키마를 만드는 방법에 대한 자세한 내용은 안내서를 참조하십시오 [UI에서 스키마 만들기 및 편집](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

다음 [!UICONTROL 표준 필드 매핑] 섹션에 패널이 표시됩니다. [!UICONTROL 표준 매핑이 적용됨], [!UICONTROL 일치하지 않는 표준 매핑] 및 [!UICONTROL 사용자 지정 매핑]. 각 카테고리에 대한 특정 정보는 다음 표를 참조하십시오.

| 표준 필드 매핑 | 설명 |
| --- | --- |
| [!UICONTROL 표준 매핑이 적용됨] | 다음 [!UICONTROL 표준 매핑이 적용됨] 패널에 매핑된 속성의 총 수가 표시됩니다. 표준 매핑은 소스의 모든 속성 간 매핑 세트를 참조합니다 [!DNL Analytics] 의 데이터 및 해당 속성 [!DNL Analytics] 필드 그룹. 미리 매핑되어 있으므로 편집할 수 없습니다. |
| [!UICONTROL 일치하지 않는 표준 매핑] | 다음 [!UICONTROL 일치하지 않는 표준 매핑] 패널은 친숙한 이름 충돌이 포함된 매핑된 속성의 수를 나타냅니다. 이러한 충돌은 다른 보고서 세트의 필드 설명자 세트가 이미 채워져 있는 스키마를 다시 사용할 때 나타납니다. 다음 작업을 수행할 수 있습니다. [!DNL Analytics] 친숙한 이름이 충돌하는 경우에도 데이터 흐름. |
| [!UICONTROL 사용자 지정 매핑] | 다음 [!UICONTROL 사용자 지정 매핑] 패널에는 eVar, prop 및 목록을 포함하여 매핑된 사용자 지정 속성 수가 표시됩니다. 사용자 지정 매핑은 소스의 사용자 지정 속성 간 매핑 세트를 의미합니다 [!DNL Analytics] 선택한 스키마에 포함된 사용자 지정 필드 그룹의 데이터 및 속성입니다. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

를 미리 보려면 [!DNL Analytics] ExperienceEvent 템플릿 스키마 필드 그룹에서 다음을 선택합니다 **[!UICONTROL 보기]** 에서 [!UICONTROL 표준 매핑이 적용됨] 패널.

![view](../../../../images/tutorials/create/analytics/view.png)

다음 [!UICONTROL Adobe Analytics ExperienceEvent 템플릿 스키마 필드 그룹] 페이지는 스키마 구조를 검사하는 데 사용할 인터페이스를 제공합니다. 완료되면 을 선택합니다 **[!UICONTROL 닫기]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform은 친숙한 이름 충돌에 대한 매핑 세트를 자동으로 감지합니다. 매핑 세트와 충돌하지 않는 경우 **[!UICONTROL 다음]** 계속 진행합니다.

![매핑](../../../../images/tutorials/create/analytics/mapping.png)

소스 보고서 세트와 선택한 스키마 간에 친숙한 이름 충돌이 있는 경우 계속 진행할 수 있습니다 [!DNL Analytics] 데이터 흐름. 필드 설명자는 변경되지 않습니다. 또는 빈 설명자 세트가 있는 새 스키마를 만들도록 선택할 수 있습니다.

선택 **[!UICONTROL 다음]** 계속 진행합니다.

![주의](../../../../images/tutorials/create/analytics/caution.png)

#### 사용자 지정 매핑

데이터 준비 함수를 사용하고 사용자 지정 속성에 대해 새 매핑 또는 계산된 필드를 추가하려면 을 선택합니다 **[!UICONTROL 사용자 지정 매핑 보기]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

다음 을 선택합니다. **[!UICONTROL 새 매핑 추가]**.

필요에 따라 다음 중 하나를 선택할 수 있습니다 **[!UICONTROL 새 매핑 추가]** 또는 **[!UICONTROL 계산된 필드 추가]** 표시됩니다.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

빈 매핑 세트가 나타납니다. 매핑 아이콘을 선택하여 소스 필드를 추가합니다.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

인터페이스를 사용하여 소스 스키마 구조를 탐색하고 사용할 새 소스 필드를 식별할 수 있습니다. 매핑할 소스 필드를 선택하면 **[!UICONTROL 선택]**.

![선택 매핑](../../../../images/tutorials/create/analytics/select-mapping.png)

그런 다음 아래에서 매핑 아이콘을 선택합니다 [!UICONTROL Target 필드] 선택한 소스 필드를 해당 대상 필드에 매핑합니다.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

소스 스키마와 유사하게 인터페이스를 사용하여 대상 스키마 구조를 탐색하고 매핑할 대상 필드를 선택할 수 있습니다. 적절한 대상 필드를 선택하면 **[!UICONTROL 선택]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

사용자 지정 매핑 세트가 완료된 상태에서 **[!UICONTROL 다음]** 계속 진행합니다.

![전체 사용자 지정 매핑](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

다음 설명서는 데이터 준비, 계산된 필드 및 매핑 기능을 이해하는 데 대한 추가 리소스를 제공합니다.

* [데이터 준비 개요](../../../../../data-prep/home.md)
* [데이터 준비 매핑 함수](../../../../../data-prep/functions.md)
* [계산된 필드 추가](../../../../../data-prep/ui/mapping.md#calculated-fields)

### 필터링 대상 [!DNL Profile Service] (베타)

>[!IMPORTANT]
>
>필터링 지원 [!DNL Analytics] 데이터는 현재 베타 버전이며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

다음에 대한 매핑을 완료하면 [!DNL Analytics] 보고서 세트 데이터를 사용하면 필터링 규칙 및 조건을 적용하여 수집에서 로 데이터를 선택적으로 포함하거나 제외할 수 있습니다 [!DNL Profile Service]. 필터링 지원은 [!DNL Analytics] 데이터 및 데이터는 입력하기 전에만 필터링됩니다 [!DNL Profile.] 모든 데이터가 데이터 레이크에 수집됩니다.

#### 행 수준 필터링

에 대한 데이터를 필터링할 수 있습니다 [!DNL Profile] 행 수준 및 열 수준에서 수집. 행 수준 필터링을 사용하여 문자열 포함, 다음과 같음, 시작 또는 다음으로 끝과 같은 기준을 정의할 수 있습니다. 행 수준 필터링을 사용하여 `AND` 뿐만 아니라 `OR`를 사용하여 조건을 무효화하고 `NOT`.

을(를) 필터링하려면 [!DNL Analytics] 행 수준에서 **[!UICONTROL 행 필터]**.

![row-filter](../../../../images/tutorials/create/analytics/row-filter.png)

왼쪽 레일을 사용하여 스키마 계층 구조를 탐색하고 특정 스키마를 추가로 드릴다운하려면 원하는 스키마 속성을 선택합니다.

![왼쪽 레일](../../../../images/tutorials/create/analytics/left-rail.png)

구성할 속성을 식별했으면 왼쪽 레일에서 속성을 선택하고 필터링 패널로 드래그합니다.

![필터링 패널](../../../../images/tutorials/create/analytics/filtering-panel.png)

다른 조건을 구성하려면 을 선택합니다 **[!UICONTROL 다음과 같음]** 그런 다음 표시되는 드롭다운 창에서 조건을 선택합니다.

구성 가능한 조건 목록은 다음과 같습니다.

* [!UICONTROL 다음과 같음]
* [!UICONTROL 다음과 같지 않음]
* [!UICONTROL 다음으로 시작]
* [!UICONTROL 다음으로 끝남]
* [!UICONTROL 다음으로 끝나지 않음]
* [!UICONTROL 다음 포함]
* [!UICONTROL 다음을 포함하지 않음]
* [!UICONTROL 존재]
* [!UICONTROL 존재하지 않음]

![조건](../../../../images/tutorials/create/analytics/conditions.png)

그런 다음 선택한 속성에 따라 포함할 값을 입력합니다. 아래 예에서는 [!DNL Apple] 및 [!DNL Google] 의 일부로 수집하도록 선택됩니다 **[!UICONTROL 제조업체]** 속성을 사용합니다.

![include-manufacturer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

필터링 조건을 추가로 지정하려면 스키마에서 다른 속성을 추가한 다음 해당 속성을 기반으로 값을 추가합니다. 아래 예에서는 **[!UICONTROL 모델]** 속성이 추가되고 와 같은 모델이 추가됩니다 [!DNL iPhone 13] 및 [!DNL Google Pixel 6] 수집하기 위해 필터링됩니다.

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

새 컨테이너를 추가하려면 줄임표(`...`)을 클릭하여 필터링 인터페이스의 오른쪽 상단에서 을 선택한 다음 을 선택합니다 **[!UICONTROL 컨테이너 추가]**.

![추가 컨테이너](../../../../images/tutorials/create/analytics/add-container.png)

새 컨테이너를 추가하고 나면 **[!UICONTROL 포함]** 그런 다음 **[!UICONTROL 제외]** 표시되는 드롭다운 창에서 클릭합니다.

![제외](../../../../images/tutorials/create/analytics/exclude.png)

다음으로, 스키마 속성을 드래그하고 필터링에서 제외할 해당 값을 추가하여 동일한 프로세스를 완료합니다. 아래 예에서는 [!DNL iPhone 12], [!DNL iPhone 12 mini], 및 [!DNL Google Pixel 5] 모두 제외에서 필터링됩니다. **[!UICONTROL 모델]** 속성, 가로 는 **[!UICONTROL 화면 방향]**, 및 모델 번호 [!DNL A1633] 에서 제외됨 **[!UICONTROL 모델 번호]**.

완료되면 을 선택합니다 **[!UICONTROL 다음]**.

![제외 예](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### 열 수준 필터링

선택 **[!UICONTROL 열 필터]** 머리글에서 열 수준 필터링을 적용할 수 있습니다.

![column-filter](../../../../images/tutorials/create/analytics/column-filter.png)

페이지가 대화식 스키마 트리로 업데이트되어 열 수준에서 스키마 속성을 표시합니다. 여기에서 제외할 데이터 열을 선택할 수 있습니다 [!DNL Profile] 수집. 또는 열을 확장하고 제외에 대한 특정 속성을 선택할 수 있습니다.

기본적으로 모두 [!DNL Analytics] 이동 [!DNL Profile] 및 이 프로세스를 통해 XDM 데이터 분기를 [!DNL Profile] 수집.

완료되면 을 선택합니다 **[!UICONTROL 다음]**.

![열 선택](../../../../images/tutorials/create/analytics/columns-selected.png)

### 데이터 흐름 세부 정보 제공

다음 **[!UICONTROL 데이터 흐름 세부 정보]** 데이터 흐름의 이름과 선택적 설명을 제공해야 하는 단계가 나타납니다. 선택 **[!UICONTROL 다음]** 완료됨.

![데이터 흐름 세부 정보](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 검토

다음 [!UICONTROL 검토] 새 Analytics 데이터 흐름을 만들기 전에 검토할 수 있는 단계가 나타납니다. 연결 세부 사항은 다음을 포함하여 카테고리별로 그룹화됩니다.

* [!UICONTROL 연결]: 연결의 소스 플랫폼을 표시합니다.
* [!UICONTROL 데이터 유형]: 선택한 보고서 세트와 해당 보고서 세트 ID를 표시합니다.

![검토](../../../../images/tutorials/create/analytics/review.png)

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 이를 통해 수집되는 데이터를 모니터링할 수 있습니다. 에서 [!UICONTROL 카탈로그] 화면, 선택 **[!UICONTROL 데이터 흐름]** analytics 계정과 연결된 설정된 흐름 목록을 보려면 .

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

다음 **데이터 흐름** 화면이 나타납니다. 이 페이지에는 이름, 소스 데이터, 생성 시간 및 상태에 대한 정보를 포함하는 데이터 세트 흐름 쌍이 있습니다.

커넥터는 두 개의 데이터 세트 흐름을 인스턴스화합니다. 한 흐름은 채우기 데이터를, 다른 흐름은 라이브 데이터에 대한 것입니다. 채우기 데이터는 프로필에 대해 구성되지 않지만 분석 및 데이터 과학 사용 사례를 위해 데이터 레이크로 전송됩니다.

채우기, 라이브 데이터 및 각 지연에 대한 자세한 내용은 [Analytics 데이터 커넥터 개요](../../../../connectors/adobe-applications/analytics.md).

목록에서 보려는 데이터 세트 흐름을 선택합니다.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

다음 **[!UICONTROL 데이터 집합 활동]** 페이지가 나타납니다. 이 페이지에는 그래프 형태로 사용되는 메시지 수가 표시됩니다. 선택 **[!UICONTROL 데이터 거버넌스]** 상단 헤더에서 레이블 지정 필드에 액세스합니다.

![데이터 세트 활동](../../../../images/tutorials/create/analytics/dataset-activity.png)

데이터 집합 흐름의 상속된 레이블을 [!UICONTROL 데이터 거버넌스] 화면. Analytics에서 가져온 데이터에 레이블을 지정하는 방법에 대한 자세한 내용은 [데이터 사용 레이블 안내서](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

데이터 흐름을 삭제하려면 [!UICONTROL 데이터 흐름] 페이지를 클릭한 다음 생략 부호(`...`)을 데이터 흐름 이름 옆에 둔 다음 을 선택합니다 [!UICONTROL 삭제].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## 다음 단계 및 추가 리소스

연결이 만들어지면 데이터 흐름이 자동으로 만들어져서 들어오는 데이터를 포함하고 데이터 세트를 선택한 스키마로 채웁니다. 또한 데이터 다시 채우기가 발생하고 최대 13개월 동안의 이전 데이터가 수집됩니다. 초기 수집이 완료되면 [!DNL Analytics] 다음과 같은 다운스트림 플랫폼 서비스에서 사용 및 데이터 사용 [!DNL Real-time Customer Profile] 세분화 서비스를 제공할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 개요](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 개요](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 개요](../../../../../query-service/home.md)

다음 비디오는 Adobe Analytics 소스 커넥터를 사용하여 데이터를 수집하는 방법에 대한 이해를 지원하기 위한 것입니다.

>[!WARNING]
>
> 다음 [!DNL Platform] 다음 비디오에 표시된 UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
