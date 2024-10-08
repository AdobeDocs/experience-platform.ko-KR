---
solution: Experience Platform
title: 사용 사례 플레이북의 데이터 인식 개요
description: 최종 영감을 주는 샌드박스에서 생성된 에셋을 다른 샌드박스에 복사하여 가치 실현 시간을 단축하는 방법에 대해 알아봅니다.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Publish 플레이북에서 생성한 에셋을 다른 샌드박스에 {#publish-to-other-sandboxes}

사용 사례 플레이북은 일반적인 마케팅 사용 사례에 대한 대상, 스키마 또는 여정과 같은 에셋을 생성하도록 설계된 마케팅 템플릿입니다. 영감을 주는 샌드박스에서 플레이북으로 생성된 에셋을 테스트할 수 있으며 준비가 되면 에셋을 다른 개발 샌드박스로 가져와서 해당 샌드박스에서 사용할 수 있는 데이터로 추가 테스트를 수행할 수 있습니다. 테스트가 만족스러우면 개발 샌드박스의 자산을 프로덕션 샌드박스로 이동할 수 있습니다.

그러나 경우에 따라 다른 개발 샌드박스에서 이미 고유한 스키마, 필드 및 필드 그룹을 설정했을 수 있습니다. 이렇게 하면 여정과 같은 사용 사례 템플릿에서 생성된 에셋 중 일부가 데이터와 호환되지 않을 수 있습니다. 데이터 인식 기능을 사용하여 생성된 에셋을 기존 에셋과 더 잘 조정하고 보완하는 방법을 이해하려면 이 자습서를 참조하십시오.

## 전제 조건 {#prerequisites}

이 자습서를 읽기 전에 기본 플레이북의 [사용 가능한 사용 사례 플레이북 템플릿](/help/use-case-playbooks/playbooks/choose.md#search-and-filter) 및 [인스턴스 만들기](/help/use-case-playbooks/playbooks/create-share-reuse.md)를 검색하십시오.

인스턴스를 생성하면 영감을 주는 샌드박스에서 여정, 세그먼트, 스키마 및 메시지와 같은 자산 세트가 생성됩니다. 이러한 자산을 다른 샌드박스로 복사하는 방법에 대해 알아보려면 계속 읽으십시오.

### 패키지 만들기 및 게시 {#create-publish-package}

>[!NOTE]
>
> 패키지를 다른 개발 샌드박스로만 가져올 수 있습니다. 필요한 모든 변경 또는 업데이트를 수행한 후 해당 개발 샌드박스에서 프로덕션으로 자산 또는 패키지를 가져올 수 있습니다. 사용 사례 플레이북 샌드박스에서 프로덕션으로 직접 가져올 수 없습니다.

1. 영감을 주는 샌드박스에서 다른 샌드박스로 개체를 가져오려면 사용 사례 플레이북의 원하는 인스턴스를 찾은 다음 **[!UICONTROL 다른 샌드박스로 Publish]**&#x200B;을(를) 선택하여 아티팩트를 패키지로 내보냅니다.

   ![다른 사용 사례 인스턴스를 보여 주는 GIF](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. **[!UICONTROL 다른 샌드박스로 Publish]** 단추를 선택하면 모달이 나타납니다. 이름과 설명(선택 사항)을 입력하고 **[!UICONTROL 만들기]**&#x200B;를 선택합니다. 이 단계에서는 생성된 에셋을 다른 샌드박스로 가져올 수 있는 패키지로 번들로 묶습니다.

   ![패키지를 만드는 모달](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. 왼쪽 탐색에서 **샌드박스** 페이지로 이동하여 **패키지** 탭을 선택하고 패키지를 찾아 게시합니다. 초안 상태의 패키지를 게시하려면 [샌드박스 도구](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) 문서의 단계를 따릅니다.

   ![초안 또는 게시되지 않은 상태의 패키지](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![패키지 게시](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. 게시가 성공하면 패키지 찾아보기 페이지에서 이름 옆에 **+** 단추가 활성화됩니다.

   샌드박스 페이지의 ![패키지 탭](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > 아직 초안 모드에 있는 동안에는 패키지를 가져올 수 없으므로 패키지 세부 사항 페이지를 열고 패키지를 게시하십시오.

5. **+** 컨트롤을 선택하고 워크플로를 시작하여 사용 사례 플레이북에서 생성된 에셋을 **[!UICONTROL Target 샌드박스]**(으)로 가져옵니다. 타겟 샌드박스를 선택하고 드롭다운을 사용하여 가져올 패키지 이름을 확인합니다. 다음 단계로 진행하기 전에 작업 이름 및 작업 설명 등 작업 세부 사항을 추가합니다.

   ![가져오기 워크플로우를 시작하고, 대상을 선택하고, 패키지를 확인하고, 작업 세부 정보를 추가합니다.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. **[!UICONTROL 종속성 보기]** 단계에서는 스키마를 매핑하고 영감을 주는 샌드박스에서 대상 샌드박스로 다른 자산을 복사할 수 있습니다. 각 스키마를 매핑할 때까지 **[!UICONTROL 마침]** 단추를 사용할 수 없습니다.

   ![&#39;종속성 보기&#39; 단계에서 스키마를 매핑하여 완료 단추를 사용하도록 설정합니다.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### 스키마 매핑 {#map-schemas}

1. 첫 번째 스키마 매핑. 대상 스키마를 선택하는 드롭다운이 스키마 매핑 대화 상자에 표시됩니다. 소스 스키마가 프로필 스키마인 경우 [개별 유니온 프로필 스키마](/help/xdm/classes/individual-profile.md) 외에 다른 대상 스키마 옵션이 없습니다. 페이지가 처음 표시될 때 Source 데이터와 대상 필드 간에 자동으로 생성된 매핑 권장 사항을 볼 수 있습니다. 대상 필드를 선택한 다음 새 필드를 선택하여 매핑을 편집할 수 있습니다. 제안된 매핑을 수정하는 경우 **유효성 검사** 단추를 사용하여 새 매핑의 유효성을 검사하고 새 매핑에 연결할 수 있는 오류를 표시합니다. 매핑이 완료되면 **저장**&#x200B;을(를) 선택하십시오.

   ![대상 스키마를 선택할 수 있는 드롭다운이 있는 스키마 매핑 대화 상자](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. 스키마의 모든 필드를 계속 매핑합니다. 스키마가 [이벤트 스키마](/help/xdm/classes/experienceevent.md)인 경우 대상 샌드박스에서 모든 이벤트 스키마를 볼 수 있는 드롭다운이 대화 상자에 표시됩니다.

   ![드롭다운에서 대상 스키마 선택](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. **Target 샌드박스**&#x200B;의 사용 가능한 스키마에서 스키마를 선택하십시오.

   ![스키마 선택](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. 매핑을 완료하고 **저장**&#x200B;을(를) 선택합니다.

   ![매핑 저장](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. 스키마의 모든 필드 매핑을 완료한 후 **완료**&#x200B;를 선택하여 가져오기 워크플로우를 완료합니다.

   ![흐름 완료](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > 영감을 주는 샌드박스이지만 패키지의 종속성이므로 스키마를 제외한 다른 에셋을 수정할 수 없습니다.

### 가져오기 상태 {#import-status}

1. 가져오기 진행 상황을 볼 수 있는 [**가져오기**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) 페이지로 자동 리디렉션됩니다.

   ![가져오기 진행률을 표시하는 페이지](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. 패키지를 가져오는 동안 패키지의 자산이 대상 샌드박스에서 생성되고 있습니다. 완료되면 가져오기 프로세스 중에 매핑한 필드를 참조합니다. 이제 프로세스가 완료되었으며 영감을 주는 샌드박스의 에셋도 대상 샌드박스에 표시되어 테스트할 수 있습니다.

   ![대상 샌드박스에서 생성된 자산](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## 다음 단계

이 안내서를 읽은 후에는 [샌드박스 도구](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details)와 함께 사용 사례 플레이북을 활용하여 스키마를 참조하는 실행 가능한 여정을 만드는 방법을 더 잘 이해할 수 있습니다. 일반적인 [Real-Time CDP 사용 사례](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)에 대해 자세히 알아보세요.
