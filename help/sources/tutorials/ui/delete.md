---
keywords: Experience Platform;home;popular topics; delete dataflows
description: 소스 작업 영역에서는 오류가 있거나 사용되지 않는 기존 일괄 처리 및 스트리밍 데이터 흐름을 삭제할 수 있습니다.
solution: Experience Platform
title: 데이터 흐름 삭제
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 7cb5862112c80e386e697aa2bd503abe49f11a3f
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 1%

---


# UI에서 데이터 흐름 삭제

소스 작업 [!UICONTROL 공간] 을 사용하면 오류를 포함하거나 오래된 데이터 흐름을 삭제할 수 있습니다.

이 자습서에서는 소스 작업 영역을 사용하여 데이터 흐름을 삭제하는 [!UICONTROL 단계를] 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [소스](../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 [!DNL Platform] 있습니다.
- [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 데이터 흐름 삭제

Experience Platform UI의 [왼쪽 탐색](https://platform.adobe.com)에서 **** 소스 [!UICONTROL 를 선택하여] 소스 작업 영역에 **[!UICONTROL 액세스한 다음 맨 위 헤더에서]** 데이터 흐름을 선택합니다.

![카탈로그](../../images/tutorials/delete/catalog.png)

데이터 흐름 **[!UICONTROL 페이지가]** 나타납니다. 이 페이지에서는 대상 데이터 세트, 소스, 계정 이름 및 작성 날짜에 대한 정보를 비롯하여 볼 수 있는 데이터 흐름 목록이 있습니다.

왼쪽 상단에 있는 필터 아이콘(![필터 아이콘](../../images/tutorials/delete/filter.png))을 선택하여 정렬 패널을 실행합니다.

![데이터 흐름](../../images/tutorials/delete/dataflows.png)

정렬 패널은 모든 소스 목록을 제공합니다. 목록에서 둘 이상의 소스를 선택하여 선택한 특정 소스와 관련된 필터링된 데이터 흐름 선택 항목에 액세스할 수 있습니다.

작업할 소스를 선택하여 기존 데이터 흐름 목록을 확인합니다. 삭제할 데이터 흐름을 식별한 후 데이터 흐름 이름 옆에 있는 줄임표(`...`)를 선택합니다.

![데이터 흐름 필터](../../images/tutorials/delete/dataflows-filter.png)

데이터 흐름 예약을 편집하거나 데이터 흐름을 비활성화하거나 완전히 삭제할 수 있는 옵션을 제공하는 드롭다운 메뉴가 나타납니다.

데이터 흐름 **[!UICONTROL 을]** 삭제하려면 삭제를 선택합니다.

![delete](../../images/tutorials/delete/delete.png)

최종 확인 대화 상자가 나타납니다. 삭제를 **[!UICONTROL 선택하여]** 프로세스를 완료합니다.

![confirm](../../images/tutorials/delete/confirm.png)

잠시 후 화면 하단에 확인 상자가 표시되어 성공적인 삭제를 확인합니다.

![확인](../../images/tutorials/delete/confirmed.png)

## 다음 단계

이 튜토리얼을 따라 소스 작업 [!UICONTROL 영역을] 사용하여 기존 데이터 흐름을 삭제합니다.

API [호출을 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 Flow Service API를](../../tutorials/api/delete-dataflows.md) 사용하여 데이터 흐름 삭제에 대한 자습서를 참조하십시오.