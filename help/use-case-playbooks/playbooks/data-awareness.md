---
solution: Experience Platform
title: 사용 사례 플레이북의 데이터 인식 개요
description: 최종 영감을 주는 샌드박스에서 생성된 에셋을 다른 샌드박스에 복사하여 가치 실현 시간을 단축하는 방법에 대해 알아봅니다.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 5b6b69d69a088f58d10f41debde859294285360d
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---


# 사용 사례 플레이북의 데이터 인식 개요

사용 사례 플레이북은 일반적인 마케팅 사용 사례에 대한 대상, 스키마 또는 여정과 같은 에셋을 생성하도록 설계된 마케팅 템플릿입니다. Adobe Experience Platform 내에서 이러한 템플릿은 여러 표준 필드와 필드 그룹을 참조합니다. 그러나 경우에 따라 이미 고유한 스키마, 필드 및 필드 그룹을 설정했을 수 있습니다. 이렇게 하면 여정과 같은 사용 사례 템플릿에서 생성된 에셋 중 일부가 데이터와 호환되지 않을 수 있습니다. 이 튜토리얼을 참조하여 데이터 인식 기능을 사용하여 생성된 에셋을 기존 에셋과 보다 효율적으로 조정하고 보완하는 방법을 알아보십시오.

## 전제 조건 {#prerequisites}

이 자습서를 읽기 전에 [사용 가능한 사용 사례 플레이북 템플릿](/help/use-case-playbooks/playbooks/discover.md#search-and-filter) 및 [인스턴스 만들기](/help/use-case-playbooks/playbooks/create-share-reuse.md) 선호하는 플레이북의

인스턴스를 생성하면 영감을 주는 샌드박스에서 여정, 세그먼트, 스키마 및 메시지와 같은 자산 세트가 생성됩니다. 이러한 자산을 다른 샌드박스로 복사하는 방법에 대해 알아보려면 계속 읽으십시오.

### 패키지 만들기 및 게시 {#create-publish-package}

1. 영감을 주는 샌드박스에서 다른 샌드박스로 오브젝트를 가져오려면 사용 사례 플레이북의 원하는 인스턴스를 찾아 다음을 선택합니다 **[!UICONTROL 다른 샌드박스에 게시]** 를 클릭하여 아티팩트를 패키지로 내보냅니다.

   ![다양한 사용 사례 인스턴스를 보여 주는 GIF](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. 을(를) 선택하면 **[!UICONTROL 다른 샌드박스에 게시]** 버튼을 누르면 모달이 나타납니다. 이름과 설명(선택 사항)을 입력하고 다음을 선택합니다. **[!UICONTROL 만들기]**. 이 단계에서는 생성된 에셋을 다른 샌드박스로 가져올 수 있는 패키지로 번들로 묶습니다.

   ![패키지를 만들기 위한 모달](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. 다음 위치로 이동 **샌드박스** 페이지를 왼쪽 탐색에서 선택하고 **패키지** 탭에서 패키지를 찾아 게시합니다. 초안 상태의 패키지를 게시하려면 [샌드박스 도구](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) 문서.

   ![초안 또는 게시되지 않은 상태의 패키지](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![패키지 게시](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. 게시가 성공하면 패키지 찾아보기 페이지에 **+** 이름 옆에 버튼이 활성화되었습니다.

   ![샌드박스 페이지의 패키지 탭](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > 아직 초안 모드에 있는 동안에는 패키지를 가져올 수 없으므로 패키지 세부 사항 페이지를 열고 패키지를 게시하십시오.

5. 다음 항목 선택 **+** 워크플로를 시작하여 사용 사례 플레이북에서 생성된 에셋을 **[!UICONTROL Target 샌드박스]**. 타겟 샌드박스를 선택하고 드롭다운을 사용하여 가져올 패키지 이름을 확인합니다. 다음 단계로 진행하기 전에 작업 이름 및 작업 설명 등 작업 세부 사항을 추가합니다.

   ![가져오기 워크플로우를 시작하고, 타겟을 선택하고, 패키지를 확인하고, 작업 세부 사항을 추가합니다.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

   >[!NOTE]
   >
   > 패키지를 다른 개발 샌드박스로만 가져올 수 있습니다. 이러한 가져오기에 대해 프로덕션 샌드박스가 비활성화되었습니다.

6. 다음에서 **[!UICONTROL 종속성 보기]** 단계에서는 스키마를 매핑하고 영감을 주는 샌드박스에서 target 샌드박스로 다른 에셋을 복사할 수 있습니다. 다음 **[!UICONTROL 완료]** 각 스키마를 매핑할 때까지 버튼이 비활성화됩니다.

   ![&#39;종속성 보기&#39; 단계에서 스키마를 매핑하고 완료 단추를 활성화합니다.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### 스키마 매핑 {#map-schemas}

1. 첫 번째 스키마 매핑. 대상 스키마를 선택하는 드롭다운이 스키마 매핑 대화 상자에 표시됩니다. 소스 스키마가 프로필 스키마인 경우 [개별 유니온 프로필 스키마](/help/xdm/classes/individual-profile.md). 페이지가 처음 표시될 때 소스 데이터와 대상 필드 간에 자동으로 생성된 매핑 권장 사항을 볼 수 있습니다. 대상 필드를 선택한 다음 새 필드를 선택하여 매핑을 편집할 수 있습니다. 제안된 매핑을 변경하는 경우 **유효성 검사** 단추를 사용하여 새 매핑의 유효성을 검사하고 새 매핑에 연결할 수 있는 오류를 표시합니다. 선택 **저장** 매핑이 완료되면

   ![드롭다운이 있는 스키마 매핑 대화 상자에서 대상 스키마를 선택합니다.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. 스키마의 모든 필드를 계속 매핑합니다. 스키마가 인 경우 [이벤트 스키마](/help/xdm/classes/experienceevent.md), 대화 상자에 target 샌드박스의 모든 이벤트 스키마를 볼 수 있는 드롭다운이 표시됩니다.

   ![드롭다운에서 타겟 스키마 선택](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. 의 사용 가능한 스키마에서 스키마 선택 **Target 샌드박스**.

   ![스키마 선택](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. 매핑을 완료하고 을(를) 선택합니다 **저장**.

   ![매핑 저장](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. 스키마의 모든 필드 매핑을 완료한 후 다음을 선택합니다. **완료** 가져오기 워크플로를 완료합니다.

   ![흐름 완료](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > 영감을 주는 샌드박스이지만 패키지의 종속성이므로 스키마를 제외한 자산에 대해 작업을 수행할 수 없습니다.

### 가져오기 상태 {#import-status}

1. 로 자동 리디렉션됩니다. [**가져오기**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) 가져오기 진행 상황을 확인할 수 있는 페이지입니다.

   ![가져오기 진행 상황을 보여 주는 페이지](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. 패키지를 가져오는 동안 패키지의 자산이 대상 샌드박스에서 생성되고 있습니다. 완료되면 가져오기 프로세스에서 방금 매핑한 필드를 참조합니다. 이제 프로세스가 완료되었으며 영감을 주는 샌드박스의 에셋도 대상 샌드박스에 표시되어 테스트할 수 있습니다.

   ![대상 샌드박스에서 생성된 에셋](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## 다음 단계

이 안내서를 읽은 후에는 사용 사례 플레이북을 함께 활용하는 방법을 더 잘 이해할 수 있습니다 [샌드박스 도구](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) 스키마를 참조하는 실행 가능한 여정을 만들려면. 공통점에 대해 자세히 알아보기 [Real-Time CDP 활용 사례](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).