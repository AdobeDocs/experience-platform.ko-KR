---
keywords: Experience Platform;홈;인기 항목;섭취;인제스트 일괄 데이터;자습서;일괄 처리 통합;자습서;ui 안내서;
solution: Experience Platform
title: Experience Platform에 데이터 인제스트
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform을 사용하면 알려진 XDM(Experience Data Model) 스키마를 준수하는 데이터 또는 쪽모이 세공 마루 파일 형식의 일괄 파일로 데이터를 손쉽게 가져올 수 있습니다.
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# Adobe Experience Platform에 데이터 인제스트

Adobe Experience Platform을 사용하면 데이터를 일괄 처리 파일로 [!DNL Platform]에 쉽게 가져올 수 있습니다. 인제스트할 데이터의 예로는 CRM 시스템의 플랫 파일(예: 쪽모이 세공 항목 파일)의 프로필 데이터 또는 스키마 레지스트리에서 알려진 [!DNL Experience Data Model](XDM) 스키마를 따르는 데이터가 포함될 수 있습니다.

## 시작하기

이 자습서를 완료하려면 [!DNL Experience Platform]에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]에서 IMS 조직에 액세스할 수 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

데이터 통합 API를 사용하여 데이터를 인제스트하려면 [일괄 처리 통합 개발자 가이드](../batch-ingestion/api-overview.md)를 읽으십시오.

## 데이터 세트 작업 영역

[!DNL Experience Platform] 내의 데이터 집합 작업 영역을 사용하면 IMS 조직에서 만든 모든 데이터 집합을 보고 관리할 수 있고 새 데이터 집합을 만들 수 있습니다.

왼쪽 탐색에서 **[!UICONTROL Datasets]**&#x200B;을 클릭하여 데이터 집합 작업 영역을 봅니다. 데이터 집합 작업 영역에는 데이터 집합이 마지막으로 업데이트된 날짜 및 시간은 물론, 이름, 만든 날짜(날짜 및 시간), 소스, 스키마 및 마지막 일괄 처리 상태를 표시하는 열을 포함한 데이터 집합 목록이 들어 있습니다.

>[!NOTE]
>
>검색 막대 옆에 있는 필터 아이콘을 클릭하여 필터링 기능을 사용하여 [!DNL Profile]에 대해 활성화된 데이터 집합만 표시합니다.

![모든 데이터 집합 보기](../images/tutorials/ingest-batch-data/datasets-overview.png)

## 데이터 세트 만들기

데이터 세트를 만들려면 데이터 집합 작업 영역의 오른쪽 위 모서리에 있는 **[!UICONTROL Create Dataset]**&#x200B;을 클릭합니다.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

**[!UICONTROL Create Dataset]** 화면에서 &quot;[!UICONTROL Create Dataset from Schema]&quot; 또는 &quot;[!UICONTROL Create Dataset from CSV File]&quot; 중 어떤 것을 원하는지 선택합니다.

이 자습서의 경우 스키마를 사용하여 데이터 세트를 만듭니다. 계속하려면 **[!UICONTROL Create Dataset from Schema]**&#x200B;을 클릭합니다.

![데이터 소스 선택](../images/tutorials/ingest-batch-data/create-dataset.png)

## 데이터 집합 스키마 선택

**[!UICONTROL Select Schema]** 화면에서 사용할 스키마 옆의 라디오 단추를 클릭하여 스키마를 선택합니다. 이 자습서의 경우 충성도 멤버 스키마를 사용하여 데이터 세트에 대해 수행됩니다. 검색 막대를 사용하여 스키마를 필터링하면 원하는 정확한 스키마를 찾을 수 있습니다.

사용할 스키마 옆에 있는 라디오 단추를 선택한 후 **[!UICONTROL Next]**&#x200B;을 클릭합니다.

![스키마 선택](../images/tutorials/ingest-batch-data/select-schema.png)

## 데이터 세트 구성

**[!UICONTROL Configure Dataset]** 화면에서 데이터 세트에 이름을 지정해야 하며 데이터 세트에 대한 설명도 제공할 수 있습니다.

**데이터 세트 이름에 대한 참고 사항:**

- 나중에 데이터세트를 라이브러리에서 쉽게 찾을 수 있도록 데이터 세트 이름은 짧고 설명이어야 합니다.
- 데이터 세트 이름은 고유해야 합니다. 즉, 나중에 다시 사용할 수 없도록 데이터 세트 이름이 구체적이어야 합니다.
- 나중에 다른 사용자가 데이터 세트를 차별화하는 데 도움이 될 수 있으므로 설명 필드를 사용하여 데이터 세트에 대한 추가 정보를 제공하는 것이 좋습니다.

