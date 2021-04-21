---
keywords: Experience Platform;홈;인기 항목;맵 csv;map csv 파일;csv 파일을 xdm에 매핑;csv를 xdm;ui 안내서;;home;popular topics;map csv file;map csv to xdm;ui guide
solution: Experience Platform
title: XDM 스키마에 CSV 파일 매핑
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 CSV 파일을 XDM 스키마에 매핑하는 방법을 설명합니다.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 1%

---

# XDM 스키마에 CSV 파일 매핑

CSV 데이터를 [!DNL Adobe Experience Platform]으로 인제스트하려면 데이터를 [!DNL Experience Data Model](XDM) 스키마에 매핑해야 합니다. 이 자습서에서는 [!DNL Platform] 사용자 인터페이스를 사용하여 CSV 파일을 XDM 스키마에 매핑하는 방법을 설명합니다.

또한 이 자습서의 부록은 [매핑 함수](#mapping-functions)의 사용에 대한 자세한 정보를 제공합니다.

## 시작하기

이 자습서에서는 [!DNL Platform]의 다음 구성 요소에 대해 제대로 이해해야 합니다.

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md):고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md):사용자가  [!DNL Platform] 제공한 데이터 파일의 데이터를 인제스트하는 방법입니다.

또한 이 자습서에서는 CSV 데이터를 인제스트할 데이터 세트를 이미 만들어야 합니다. UI에서 데이터 세트를 만드는 단계는 [데이터 인제스트 자습서](./ingest-batch-data.md)를 참조하십시오.

## 대상 선택

[[!DNL Adobe Experience Platform]](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL Workflows]**&#x200B;를 선택하여 **[!UICONTROL Workflows]** 작업 영역에 액세스합니다.

**[!UICONTROL Workflows]** 화면에서 **[!UICONTROL Data ingestion]** 섹션 아래의 **[!UICONTROL Map CSV to XDM schema]**&#x200B;을 선택한 다음 **[!UICONTROL Launch]**&#x200B;을 선택합니다.

![](../images/tutorials/map-a-csv-file/workflows.png)

**[!UICONTROL Destination]** 단계부터 **[!UICONTROL Map CSV to XDM schema]** 워크플로우가 나타납니다. 수집할 인바운드 데이터의 데이터 세트를 선택합니다. 기존 데이터 집합을 사용하거나 새 데이터 집합을 만들 수 있습니다.

**기존 데이터 세트 사용**

CSV 데이터를 기존 데이터 세트에 인제스트하려면 **[!UICONTROL Use existing dataset]**&#x200B;을 선택합니다. 검색 기능을 사용하여 기존 데이터 집합을 검색하거나 패널의 기존 데이터 집합 목록을 스크롤하여 검색할 수 있습니다.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

CSV 데이터를 새 데이터 세트에 인제스트하려면 **[!UICONTROL Create new dataset]**&#x200B;을 선택하고 제공된 필드에 데이터 세트에 대한 이름과 설명을 입력합니다. 검색 함수를 사용하거나 제공된 스키마 목록을 스크롤하여 스키마를 선택합니다. 계속하려면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 데이터 추가

**[!UICONTROL Add data]** 단계가 나타납니다. CSV 파일을 제공된 공간으로 드래그하여 놓거나 **[!UICONTROL Choose files]**&#x200B;을 선택하여 CSV 파일을 수동으로 입력합니다.

![](../images/tutorials/map-a-csv-file/add-data.png)

파일이 업로드되면 **[!UICONTROL Sample data]** 섹션이 나타나 처음 10개의 데이터 행을 표시합니다. 데이터가 예상대로 업로드되었음을 확인했으면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## XDM 스키마 필드에 CSV 필드 매핑

**[!UICONTROL Mapping]** 단계가 나타납니다. CSV 파일의 열은 **[!UICONTROL Source Field]** 아래에 나열되고 해당 XDM 스키마 필드가 **[!UICONTROL Target Field]** 아래에 나열됩니다.

[!DNL Platform] 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑 필드에 대한 지능적인 권장 사항을 자동으로 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

