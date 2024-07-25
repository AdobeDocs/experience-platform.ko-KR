---
keywords: Experience Platform;홈;인기 항목; 데이터 흐름 삭제
description: 소스 작업 영역에서는 오류가 있거나 더 이상 사용되지 않는 기존 일괄 처리 및 스트리밍 데이터 흐름을 삭제할 수 있는 기능을 제공합니다.
solution: Experience Platform
title: UI에서 데이터 흐름 삭제
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 1%

---

# UI에서 데이터 흐름 삭제

[!UICONTROL 소스] 작업 영역을 사용하면 오류가 있거나 더 이상 사용되지 않는 기존 일괄 처리 및 스트리밍 데이터 흐름을 삭제할 수 있습니다.

이 자습서에서는 [!UICONTROL 소스] 작업 영역을 사용하여 데이터 흐름을 삭제하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [원본](../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
- [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

## 데이터 흐름 삭제

[Experience Platform UI](https://platform.adobe.com)의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스한 다음 상단 헤더에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택합니다.

![카탈로그](../../images/tutorials/delete/catalog.png)

**[!UICONTROL 데이터 흐름]** 페이지가 나타납니다. 이 페이지에는 대상 데이터 세트, 소스, 계정 이름 및 생성 날짜에 대한 정보를 포함하여 볼 수 있는 데이터 흐름 목록이 있습니다.

왼쪽 상단의 필터 아이콘(![filter-icon](/help/images/icons/filter.png))을 선택하여 정렬 패널을 시작합니다.

![데이터 흐름](../../images/tutorials/delete/dataflows.png)

정렬 패널은 모든 소스의 목록을 제공합니다. 목록에서 둘 이상의 소스를 선택하여 선택한 특정 소스와 연관된 필터링된 데이터 흐름 선택에 액세스할 수 있습니다.

작업할 소스를 선택하여 기존 데이터 흐름 목록을 확인합니다. 삭제할 데이터 흐름을 식별했으면 데이터 흐름 이름 옆의 생략 부호(`...`)를 선택합니다.

![데이터 흐름 필터](../../images/tutorials/delete/dataflows-filter.png)

드롭다운 메뉴가 나타나며 데이터 흐름의 일정을 편집하거나, 데이터 흐름을 비활성화하거나, 완전히 삭제할 수 있는 옵션을 제공합니다.

데이터 흐름을 삭제하려면 **[!UICONTROL 삭제]**&#x200B;를 선택하십시오.

![삭제](../../images/tutorials/delete/delete.png)

마지막 확인 대화 상자가 나타납니다. **[!UICONTROL 삭제]**&#x200B;를 선택하여 프로세스를 완료합니다.

![확인](../../images/tutorials/delete/confirm.png)

잠시 후 화면 하단에 성공적인 삭제를 확인하는 확인 상자가 나타납니다.

![확인](../../images/tutorials/delete/confirmed.png)

## 다음 단계

이 자습서에 따라 [!UICONTROL 소스] 작업 영역을 사용하여 기존 데이터 흐름을 삭제했습니다.

API 호출을 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 [흐름 서비스 API를 사용하여 데이터 흐름 삭제](../../tutorials/api/delete-dataflows.md)에 대한 자습서를 참조하십시오.