데이터 세트에 이름과 설명이 있으면 **[!UICONTROL Finish]**&#x200B;을 클릭합니다.

![데이터 세트 구성](../images/tutorials/ingest-batch-data/configure-dataset.png)

## 데이터 집합 활동

이제 빈 데이터 세트가 만들어졌고 데이터 집합 작업 영역의 **[!UICONTROL Dataset Activity]** 탭으로 돌아갑니다. &quot;배치가 추가되지 않았습니다.&quot;라는 알림과 함께 작업 공간의 왼쪽 위 모서리에 데이터 세트 이름이 표시됩니다. 이 데이터 세트에 아직 배치를 추가하지 않았기 때문에 이 작업이 필요합니다.

데이터 집합 작업 영역의 오른쪽에는 데이터 집합 ID, 이름, 설명, 테이블 이름, 스키마, 스트리밍 및 소스 등의 새 데이터 집합과 관련된 정보가 들어 있는 **[!UICONTROL Info]** 탭이 표시됩니다. 또한 정보 탭에는 데이터 세트를 만든 날짜와 마지막으로 수정한 날짜에 대한 정보도 포함되어 있습니다.

또한 정보 탭에서는 [!DNL Real-time Customer Profile]에서 데이터 세트를 사용할 수 있도록 설정하는 데 사용되는 **[!UICONTROL Profile]** 토글도 있습니다. 이 전환 및 [!DNL Real-time Customer Profile]의 사용은 다음에 나오는 섹션에 자세히 설명되어 있습니다.

![데이터 집합 활동](../images/tutorials/ingest-batch-data/sample-dataset.png)

## [!DNL Real-time Customer Profile]에 대한 데이터 집합 사용

데이터 세트는 데이터를 [!DNL Experience Platform]에 인제스트하는 데 사용되며, 이 데이터는 궁극적으로 개인을 식별하고 여러 소스에서 나오는 정보를 통합하는 데 사용됩니다. 이러한 정보를 모두 결합하는 것을 [!DNL Real-Time Customer Profile]이라고 합니다. [!DNL Platform]이(가) [!DNL Real-Time Profile]에 포함되어야 하는 정보를 알 수 있도록 데이터 집합을 **[!UICONTROL Profile]** 전환을 사용하여 포함할 것으로 표시할 수 있습니다.

기본적으로 이 토글은 꺼져 있습니다. [!DNL Profile]을 토글하도록 선택하면 데이터 세트에 인제스트된 모든 데이터가 개인을 식별하고 해당 [!DNL Real-Time Profile]을 함께 연결하는 데 사용됩니다.

[!DNL Real-time Customer Profile]에 대한 자세한 내용과 ID를 사용한 작업을 살펴보려면 [ID 서비스](../../identity-service/home.md) 설명서를 참조하십시오.

[!DNL Real-time Customer Profile]에 대한 데이터 세트를 활성화하려면 **[!UICONTROL Info]** 탭에서 **[!UICONTROL Profile]** 전환을 클릭합니다.

