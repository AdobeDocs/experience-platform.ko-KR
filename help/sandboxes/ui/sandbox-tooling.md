---
title: 샌드박스 도구
description: 샌드박스 간에 샌드박스 구성을 원활하게 내보내고 가져옵니다.
source-git-commit: 900cb35f6cb758f145904666c709c60dc760eff2
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 8%

---


# [!BADGE 베타] 샌드박스 도구

>[!IMPORTANT]
>
>다음 **샌드박스 도구** 아래 설명된 기능은 일부 베타 고객만 사용할 수 있습니다.

>[!NOTE]
>
>샌드박스 툴링은 두 가지를 모두 지원하는 기본 기능입니다 [!DNL Real-Time Customer Data Platform] 및 [!DNL Journey Optimizer] 개발 주기 효율성 및 구성 정확도를 개선합니다.<br><br>샌드박스 도구 기능을 사용하려면 다음 두 가지 역할 기반 액세스 제어 권한이 필요합니다.<br>- `manage-sandbox` 또는 `view-sandbox`<br>- `manage-package`

샌드박스 간 구성 정확도를 높이고 샌드박스 도구 기능을 사용하여 샌드박스 간에 샌드박스 구성을 원활하게 내보내고 가져올 수 있습니다. 샌드박스 도구를 사용하여 구현 프로세스에 대한 가치 창출 시간을 줄이고 샌드박스 간에 성공적인 구성을 이동할 수 있습니다.

샌드박스 도구 기능을 사용하여 다른 개체를 선택하고 패키지로 내보낼 수 있습니다. 패키지는 단일 개체, 여러 개체 또는 전체 샌드박스로 구성될 수 있습니다. 패키지에 포함된 모든 객체는 동일한 샌드박스의 객체여야 합니다.

## 샌드박스 도구에 지원되는 오브젝트 {#supported-objects}

아래 표에는 현재 샌드박스 툴이 지원되는 객체가 나와 있습니다.

| 플랫폼 | 오브젝트 |
| --- | --- |
| [!DNL Adobe Journey Optimizer] | 여정 |
| 고객 데이터 플랫폼 | 소스 |
| 고객 데이터 플랫폼 | 세그먼트 |
| 고객 데이터 플랫폼 | ID |
| 고객 데이터 플랫폼 | 정책 |
| 고객 데이터 플랫폼 | 스키마 |
| 고객 데이터 플랫폼 | 데이터 세트 |

다음 객체를 가져오지만 초안 또는 비활성화 상태입니다.

| 기능 | 오브젝트 | 상태 |
| --- | --- | --- |
| 가져오기 상태 | 소스 데이터 흐름 | 초안 |
| 가져오기 상태 | 여정 | 초안 |
| 통합 프로필 | 스키마 | 비활성화됨 |
| 통합 프로필 | 데이터 세트 | 비활성화됨 |
| 정책 | 동의 정책 | 비활성화됨 |
| 정책 | 데이터 거버넌스 정책 | 비활성화됨 |

아래 나열된 극단적 사례는 패키지에 포함되지 않습니다.

* 스키마 관계

## 개체를 패키지로 내보내기 {#export-objects}

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="패키지 저장 및 종료"
>abstract="패키지를 종료 및 저장하려면 사용자는 뒤로 옵션을 사용하면 됩니다."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="오브젝트 제거"
>abstract="사용자는 행을 선택한 다음 삭제 옵션(선택 시 사용 가능)을 사용하여 행을 제거해야 합니다."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="패키지 만료 설정"
>abstract="만료일은 오늘날짜로부터 90일로 설정됩니다. 패키지가 게시될 때까지 이 날짜는 계속 변경됩니다. 사용자가 내일 초안 상태의 패키지를 방문하는 경우 날짜가 1일씩 이동합니다(사용자가 설정하지 않는 한)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="패키지 상태"
>abstract="기본적으로 상태는 초안으로 설정되어 있습니다. 패키지가 게시되면 상태가 게시됨으로 변경됩니다. 패키지가 게시된 후에는 변경될 수 없습니다."

>[!NOTE]
>
>개체에 액세스할 수 있는 권한이 있는 경우에만 패키지를 가져올 수 있습니다.

이 예제에서는 스키마를 내보내고 패키지에 추가하는 프로세스를 설명합니다. 동일한 프로세스를 사용하여 데이터 세트, 여정 등과 같은 다른 객체를 내보낼 수 있습니다.

### 새 패키지에 개체 추가 {#add-object-to-new-package}

