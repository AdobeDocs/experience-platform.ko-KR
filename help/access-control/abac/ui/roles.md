---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;ABAC
title: 속성 기반 액세스 제어 역할 만들기
description: 이 문서에서는 Adobe Experience Cloud의 권한 인터페이스를 통한 역할 관리에 대한 정보를 제공합니다
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 7%

---

# 역할 관리

역할은 관리자, 전문가 또는 최종 사용자가 조직의 리소스에 액세스할 수 있는 권한을 정의합니다. 역할 기반 액세스 제어 환경에서 사용자 액세스 프로비저닝은 일반적인 책임과 요구 사항을 통해 그룹화됩니다. 역할에는 주어진 권한 집합이 있으며, 조직의 멤버들은 필요한 보기 또는 쓰기 액세스 범위에 따라 하나 이상의 역할에 할당될 수 있습니다.

## 새 역할 만들기

새 역할을 만들려면 **[!UICONTROL 역할]** 사이드바에서 탭을 클릭하고 다음을 선택합니다. **[!UICONTROL 역할 만들기]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

다음 **[!UICONTROL 새 역할 만들기]** 대화 상자가 나타나고 이름과 설명(선택 사항)을 입력하라는 메시지가 표시됩니다.

완료되면 다음을 선택합니다. **[!UICONTROL 확인]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

그런 다음 드롭다운 메뉴를 사용하여 역할에 포함할 리소스 권한을 선택합니다.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

리소스를 추가하려면 다음을 선택합니다. **[!UICONTROL Adobe Experience Platform]** 리소스 목록이 표시되는 왼쪽 탐색 패널에서 액세스할 수 있습니다. 또는 왼쪽 탐색 패널의 검색 막대에 리소스 이름을 입력합니다.

![flac 추가 리소스](../../images/flac-ui/flac-add-additional-resources.png)

관련 리소스를 클릭하고 드래그하여 기본 패널에 놓습니다.

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

드롭다운 메뉴를 사용하여 역할에 포함할 리소스 권한을 선택합니다. 역할에 포함할 모든 리소스에 대해 이 작업을 반복합니다. 완료되면 다음을 선택합니다. **[!UICONTROL 저장 및 종료]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

새 역할이 성공적으로 만들어지고으로 리디렉션됩니다. **[!UICONTROL 역할]** 새로 생성된 역할이 목록에 표시되는 페이지입니다.

![flac 역할 저장됨](../../images/flac-ui/flac-role-saved.png)

의 섹션을 참조하십시오. [역할에 대한 권한 관리](#manage-permissions-for-a-role) 역할 권한이 생성되면 관리하는 방법에 대한 자세한 내용을 보려면 여기를 클릭하십시오.

## 역할 복제

기존 역할을 복제하려면 다음에서 역할을 선택합니다 **[!UICONTROL 역할]** 탭. 또는 필터 옵션을 사용하여 결과를 필터링하여 복제할 역할을 찾습니다.

![flac-duplex-role](../../images/flac-ui/flac-duplicate-role.png)

그런 다음 을 선택합니다. **[!UICONTROL 복제]** 화면 오른쪽 상단에서

![flac-복제](../../images/flac-ui/flac-duplicate.png)

다음 **[!UICONTROL 역할 복제]** 복제를 확인하는 대화 상자가 나타납니다.

![flac-duplex-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

그런 다음 역할의 이름 및 권한을 변경할 수 있는 역할의 세부 사항 페이지로 이동합니다. 세부 정보, 레이블 및 샌드박스는 이전 역할과 중복됩니다. 사용자 탭을 통해 사용자를 추가해야 합니다. 다음을 볼 수 있습니다. [역할에 대한 권한 관리](permissions.md) 세부 정보, 레이블, 샌드박스 및 사용자를 역할에 추가하는 방법에 대해 자세히 알아보려면 문서를 참조하십시오.

왼쪽 화살표를 클릭하여 로 돌아갑니다 **[!UICONTROL 역할]** 탭.

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

새 역할이 다음 목록에 나타납니다. **[!UICONTROL 역할]** 페이지를 가리키도록 업데이트하는 중입니다.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## 역할 삭제

줄임표(`…`) 역할 이름 옆에 드롭다운에 역할을 편집, 삭제 또는 복제할 컨트롤이 표시됩니다. 드롭다운에서 삭제 를 선택합니다.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

다음 **[!UICONTROL 사용자 역할 삭제]** 대화 상자가 나타나고 삭제를 확인하라는 메시지가 표시됩니다.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

(으)로 반환됩니다. **[!UICONTROL 역할]** 탭.

## 다음 단계

새 역할이 생성되면 다음 단계로 진행할 수 있습니다. [역할에 대한 권한 관리](permissions.md).
