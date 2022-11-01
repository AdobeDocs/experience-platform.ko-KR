---
keywords: Experience Platform;홈;인기 항목;csv 매핑;csv 파일 매핑;csv 파일을 xdm에 매핑;xdm에 csv 매핑;ui 안내서;
solution: Experience Platform
title: 기존 XDM 스키마에 CSV 파일 매핑
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 CSV 파일을 기존 XDM 스키마에 매핑하는 방법을 설명합니다.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: 160a75a1811afa002717e167887550715eee5471
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# 기존 XDM 스키마에 CSV 파일 매핑

>[!NOTE]
>
>이 문서에서는 기존 XDM 스키마에 CSV 파일을 매핑하는 방법을 설명합니다. AI에서 생성한 스키마 권장 사항 도구(현재 베타 버전)를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오 [기계 학습 권장 사항을 사용하여 CSV 파일 매핑](./recommendations.md).

CSV 데이터를 로 수집하려면 [!DNL Adobe Experience Platform]를 지정하는 경우 데이터를 [!DNL Experience Data Model] (XDM) 스키마. 이 자습서에서는 를 사용하여 CSV 파일을 XDM 스키마에 매핑하는 방법을 설명합니다 [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 다음 구성 요소를 이해하고 있어야 합니다 [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.
- [일괄 수집](../../batch-ingestion/overview.md): 메서드를 사용하는 방법 [!DNL Platform] 사용자가 제공한 데이터 파일에서 데이터를 가져옵니다.
- [Adobe Experience Platform 데이터 준비](../../batch-ingestion/overview.md): 수집된 데이터를 XDM 스키마에 맞게 매핑하고 변형할 수 있는 기능 세트입니다. 에 대한 문서 [데이터 준비 함수](../../../data-prep/functions.md) 는 특히 스키마 매핑에 관련되어 있습니다.

또한 이 자습서에서는 CSV 데이터를 로 수집할 데이터 세트를 이미 만들어야 합니다. UI에서 데이터 세트를 만드는 단계는 다음을 참조하십시오. [데이터 수집 튜토리얼](../ingest-batch-data.md).

## 대상 선택

에 로그인합니다. [[!DNL Adobe Experience Platform]](https://platform.adobe.com) 그런 다음 **[!UICONTROL 워크플로우]** 왼쪽 탐색 모음에서 를 클릭하여 **[!UICONTROL 워크플로우]** 작업 공간.

에서 **[!UICONTROL 워크플로우]** 화면, 선택 **[!UICONTROL XDM 스키마에 CSV 매핑]** 아래에 **[!UICONTROL 데이터 수집]** 섹션을 선택한 다음 **[!UICONTROL Launch]**.

![](../../images/tutorials/map-a-csv-file/workflows.png)

다음 **[!UICONTROL XDM 스키마에 CSV 매핑]** 워크플로우가 나타나고, **[!UICONTROL 대상]** 단계. 수집할 인바운드 데이터에 대한 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

**기존 데이터 세트 사용**

CSV 데이터를 기존 데이터 세트에 수집하려면 을 선택합니다 **[!UICONTROL 기존 데이터 세트 사용]**. 검색 함수를 사용하거나 패널에서 기존 데이터 세트 목록을 스크롤하여 기존 데이터 세트를 검색할 수 있습니다.

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

CSV 데이터를 새 데이터 세트에 수집하려면 을 선택합니다 **[!UICONTROL 새 데이터 세트 만들기]** 제공된 필드에 데이터 집합의 이름과 설명을 입력합니다. 검색 함수를 사용하거나 제공된 스키마 목록을 스크롤하여 스키마를 선택합니다. 선택 **[!UICONTROL 다음]** 계속 진행합니다.

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 데이터 추가

다음 **[!UICONTROL 데이터 추가]** 단계가 나타납니다. CSV 파일을 제공된 공간으로 끌어다 놓거나 선택합니다 **[!UICONTROL 파일 선택]** 수동으로 CSV 파일을 입력합니다.

![](../../images/tutorials/map-a-csv-file/add-data.png)

다음 **[!UICONTROL 샘플 데이터]** 섹션이 파일이 업로드되면 나타나고 처음 10개의 데이터 행이 표시됩니다. 데이터가 예상대로 업로드되었음을 확인했으면 을 선택합니다 **[!UICONTROL 다음]**.

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## XDM 스키마 필드에 CSV 필드 매핑

다음 **[!UICONTROL 매핑]** 단계가 나타납니다. CSV 파일의 열은 아래에 나열됩니다 **[!UICONTROL 소스 필드]**&#x200B;아래에 해당 XDM 스키마 필드가 나열된 상태로 **[!UICONTROL Target 필드]**.

[!DNL Platform] 은(는) 선택한 대상 스키마나 데이터 세트를 기반으로 자동 매핑 필드에 대한 지능형 권장 사항을 자동으로 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

모든 자동 생성 매핑 값을 허용하려면 &quot; 확인란을 선택합니다.[!UICONTROL 모든 대상 필드 허용]&quot;.

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

경우에 따라 소스 스키마에 대해 두 개 이상의 권장 사항을 사용할 수 있습니다. 이렇게 되면 매핑 카드에 가장 두드러진 권장 사항이 표시되고 그 뒤에는 사용 가능한 추가 권장 사항의 수가 포함된 파란색 원이 표시됩니다. 전구 아이콘을 선택하면 추가 권장 사항 목록이 표시됩니다. 대신 매핑할 권장 사항 옆에 있는 확인란을 선택하여 대체 권장 사항 중 하나를 선택할 수 있습니다.

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

또는 소스 스키마를 대상 스키마에 수동으로 매핑하도록 선택할 수 있습니다. 매핑할 소스 스키마를 마우스로 가리킨 다음 더하기 아이콘을 선택합니다.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

다음 **[!UICONTROL 대상 필드에 소스 매핑]** 팝오버가 나타납니다. 여기에서 매핑할 필드를 선택한 후 **[!UICONTROL 저장]** 새 매핑을 추가하려면

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

매핑 중 하나를 제거하려면 해당 매핑을 마우스로 가리킨 다음 빼기 아이콘을 선택합니다.

### 계산된 필드 추가 {#add-calculated-field}

계산된 필드를 사용하면 입력 스키마의 속성을 기반으로 값을 만들 수 있습니다. 그런 다음 이러한 값을 대상 스키마의 속성에 지정하고 쉽게 참조할 수 있도록 이름 및 설명을 제공할 수 있습니다.

을(를) 선택합니다 **[!UICONTROL 계산된 필드 추가]** 단추를 눌러 진행합니다.

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

다음 **[!UICONTROL 계산된 필드 만들기]** 패널이 나타납니다. 왼쪽 대화 상자에는 계산된 필드에서 지원되는 필드, 함수 및 연산자가 포함되어 있습니다. 탭 중 하나를 선택하여 표현식 편집기에 함수, 필드 또는 연산자를 추가합니다.

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 탭 | 설명 |
| --------- | ----------- |
| 필드 | 필드 탭에는 소스 스키마에서 사용할 수 있는 필드와 속성이 나열됩니다. |
| 함수 | 함수 탭에는 데이터를 변형하는 데 사용할 수 있는 함수가 나열됩니다. 계산된 필드 내에서 사용할 수 있는 기능에 대한 자세한 내용은 다음 안내서를 참조하십시오 [데이터 준비(매퍼) 함수 사용](../../../data-prep/functions.md). |
| 연산자 | 연산자 탭에는 데이터를 변형하는 데 사용할 수 있는 연산자가 나열됩니다. |

가운데 표현식 편집기를 사용하여 필드, 함수 및 연산자를 수동으로 추가할 수 있습니다. 편집기를 선택하여 표현식 만들기를 시작합니다.

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

선택 **[!UICONTROL 저장]** 계속 진행합니다.

새로 만든 소스 필드와 함께 매핑 화면이 다시 나타납니다. 해당 대상 필드를 적용하고 을 선택합니다 **[!UICONTROL 완료]** 매핑을 완료하려면

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## 데이터 수집 모니터링

CSV 파일이 매핑되고 생성되면 CSV 파일을 통해 수집되는 데이터를 모니터링할 수 있습니다. 데이터 수집 모니터링에 대한 자세한 내용은 [데이터 수집 모니터링](../../../ingestion/quality/monitor-data-ingestion.md).

## 다음 단계

이 자습서를 따라 플랫 CSV 파일을 XDM 스키마에 매핑하고 XDM에 수집했습니다 [!DNL Platform]. 이제 이 데이터를 다운스트림에서 사용할 수 있습니다 [!DNL Platform] 와 같은 서비스 [!DNL Real-time Customer Profile]. 다음 기간 동안 개요를 참조하십시오. [[!DNL Real-time Customer Profile]](../../../profile/home.md) 추가 정보.
