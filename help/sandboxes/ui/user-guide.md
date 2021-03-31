---
keywords: Experience Platform;홈;인기 있는 항목;샌드박스 사용 안내서;샌드박스 안내서
solution: Experience Platform
title: 샌드박스 UI 안내서
topic: 사용 안내서
description: 이 문서에서는 Adobe Experience Platform 사용자 인터페이스의 샌드박스와 관련된 다양한 작업을 수행하는 방법에 대해 설명합니다.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---


# 샌드박스 UI 안내서

이 문서에서는 Adobe Experience Platform 사용자 인터페이스의 샌드박스와 관련된 다양한 작업을 수행하는 방법에 대해 설명합니다.

## 샌드박스 보기

Experience Platform UI의 왼쪽 탐색 메뉴에서 **[!UICONTROL Sandboxes]**&#x200B;을 선택하여 **[!UICONTROL Sandboxes]** 대시보드를 엽니다. 대시보드에는 샌드박스 유형(프로덕션 또는 개발) 및 상태(활성, 생성, 삭제 또는 실패)를 비롯하여 조직에 사용할 수 있는 모든 샌드박스가 나열됩니다.

![](../images/ui/view-sandboxes.png)

## 샌드박스 간 전환

화면 왼쪽 상단에 있는 **샌드박스 전환기** 컨트롤은 현재 활성 샌드박스를 표시합니다.

![](../images/ui/sandbox-switcher.png)

샌드박스 사이를 전환하려면 샌드박스 전환기를 선택하고 드롭다운 목록에서 원하는 샌드박스를 선택합니다.

![](../images/ui/switcher-menu.png)

샌드박스가 선택되면 이제 샌드박스 전환기에서 선택된 샌드박스로 화면이 새로 고쳐집니다.

![](../images/ui/switched.png)

## 샌드박스의 세션

샌드박스 전환기 메뉴에서 검색 기능을 사용하여 사용할 수 있는 샌드박스 목록을 탐색할 수 있습니다. 조직에서 사용할 수 있는 모든 샌드박스를 통해 필터링하기 위해 액세스할 샌드박스 이름을 입력합니다.

![](../images/ui/sandbox-search.png)

## 새 샌드박스 만들기

Experience Platform에서 샌드박스를 사용하는 방법에 대한 간단한 개요를 보려면 다음 비디오를 사용하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

UI에서 새 샌드박스를 만들려면 화면 오른쪽 상단에 있는 **[!UICONTROL Create Sandbox]** 버튼을 선택합니다.

![](../images/ui/create-sandbox.png)

샌드박스의 표시 제목과 이름을 제공하라는 **[!UICONTROL Create Sandbox]** 대화 상자가 나타납니다. **표시 제목**&#x200B;은 사람이 읽을 수 있도록 만들어진 것으로 쉽게 식별할 수 있도록 설명적이어야 합니다. 샌드박스 **[!UICONTROL Name]**&#x200B;는 API 호출에 사용할 수 있는 소문자로 모두 구분되므로 고유하고 간결해야 합니다. 샌드박스 **[!UICONTROL Name]**&#x200B;은(는) 영숫자 문자와 하이픈 **(-)**&#x200B;만 포함해야 하며 문자로 시작해야 하며 최대 256자까지 포함해야 합니다.

완료되면 **[!UICONTROL Create]**&#x200B;을 선택합니다.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>비프로덕션 샌드박스 유형만 만드는 것으로 제한되므로 **[!UICONTROL type]** 옵션은 &quot;비프로덕션&quot;에서 잠겨 조작될 수 없습니다.

샌드박스 만들기를 완료하면 페이지를 새로 고치면 새 샌드박스가 &quot;[!UICONTROL Creating]&quot; 상태로 **[!UICONTROL Sandboxes]** 대시보드에 나타납니다. 새 샌드박스의 상태가 &quot;[!UICONTROL Active]&quot;으로 변경된 후 시스템에서 프로비저닝하는 데 약 15분이 소요됩니다.

![](../images/ui/creating.png)

## 샌드박스 재설정

>[!NOTE]
>
>이 기능은 비프로덕션 샌드박스에만 사용할 수 있습니다. 프로덕션 샌드박스를 재설정할 수 없습니다.

비프로덕션 샌드박스를 재설정하면 샌드박스의 이름 및 관련 권한을 유지하면서 해당 샌드박스와 연관된 모든 리소스(스키마, 데이터 집합 등)가 삭제됩니다. 이 &quot;클린&quot; 샌드박스는 액세스 권한이 있는 사용자에 대해 동일한 이름으로 계속 사용할 수 있습니다.

UI에서 샌드박스를 재설정하려면 왼쪽 탐색 도구에서 **[!UICONTROL Sandboxes]**&#x200B;을 선택한 다음 재설정할 샌드박스를 선택합니다. 화면 오른쪽에 표시되는 대화 상자에서 **[!UICONTROL Reset Sandbox]**&#x200B;을 선택합니다.

![](../images/ui/reset-sandbox.png)

선택을 확인하라는 대화 상자가 나타납니다. 계속하려면 **[!UICONTROL Reset]**&#x200B;을 선택합니다.

![](../images/ui/reset-confirm.png)

확인 메시지가 나타나고 샌드박스의 상태가 &quot;**[!UICONTROL Resetting]&quot;**&#x200B;로 변경됩니다. 시스템에 의해 프로비저닝되면 해당 상태는 **&quot;[!UICONTROL Active]&quot;** 또는 **&quot;[!UICONTROL Failed]&quot;**&#x200B;로 업데이트됩니다.

![](../images/ui/resetting.png)

## 샌드박스 삭제

>[!NOTE]
>
>이 기능은 비프로덕션 샌드박스에만 사용할 수 있습니다. 프로덕션 샌드박스는 삭제할 수 없습니다.

비프로덕션 샌드박스를 삭제하면 권한을 포함하여 해당 샌드박스와 연결된 모든 리소스가 영구적으로 제거됩니다.

UI에서 샌드박스를 삭제하려면 왼쪽 탐색 도구에서 **[!UICONTROL Sandboxes]**&#x200B;을 선택한 다음 삭제할 샌드박스를 선택합니다. 화면 오른쪽에 표시되는 대화 상자에서 **[!UICONTROL Delete Sandbox]**&#x200B;을 선택합니다.

![](../images/ui/delete-sandbox.png)

선택을 확인하라는 대화 상자가 나타납니다. 계속하려면 **[!UICONTROL Delete]**&#x200B;을 선택합니다.

![](../images/ui/delete-confirm.png)

확인 메시지가 나타나고 샌드박스가 **[!UICONTROL Sandboxes]** 작업 영역에서 제거됩니다.

## 다음 단계

이 문서에서는 Experience Platform UI 내의 샌드박스를 관리하는 방법을 설명했습니다. 샌드박스 API를 사용하여 샌드박스를 관리하는 방법에 대한 자세한 내용은 [샌드박스 개발자 안내서](../api/getting-started.md)를 참조하십시오.