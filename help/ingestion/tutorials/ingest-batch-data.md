---
keywords: Experience Platform;home;popular topics;ingestion;ingest batch data;tutorial;batch ingestion;tutorial;ui guide;
solution: Experience Platform
title: Adobe Experience Platform에 데이터 수집
topic: tutorial
type: Tutorial
description: Adobe Experience Platform을 사용하면 알려진 XDM(Experience Data Model) 스키마를 준수하는 데이터 또는 쪽모이 세공 마룻파일의 형태로 데이터를 일괄적으로 간편하게 가져올 수 있습니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 0%

---


# Adobe Experience Platform에 데이터 수집

Adobe Experience Platform을 사용하면 데이터를 일괄 처리 파일 [!DNL Platform] 로 손쉽게 가져올 수 있습니다. 인제스트할 데이터의 예로는 CRM 시스템의 플랫 파일의 프로필 데이터(예: 쪽모이 세공 파일)나 스키마 레지스트리에서 알려진 [!DNL Experience Data Model] (XDM) 스키마를 준수하는 데이터가 포함될 수 있습니다.

## 시작하기

이 자습서를 완료하려면 액세스 권한이 있어야 합니다 [!DNL Experience Platform]. 에서 IMS 조직에 액세스할 수 없는 경우 시스템 관리자 [!DNL Experience Platform]에게 연락하여 진행하십시오.

데이터 통합 API를 사용하여 데이터를 인제스트하려는 경우 먼저 [일괄 처리 통합 개발자 안내서를 읽어 보십시오](../batch-ingestion/api-overview.md).

## 데이터 세트 작업 영역

데이터 세트 작업 영역을 사용하면 IMS 조직에서 만든 모든 데이터 세트를 보고 관리할 수 [!DNL Experience Platform] 있을 뿐만 아니라 새 데이터 세트를 만들 수 있습니다.

왼쪽 탐색에서 데이터 세트 **[!UICONTROL 를]** 클릭하여 데이터 집합 작업 영역을 봅니다. 데이터 집합 작업 영역에는 데이터 집합이 마지막으로 업데이트된 날짜 및 시간은 물론, 이름, 만들어진 날짜 및 시간, 소스, 스키마 및 마지막 일괄 처리 상태를 보여주는 열을 포함한 데이터 집합 목록이 들어 있습니다.

>[!NOTE]
>
>검색 막대 옆에 있는 필터 아이콘을 클릭하여 필터링 기능을 사용하여 이 데이터 세트를 사용할 수 있도록 설정한 데이터 집합만 표시합니다 [!DNL Profile].

![모든 데이터 집합 보기](../images/tutorials/ingest-batch-data/datasets-overview.png)

## 데이터 세트 만들기

데이터 세트를 만들려면 데이터 집합 작업 **[!UICONTROL 영역의 오른쪽]** 맨 위에 있는 데이터 집합 만들기를 클릭합니다.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

데이터 집합 **[!UICONTROL 만들기]** 화면에서 &quot;스키마에서 데이터 집합[!UICONTROL 만들기&quot; 또는 &quot;]CSV 파일에서 데이터 집합[!UICONTROL 만들기&quot;]를선택합니다.

이 자습서의 경우 스키마는 데이터 세트를 만드는 데 사용됩니다. 계속하려면 **[!UICONTROL 스키마에서 데이터 세트]** 만들기를 클릭합니다.

![데이터 소스 선택](../images/tutorials/ingest-batch-data/create-dataset.png)

## 데이터 집합 스키마 선택

스키마 **[!UICONTROL 선택]** 화면에서 사용할 스키마 옆에 있는 라디오 단추를 클릭하여 스키마를 선택합니다. 이 자습서의 경우 충성도 멤버 스키마를 사용하여 데이터 세트에 대해 수행됩니다. 검색 막대를 사용하여 스키마를 필터링하면 원하는 정확한 스키마를 찾을 수 있습니다.

사용할 스키마 옆에 있는 라디오 단추를 선택한 후 **[!UICONTROL 다음을 클릭합니다]**.

![스키마 선택](../images/tutorials/ingest-batch-data/select-schema.png)

## 데이터 세트 구성

데이터 세트 **[!UICONTROL 구성]** 화면에서 데이터 세트에 이름을 지정해야 하며 데이터 세트에 대한 설명도 제공할 수 있습니다.

**데이터 세트 이름에 대한 참고 사항:**

