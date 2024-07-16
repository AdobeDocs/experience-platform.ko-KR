---
solution: Experience Platform
title: 대상자 내보내기를 위한 데이터 세트 만들기
type: Tutorial
description: Experience Platform UI를 사용하여 대상을 내보내는 데 사용할 수 있는 데이터 세트를 만드는 방법을 알아봅니다.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# 대상자 내보내기를 위한 데이터 세트 만들기

[!DNL Adobe Experience Platform]을(를) 사용하면 고객 프로필을 특정 특성에 따라 대상으로 세그먼트화할 수 있습니다. 세그먼트 정의가 생성되면 결과 대상을 액세스하고 작업할 수 있는 데이터 세트로 내보낼 수 있습니다. 내보내기에 성공하려면 데이터 세트를 올바르게 구성해야 합니다.

이 자습서에서는 [!DNL Experience Platform] UI를 사용하여 대상을 내보내는 데 사용할 수 있는 데이터 집합을 만드는 데 필요한 단계를 안내합니다.

이 자습서는 [세그먼테이션 결과 평가 및 액세스](./evaluate-a-segment.md)에 대한 자습서에 설명된 단계와 직접적으로 관련되어 있습니다. 세그먼트 정의 평가 튜토리얼에서는 [!DNL Catalog Service] API를 사용하여 데이터 집합을 만드는 단계를 제공하는 반면, 이 튜토리얼에서는 [!DNL Experience Platform] UI를 사용하여 데이터 집합을 만드는 단계를 간략하게 설명합니다.

## 시작하기

대상을 내보내려면 데이터 집합이 [!DNL XDM Individual Profile Union Schema]을(를) 기반으로 해야 합니다. 유니온 스키마는 동일한 클래스를 공유하는 모든 스키마의 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다. 유니온 스키마에 대한 자세한 내용은 [스키마 컴포지션의 기본 사항](../../xdm/schema/composition.md#union)에 대한 안내서를 참조하십시오.

UI에서 유니온 스키마를 보려면 아래와 같이 왼쪽 탐색에서 **[!UICONTROL 프로필]**&#x200B;을 선택한 다음 **[!UICONTROL 유니온 스키마]**&#x200B;을 선택하십시오.

![유니온 스키마 탭이 강조 표시되어 있습니다.](../images/tutorials/segment-export-dataset/union.png)

## 데이터 세트 작업 공간

[!UICONTROL 데이터 세트] 작업 영역에서는 조직의 모든 데이터 세트를 보고 관리할 수 있습니다.

작업 영역에 액세스하려면 왼쪽 탐색에서 **[!UICONTROL 데이터 세트]**&#x200B;를 선택한 다음 **[!UICONTROL 찾아보기]**&#x200B;를 선택하십시오. 이 탭에는 데이터 세트 목록과 세부 정보가 표시됩니다. 각 열의 너비에 따라 모든 열을 보려면 왼쪽 또는 오른쪽으로 스크롤해야 할 수 있습니다.

>[!NOTE]
>
>[!DNL Real-Time Customer Profile]에 대해 활성화된 데이터 세트만 보려면 필터링 기능을 사용하려면 검색 창 옆의 필터 아이콘을 선택하십시오.

![데이터 세트 작업 영역이 표시됩니다.](../images/tutorials/segment-export-dataset/browse.png)

## 데이터 세트 만들기

데이터 집합을 만들려면 **[!UICONTROL 데이터 집합 만들기]**&#x200B;를 선택하십시오.

![데이터 집합 만들기 단추가 강조 표시되어 있습니다.](../images/tutorials/segment-export-dataset/create-dataset.png)

다음 화면에서는 **[!UICONTROL 스키마에서 데이터 집합 만들기]**&#x200B;를 선택합니다.

![스키마에서 데이터 집합 만들기 옵션이 강조 표시되어 있습니다.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## XDM 개별 프로필 통합 스키마 선택

데이터 세트에 사용할 [!DNL XDM Individual Profile Union Schema]을(를) 선택하려면 **[!UICONTROL 스키마 선택]** 화면에서 &quot;[!UICONTROL XDM 개인 프로필]&quot; 스키마를 찾으십시오. 스키마를 선택하면 해당 스키마가 오른쪽 레일의 **[!UICONTROL API 사용]**&#x200B;에서 유니온 스키마인지 확인할 수 있습니다. [!UICONTROL 스키마] 경로가 `_union`(으)로 끝나는 경우 유니온 스키마입니다.

>[!NOTE]
>
>공용 구조체 스키마는 실시간 고객 프로필에 정의로 참여하지만 기존 스키마와 동일한 방식으로 프로필에 대해 활성화되지 않아 &quot;활성화되지 않음&quot;으로 표시됩니다.

**[!UICONTROL XDM 개별 프로필]** 옆에 있는 라디오 단추를 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![XDM 개인 프로필 스키마가 강조 표시됩니다.](../images/tutorials/segment-export-dataset/select-schema.png)

## 데이터 세트 구성

다음 화면에서는 데이터 세트에 이름을 지정해야 합니다. 원할 경우 설명을 추가할 수도 있습니다.

**데이터 집합 이름에 대한 참고 사항:**

* 데이터 세트 이름은 짧고 설명적이어야 나중에 라이브러리에서 데이터 세트를 쉽게 찾을 수 있습니다.
* 데이터 세트 이름은 고유해야 합니다. 즉, 나중에 재사용되지 않을 만큼 구체적이어야 합니다.
* 향후 다른 사용자가 데이터 세트를 구분하는 데 도움이 될 수 있으므로 설명 필드를 사용하여 데이터 세트에 대한 추가 정보를 제공해야 합니다.

데이터 집합에 이름과 설명이 있으면 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

![데이터 집합 구성 페이지가 표시됩니다. 구성 옵션이 강조 표시됩니다.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 데이터 세트 활동

데이터 세트가 만들어지면 해당 데이터 세트에 대한 활동 페이지가 표시됩니다. 작업 영역의 왼쪽 상단 모서리에 &quot;추가된 일괄 처리가 없습니다.&quot;라는 알림과 함께 데이터 세트 이름이 표시됩니다. 이 데이터 세트에 아직 배치를 추가하지 않았기 때문에 이는 예상되었습니다.

오른쪽 레일에는 데이터 세트 ID, 이름, 설명, 스키마 등과 같은 새 데이터 세트와 관련된 정보가 포함되어 있습니다. 대상 내보내기 워크플로우를 완료하려면 이 값이 필요하므로 **[!UICONTROL 데이터 세트 ID]**&#x200B;을(를) 메모해 두십시오.

![데이터 집합 활동 페이지가 표시됩니다. 데이터 세트 ID는 다음 단계를 위해 이 값을 기록해야 하므로 강조 표시됩니다.](../images/tutorials/segment-export-dataset/activity.png)

## 다음 단계

[!DNL XDM Individual Profile Union Schema]을(를) 기반으로 데이터 세트를 만들었으므로 이제 데이터 세트 ID를 사용하여 [세그먼트 정의 결과 평가 및 액세스](./evaluate-a-segment.md) 자습서를 계속할 수 있습니다.

이제 평가 세그먼트 정의 결과 튜토리얼로 돌아가서 대상 워크플로우 내보내기의 [대상 구성원에 대한 프로필 생성](./evaluate-a-segment.md#generate-profiles) 단계에서 선택하십시오.