선택 **[!UICONTROL 스키마]** 왼쪽 탐색에서 를 선택하고 **[!UICONTROL 찾아보기]** 사용 가능한 스키마를 나열하는 탭입니다. 그런 다음 줄임표(`...`) 선택한 스키마 옆에 드롭다운에 컨트롤이 표시됩니다. 선택 **[!UICONTROL 패키지에 추가]** 드롭다운에서 을 클릭합니다.

![다음을 강조 표시하는 드롭다운 메뉴를 표시하는 스키마 목록 [!UICONTROL 패키지에 추가] 제어.](../images/ui/sandbox-tooling/add-to-package.png)

다음에서 **[!UICONTROL 패키지에 추가]** 대화 상자에서 **[!UICONTROL 새 패키지 만들기]** 옵션을 선택합니다. 다음을 제공합니다. [!UICONTROL 이름] 패키지 및 옵션 [!UICONTROL 설명]을 선택한 다음 을 선택합니다. **[!UICONTROL 추가]**.

![다음 [!UICONTROL 패키지에 추가] 대화 상자 [!UICONTROL 새 패키지 만들기] 선택 및 강조 표시 [!UICONTROL 추가].](../images/ui/sandbox-tooling/create-new-package.png)

(으)로 돌아갑니다. **[!UICONTROL 스키마]** 환경. 이제 아래 나열된 다음 단계를 수행하여 만든 패키지에 개체를 추가할 수 있습니다.

### 기존 패키지에 개체 추가 및 게시 {#add-object-to-existing-package}

사용 가능한 스키마 목록을 보려면 **[!UICONTROL 스키마]** 왼쪽 탐색에서 를 선택하고 **[!UICONTROL 찾아보기]** 탭. 그런 다음 줄임표(`...`) 드롭다운 메뉴에서 제어 옵션을 보려면 선택한 스키마 옆에 있어야 합니다. 선택 **[!UICONTROL 패키지에 추가]** 드롭다운에서 을 클릭합니다.

![다음을 강조 표시하는 드롭다운 메뉴를 표시하는 스키마 목록 [!UICONTROL 패키지에 추가] 제어.](../images/ui/sandbox-tooling/add-to-package.png)

다음 **[!UICONTROL 패키지에 추가]** 대화 상자가 나타납니다. 다음 항목 선택 **[!UICONTROL 기존 패키지]** 옵션을 선택한 다음 **[!UICONTROL 패키지 이름]** 드롭다운을 클릭하고 필요한 패키지를 선택합니다. 마지막으로 다음을 선택합니다. **[!UICONTROL 추가]** 을 클릭하여 선택 항목을 확인합니다.

![[!UICONTROL 패키지에 추가] 드롭다운에서 선택한 패키지를 표시하는 대화 상자입니다.](../images/ui/sandbox-tooling/add-to-existing-package.png)

패키지에 추가된 오브젝트 목록이 나열됩니다. 패키지를 게시하여 샌드박스로 가져올 수 있도록 하려면 을 선택합니다. **[!UICONTROL 게시]**.

![패키지를 강조 표시하는 패키지 내 오브젝트 목록 [!UICONTROL 게시] 옵션을 선택합니다.](../images/ui/sandbox-tooling/publish-package.png)

선택 **[!UICONTROL 게시]** 패키지 게시를 확인합니다.

