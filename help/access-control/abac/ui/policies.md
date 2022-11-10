---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;ABAC
title: 속성 기반 액세스 제어 정책 만들기
description: 이 문서에서는 Adobe Experience Cloud의 권한 인터페이스를 통해 정책 관리에 대한 정보를 제공합니다
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 1a755fa5480e036bde50617f01440cfabbaf64c2
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# 정책 관리

정책은 허용 및 허용되지 않는 작업을 설정하기 위해 특성을 함께 가져오는 구문입니다. 정책은 로컬 또는 글로벌 정책일 수 있으며 다른 정책을 재정의할 수 있습니다.

## 새 정책 만들기

새 정책을 만들려면 **[!UICONTROL 정책]** 탭하고 을 선택합니다. **[!UICONTROL 정책 만들기]**.

![flash-new-policy](../../images/flac-ui/flac-new-policy.png)

다음 **[!UICONTROL 새 정책 만들기]** 이름 및 선택적 설명을 입력하라는 대화 상자가 나타납니다. 완료되면 을 선택합니다 **[!UICONTROL 확인]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

드롭다운 화살표를 사용하여 다음을 선택합니다 **액세스 권한 허용** (![flac-permission-access-to](../../images/flac-ui/flac-permit-access-to.png)) 리소스 또는 **액세스 거부** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) 리소스.

그런 다음 드롭다운 메뉴 및 검색 액세스 유형, 읽기 또는 쓰기를 사용하여 정책에 포함할 리소스를 선택합니다.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

그런 다음 드롭다운 화살표를 사용하여 이 정책에 적용할 조건을 선택합니다. **다음 내용이 참인 경우** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) 또는 **다음은 false입니다** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

더하기 아이콘을 선택하여 **일치 표현식 추가** 또는 **표현식 그룹 추가** 추가 리소스

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

드롭다운을 사용하여 **리소스**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

그런 다음 드롭다운을 사용하여 **일치**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

그런 다음 드롭다운을 사용하여 레이블 유형(**[!UICONTROL 코어 레이블]** 또는 **[!UICONTROL 사용자 지정 레이블]**)을 클릭하여 롤의 사용자에게 할당된 레이블과 일치시킵니다.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

마지막으로 **샌드박스** 에 적용할 정책 조건을 지정합니다. 드롭다운 메뉴를 사용합니다.

![flac-policy-sandboxes-드롭다운](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

선택 **리소스 추가** 리소스를 더 추가하려면 완료되면 을 선택합니다. **[!UICONTROL 저장 및 종료]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

새 정책이 성공적으로 만들어지면 **[!UICONTROL 정책]** 탭에 새로 만든 정책이 목록에 표시됩니다.

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## 정책 편집

기존 정책을 편집하려면 **[!UICONTROL 정책]** 탭. 또는 필터 옵션을 사용하여 결과를 필터링하여 편집할 정책을 찾습니다.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

다음으로 줄임표(`…`)를 클릭하면 해당 역할을 편집, 비활성화, 삭제 또는 복제하는 컨트롤이 드롭다운에 표시됩니다. 드롭다운에서 편집을 선택합니다.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

정책 권한 화면이 나타납니다. 업데이트를 만든 다음 을 선택합니다 **[!UICONTROL 저장 및 종료]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

정책이 성공적으로 업데이트되었으며, 이(가) **[!UICONTROL 정책]** 탭.

## 정책 복제

기존 정책을 복제하려면 **[!UICONTROL 정책]** 탭. 또는 필터 옵션을 사용하여 결과를 필터링하여 편집할 정책을 찾습니다.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

다음으로 줄임표(`…`)을 클릭합니다. 그러면 드롭다운에 역할을 편집, 비활성화, 삭제 또는 복제하는 컨트롤이 표시됩니다. 드롭다운에서 중복을 선택합니다.

![flc-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

다음 **[!UICONTROL 정책 복제]** 중복을 확인하는 대화 상자가 나타납니다.

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

새 정책이 목록에 원본 파일의 사본으로 나타납니다 **[!UICONTROL 정책]** 탭.

![flc-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## 정책 삭제

기존 정책을 삭제하려면 **[!UICONTROL 정책]** 탭. 또는 필터 옵션을 사용하여 결과를 필터링하여 삭제할 정책을 찾습니다.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

다음으로 줄임표(`…`)을 클릭합니다. 그러면 드롭다운에 역할을 편집, 비활성화, 삭제 또는 복제하는 컨트롤이 표시됩니다. 드롭다운에서 삭제 를 선택합니다.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

다음 **[!UICONTROL 사용자 정책 삭제]** 대화 상자가 나타나서 삭제를 확인하는 메시지가 나타납니다.

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

에 반환됩니다 **[!UICONTROL 정책]** 탭 및 삭제 확인 팝업이 나타납니다.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## 정책 활성화

기존 정책을 활성화하려면 **[!UICONTROL 정책]** 탭. 또는 필터 옵션을 사용하여 결과를 필터링하여 삭제할 정책을 찾습니다.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

다음으로 줄임표(`…`)를 클릭하면 해당 역할이 편집, 활성화, 삭제 또는 복제되는 컨트롤이 드롭다운에 표시됩니다. 드롭다운에서 활성화 를 선택합니다.

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

다음 **[!UICONTROL 사용자 정책 활성화]** 활성화 여부를 확인하는 대화 상자가 나타납니다.

![flash-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

에 반환됩니다 **[!UICONTROL 정책]** 탭 및 활성화 확인 팝업이 나타납니다. 정책 상태가 활성으로 표시됩니다.

![flac-policy-activated](../../images/flac-ui/flac-policy-activated.png)

## 다음 단계

새 정책을 만든 후에는 다음 단계로 진행할 수 있습니다. [역할에 대한 권한 관리](permissions.md).
