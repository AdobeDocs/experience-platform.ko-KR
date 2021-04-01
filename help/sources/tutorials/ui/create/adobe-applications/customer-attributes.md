---
keywords: Experience Platform;홈;인기 항목;사용자 특성;InDesign;home;popular topics;customer attributes
solution: Experience Platform
title: UI에서 고객 속성 소스 연결 만들기
topic: 개요
type: 튜토리얼
description: 고객 속성 프로필 데이터를 Adobe Experience Platform에 수집하기 위해 UI에서 소스 연결을 만드는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 08a3026e969a8739a8b57226c35a6d1d3150006e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---


# UI에서 고객 속성 소스 연결 만들기

이 자습서에서는 고객 속성 프로필 데이터를 Adobe Experience Platform에 수집하기 위해 UI에서 소스 연결을 만드는 단계를 제공합니다. 고객 속성에 대한 자세한 내용은 [고객 속성 개요](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html)를 참조하십시오.

>[!IMPORTANT]
>
>데이터 흐름 비활성화, 활성화 및 삭제는 현재 고객 속성 소스에서 지원되지 않습니다.

## 소스 연결 만들기

플랫폼 UI의 왼쪽 탐색 메뉴에서 **[!UICONTROL Sources]**&#x200B;을 선택하여 [!UICONTROL Sources] 작업 영역에 액세스합니다. [!UICONTROL Catalog] 화면에는 연결을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL Adobe applications] 범주에서 **[!UICONTROL Customer Attributes]**&#x200B;을 선택한 다음 **[!UICONTROL Add data]**&#x200B;를 선택합니다.

>[!NOTE]
>
>고객 속성 프로필 데이터에 대한 소스 연결을 이미 설정한 경우 소스와 연결하는 옵션이 비활성화됩니다.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

[!UICONTROL Add data] 화면에는 고객 속성에 사용할 수 있는 모든 데이터 소스가 표시됩니다. 새 연결을 만들려면 목록에서 데이터 소스를 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택합니다.

>[!NOTE]
>
>고객 속성 소스 연결당 하나의 데이터 세트만 선택할 수 있습니다.

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

[!UICONTROL Dataflow detail] 단계가 나타나 새 데이터 흐름 이름을 지정하고 간단한 설명을 제공할 수 있습니다.

이 프로세스 동안 [!UICONTROL Partial ingestion] 및 [!UICONTROL Error diagnostics]을(를) 활성화할 수도 있습니다. [!UICONTROL Partial ingestion] 에서는 오류가 포함된 데이터를 인제스트할 수 있으며, 설정할 수 있는 특정 임계값까지 인제스트할  [!UICONTROL Error diagnostics] 수 있으며, 별도로 묶인 잘못된 데이터에 대한 세부 정보를 제공합니다. 자세한 내용은 [부분 일괄 처리 통합 개요](../../../../../ingestion/batch-ingestion/partial.md)를 참조하십시오.

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

[!UICONTROL Review] 단계가 나타나 새 데이터 흐름을 만들기 전에 검토할 수 있습니다. 세부 사항은 다음 카테고리 내에서 그룹화됩니다.

* **[!UICONTROL Connection]**:소스 유형, 선택한 소스 파일의 관련 경로 및 해당 소스 파일 내의 열 수를 표시합니다.
* **[!UICONTROL Assign dataset & map fields]**:데이터 세트가 준수하는 스키마를 포함하여 원본 데이터를 수집할 데이터 집합을 표시합니다.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## 다음 단계

연결이 만들어지면 들어오는 데이터를 포함하도록 대상 스키마와 데이터 세트가 자동으로 생성됩니다. 초기 수집이 완료되면 고객 속성 프로필 데이터를 [!DNL Real-time Customer Profile] 및 [!DNL Segmentation Service] 같은 다운스트림 플랫폼 서비스에서 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 개요](../../../../../segmentation/home.md)