- 데이터 세트 이름은 나중에 라이브러리에서 쉽게 찾을 수 있도록 짧고 설명이어야 합니다.
- 데이터 집합 이름은 고유해야 합니다. 즉, 나중에 다시 사용할 수 없도록 충분히 구체적이어야 합니다.
- 설명 필드를 사용하여 데이터 세트에 대한 추가 정보를 제공하는 것이 가장 좋습니다. 이렇게 하면 나중에 다른 사용자가 데이터 세트를 구별할 수 있습니다.

데이터 세트에 이름과 설명이 있으면 마침을 **[!UICONTROL 클릭합니다]**.

![데이터 세트 구성](../images/tutorials/ingest-batch-data/configure-dataset.png)

## 데이터 집합 활동

이제 빈 데이터 세트가 만들어져서 데이터 집합 작업 영역의 **[!UICONTROL 데이터 집합 활동]** 탭으로 돌아갑니다. &quot;배치가 추가되지 않았습니다.&quot;라는 알림과 함께 작업 공간의 왼쪽 위 모서리에 데이터 세트 이름이 표시됩니다. 이 데이터 세트에 아직 배치를 추가하지 않았기 때문에 예상됩니다.

데이터 집합 작업 영역의 오른쪽에는 데이터 집합 ID, 이름, 설명, 테이블 이름, 스키마, 스트리밍 및 소스 같은 새 데이터 집합과 관련된 정보가 들어 있는 **[!UICONTROL 정보]** 탭이 표시됩니다. 또한 정보 탭에는 데이터 세트를 만든 날짜와 마지막으로 수정한 날짜에 대한 정보도 포함되어 있습니다.

또한 정보 탭에서는 데이터 **[!UICONTROL 세트]** 사용 시 사용되는 프로필 [!DNL Real-time Customer Profile]토글입니다. 이 전환 기능의 사용 및 [!DNL Real-time Customer Profile]다음 섹션에 더 자세히 설명되어 있습니다.

![데이터 집합 활동](../images/tutorials/ingest-batch-data/sample-dataset.png)

## 데이터 세트 사용 [!DNL Real-time Customer Profile]

데이터 집합은 데이터를 인제스트하는 데 사용되며, 이 데이터 [!DNL Experience Platform]는 결국 개인을 식별하고 여러 소스에서 나오는 정보를 통합하는 데 사용됩니다. 이렇게 한데 엮인 정보를 A라고 부른다 [!DNL Real-Time Customer Profile]. 데이터 세트 [!DNL Platform] 를 사용하여 어떤 정보를 포함해야 하는지 알 수 있도록 [!DNL Real-Time Profile]**[!UICONTROL 프로필]** 전환을 사용하여 데이터 세트를 포함하도록 표시할 수 있습니다.

기본적으로 이 토글은 꺼져 있습니다. 켜짐으로 전환하는 경우 데이터 세트에 [!DNL Profile]수집되는 모든 데이터는 개인을 식별하고 해당 데이터를 함께 연결하는 데 사용됩니다 [!DNL Real-Time Profile].

ID 사용 및 작업에 대한 자세한 내용 [!DNL Real-time Customer Profile] 은 [ID 서비스](../../identity-service/home.md) 설명서를 참조하십시오.

데이터 세트를 활성화하려면 [!DNL Real-time Customer Profile]정보 **[!UICONTROL 탭]** 에서 **[!UICONTROL 프로필]** 토글을클릭합니다.

