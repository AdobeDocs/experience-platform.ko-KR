---
title: Insight SQL 보기
description: 프로필, 대상자, 대상 및 맞춤화된 인사이트 뒤에 있는 SQL을 보고 쿼리 편집기를 통해 요청 시 쿼리를 실행합니다.
exl-id: fd728926-c113-4593-92b1-916a02d09d41
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# 인사이트 SQL 보기

[!UICONTROL SQL 보기] 기능을 사용하여 프로필, 대상 및 사용자 지정된 인사이트 뒤에 있는 SQL을 보고 쿼리 편집기를 통해 요청 시 쿼리를 실행합니다. 40개 이상의 기존 인사이트의 SQL에서 영감을 얻어 비즈니스 요구 사항에 따라 플랫폼 데이터에서 고유한 인사이트를 도출하는 새로운 쿼리를 만들 수 있습니다.

## 대시보드 개요로 이동합니다. {#navigate-to-overview}

선택한 대시보드를 열려면 왼쪽 탐색에서 **[!UICONTROL 프로필]**, **[!UICONTROL 대상]** 또는 **[!UICONTROL 대상]**&#x200B;을 선택하십시오. 작업 영역이 자동으로 나타나지 않으면 탭 옵션에서 **[!UICONTROL 개요]**&#x200B;를 선택합니다.

또는 왼쪽 탐색 메뉴에서 **[!UICONTROL 대시보드]**&#x200B;를 선택한 다음 사용자 지정 대시보드의 이름을 선택합니다. 사용자 정의 대시보드의 개요가 나타납니다.

![강조 표시된 [!UICONTROL 프로필], [!UICONTROL 대상], [!UICONTROL 대상] 및 [!UICONTROL 대시보드]의 Experience Platform UI.](./images/view-sql/dashboard-navigation.png)

## SQL 보기 토글 {#toggle}

프로필, 대상, 대상 및 사용자 정의 대시보드의 개요에서 토글을 사용하여 기능을 활성화하거나 비활성화할 수 있습니다.

>[!NOTE]
>
>[!UICONTROL SQL 보기] 전환을 사용하면 기능을 사용하지 않도록 설정할 때까지 전역 및 위젯 수준 필터를 변경할 수 없습니다.

![[!UICONTROL SQL 보기] 토글이 강조 표시되었습니다.](./images/view-sql/view-sql-toggle.png)

각 개별 인사이트에서 [!UICONTROL SQL 보기] 텍스트를 표시하려면 토글을 활성화하십시오.

![SQL 보기]가 강조 표시된 인사이트[!UICONTROL 입니다.](./images/view-sql/insight-view-sql.png)

**[!UICONTROL SQL 보기]**&#x200B;를 선택하여 위젯의 SQL이 포함된 대화 상자를 엽니다.

## SQL 대화 상자 {#sql-dialog}

통찰력의 제목과 이를 생성하는 SQL을 포함하는 대화 상자가 나타납니다.

>[!TIP]
>
>복사 아이콘(![복사 아이콘)을 선택하여 전체 SQL 문을 클립보드에 복사할 수 있습니다.대화 상자의 오른쪽 맨 위에 있는 ](./images/view-sql/copy-icon.png)).

![강조 표시된 SQL 문이 있는 인사이트 대화 상자입니다.](./images/view-sql/sql-dialog.png)

쿼리가 미리 채워진 쿼리 편집기를 열려면 **[!UICONTROL SQL 실행]**&#x200B;을 선택하십시오.

![[!UICONTROL SQL 실행]이 강조 표시된 인사이트 대화 상자.](./images/view-sql/run-sql.png)

## 기존 SQL 편집 {#edit-sql}

쿼리 편집기가 나타납니다. 이제 보고 요구 사항에 더 적합한 방식으로 명령문을 편집하고 플랫폼 데이터를 쿼리할 수 있습니다. 새 쿼리 템플릿을 적절한 이름으로 저장합니다.

![선택한 인사이트 SQL이 미리 채워진 쿼리 편집기.](./images/view-sql/edit-sql.png)

## 다음 단계

이 문서를 읽고 나면 이제 표준 대시보드 또는 사용자 정의 대시보드 내의 통찰력을 위해 SQL에 액세스하는 방법을 이해할 수 있습니다. 아직 읽지 않았다면 [Real-time Customer Data Platform 인사이트 데이터 모델 문서](./data-models/cdp-insights-data-model-b2c.md)를 읽는 것이 좋습니다. 이 문서에는 마케팅 및 KPI 요구 사항에 맞게 Real-Time CDP 보고서의 SQL 템플릿을 사용자 지정하는 방법에 대한 통찰력이 포함되어 있습니다.
