---
keywords: Experience Platform;홈;인기 있는 주제 데이터 흐름 삭제
description: 소스 작업 영역은 오류가 있거나 더 이상 사용되지 않는 기존 일괄 처리 및 스트리밍 데이터 흐름을 삭제하는 기능을 제공합니다.
solution: Experience Platform
title: UI에서 데이터 흐름 삭제
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# UI에서 데이터 흐름 삭제

다음 [!UICONTROL 소스] 작업 공간을 사용하면 오류가 있거나 더 이상 사용되지 않는 기존 일괄 처리 및 스트리밍 데이터 흐름을 삭제할 수 있습니다.

이 자습서에서는 [!UICONTROL 소스] 작업 공간.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [소스](../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
- [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

## 데이터 흐름 삭제

에서 [Experience Platform UI](https://platform.adobe.com), 선택 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 영역, **[!UICONTROL 데이터 흐름]** 상단 헤더에서

![카탈로그](../../images/tutorials/delete/catalog.png)

다음 **[!UICONTROL 데이터 흐름]** 페이지가 나타납니다. 이 페이지에는 대상 데이터 세트, 소스, 계정 이름 및 작성 날짜에 대한 정보를 포함하여 볼 수 있는 데이터 흐름 목록이 있습니다.

필터 아이콘(![filter-icon](../../images/tutorials/delete/filter.png))을 클릭하여 정렬 패널을 시작합니다.

![데이터 흐름](../../images/tutorials/delete/dataflows.png)

정렬 패널에서는 모든 소스 목록을 제공합니다. 목록에서 두 개 이상의 소스를 선택하여 선택한 특정 소스와 연결된 필터링된 데이터 흐름 선택에 액세스할 수 있습니다.

작업할 소스를 선택하여 기존 데이터 흐름 목록을 확인합니다. 삭제할 데이터 흐름을 식별한 후 줄임표( )를 선택합니다`...`)을 데이터 흐름 이름 옆에 추가합니다.

![데이터 흐름 필터](../../images/tutorials/delete/dataflows-filter.png)

드롭다운 메뉴가 나타나고 데이터 흐름의 예약을 편집하거나 데이터 흐름을 비활성화하거나 완전히 삭제할 수 있는 옵션을 제공합니다.

선택 **[!UICONTROL 삭제]** 데이터 흐름을 삭제하려면

![delete](../../images/tutorials/delete/delete.png)

최종 확인 대화 상자가 나타납니다. 선택 **[!UICONTROL 삭제]** 프로세스를 완료합니다.

![confirm](../../images/tutorials/delete/confirm.png)

잠시 후 화면 하단에 확인 상자가 표시되어 성공적인 삭제를 확인합니다.

![확인됨](../../images/tutorials/delete/confirmed.png)

## 다음 단계

이 자습서를 따라 다음을 성공적으로 사용했습니다. [!UICONTROL 소스] 기존 데이터 흐름을 삭제하는 작업 공간입니다.

다음에서 자습서를 참조하십시오. [흐름 서비스 API를 사용하여 데이터 흐름 삭제](../../tutorials/api/delete-dataflows.md) api 호출을 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계입니다.
