---
keywords: Experience Platform;홈;인기 항목;날짜 범위
title: 경고 UI 안내서
description: Experience Platform 사용자 인터페이스에서 경고를 관리하는 방법을 알아봅니다.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 8d63e9fa4c7eb09ffb90edca612a6e6d44dd18fa
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# 경고 UI 안내서

Adobe Experience Platform 사용자 인터페이스를 사용하면 Adobe Experience Platform Observability Insights에서 공개한 지표를 기반으로 받은 경고 내역을 볼 수 있습니다. 또한 UI를 통해 사용 가능한 경고 규칙을 보고, 활성화하고, 비활성화하고, 구독할 수 있습니다.

>[!NOTE]
>
>Experience Platform의 경고에 대한 소개는 [경고 개요](./overview.md).

시작하려면 다음을 선택합니다. **[!UICONTROL 경고]** 왼쪽 탐색.

![경고 페이지 강조 표시 [!UICONTROL 경고] 왼쪽 탐색.](../images/alerts/ui/workspace.png)

## 경고 규칙 관리

다음 **[!UICONTROL 찾아보기]** 탭에는 경고를 트리거할 수 있는 사용 가능한 규칙이 나열됩니다.

![사용 가능한 경고 목록이에 표시 [!UICONTROL 찾아보기] 탭.](../images/alerts/ui/rules.png)

목록에서 규칙을 선택하여 해당 설명 및 해당 구성 매개 변수를 오른쪽 레일에서 확인합니다(예: 임계값 및 심각도).

![오른쪽 레일에 세부 사항을 보여주는 강조 표시된 경고 규칙입니다.](../images/alerts/ui/rule-details.png)

줄임표(**...**) 규칙 이름 옆에 있는 드롭다운에 경고를 활성화 또는 비활성화하고(현재 상태에 따라) 경고에 대한 이메일 알림을 구독 또는 구독 취소하는 컨트롤이 표시됩니다.

![선택한 줄임표에 드롭다운 메뉴가 표시됩니다.](../images/alerts/ui/disable-subscribe.png)

## 경고 구독자 관리

>[!NOTE]
>
> Adobe 사용자 ID, 외부 이메일 주소 또는 이메일 그룹 목록에 경고를 할당하려면 관리자여야 합니다.

다음 **[!UICONTROL 찾아보기]** 탭에는 경고를 트리거할 수 있는 사용 가능한 규칙이 나열됩니다.

![에 표시된 사용 가능한 경고 규칙 목록 [!UICONTROL 찾아보기] 탭.](../images/alerts/ui/rules.png)

줄임표(**...**) 규칙 이름 옆에 컨트롤이 드롭다운에 표시됩니다. 선택 **[!UICONTROL 경고 구독자 관리]**.

![타원을 선택하여 드롭다운 메뉴를 표시합니다. 다음 [!UICONTROL 경고 구독자 관리] 옵션이 강조 표시됩니다.](../images/alerts/ui/manage-alert-subscribers.png)

다음 [!UICONTROL 경고 구독자 관리] 페이지가 나타납니다. 특정 사용자에게 알림을 할당하려면 Adobe 사용자 ID, 외부 이메일 주소 또는 이메일 그룹 목록을 입력한 다음 Enter 키를 누릅니다.

>[!NOTE]
>
>여러 사용자에게 이 알림을 한 번에 보내려면 쉼표로 구분하여 사용자 ID 또는 이메일 주소 목록을 제공하십시오.

![입력된 이메일 주소를 표시하는 경고 가입자 관리 페이지입니다.](../images/alerts/ui/manage-alert-add-email.png)

이메일 주소는 나열된 현재 구독자 목록에 나타납니다. **[!UICONTROL 업데이트]**&#x200B;를 선택합니다.

![경고 가입자 관리 페이지는 가입자를 강조 표시하고 [!UICONTROL 업데이트].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

경고 알림 목록에 사용자를 추가했습니다. 이제 제출된 사용자는 아래 이미지에 표시된 대로 이 경고에 대한 이메일 알림을 받게 됩니다.

![수신된 경고 알림의 이메일 예.](../images/alerts/ui/manage-alert-subscribers-email.png)

## 이메일 경고 활성화

경고 알림은 이메일로 직접 전달될 수 있습니다.

벨 아이콘(![벨 아이콘](../images/alerts/ui/bell-icon.png)) 알림 및 공지를 표시할 오른쪽 상단 리본에 있습니다. 표시되는 드롭다운에서 cog 아이콘(![톱니바퀴 아이콘](../images/alerts/ui/cog-icon.png))을 클릭하여 Experience Cloud 환경 설정 페이지에 액세스합니다.

![벨 아이콘과 톱니바퀴 아이콘을 강조 표시하는 경고 목록입니다.](../images/alerts/ui/edit-preferences.png)

다음 **프로필** 페이지가 표시됩니다. 다음 항목 선택 **[!UICONTROL 알림]** 왼쪽 탐색에서 이메일 경고 기본 설정에 액세스합니다.

![프로필 페이지 강조 표시 [!UICONTROL 알림] 왼쪽 탐색.](../images/alerts/ui/profile.png)

다음으로 스크롤 **이메일** 페이지 하단에 있는 섹션을 선택하고 다음을 선택합니다. **[!UICONTROL 인스턴트 알림]**

![프로필 페이지에서 강조 표시된 이메일 섹션.](../images/alerts/ui/notifications.png)

구독한 모든 경고는 이제 Adobe ID 계정에 연결된 이메일 주소로 전달됩니다.

## 경고 내역 보기

다음 **[!UICONTROL 기록]** 탭에는 경고를 트리거한 규칙, 트리거된 날짜 및 해결된 날짜(해당되는 경우)를 포함하여 조직에 대해 받은 경고 내역이 표시됩니다.

![받은 경고 목록이에 표시: [!UICONTROL 기록] 탭.](../images/alerts/ui/history.png)

나열된 경고를 선택하면 경고를 트리거한 이벤트에 대한 간단한 요약을 포함하여 자세한 정보가 오른쪽 레일에 표시됩니다.

![오른쪽 레일에 세부 사항을 보여주는 강조 표시된 경고.](../images/alerts/ui/history-details.png)

## 다음 단계

이 문서에서는 Platform UI에서 경고를 보고 관리하는 방법에 대한 개요를 제공했습니다. 의 개요 보기 [가시성 통찰력](../home.md) 를 참조하십시오.
