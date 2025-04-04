---
keywords: Experience Platform;홈;자주 찾는 주제;수집;배치 데이터 수집;튜토리얼;배치 수집;튜토리얼;ui 안내서;
solution: Experience Platform
title: Experience Platform에 데이터 수집
type: Tutorial
description: Adobe Experience Platform을 사용하면 데이터를 Parquet 파일 또는 알려진 XDM(Experience Data Model) 스키마를 준수하는 데이터의 형태로 배치 파일로 쉽게 가져올 수 있습니다.
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---

# Adobe Experience Platform에 데이터 수집

Adobe Experience Platform을 사용하면 데이터를 [!DNL Experience Platform]에 배치 파일로 쉽게 가져올 수 있습니다. 수집할 데이터의 예로는 CRM 시스템의 플랫 파일(예: Parquet 파일)의 프로필 데이터 또는 스키마 레지스트리의 알려진 [!DNL Experience Data Model]&#x200B;(XDM) 스키마를 준수하는 데이터가 포함될 수 있습니다.

## 시작하기

이 자습서를 완료하려면 [!DNL Experience Platform]에 대한 액세스 권한이 있어야 합니다. [!DNL Experience Platform]의 조직에 대한 액세스 권한이 없는 경우 계속하기 전에 시스템 관리자에게 문의하십시오.

데이터 수집 API를 사용하여 데이터를 수집하려면 [일괄 처리 수집 개발자 안내서](../batch-ingestion/api-overview.md)를 읽는 것부터 시작하십시오.

## 데이터 세트 작업 공간

[!DNL Experience Platform] 내의 데이터 세트 작업 영역을 사용하면 조직에서 만든 모든 데이터 세트를 보고 관리할 수 있을 뿐만 아니라 새 데이터 세트를 만들 수 있습니다.

왼쪽 탐색에서 **[!UICONTROL 데이터 세트]**&#x200B;를 클릭하여 데이터 세트 작업 영역을 봅니다. 데이터 세트 작업 공간에는 이름, 생성됨(날짜 및 시간), 소스, 스키마 및 마지막 배치 상태를 표시하는 열과 데이터 세트가 마지막으로 업데이트된 날짜 및 시간을 포함하는 데이터 세트 목록이 포함되어 있습니다.

>[!NOTE]
>
>필터링 기능을 사용하여 [!DNL Profile]에 대해 활성화된 데이터 세트만 보려면 검색 창 옆에 있는 필터 아이콘을 클릭하십시오.

![모든 데이터 세트 보기](../images/tutorials/ingest-batch-data/datasets-overview.png)

## 데이터 세트 만들기

데이터 집합을 만들려면 데이터 집합 작업 영역의 오른쪽 맨 위에 있는 **[!UICONTROL 데이터 집합 만들기]**&#x200B;를 클릭합니다.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

**[!UICONTROL 데이터 집합 만들기]** 화면에서 &quot;[!UICONTROL 스키마에서 데이터 집합 만들기]&quot; 또는 &quot;[!UICONTROL CSV 파일에서 데이터 집합 만들기]&quot;를 사용할지 여부를 선택합니다.

이 자습서의 경우 데이터 세트를 만드는 데 스키마가 사용됩니다. 계속하려면 **[!UICONTROL 스키마에서 데이터 집합 만들기]**&#x200B;를 클릭하십시오.

![데이터 원본 선택](../images/tutorials/ingest-batch-data/create-dataset.png)

## 데이터 세트 스키마 선택

**[!UICONTROL 스키마 선택]** 화면에서 사용할 스키마 옆에 있는 라디오 단추를 클릭하여 스키마를 선택합니다. 이 자습서의 경우 충성도 멤버 스키마를 사용하여 데이터 세트를 만듭니다. 검색 창을 사용하여 스키마를 필터링하면 원하는 스키마를 정확하게 찾을 수 있습니다.

사용할 스키마 옆에 있는 라디오 단추를 선택한 후 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

![스키마 선택](../images/tutorials/ingest-batch-data/select-schema.png)

## 데이터 세트 구성

**[!UICONTROL 데이터 집합 구성]** 화면에서 데이터 집합 이름을 지정해야 하며 데이터 집합에 대한 설명도 제공할 수 있습니다.

**데이터 집합 이름에 대한 참고 사항:**

