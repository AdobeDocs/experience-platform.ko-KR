---
keywords: Experience Platform;홈;인기 항목;세그멘테이션 서비스;세그멘테이션;데이터 세트 만들기;대상 세그먼트 내보내기;세그먼트 내보내기
solution: Experience Platform
title: 대상 세그먼트 내보내기를 위한 데이터 세트 만들기
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 Experience Platform UI를 사용하여 대상 세그먼트를 내보내는 데 사용할 수 있는 데이터 세트를 만드는 데 필요한 단계를 안내합니다.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---

# 대상 세그먼트를 내보낼 데이터 세트 만들기

[!DNL Adobe Experience Platform] 특정 속성에 따라 고객 프로파일을 손쉽게 고객으로 세분화할 수 있습니다. 세그먼트가 만들어지면 액세스 및 작업이 가능한 데이터 세트에 해당 대상을 내보낼 수 있습니다. 내보내기가 성공하려면 데이터 세트를 올바르게 구성해야 합니다.

이 자습서에서는 [!DNL Experience Platform] UI를 사용하여 대상 세그먼트를 내보내는 데 사용할 수 있는 데이터 세트를 만드는 데 필요한 단계를 안내합니다.

이 자습서는 [세그먼트 결과 평가 및 액세스](./evaluate-a-segment.md)에 대한 자습서에 나와 있는 단계와 직접 관련이 있습니다. 세그먼트 평가 자습서에서는 [!DNL Catalog Service] API를 사용하여 데이터 세트를 만드는 단계를 제공하는 반면 이 자습서에서는 [!DNL Experience Platform] UI를 사용하여 데이터 세트를 만드는 단계를 간략히 설명합니다.

## 시작하기

