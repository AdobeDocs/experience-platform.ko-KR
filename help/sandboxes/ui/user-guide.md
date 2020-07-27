---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 샌드박스 사용 안내서
topic: user guide
translation-type: tm+mt
source-git-commit: c52d8cdbc5a4ee6fab8c2b1b284efea5f735d424
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# 샌드박스 사용 안내서

이 문서에서는 Adobe Experience Platform 사용자 인터페이스의 샌드박스와 관련된 다양한 작업을 수행하는 방법에 대해 설명합니다.

## 샌드박스 보기

Experience Platform UI에서 왼쪽 탐색 **[!UICONTROL 에서 샌드박스]** 를 클릭하여 _[!UICONTROL 샌드박스]_대시보드를 엽니다. 대시보드에는 샌드박스 유형(프로덕션 또는 개발) 및 상태(활성, 생성, 삭제 또는 실패)를 비롯하여 조직에 사용할 수 있는 모든 샌드박스가 나열됩니다.

![](../images/ui/sandboxes-tab.png)

## 샌드박스 간 전환

화면의 왼쪽 상단에 있는 **샌드박스 전환기** 컨트롤은 현재 활성 샌드박스를 표시합니다.

![](../images/ui/sandbox-selector.png)

샌드박스 간을 전환하려면 샌드박스 전환기를 클릭하고 드롭다운 목록에서 원하는 샌드박스를 선택합니다.

![](../images/ui/switch-sandbox.png)

샌드박스를 선택하면 이제 샌드박스 전환기에서 선택된 샌드박스를 사용하여 화면이 새로 고쳐집니다.

![](../images/ui/sandbox-switched.png)

## 새 샌드박스 만들기

Experience Platform에서 샌드박스를 사용하는 방법에 대한 간단한 개요를 보려면 다음 비디오를 사용하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

UI에서 새 샌드박스를 만들려면 왼쪽 탐색 **[!UICONTROL 에서 샌드박스]** 를 클릭한 다음 샌드박스 **[!UICONTROL 만들기를 클릭합니다]**.

![](../images/ui/create-sandbox-button.png)

샌드박스 _[!UICONTROL 만들기]_대화 상자가 나타나고 샌드박스의 표시 제목과 이름을 제공하라는 메시지가 표시됩니다. 표시 제목&#x200B;****은 사람이 읽을 수 있도록 하기 위한 것으로 쉽게 식별할 수 있도록 설명적이어야 합니다. 샌드박스**[!UICONTROL &#x200B;이름&#x200B;]**은 API 호출에서 사용할 수 있는 소문자 식별자이며, 따라서 고유하고 간결해야 합니다.

완료되면 **[!UICONTROL 만들기를 클릭합니다]**.

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE]
>
>비프로덕션 샌드박스 유형만 만들기로 제한되어 있으므로 **[!UICONTROL 유형]** 옵션은 &quot;비프로덕션&quot;에서 잠겨 조작될 수 없습니다.

샌드박스 만들기를 완료하면 페이지를 새로 고치면 새 샌드박스가 샌드박스 _[!UICONTROL 대시보드에 &quot;생성]_&quot;[!UICONTROL 으로]나타납니다. 새 샌드박스는 시스템에서 프로비저닝하는 데 약 15분이 소요되며 이후 샌드박스의 상태가 &quot;[!UICONTROL 활성]&quot;으로 변경됩니다.

![](../images/ui/sandbox-created.png)

## 샌드박스 재설정

>[!NOTE]
>
>이 기능은 비프로덕션 샌드박스에만 사용할 수 있습니다. 프로덕션 샌드박스를 재설정할 수 없습니다.

비프로덕션 샌드박스를 재설정하면 샌드박스의 이름과 관련 권한을 유지하면서 해당 샌드박스와 연관된 모든 리소스(스키마, 데이터 세트 등)가 삭제됩니다. 이 &quot;클린&quot; 샌드박스는 액세스 권한이 있는 사용자에 대해 동일한 이름으로 계속 사용할 수 있습니다.

UI에서 샌드박스를 재설정하려면 왼쪽 탐색 **[!UICONTROL 도구에서 샌드박스]** 를 클릭한 다음 재설정할 샌드박스를 클릭합니다. 화면 오른쪽에 표시되는 대화 상자에서 샌드박스 **[!UICONTROL 재설정을 클릭합니다]**.

![](../images/ui/reset-sandbox-button.png)

선택을 확인하라는 대화 상자가 나타납니다. Click **[!UICONTROL Reset]** to continue.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

확인 메시지가 나타나고 샌드박스의 상태가 &quot;재설정&quot;으로[!UICONTROL 변경됩니다]. 시스템에서 프로비저닝하면 상태가 &quot;[!UICONTROL 활성]&quot; 또는 &quot;[!UICONTROL 실패]&quot;로 업데이트됩니다.

![](../images/ui/sandbox-resetting.png)

## 샌드박스 삭제

>[!NOTE]
>
>이 기능은 비프로덕션 샌드박스에만 사용할 수 있습니다. 프로덕션 샌드박스를 삭제할 수 없습니다.

비프로덕션 샌드박스를 삭제하면 해당 샌드박스와 연관된 권한 등 모든 리소스가 영구적으로 제거됩니다.

UI에서 샌드박스를 삭제하려면 왼쪽 탐색 도구에서 **[!UICONTROL 샌드박스]** 를 클릭한 다음 삭제할 샌드박스를 클릭합니다. 화면 오른쪽에 표시되는 대화 상자에서 샌드박스 **[!UICONTROL 삭제를 클릭합니다]**.

![](../images/ui/delete-sandbox-button.png)

선택을 확인하라는 대화 상자가 나타납니다. Click **[!UICONTROL Delete]** to continue.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

확인 메시지가 나타나고 샌드박스 작업 영역에서 샌드박스가 __제거됩니다.

## 다음 단계

이 문서에서는 Experience Platform UI 내의 샌드박스를 관리하는 방법을 설명했습니다. 샌드박스 API를 사용하여 샌드박스를 관리하는 방법에 대한 자세한 내용은 [샌드박스 개발자 안내서를 참조하십시오](../api/getting-started.md).