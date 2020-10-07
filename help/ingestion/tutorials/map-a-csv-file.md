---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: XDM 스키마에 CSV 파일 매핑
topic: tutorial
type: Tutorial
description: 이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 XDM 스키마에 CSV 파일을 매핑하는 방법을 설명합니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 1%

---


# XDM 스키마에 CSV 파일 매핑

CSV 데이터를 인제스트하려면 데이터 [!DNL Adobe Experience Platform]를 [!DNL Experience Data Model] (XDM) 스키마에 매핑해야 합니다. 이 자습서에서는 [!DNL Platform] 사용자 인터페이스를 사용하여 XDM 스키마에 CSV 파일을 매핑하는 방법을 설명합니다.

또한 이 자습서의 부록에서는 [매핑 함수 사용에 대한 자세한 정보를 제공합니다](#mapping-functions).

## 시작하기

이 자습서에서는 다음의 구성 요소에 대해 작업해야 [!DNL Platform]합니다.

- [[!DNL 경험 데이터 모델(XDM 시스템)]](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크
- [[!DNL 일괄 처리]](../batch-ingestion/overview.md):사용자가 제공한 데이터 파일에서 데이터를 [!DNL Platform] 인제스트하는 방법입니다.

또한 이 자습서에서는 CSV 데이터를 인제스트하기 위한 데이터 세트를 이미 만들어야 합니다. UI에서 데이터 세트를 만드는 단계는 [데이터 인제스트 자습서를 참조하십시오](./ingest-batch-data.md).

## 대상 선택

[!DNL Adobe Experience Platform]에 [로그인한 다음](https://platform.adobe.com) 왼쪽 탐색 막대에서 **[!UICONTROL 워크플로우]** 를 선택하여 **[!UICONTROL 워크플로우 작업 영역에]** 액세스합니다.

워크플로우 **[!UICONTROL 화면에서]** **[!UICONTROL 데이터 수집]** 섹션 **[!UICONTROL 에서 CSV를 XDM에]** 매핑합니다 **[!UICONTROL 를 선택한 다음 LaunchDm을]**&#x200B;선택합니다.

![](../images/tutorials/map-a-csv-file/workflows.png)

대상 **[!UICONTROL 단계부터 시작하여 XDM 스키마에]** CSV **[!UICONTROL 매핑 워크플로우가]** 나타납니다. 수집할 인바운드 데이터의 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

**기존 데이터 세트 사용**

CSV 데이터를 기존 데이터 세트에 인제스트하려면 기존 데이터 세트 **[!UICONTROL 사용을 선택합니다]**. 검색 기능을 사용하거나 패널의 기존 데이터 집합 목록을 스크롤하여 기존 데이터 집합을 검색할 수 있습니다.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

CSV 데이터를 새 데이터 세트에 인제스트하려면 **[!UICONTROL 새 데이터 세트]** 만들기를 선택하고 제공된 필드에 데이터 세트에 대한 이름과 설명을 입력합니다. 검색 기능을 사용하거나 제공된 스키마 목록을 스크롤하여 스키마를 선택합니다. 계속하려면 **[!UICONTROL 다음]** 을 선택합니다.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 데이터 추가

데이터 **[!UICONTROL 추가]** 단계가 나타납니다. CSV 파일을 제공된 공간으로 끌어다 놓거나 파일 선택 **[!UICONTROL 을 선택하여 CSV]** 파일을 수동으로 입력합니다.

![](../images/tutorials/map-a-csv-file/add-data.png)

파일이 업로드되면 **[!UICONTROL 샘플 데이터]** 섹션이 나타나 처음 10개의 데이터 행을 보여 줍니다. 데이터가 예상대로 업로드되었음을 확인했으면 다음을 **[!UICONTROL 선택합니다]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## XDM 스키마 필드에 CSV 필드 매핑

매핑 **[!UICONTROL 단계가]** 나타납니다. CSV 파일의 열은 **[!UICONTROL 소스 필드]**&#x200B;아래에 나열되며 해당 XDM 스키마 필드는 **[!UICONTROL Target 필드]**&#x200B;아래에 나열됩니다. 선택되지 않은 대상 필드는 빨간색으로 표시됩니다. 필터 필드 옵션을 사용하여 사용 가능한 소스 필드 목록의 범위를 좁힐 수 있습니다.

>[!TIP]
>
>[!DNL Platform] 선택한 대상 스키마나 데이터 세트에 따라 자동 매핑 필드에 대한 지능적인 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다.

CSV 열을 XDM 필드에 매핑하려면 열의 해당 대상 필드 옆에 있는 스키마 아이콘을 선택합니다.

![](../images/tutorials/map-a-csv-file/mapping.png)

스키마 **[!UICONTROL 선택 필드]** 창이 나타납니다. XDM 스키마의 구조를 탐색하고 CSV 열을 매핑할 필드를 찾을 수 있습니다. XDM 필드를 클릭하여 선택한 다음 **[!UICONTROL 선택을 클릭합니다]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

매핑되지 않은 나머지 소스 필드에 대한 단계를 완료하면 **[!UICONTROL 매핑]** 화면이 다시 나타나고 선택한 XDM 필드가 **[!UICONTROL Target 필드]**&#x200B;아래에 나타납니다.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

필드를 매핑할 때 입력 소스 필드를 기반으로 값을 계산하는 함수를 포함할 수도 있습니다. 자세한 내용은 부록에 있는 [매핑 기능](#mapping-functions) 섹션을 참조하십시오.

### 계산된 필드 추가

계산된 필드를 사용하면 입력 스키마의 특성을 기반으로 값을 만들 수 있습니다. 그런 다음 이러한 값을 대상 스키마의 속성에 할당할 수 있으며 쉽게 참조할 수 있도록 이름 및 설명을 제공할 수 있습니다.

계속하려면 계산된 필드 **[!UICONTROL 추가]** 단추를 선택합니다.

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

계산된 필드 **[!UICONTROL 만들기]** 패널이 나타납니다. 왼쪽 대화 상자에는 계산된 필드에서 지원되는 필드, 함수 및 연산자가 있습니다. 표현식 편집기에 함수, 필드 또는 연산자를 추가할 탭 중 하나를 선택합니다.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 탭 | 설명 |
| --------- | ----------- |
| 필드 | 필드 탭에는 소스 스키마에서 사용할 수 있는 필드 및 속성이 나열됩니다. |
| 함수 | 함수 탭에는 데이터를 변형하는 데 사용할 수 있는 기능이 나열됩니다. |
| 연산자 | 연산자 탭에는 데이터를 변형하는 데 사용할 수 있는 연산자가 나열됩니다. |

가운데 표현식 편집기를 사용하여 필드, 함수 및 연산자를 수동으로 추가할 수 있습니다. 표현식 생성을 시작하려면 편집기를 선택합니다.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

계속하려면 **[!UICONTROL 저장을]** 선택합니다.

새로 만든 소스 필드와 함께 매핑 화면이 다시 나타납니다. 적절한 대상 필드를 적용하고 **[!UICONTROL 마침을]** 선택하여 매핑을 완료합니다.

![](../images/tutorials/map-a-csv-file/new-field.png)

## 데이터 흐름 모니터링

CSV 파일을 매핑하고 만들면 CSV 파일을 통해 수집되는 데이터를 모니터링할 수 있습니다. 데이터 흐름 모니터링에 대한 자세한 내용은 스트리밍 데이터 흐름 [모니터링에 대한 자습서를 참조하십시오](../../ingestion/quality/monitor-data-flows.md).

## 매핑 함수 사용

함수를 사용하려면 적절한 구문 및 입력 **[!UICONTROL 과 함께 소스 필드]** 아래에 입력합니다.

예를 들어 구/군/시 CSV 필드를 연결하고 구/군/시 XDM 필드에 지정하려면 소스 필드를 로 설정합니다 `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

열을 XDM 필드에 매핑하는 방법에 대한 자세한 내용은 Data Prep (Mapper) 함수 [사용 설명서를 참조하십시오](../../data-prep/functions.md).

## 다음 단계

이 자습서를 따라 플랫 CSV 파일을 XDM 스키마에 매핑하고 인제스트했습니다 [!DNL Platform]. 이제 이 데이터를 같은 다운스트림 [!DNL Platform] 서비스에서 사용할 수 있습니다 [!DNL Real-time Customer Profile]. 자세한 내용은 [[!DNL 실시간 고객 프로필]](../../profile/home.md) 개요를 참조하십시오.