- 데이터 세트 이름은 짧고 설명적이어야 나중에 라이브러리에서 데이터 세트를 쉽게 찾을 수 있습니다.
- 데이터 세트 이름은 고유해야 합니다. 즉, 향후 재사용되지 않을 만큼 구체적이어야 합니다.
- 향후 다른 사용자가 데이터 세트를 구분하는 데 도움이 될 수 있으므로 설명 필드를 사용하여 데이터 세트에 대한 추가 정보를 제공하는 것이 좋습니다.

데이터 집합에 이름과 설명이 있으면 **[!UICONTROL 마침]**&#x200B;을 클릭합니다.

![데이터 집합 구성](../images/tutorials/ingest-batch-data/configure-dataset.png)

## 데이터 세트 활동

이제 빈 데이터 세트가 만들어졌고 데이터 세트 작업 영역의 **[!UICONTROL 데이터 세트 활동]** 탭으로 돌아왔습니다. 작업 영역의 왼쪽 상단 모서리에 &quot;추가된 일괄 처리가 없습니다.&quot;라는 알림과 함께 데이터 세트 이름이 표시됩니다. 이 데이터 세트에 아직 배치를 추가하지 않았기 때문에 이는 예상되었습니다.

데이터 세트 작업 영역의 오른쪽에는 데이터 세트 ID, 이름, 설명, 테이블 이름, 스키마, 스트리밍 및 소스와 같은 새 데이터 세트와 관련된 정보가 들어 있는 **[!UICONTROL 정보]** 탭이 표시됩니다. 정보 탭에는 데이터 세트가 만들어진 시간과 마지막 수정 날짜에 대한 정보도 포함됩니다.

또한 정보 탭에는 [!DNL Real-Time Customer Profile]에서 사용할 데이터 집합을 활성화하는 데 사용되는 **[!UICONTROL 프로필]** 전환이 있습니다. 이 토글 및 [!DNL Real-Time Customer Profile]의 사용에 대해서는 다음 섹션에서 자세히 설명합니다.

![데이터 집합 활동](../images/tutorials/ingest-batch-data/sample-dataset.png)

## [!DNL Real-Time Customer Profile]에 대한 데이터 집합 사용

데이터 세트는 데이터를 [!DNL Experience Platform]&#x200B;(으)로 수집하는 데 사용되며, 이 데이터는 궁극적으로 개인을 식별하고 여러 소스에서 가져온 정보를 결합하는 데 사용됩니다. 결합된 정보를 [!DNL Real-Time Customer Profile]이라고 합니다. [!DNL Experience Platform]이(가) [!DNL Real-Time Profile]에 포함해야 하는 정보를 알 수 있도록 **[!UICONTROL 프로필]** 전환을 사용하여 데이터 세트를 포함용으로 표시할 수 있습니다.

기본적으로 이 토글은 꺼져 있습니다. [!DNL Profile]을(를) 켜도록 선택하면 데이터 집합에 수집된 모든 데이터가 개인을 식별하고 해당 [!DNL Real-Time Profile]을(를) 연결하는 데 사용됩니다.

[!DNL Real-Time Customer Profile] 및 ID 작업에 대한 자세한 내용은 [ID 서비스](../../identity-service/home.md) 설명서를 참조하십시오.

[!DNL Real-Time Customer Profile]에 대한 데이터 집합을 사용하려면 **[!UICONTROL 정보]** 탭에서 **[!UICONTROL 프로필]** 전환을 클릭하세요.

