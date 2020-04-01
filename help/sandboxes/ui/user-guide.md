---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 샌드박스 사용 안내서
topic: user guide
translation-type: tm+mt
source-git-commit: 6438c1841889ff345e1ebaedabfed0531c1f97f9

---


# 샌드박스 사용 안내서

이 문서에서는 Adobe Experience Platform 사용자 인터페이스에서 샌드박스와 관련된 다양한 작업을 수행하는 방법에 대해 설명합니다.

## 샌드박스 보기

경험 플랫폼 UI에서 왼쪽 **탐색의 샌드박스를** 클릭하여 샌드박스 _대시보드를 엽니다_ . 대시보드에는 샌드박스 유형(프로덕션 또는 개발) 및 상태(활성, 생성, 삭제 또는 실패)를 비롯하여 조직에 사용할 수 있는 모든 샌드박스가 나열됩니다.

![](../images/ui/sandboxes-tab.png)

## 샌드박스 간 전환

화면의 왼쪽 상단에 있는 **샌드박스 전환기** 컨트롤은 현재 활성 샌드박스를 표시합니다.

![](../images/ui/sandbox-selector.png)

샌드박스 간을 전환하려면 샌드박스 전환기를 클릭하고 드롭다운 목록에서 원하는 샌드박스를 선택합니다.

![](../images/ui/switch-sandbox.png)

샌드박스를 선택하면 이제 샌드박스 전환기에서 선택한 샌드박스로 화면이 새로 고쳐집니다.

![](../images/ui/sandbox-switched.png)

## 새 샌드박스 만들기

UI에서 새 샌드박스를 만들려면 왼쪽 탐색 **도구에서 샌드박스를** 클릭한 다음 샌드박스 **만들기를 클릭합니다**.

![](../images/ui/create-sandbox-button.png)

샌드박스 _만들기_ 대화 상자가 표시되어 샌드박스의 표시 제목과 이름을 제공하라는 메시지가 나타납니다. 표시 **제목은** 사람이 읽을 수 있도록 작성되었으며 쉽게 식별할 수 있도록 설명적이어야 합니다. 샌드박스 **이름은** API 호출에 사용할 수 있도록 모두 소문자로 식별되므로 고유하고 간결해야 합니다.

완료되면 만들기를 **클릭합니다**.

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE] 비프로덕션 샌드박스 유형만 만들 수 있으므로 **유형** 옵션은 &quot;비프로덕션&quot;에서 잠겨서 조작할 수 없습니다.

샌드박스 만들기를 완료하면 페이지를 새로 고치면 새 샌드박스가 샌드박스 _대시보드에_ &quot;만들기&quot; 상태로 나타납니다. 새 샌드박스는 시스템에서 프로비전되는 데 약 15분이 소요되며, 그 후 상태는 &quot;활성&quot;으로 변경됩니다.

![](../images/ui/sandbox-created.png)

## 샌드박스 재설정

>[!NOTE] 이 기능은 비프로덕션 샌드박스에만 사용할 수 있습니다. 프로덕션 샌드박스를 재설정할 수 없습니다.

비프로덕션 샌드박스를 재설정하면 샌드박스의 이름 및 관련 권한을 유지하면서 해당 샌드박스와 연결된 모든 리소스(스키마, 데이터 집합 등)가 삭제됩니다. 이 &quot;클린&quot; 샌드박스는 액세스 권한이 있는 사용자에 대해 동일한 이름으로 계속 사용할 수 있습니다.

UI에서 샌드박스를 재설정하려면 왼쪽 탐색 **도구에서 샌드박스를** 클릭한 다음 재설정할 샌드박스를 클릭합니다. 화면의 오른쪽에 표시되는 대화 상자에서 샌드박스 **재설정을 클릭합니다**.

![](../images/ui/reset-sandbox-button.png)

선택을 확인하라는 대화 상자가 나타납니다. Click **Reset** to continue.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

확인 메시지가 나타나고 샌드박스의 상태가 &quot;재설정&quot;으로 변경됩니다. 시스템에서 프로비저닝한 후 상태가 &quot;활성&quot; 또는 &quot;실패&quot;로 업데이트됩니다.

![](../images/ui/sandbox-resetting.png)

## 샌드박스 삭제

>[!NOTE] 이 기능은 비프로덕션 샌드박스에만 사용할 수 있습니다. 프로덕션 샌드박스를 삭제할 수 없습니다.

비프로덕션 샌드박스를 삭제하면 해당 샌드박스와 연결된 권한 등 모든 리소스가 영구적으로 제거됩니다.

UI에서 샌드박스를 삭제하려면 왼쪽 **탐색 도구에서 샌드박스를** 클릭한 다음 삭제할 샌드박스를 클릭합니다. 화면의 오른쪽에 표시되는 대화 상자에서 샌드박스 **삭제를 클릭합니다**.

![](../images/ui/delete-sandbox-button.png)

선택을 확인하라는 대화 상자가 나타납니다. Click **Delete** to continue.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

확인 메시지가 나타나고 샌드박스 작업 영역에서 샌드박스가 _제거됩니다_ .

## 다음 단계

이 문서에서는 Experience Platform UI 내에서 샌드박스를 관리하는 방법을 설명했습니다. 샌드박스 API를 사용하여 샌드박스를 관리하는 방법에 대한 자세한 내용은 [샌드박스 개발자 안내서를](../api/getting-started.md)참조하십시오.