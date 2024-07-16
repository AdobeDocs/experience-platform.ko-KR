---
title: Data Lifecycle UI 안내서
description: Adobe Experience Platform 사용자 인터페이스에서 데이터 라이프사이클 작업을 관리하는 방법을 알아봅니다.
exl-id: 7199151a-5390-4150-8a1d-daf53b7a1f5b
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 36%

---

# 데이터 라이프사이클 UI 안내서 {#lifecycle-ui-guide}

>[!CONTEXTUALHELP]
>id="platform_hygiene_privacyconsole_consumer"
>title="데이터 라이프사이클 요청 상태"
>abstract="이 위젯은 생성, 실패 및 완료된 데이터 라이프사이클 레코드 삭제 작업의 총 개수를 보여 줍니다. 데이터 라이프사이클 프로세스에 대한 자세한 내용을 보려면 왼쪽 탐색 메뉴의 **데이터 라이프사이클**&#x200B;를 선택합니다."

>[!CONTEXTUALHELP]
>id="platform_hygiene_privacyconsole_recents"
>title="최근 데이터 라이프사이클 작업 주문"
>abstract="이 위젯은 오른쪽 상단에서 선택한 옵션에 따라 가장 최근에 생성 또는 업데이트된 5개의 데이터 라이프사이클 작업 주문을 보여 줍니다. 데이터 라이프사이클 프로세스에 대한 자세한 내용을 보려면 왼쪽 탐색 메뉴의 **데이터 라이프사이클**&#x200B;를 선택합니다."

Adobe Experience Platform UI의 **[!UICONTROL 데이터 수명 주기]** 작업 영역을 사용하면 레코드 삭제 및 데이터 세트 만료 일정 예약 등 다양한 데이터 수명 주기 관리 작업을 만들고 모니터링할 수 있습니다.

이 안내서에서는 Platform UI에서 데이터 라이프사이클 작업을 관리하는 방법을 다룹니다. API 호출을 사용하여 이러한 작업을 수행하는 방법에 대한 자세한 내용은 [데이터 위생 API 안내서](../api/overview.md)를 참조하십시오.

작업 영역에 액세스하려면 왼쪽 탐색에서 **데이터 수명 주기**&#x200B;를 선택하십시오.

![Platform UI의 [!UICONTROL 데이터 주기] 작업 영역에서 [!UICONTROL 데이터 주기]가 왼쪽 탐색에서 강조 표시됩니다.](../images/ui/overview/home.png)

여기에서 기존 작업 주문을 탐색하고 새 데이터 라이프사이클 작업을 구성할 수 있습니다. 자세한 내용은 이 안내서의 다음 섹션을 참조하십시오.

* [기존 작업 주문 찾아보기](./browse.md)
* [데이터 세트 만료 요청 만들기](./dataset-expiration.md)
* [레코드 삭제 요청 만들기](./record-delete.md)