자동 생성 매핑 값을 모두 사용하려면 &quot;[!UICONTROL Accept all target fields]&quot; 확인란을 선택합니다.

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

경우에 따라 소스 스키마에 대해 두 개 이상의 권장 사항을 사용할 수 있습니다. 이렇게 되면 매핑 카드에 가장 중요한 권장 사항이 표시되고 이용 가능한 추가 권장 사항의 수가 포함된 파란색 원이 표시됩니다. 전구 아이콘을 선택하면 추가 권장 사항 목록이 표시됩니다. 대신 매핑할 권장 사항 옆의 확인란을 선택하여 대체 권장 사항 중 하나를 선택할 수 있습니다.

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

또는 소스 스키마를 대상 스키마에 수동으로 매핑하도록 선택할 수 있습니다. 매핑할 소스 스키마 위로 마우스를 가져간 다음 더하기 아이콘을 선택합니다.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

**[!UICONTROL Map source to target field]** 팝업 창이 나타납니다. 여기서 매핑할 필드를 선택하고 **[!UICONTROL Save]** 뒤에 새 매핑을 추가할 수 있습니다.

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

매핑 중 하나를 제거하려면 해당 매핑 위로 마우스를 가져간 다음 빼기 아이콘을 선택합니다.

### 계산된 필드 추가

계산된 필드를 사용하면 입력 스키마의 특성에 따라 값을 만들 수 있습니다. 그런 다음 이러한 값을 대상 스키마의 속성에 할당할 수 있으며 쉽게 참조할 수 있도록 이름과 설명을 제공합니다.

계속하려면 **[!UICONTROL Add calculated field]** 단추를 선택합니다.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

**[!UICONTROL Create calculated field]** 패널이 나타납니다. 왼쪽 대화 상자에는 계산된 필드에서 지원되는 필드, 함수 및 연산자가 포함되어 있습니다. 표현식 편집기에 함수, 필드 또는 연산자를 추가하기 시작할 탭 중 하나를 선택합니다.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 탭 | 설명 |
| --------- | ----------- |
| 필드 | 필드 탭에는 소스 스키마에서 사용할 수 있는 필드 및 속성이 나열됩니다. |
| 함수 | 함수 탭에는 데이터를 변형하는 데 사용할 수 있는 함수가 나열됩니다. 계산된 필드 내에서 사용할 수 있는 기능에 대한 자세한 내용은 [데이터 준비(매퍼) 함수](../../data-prep/functions.md)에 대한 안내서를 참조하십시오. |
| 연산자 | 연산자 탭에는 데이터를 변형하는 데 사용할 수 있는 연산자가 나열됩니다. |

중앙에 있는 표현식 편집기를 사용하여 필드, 함수 및 연산자를 수동으로 추가할 수 있습니다. 표현식 만들기를 시작할 편집기를 선택합니다.

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

계속하려면 **[!UICONTROL Save]**&#x200B;을 선택합니다.

새로 만든 소스 필드와 함께 매핑 화면이 다시 나타납니다. 적절한 대상 필드를 적용하고 **[!UICONTROL Finish]**&#x200B;을 선택하여 매핑을 완료합니다.

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## 데이터 수집 모니터링

CSV 파일을 매핑하고 만들면 CSV 파일을 통해 인제스트되는 데이터를 모니터링할 수 있습니다. 데이터 수집 모니터링에 대한 자세한 내용은 [데이터 통합 모니터링](../../ingestion/quality/monitor-data-ingestion.md)에서 자습서를 참조하십시오.

## 다음 단계

이 자습서를 따라 플랫 CSV 파일을 XDM 스키마에 매핑하고 이를 [!DNL Platform]에 인제스트했습니다. 이제 이 데이터를 [!DNL Real-time Customer Profile] 등의 다운스트림 [!DNL Platform] 서비스에서 사용할 수 있습니다. 자세한 내용은 [[!DNL Real-time Customer Profile]](../../profile/home.md)의 개요를 참조하십시오.