![패키지 게시 확인 대화 상자, 강조 표시 [!UICONTROL 게시] 옵션을 선택합니다.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>게시되면 패키지의 콘텐츠를 변경할 수 없습니다. 호환성 문제를 방지하려면 필요한 모든 에셋을 선택했는지 확인하십시오. 변경해야 하는 경우 새 패키지를 만들어야 합니다.

(으)로 돌아갑니다. **[!UICONTROL 패키지]** 의 탭 [!UICONTROL 샌드박스] 게시된 새 패키지를 볼 수 있는 환경입니다.

![새로 게시된 패키지를 강조 표시하는 샌드박스 패키지 목록입니다.](../images/ui/sandbox-tooling/published-packages.png)

## 대상 샌드박스로 패키지 가져오기 {#import-package-to-target-sandbox}

패키지를 대상 샌드박스로 가져오려면 샌드박스로 이동합니다 **[!UICONTROL 찾아보기]** 을 탭하고 샌드박스 이름 옆에 있는 더하기(+) 옵션을 선택합니다.

![샌드박스 **[!UICONTROL 찾아보기]** 패키지 가져오기 선택 항목을 강조 표시하는 탭입니다.](../images/ui/sandbox-tooling/browse-sandboxes.png)

드롭다운 메뉴를 사용하여 **[!UICONTROL 패키지 이름]** 타겟팅된 샌드박스로 가져오려고 합니다. 옵션 추가 **[!UICONTROL 작업 이름]**&#x200B;향후 모니터링에 사용될 를 선택한 다음 **[!UICONTROL 다음]**.

![다음을 표시하는 가져오기 세부 정보 페이지 [!UICONTROL 패키지 이름] 드롭다운 선택](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

다음 [!UICONTROL 패키지 개체 및 종속성] 페이지는 이 패키지에 포함된 모든 에셋 목록을 제공합니다. 시스템은 선택한 상위 객체를 성공적으로 가져오는 데 필요한 종속 객체를 자동으로 검색합니다.

![다음 [!UICONTROL 패키지 개체 및 종속성] 페이지에 패키지에 포함된 에셋 목록이 표시됩니다.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>종속 객체는 Target 샌드박스의 기존 객체로 대체할 수 있으므로 새 버전을 만드는 대신 기존 객체를 재사용할 수 있습니다. 예를 들어 스키마를 포함하는 패키지를 가져올 때 대상 샌드박스에서 기존 사용자 정의 필드 그룹 및 ID 네임스페이스를 다시 사용할 수 있습니다. 또는 여정이 포함된 패키지를 가져올 때 target 샌드박스에서 기존 세그먼트를 재사용할 수 있습니다.

기존 개체를 사용하려면 종속 개체 옆에 있는 연필 아이콘을 선택합니다. 새로 만들거나 기존 항목을 사용하는 옵션이 표시됩니다. 선택 **[!UICONTROL 기존 항목 사용]**.

![다음 [!UICONTROL 패키지 개체 및 종속성] 종속 개체 옵션을 보여 주는 페이지 [!UICONTROL 새로 만들기] 및 [!UICONTROL 기존 항목 사용].](../images/ui/sandbox-tooling/use-existing-object.png)

다음 **[!UICONTROL 필드 그룹]** 대화 상자는 객체에 사용할 수 있는 필드 그룹 목록을 표시합니다. 필요한 필드 그룹을 선택한 다음 을 선택합니다. **[!UICONTROL 저장]**.

![에 표시된 필드 목록 [!UICONTROL 필드 그룹] 대화 상자, 강조 표시 [!UICONTROL 저장] 선택 항목. ](../images/ui/sandbox-tooling/field-group-list.png)

(으)로 돌아갑니다. [!UICONTROL 패키지 개체 및 종속성] 페이지를 가리키도록 업데이트하는 중입니다. 여기에서 다음을 선택합니다. **[!UICONTROL 완료]** 패키지 가져오기를 완료합니다.

![다음 [!UICONTROL 패키지 개체 및 종속성] 페이지에 패키지에 포함된 에셋 목록이 강조 표시됩니다. [!UICONTROL 완료].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## 전체 샌드박스 내보내기 및 가져오기

### 전체 샌드박스 내보내기 {#export-entire-sandbox}

전체 샌드박스를 내보내려면 [!UICONTROL 샌드박스] **[!UICONTROL 패키지]** 탭하고 선택 **[!UICONTROL 패키지 만들기]**.

![다음 [!UICONTROL 샌드박스] **[!UICONTROL 패키지]** 탭 강조 표시 [!UICONTROL 패키지 만들기].](../images/ui/sandbox-tooling/create-sandbox-package.png)

선택 **[!UICONTROL 전체 샌드박스]** 의 패키지 유형에 대해 [!UICONTROL 패키지 만들기] 대화 상자. 다음을 제공합니다. [!UICONTROL 패키지 이름] 패키지를 확인하고 다음을 선택합니다. **[!UICONTROL 샌드박스]** 드롭다운에서 을 클릭합니다. 마지막으로 다음을 선택합니다. **[!UICONTROL 만들기]** 을 눌러 항목을 확인합니다.

![다음 [!UICONTROL 패키지 만들기] 완료된 필드와 강조 표시를 표시하는 대화 상자 [!UICONTROL 만들기].](../images/ui/sandbox-tooling/create-package-dialog.png)

패키지가 성공적으로 생성되었습니다. 다음을 선택하십시오. **[!UICONTROL 게시]** 패키지를 게시합니다.

![새로 게시된 패키지를 강조 표시하는 샌드박스 패키지 목록입니다.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

(으)로 돌아갑니다. **[!UICONTROL 패키지]** 의 탭 [!UICONTROL 샌드박스] 게시된 새 패키지를 볼 수 있는 환경입니다.

### 전체 샌드박스 패키지 가져오기 {#import-entire-sandbox-package}

패키지를 대상 샌드박스로 가져오려면 다음으로 이동합니다. [!UICONTROL 샌드박스] **[!UICONTROL 찾아보기]** 을 탭하고 샌드박스 이름 옆에 있는 더하기(+) 옵션을 선택합니다.

![샌드박스 **[!UICONTROL 찾아보기]** 패키지 가져오기 선택 항목을 강조 표시하는 탭입니다.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

드롭다운 메뉴를 사용하여 다음을 사용하여 전체 샌드박스 선택 **[!UICONTROL 패키지 이름]** 드롭다운입니다. 옵션 추가 **[!UICONTROL 작업 이름]**&#x200B;향후 모니터링에 사용될 를 선택한 다음 **[!UICONTROL 다음]**.

![다음을 표시하는 가져오기 세부 정보 페이지 [!UICONTROL 패키지 이름] 드롭다운 선택](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>전체 샌드박스를 가져올 때 모든 객체가 패키지에서 새 객체로 만들어집니다. 개체에 나열되지 않음 [!UICONTROL 패키지 개체 및 종속성] 여러 개가 있을 수 있으므로 페이지를 표시합니다. 지원되지 않는 객체 유형을 알리는 인라인 메시지가 표시됩니다.

다음으로 이동되었습니다. [!UICONTROL 패키지 개체 및 종속성] 가져온 객체와 제외된 객체의 수를 볼 수 있는 페이지입니다. 여기에서 다음을 선택합니다. **[!UICONTROL 가져오기]** 패키지 가져오기를 완료합니다.

![다음 [!UICONTROL 패키지 개체 및 종속성] 페이지에 지원되지 않는 개체 유형의 인라인 메시지가 표시되며 강조 표시됩니다. [!UICONTROL 가져오기].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

## 가져오기 작업 모니터링 및 가져오기 객체 세부 정보 보기

가져온 개체 및 가져온 세부 정보를 보려면 [!UICONTROL 샌드박스] **[!UICONTROL 가져오기]** 을(를) 탭하고 목록에서 패키지를 선택합니다. 또는 검색 창을 사용하여 패키지를 검색합니다.

![샌드박스 [!UICONTROL 가져오기] 탭에서는 패키지 가져오기 선택 사항이 강조 표시됩니다.](../images/ui/sandbox-tooling/imports-tab.png)

### 가져온 개체 보기 {#view-imported-objects}

다음에서 **[!UICONTROL 가져오기]** 의 탭 [!UICONTROL 샌드박스] 환경, 선택 **[!UICONTROL 가져온 개체 보기]** 오른쪽 세부 정보 창에서 액세스합니다.

선택 **[!UICONTROL 가져온 개체 보기]** 의 오른쪽 세부 정보 창에서 **[!UICONTROL 가져오기]** 의 탭 [!UICONTROL 샌드박스] 환경.

![샌드박스 [!UICONTROL 가져오기] 탭에서는 [!UICONTROL 가져온 개체 보기] 오른쪽 창에서 선택합니다.](../images/ui/sandbox-tooling/view-imported-objects.png)

화살표를 사용하여 개체를 확장하면 패키지로 가져온 필드의 전체 목록을 볼 수 있습니다.

![샌드박스 [!UICONTROL 가져온 오브젝트] 패키지로 가져온 개체 목록을 표시합니다.](../images/ui/sandbox-tooling/expand-imported-objects.png)

### 가져오기 세부 정보 보기 {#view-import-details}

선택 **[!UICONTROL 가져오기 세부 정보 보기]** 의 오른쪽 세부 정보 창에서 **[!UICONTROL 가져오기]** 샌드박스 환경의 탭입니다.

![샌드박스 [!UICONTROL 가져오기] 탭에서는 [!UICONTROL 가져오기 세부 정보 보기] 오른쪽 창에서 선택합니다.](../images/ui/sandbox-tooling/view-import-details.png)

다음 **[!UICONTROL 세부 정보 가져오기]** 대화 상자에 가져오기의 세부 분류가 표시됩니다.

![다음 [!UICONTROL 세부 정보 가져오기] 가져오기의 세부 분류를 보여 주는 대화 상자.](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>가져오기가 완료되면 Platform UI에서 알림을 받습니다. 경고 아이콘에서 이러한 알림에 액세스할 수 있습니다. 작업이 실패한 경우 여기에서 문제 해결로 이동할 수 있습니다.

## 다음 단계

이 문서에서는 Experience Platform UI 내에서 샌드박스 도구 기능을 사용하는 방법을 보여 줍니다. 샌드박스에 대한 자세한 내용은 [샌드박스 사용 안내서](../ui/user-guide.md).

샌드박스 API를 사용하여 다른 작업을 수행하는 방법에 대한 자세한 내용은 [샌드박스 개발자 안내서](../api/getting-started.md). Experience Platform의 샌드박스에 대한 높은 수준의 개요는 [개요 설명서](../home.md).