세그먼트를 내보내려면 데이터 세트는 [!DNL XDM Individual Profile Union Schema]을 기반으로 해야 합니다. 결합 스키마는 동일한 클래스를 공유하는 모든 스키마의 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다(이 경우 [!DNL XDM Individual Profile] 클래스). 결합 보기 스키마에 대한 자세한 내용은 스키마 레지스트리 개발자 안내서](../../xdm/schema/composition.md#union)의 [실시간 고객 프로필 섹션을 참조하십시오.

UI에서 결합 스키마를 보려면 왼쪽 탐색 영역에서 **[!UICONTROL Profiles]**&#x200B;을 클릭한 다음 아래 표시된 대로 **[!UICONTROL Union schema]** 탭을 클릭합니다.

![Experience Platform UI의 결합 스키마 탭](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## 데이터 세트 작업 영역

[!DNL Experience Platform] UI 내의 데이터 집합 작업 영역을 사용하면 IMS 조직에서 만든 모든 데이터 집합을 보고 관리할 수 있고 새 데이터 집합을 만들 수 있습니다.

데이터 집합 작업 영역을 보려면 왼쪽 탐색 영역에서 **[!UICONTROL Datasets]**&#x200B;을 클릭한 다음 **[!UICONTROL Browse]** 탭을 클릭합니다. 데이터 집합 작업 영역에는 데이터 집합이 마지막으로 업데이트된 날짜 및 시간은 물론, 이름, 만든 날짜(날짜 및 시간), 소스, 스키마 및 마지막 일괄 처리 상태를 표시하는 열을 포함한 데이터 집합 목록이 들어 있습니다. 각 열의 너비에 따라 모든 열을 보려면 왼쪽이나 오른쪽으로 스크롤해야 할 수 있습니다.

>[!NOTE]
>
>필터링 기능을 사용하여 [!DNL Real-time Customer Profile]에 대해 활성화된 데이터 집합만 보려면 검색 막대 옆에 있는 필터 아이콘을 클릭합니다.

![모든 데이터 집합 보기](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## 데이터 세트 만들기

데이터 세트를 만들려면 **[!UICONTROL Datasets]** 작업 영역의 오른쪽 위 모서리에 있는 **[!UICONTROL Create Dataset]**&#x200B;을 클릭합니다.

![데이터 세트 만들기를 클릭합니다.](../images/tutorials/segment-export-dataset/dataset-click-create.png)

**[!UICONTROL Create Dataset]** 화면에서 **[!UICONTROL Create Dataset from Schema]**&#x200B;을 클릭하여 계속합니다.

![데이터 소스 선택](../images/tutorials/segment-export-dataset/create-dataset.png)

## XDM 개별 프로필 조합 스키마 선택

데이터 세트에 사용할 [!DNL XDM Individual Profile Union Schema]을 선택하려면 **[!UICONTROL Select Schema]** 화면에서 &quot;[!UICONTROL Union]&quot; 유형의 &quot;[!UICONTROL XDM Individual Profile]&quot; 스키마를 찾습니다.

**[!UICONTROL XDM Individual Profile]** 옆의 라디오 단추를 선택한 다음 오른쪽 위 모서리에서 **[!UICONTROL Next]**&#x200B;을 클릭합니다.

![스키마 선택](../images/tutorials/segment-export-dataset/select-schema.png)

## 데이터 세트 구성

**[!UICONTROL Configure Dataset]** 화면에서 데이터 세트에 이름을 지정해야 하며 데이터 세트에 대한 설명도 제공할 수 있습니다.

**데이터 세트 이름에 대한 참고 사항:**
- 나중에 데이터세트를 라이브러리에서 쉽게 찾을 수 있도록 데이터 세트 이름은 짧고 설명이어야 합니다.
- 데이터 세트 이름은 고유해야 합니다. 즉, 나중에 다시 사용할 수 없도록 데이터 세트 이름이 구체적이어야 합니다.
- 나중에 다른 사용자가 데이터 세트를 차별화하는 데 도움이 될 수 있으므로 설명 필드를 사용하여 데이터 세트에 대한 추가 정보를 제공하는 것이 좋습니다.

데이터 세트에 이름과 설명이 있으면 **[!UICONTROL Finish]**&#x200B;을 클릭합니다.

![데이터 세트 구성](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 데이터 집합 활동

이제 빈 데이터 세트가 만들어졌고 **[!UICONTROL Datasets]** 작업 영역의 **[!UICONTROL Dataset Activity]** 탭으로 돌아갑니다. &quot;배치가 추가되지 않았습니다.&quot;라는 알림과 함께 작업 공간의 왼쪽 위 모서리에 데이터 세트 이름이 표시됩니다. 이 데이터 세트에 아직 배치를 추가하지 않았기 때문에 이 작업이 필요합니다.

데이터 집합 작업 영역의 오른쪽에는 데이터 집합 ID, 이름, 설명, 테이블 이름, 스키마, 스트리밍 및 소스 등의 새 데이터 집합과 관련된 정보가 들어 있는 **[!UICONTROL Info]** 탭이 표시됩니다. 또한 **[!UICONTROL Info]** 탭에는 데이터 세트를 만든 날짜와 마지막으로 수정한 날짜에 대한 정보도 포함되어 있습니다.

대상 세그먼트 내보내기 작업 과정을 완료하려면 이 값이 필요하므로 **[!UICONTROL Dataset ID]**&#x200B;을 참고하시기 바랍니다.

![데이터 집합 활동](../images/tutorials/segment-export-dataset/dataset-activity.png)

## 다음 단계

이제 [!DNL XDM Individual Profile Union Schema]을 기반으로 데이터 세트를 만들었으므로 데이터 세트 ID를 사용하여 [세그먼트 결과 평가 및 액세스](./evaluate-a-segment.md) 자습서를 계속 진행할 수 있습니다.

현재 세그먼트 결과 평가 자습서로 돌아가서 세그먼트 워크플로우 내보내기의 대상 구성원(](./evaluate-a-segment.md#generate-profiles)>)에 대한 프로필 생성 단계에서 선택하십시오.[
