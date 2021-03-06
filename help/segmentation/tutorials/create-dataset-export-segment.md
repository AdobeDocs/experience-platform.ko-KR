---
keywords: Experience Platform;홈;인기 항목;세그멘테이션 서비스;세그멘테이션;데이터 세트 만들기;대상 세그먼트 내보내기;세그먼트 내보내기;
solution: Experience Platform
title: 대상 세그먼트 내보내기를 위한 데이터 세트 만들기
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 Experience Platform UI를 사용하여 대상 세그먼트를 내보내는 데 사용할 수 있는 데이터 세트를 만드는 데 필요한 단계를 안내합니다.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 44d7e11e79ed0e6041ff2e4438ddb7141ae3532d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---

# 대상 세그먼트 내보내기를 위한 데이터 세트 만들기

[!DNL Adobe Experience Platform] 특정 속성에 따라 고객 프로필을 대상으로 세그먼트화할 수 있습니다. 세그먼트가 만들어지면 해당 대상을 액세스 및 작업할 수 있는 데이터 세트로 내보낼 수 있습니다. 내보내기에 성공하려면 데이터 세트를 올바르게 구성해야 합니다.

이 자습서에서는 [!DNL Experience Platform] UI를 사용하여 대상 세그먼트를 내보내는 데 사용할 수 있는 데이터 세트를 만드는 데 필요한 단계를 안내합니다.

이 자습서는 [세그먼트 결과 평가 및 액세스](./evaluate-a-segment.md)에 설명된 단계에 직접 관련되어 있습니다. 세그먼트 평가 자습서에서는 [!DNL Catalog Service] API를 사용하여 데이터 세트를 만드는 단계를 제공하지만, 이 자습서에서는 [!DNL Experience Platform] UI를 사용하여 데이터 세트를 만드는 단계를 간략하게 설명합니다.

## 시작

세그먼트를 내보내려면 데이터 세트가 [!DNL XDM Individual Profile Union Schema]을 기반으로 해야 합니다. 결합 스키마는 동일한 클래스를 공유하는 모든 스키마의 필드를 집계하는 시스템에서 생성한 읽기 전용 스키마입니다. 결합 스키마에 대한 자세한 내용은 스키마 구성](../../xdm/schema/composition.md#union)의 기본 사항에 대한 안내서를 참조하십시오.[

UI에서 결합 스키마를 보려면 왼쪽 탐색에서 **[!UICONTROL 프로필]**&#x200B;을 선택한 다음 아래 표시된 대로 **[!UICONTROL 결합 스키마]**&#x200B;를 선택합니다.

![Experience Platform UI의 결합 스키마 탭](../images/tutorials/segment-export-dataset/union.png)


## 데이터 세트 작업 공간

[!UICONTROL 데이터 세트] 작업 공간을 사용하면 조직의 모든 데이터 세트를 보고 관리할 수 있습니다.

왼쪽 탐색에서 **[!UICONTROL 데이터 세트]**&#x200B;를 선택하여 작업 영역에 액세스한 다음 **[!UICONTROL 찾아보기]**&#x200B;를 선택합니다. 이 탭에는 데이터 세트 목록과 세부 정보가 표시됩니다. 각 열의 너비에 따라 모든 열을 보려면 왼쪽이나 오른쪽으로 스크롤해야 할 수 있습니다.

>[!NOTE]
>
>검색 창 옆의 필터 아이콘을 선택하여 필터링 기능을 사용하여 [!DNL Real-time Customer Profile]에 대해 활성화된 데이터 세트만 확인합니다.

![데이터 세트 보기](../images/tutorials/segment-export-dataset/browse.png)

## 데이터 집합 만들기

데이터 집합을 만들려면 **[!UICONTROL 데이터 집합 만들기]**&#x200B;를 선택합니다.

![데이터 집합 만들기 를 선택합니다](../images/tutorials/segment-export-dataset/create-dataset.png)

다음 화면에서 **[!UICONTROL 스키마에서 데이터 집합 만들기]**&#x200B;를 선택합니다.

![데이터 소스 선택](../images/tutorials/segment-export-dataset/create-from-schema.png)

## XDM 개별 프로필 결합 스키마 선택

데이터 세트에 사용할 [!DNL XDM Individual Profile Union Schema]을(를) 선택하려면 **[!UICONTROL 스키마 선택]** 화면에서 &quot;[!UICONTROL XDM 개별 프로필]&quot; 스키마를 찾습니다. 스키마를 선택하면 오른쪽 레일의 **[!UICONTROL API 사용]** 아래에 있는 결합 스키마인지 확인할 수 있습니다. [!UICONTROL 스키마] 경로가 `_union`로 끝나는 경우 결합 스키마입니다.

>[!NOTE]
>
>정의 기준으로 결합 스키마가 실시간 고객 프로필에 참여하지만 기존 스키마와 동일한 방식으로 프로필에 대해 활성화되어 있지 않으므로 &quot;활성화되지 않음&quot;으로 표시됩니다.

**[!UICONTROL XDM 개별 프로필]** 옆의 라디오 단추를 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![스키마 선택](../images/tutorials/segment-export-dataset/select-schema.png)

## 데이터 세트 구성

다음 화면에서 데이터 세트에 이름을 지정해야 합니다. 선택적 설명을 추가할 수도 있습니다.

**데이터 집합 이름에 대한 참고 사항:**
* 데이터 세트 이름은 나중에 라이브러리에서 데이터 세트를 쉽게 찾을 수 있도록 짧고 설명적이어야 합니다.
* 데이터 세트 이름은 고유해야 합니다. 즉, 나중에 다시 사용할 수 없도록 충분히 구체적이어야 합니다.
* 설명 필드를 사용하여 데이터 세트에 대한 추가 정보를 제공하는 것이 가장 좋습니다. 이렇게 하면 다른 사용자가 나중에 데이터 세트를 구분할 수 있기 때문입니다.

데이터 집합에 이름과 설명이 있으면 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

![데이터 세트 구성](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 데이터 집합 활동

데이터 세트가 만들어지면 해당 데이터 세트에 대한 활동 페이지가 표시됩니다. 작업 공간의 왼쪽 위 모서리에 &quot;일괄 처리가 추가되지 않음&quot;이라는 알림과 함께 데이터 세트 이름이 표시됩니다. 이 데이터 세트에 일괄 처리를 아직 추가하지 않았기 때문에 발생할 수 있습니다.

오른쪽 레일에는 데이터 세트 ID, 이름, 설명, 스키마 등과 같은 새로운 데이터 세트에 대한 정보가 포함되어 있습니다. 대상 세그먼트 내보내기 워크플로우를 완료하려면 이 값이 필요하므로 **[!UICONTROL 데이터 세트 ID]**&#x200B;를 기록해 두십시오.

![데이터 집합 활동](../images/tutorials/segment-export-dataset/activity.png)

## 다음 단계

이제 [!DNL XDM Individual Profile Union Schema] 을 기반으로 데이터 세트를 만들었으므로 데이터 세트 ID를 사용하여 [세그먼트 결과 평가 및 액세스](./evaluate-a-segment.md) 자습서를 계속 진행할 수 있습니다.

현재, 세그먼트 결과 평가 자습서로 돌아가서 세그먼트 워크플로우 내보내기의 대상 구성원](./evaluate-a-segment.md#generate-profiles) 단계의 프로필 생성 [에서 선택하십시오.