![프로필 전환](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

[!DNL Real-time Customer Profile]에 대한 데이터 세트를 활성화할지 확인하는 대화 상자가 나타납니다.

![프로필 대화 상자 활성화](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

**[!UICONTROL Enable]**&#x200B;을(를) 클릭하면 토글이 파란색으로 바뀝니다. 이 메시지는 켜져 있음을 나타냅니다.

![프로필 사용](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## 데이터 세트에 데이터 추가

여러 가지 방법으로 데이터를 데이터 세트에 추가할 수 있습니다. [!DNL Data Ingestion] API나 [!DNL Unifi] 또는 [!DNL Informatica]와 같은 ETL 파트너를 사용하도록 선택할 수 있습니다. 이 자습서의 경우 UI 내의 **[!UICONTROL Add Data]** 탭을 사용하여 데이터를 데이터 세트에 추가합니다.

데이터 세트에 데이터를 추가하기 시작하려면 **[!UICONTROL Add Data]** 탭을 클릭합니다. 이제 파일을 드래그 앤 드롭하거나 컴퓨터에 추가할 파일을 검색할 수 있습니다.

>[!NOTE]
>
>플랫폼은 데이터 수집, 쪽모이 세공식 또는 JSON을 위한 두 가지 파일 유형을 지원합니다. 한 번에 최대 5개의 파일을 추가할 수 있으며 각 파일의 최대 파일 크기는 10GB입니다.

![데이터 추가 탭](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## 파일 업로드

업로드하려는 Pareken 또는 JSON 파일을 드래그 앤 드롭하거나 찾아보고 선택하면 [!DNL Platform]이 즉시 파일 처리를 시작하며 파일 업로드 진행 상황을 보여주는 **[!UICONTROL Add Data]** 탭에 **[!UICONTROL Uploading]** 대화 상자가 나타납니다.

![업로드 대화 상자](../images/tutorials/ingest-batch-data/uploading-file.png)

## 데이터 세트 지표

파일 업로드를 완료한 후 **[!UICONTROL Dataset Activity]** 탭에 &quot;추가된 일괄 처리가 없습니다.&quot;가 표시되는 문제가 해결되었습니다. 대신 이제 **[!UICONTROL Dataset Activity]** 탭에 데이터 세트 지표가 표시됩니다. 배치가 아직 로드되지 않았으므로 모든 지표는 이 단계에서 &quot;0&quot;을 표시합니다.

탭 아래쪽에 [&quot;데이터 세트에 데이터 추가&quot;](#add-data-to-dataset) 프로세스를 통해 인제스트된 데이터의 **[!UICONTROL Batch ID]**&#x200B;을(를) 보여주는 목록이 있습니다. 인제스트된 날짜, 인제스트된 레코드 수 및 현재 배치 상태를 포함하여 배치와 관련된 정보가 포함되어 있습니다.

![데이터 세트 지표](../images/tutorials/ingest-batch-data/batch-id.png)

## 일괄 처리 세부 사항

**[!UICONTROL Batch ID]**&#x200B;을 클릭하여 **[!UICONTROL Batch Overview]**&#x200B;을 보고 일괄 처리에 대한 추가 세부 정보를 표시합니다. 일괄 처리가 로드를 완료하면 일괄 처리에 대한 정보가 업데이트되어 처리된 레코드 수와 파일 크기가 표시됩니다. 상태는 &quot;성공&quot; 또는 &quot;실패&quot;로도 변경됩니다. 일괄 처리에 실패할 경우 **[!UICONTROL Error Code]** 섹션에는 통합 중 오류에 대한 세부 정보가 포함됩니다.

일괄 처리에 대한 자세한 내용 및 FAQ는 [일괄 처리 통합 문제 해결 안내서](../batch-ingestion/troubleshooting.md)를 참조하십시오.

**[!UICONTROL Dataset Activity]** 화면으로 돌아가려면 탐색 경로에서 데이터 세트(**[!UICONTROL Loyalty Details]**)의 이름을 클릭합니다.

![일괄 처리 개요](../images/tutorials/ingest-batch-data/batch-details.png)

## 데이터 세트 미리 보기

데이터 세트가 준비되면 **[!UICONTROL Dataset Activity]** 탭의 맨 위에 **[!UICONTROL Preview Dataset]** 옵션이 나타납니다.

데이터 세트 내의 샘플 데이터를 표시하는 대화 상자를 열려면 **[!UICONTROL Preview Dataset]**&#x200B;을 클릭합니다. 스키마를 사용하여 데이터 집합을 만든 경우 데이터 집합 스키마에 대한 세부 정보가 미리 보기의 왼쪽에 표시됩니다. 화살표를 사용하여 스키마를 확장하여 스키마 구조를 볼 수 있습니다. 미리 보기 데이터의 각 열 헤더는 데이터 세트의 필드를 나타냅니다.

![데이터 세트 세부 정보](../images/tutorials/ingest-batch-data/dataset-preview.png)

## 다음 단계 및 추가 리소스

이제 데이터 세트를 만들고 데이터를 [!DNL Experience Platform]에 성공적으로 인제스트하였으므로 이 단계를 반복하여 새 데이터 세트를 만들거나 기존 데이터 세트에 더 많은 데이터를 인제스트할 수 있습니다.

일괄 처리에 대한 자세한 내용을 보려면 [일괄 처리 통합 개요](../batch-ingestion/overview.md)를 읽고 아래 비디오를 시청하여 학습 내용을 보완하십시오.

>[!WARNING]
>
>다음 비디오에 표시된 [!DNL Platform] UI가 최신 상태가 아닙니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