![프로필 전환](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

데이터 세트를 활성화할지 확인하는 대화 상자가 나타납니다 [!DNL Real-time Customer Profile].

![프로필 사용 대화 상자](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

활성화 **[!UICONTROL 를]** 클릭하면 토글이 파란색으로 바뀝니다. 이 메시지는 켜져 있음을 나타냅니다.

![프로필 사용](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## 데이터 세트에 데이터 추가

다양한 방법으로 데이터를 데이터 세트에 추가할 수 있습니다. API나 또는 [!DNL Data Ingestion] 과 같은 ETL 파트너 [!DNL Unifi] 를 사용하도록 선택할 수 [!DNL Informatica]있습니다. 이 자습서의 경우 UI 내의 데이터 **[!UICONTROL 추가]** 탭을 사용하여 데이터가 데이터 세트에 추가됩니다.

데이터 세트에 데이터를 추가하려면 데이터 추가 **[!UICONTROL 탭을]** 클릭합니다. 이제 파일을 드래그 앤 드롭하거나 컴퓨터를 검색하여 추가할 파일을 찾을 수 있습니다.

>[!NOTE]
>
>플랫폼은 데이터 수집, 쪽모이 세공식 또는 JSON을 위한 두 가지 파일 유형을 지원합니다. 한 번에 최대 5개의 파일을 추가할 수 있으며 각 파일의 최대 파일 크기는 10GB입니다.

![데이터 추가 탭](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## 파일 업로드

업로드하려는 쪽모이 세공된 또는 JSON 파일을 드래그 앤 드롭하거나 검색 및 선택하면 파일 처리가 즉시 [!DNL Platform] 시작되고 파일 업로드 진행 상황을 보여주는 **[!UICONTROL 업로드]** 대화 상자가 **[!UICONTROL 데이터]** 추가탭에나타납니다.

![업로드 대화 상자](../images/tutorials/ingest-batch-data/uploading-file.png)

## 데이터 세트 지표

파일 업로드가 완료된 후 데이터 세트 **[!UICONTROL 활동]** 탭에 더 이상 &quot;추가된 일괄 처리가 없습니다&quot;가 표시되지 않습니다. 대신 이제 데이터 집합 **[!UICONTROL 활동]** 탭에 데이터 집합 지표가 표시됩니다. 일괄 처리가 아직 로드되지 않았기 때문에 모든 지표가 이 단계에서 &quot;0&quot;으로 표시됩니다.

탭 아래쪽에는 **[!UICONTROL &quot;데이터 세트에 데이터 추가&quot;]** 프로세스를 통해 인제스트된 데이터의 [배치](#add-data-to-dataset) ID를 보여주는 목록이있습니다. 인제스트된 날짜, 인제스트된 레코드 수 및 현재 배치 상태를 포함하여 배치와 관련된 정보가 포함됩니다.

![데이터 세트 지표](../images/tutorials/ingest-batch-data/batch-id.png)

## 배치 세부 사항

배치 **[!UICONTROL ID를]** 클릭하여 배치 **[!UICONTROL 개요를]**&#x200B;보고 배치와 관련된 추가 세부 사항을 표시합니다. 일괄 처리가 로드를 완료하면 일괄 처리에 대한 정보가 업데이트되어 수집되는 레코드 수와 파일 크기가 표시됩니다. 상태는 &quot;성공&quot; 또는 &quot;실패&quot;로 변경됩니다. 일괄 처리에 실패할 경우 오류 코드 **** 섹션에는 통합 중 오류에 대한 세부 사항이 포함됩니다.

일괄 처리 수집에 대한 자세한 내용 및 FAQ는 [일괄 처리 처리 처리 문제 해결 가이드를 참조하십시오](../batch-ingestion/troubleshooting.md).

데이터 세트 **[!UICONTROL 활동]** 화면으로 돌아가려면 탐색 경로에서 데이터 세트 이름(**[!UICONTROL 충성도 세부]**&#x200B;사항)을 클릭합니다.

![배치 개요](../images/tutorials/ingest-batch-data/batch-details.png)

## 데이터 세트 미리 보기

데이터 세트를 준비하면 데이터 세트 미리 **[!UICONTROL 보기]** 옵션이 **[!UICONTROL 데이터 세트 활동]** 탭 상단에나타납니다.

데이터 세트 **[!UICONTROL 미리]** 보기를 클릭하여 데이터 세트 내의 샘플 데이터를 보여주는 대화 상자를 엽니다. 스키마를 사용하여 데이터 세트를 만든 경우 데이터 집합 스키마에 대한 세부 정보가 미리 보기의 왼쪽에 표시됩니다. 화살표를 사용하여 스키마를 확장하여 스키마 구조를 볼 수 있습니다. 미리 보기 데이터의 각 열 헤더는 데이터 세트에 있는 필드를 나타냅니다.

![데이터 세트 세부 정보](../images/tutorials/ingest-batch-data/dataset-preview.png)

## 다음 단계 및 추가 리소스

데이터 세트를 만들고 데이터를 성공적으로 인제스트한 후에는 이러한 단계를 반복하여 새 데이터 세트 [!DNL Experience Platform]를 만들거나 기존 데이터 세트에 더 많은 데이터를 인제스트할 수 있습니다.

일괄 처리에 대한 자세한 내용은 [일괄 처리 통합 개요를](../batch-ingestion/overview.md) 읽고 아래 비디오를 시청하여 학습 내용을 보완해 보십시오.

>[!WARNING]
>
>다음 비디오에 표시된 [!DNL Platform] UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)