![프로필 전환](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

[!DNL Real-Time Customer Profile]에 대한 데이터 집합을 사용하도록 설정할지 확인하는 대화 상자가 나타납니다.

![프로필 대화 상자 사용](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

**[!UICONTROL 사용]**&#x200B;을 클릭하면 전환이 파란색으로 바뀌어 켜져 있음을 나타냅니다.

![프로필에 대해 활성화됨](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## 데이터 세트에 데이터 추가

데이터는 다양한 방법으로 데이터 세트에 추가할 수 있습니다. [!DNL Data Ingestion]개의 API 또는 [!DNL Unifi] 또는 [!DNL Informatica]과(와) 같은 ETL 파트너를 사용하도록 선택할 수 있습니다. 이 자습서의 경우 UI 내의 **[!UICONTROL 데이터 추가]** 탭을 사용하여 데이터 집합에 데이터가 추가됩니다.

데이터 집합에 데이터를 추가하려면 **[!UICONTROL 데이터 추가]** 탭을 클릭합니다. 이제 파일을 드래그 앤 드롭하거나 추가할 파일을 컴퓨터에서 검색할 수 있습니다.

>[!NOTE]
>
>Experience Platform은 데이터 수집에 Parquet 또는 JSON의 두 가지 파일 유형을 지원합니다. 한 번에 최대 5개의 파일을 추가할 수 있으며, 각 파일의 최대 파일 크기는 1GB입니다.

![데이터 탭 추가](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## 파일 업로드 {#upload-file}

업로드하려는 Parquet 또는 JSON 파일을 드래그 앤 드롭(또는 찾아보기 및 선택)하면 [!DNL Experience Platform]이(가) 즉시 파일 처리를 시작하며 **[!UICONTROL 데이터 추가]** 탭에 파일 업로드 진행 상황을 보여주는 **[!UICONTROL 업로드]** 대화 상자가 나타납니다.

![대화 상자 업로드](../images/tutorials/ingest-batch-data/uploading-file.png)

## 데이터 세트 지표

파일 업로드가 완료되면 **[!UICONTROL 데이터 집합 활동]** 탭에 더 이상 &quot;추가된 일괄 처리가 없습니다&quot;라는 메시지가 표시되지 않습니다. 대신 이제 **[!UICONTROL 데이터 집합 활동]** 탭에 데이터 집합 지표가 표시됩니다. 배치가 아직 로드되지 않았으므로 모든 지표는 이 단계에서 &quot;0&quot;을 표시합니다.

탭 하단에 [&quot;데이터 세트에 데이터 추가&quot;](#add-data-to-dataset) 프로세스를 통해 방금 수집된 데이터의 **[!UICONTROL 배치 ID]**&#x200B;을(를) 표시하는 목록이 있습니다. 또한 수집된 날짜, 수집된 레코드 수 및 현재 배치 상태 등 배치와 관련된 정보도 포함됩니다.

![데이터 집합 지표](../images/tutorials/ingest-batch-data/batch-id.png)

## 일괄 처리 세부 정보

**[!UICONTROL 일괄 처리 ID]**&#x200B;을(를) 클릭하여 일괄 처리와 관련된 추가 세부 정보를 보여주는 **[!UICONTROL 일괄 처리 개요]**&#x200B;를 봅니다. 배치 로드가 완료되면 배치에 대한 정보가 업데이트되어 수집된 레코드 수와 파일 크기가 표시됩니다. 상태도 &quot;성공&quot; 또는 &quot;실패&quot;로 변경됩니다. 일괄 처리가 실패하면 **[!UICONTROL 오류 코드]** 섹션에는 수집 중 발생한 오류에 대한 세부 정보가 포함됩니다.

일괄 처리 수집에 대한 자세한 내용 및 FAQ는 [일괄 처리 수집 문제 해결 안내서](../batch-ingestion/troubleshooting.md)를 참조하십시오.

**[!UICONTROL 데이터 집합 활동]** 화면으로 돌아가려면 이동 경로에서 데이터 집합 이름(**[!UICONTROL 충성도 세부 정보]**)을 클릭합니다.

![일괄 처리 개요](../images/tutorials/ingest-batch-data/batch-details.png)

## 데이터 세트 미리 보기

데이터 세트가 준비되면 **[!UICONTROL 데이터 세트 미리 보기]**&#x200B;에 대한 옵션이 **[!UICONTROL 데이터 세트 활동]** 탭의 맨 위에 나타납니다.

**[!UICONTROL 데이터 집합 미리 보기]**&#x200B;를 클릭하여 데이터 집합 내의 샘플 데이터를 표시하는 대화 상자를 엽니다. 스키마를 사용하여 데이터 세트를 만든 경우 데이터 세트 스키마에 대한 세부 사항이 미리보기의 왼쪽에 나타납니다. 화살표를 사용하여 스키마를 확장하면 스키마 구조를 볼 수 있습니다. 미리보기 데이터의 각 열 헤더는 데이터 세트의 필드를 나타냅니다.

![데이터 집합 세부 정보](../images/tutorials/ingest-batch-data/dataset-preview.png)

## 다음 단계 및 추가 리소스

데이터 집합을 만들고 [!DNL Experience Platform]에 데이터를 수집했으므로 이 단계를 반복하여 새 데이터 집합을 만들거나 기존 데이터 집합에 더 많은 데이터를 수집할 수 있습니다.

일괄 처리에 대한 자세한 내용은 [일괄 처리 수집 개요](../batch-ingestion/overview.md)를 읽고 아래 비디오를 통해 학습 내용을 보완해 주십시오.

>[!WARNING]
>
>다음 비디오에 표시된 [!DNL Experience Platform] UI가 최신 상태가 아닙니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
