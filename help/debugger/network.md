---
title: 네트워크 탭
description: Adobe Experience Platform Debugger에서 네트워크 탭을 사용하는 방법에 대해 알아봅니다.
keywords: debugger;experience Platform Debugger 확장 프로그램;chrome;확장 프로그램;네트워크;정보
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 62%

---

# 네트워크 탭

**네트워크** 탭은 페이지에서 수행된 모든 Adobe Experience Cloud 솔루션 호출을 집계하여 왼쪽에서 오른쪽으로 표시합니다. 표준 매개 변수는 친숙한 이름으로 자동으로 레이블이 지정되며, 동일한 역할에 따라 일반 매개 변수를 그룹화하여 정렬됩니다.

![](images/network.jpg)

이 화면은 전체 조회수의 키 값 쌍 비교에 유용합니다. Experience Cloud 방문자 ID 또는 추가 데이터 ID와 같이 통합에 사용된 매개 변수가 통합에서 일관되는지 확인할 수 있습니다.

>[!NOTE]
>
>현재 솔루션 호출에서 전달된 모든 매개 변수(예: Analytics 컨텍스트 변수, Target 사용자 지정 매개 변수 또는 Experience Cloud ID 서비스 고객 ID)가 네트워크 화면에 표시되는 것은 아닙니다.

솔루션별로 정보를 변경하려면 왼쪽 탐색 메뉴의 목록에서 보려는 솔루션을 선택합니다. 다음은 Analytics만 표시되도록 필터링하는 예입니다.

![](images/network-analytics.jpg)

모든 솔루션이 표시되도록 돌아가려면 **[!UICONTROL 네트워크]**&#x200B;를 선택하십시오.

확장된 보기를 보려면 네트워크 보기에서 항목을 선택합니다. 확장된 보기 창에서 표시된 정보를 클립보드에 복사할 수 있습니다.

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

목록을 지우려면 **[!UICONTROL 이벤트 제거]**&#x200B;를 선택하십시오.

이 화면의 정보가 포함된 Excel 파일을 다운로드하려면 **[!UICONTROL 다운로드]**&#x200B;를 선택하십시오.
