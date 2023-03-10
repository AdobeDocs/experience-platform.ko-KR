---
keywords: Experience Platform;홈;인기 항목;통합 태그;태그;
title: (Beta) 통합 태그 개요
description: 이 문서에서는 Adobe Experience Platform의 통합 태그에 대한 정보를 제공합니다
source-git-commit: 6f9787909b8155d2bf032b4a42483f2cb4d44eb4
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# (Beta) 통합 태그 개요

>[!IMPORTANT]
>
>통합 태그는 Beta 버전입니다. 피드백을 남기려면 태그 관리 페이지 상단에 있는 버튼을 선택하여 피드백 하세요.

태그는 관리자가 비즈니스 오브젝트를 분류하여 쉽게 검색하고 분류할 수 있도록 메타데이터 분류를 관리할 수 있는 Adobe Experience Platform의 기능입니다. 태그는 검색을 통해 해당 개체 및 관련 개체를 찾을 수 있도록 하기 위해 세그먼트, 데이터 세트, 여정 또는 기타 개체에 첨부할 수 있는 키워드로 생각할 수 있는 메타데이터입니다. 태그는 범주화된 태그와 분류되지 않은 태그로 분류된다.

더 많은 컨텍스트를 제공하고 태그의 목적을 정의하기 위해 범주는 태그를 유용한 세트로 구성합니다. 관리자는 사용자가 오브젝트에 추가할 수 있는 분류된 태그를 정의합니다. 카테고리가 포함되지 않은 새 태그는 태그가 적용되는 워크플로우에서 인라인으로 만들 수도 있습니다. 이러한 태그는 태그 인벤토리의 분류되지 않은 섹션에 표시됩니다. 태그는 만든 사람에 관계없이 관리자와 사용자가 모두 적용할 수 있습니다. 객체에 할당하거나, 검색하거나, 필터링할 때 모든 유형의 태그를 선택할 수 있습니다.

## 태그 용어

태깅에는 다음 구성 요소가 포함됩니다.

| 용어 | 정의 |
| --- | --- |
| 보관됨 | 현재 개체와의 연결은 유지하지만 태그가 다른 개체에 적용되지 않도록 제한하는 태그의 상태입니다.  보관된 태그는 태그 선택기에서 숨겨집니다. |
| 오브젝트 | 태그가 적용될 수 있는 Experience Cloud 항목입니다.  예: 세그먼트, 여정, 데이터 세트. |
| 태그 | 태그는 메타데이터이며, 세그먼트, 데이터 세트, 여정 또는 기타 객체에 연결하여 검색으로 해당 객체 및 관련 객체를 찾을 수 있는 키워드로 간주될 수 있습니다. |
| 태그 범주 | 태그 카테고리 는 태그를 의미 있는 세트로 그룹화하여 더 큰 컨텍스트를 제공하거나 태그의 목적을 설명합니다.  관리자는 태그 범주와 범주 내의 태그를 관리합니다. |
| 분류되지 않은 태그 | 태그가 적용되는 인라인으로 생성되는 새 태그입니다. 이러한 태그는 모든 사용자가 만들고 적용할 수 있지만 범주에 바인딩되어 있지 않습니다.  관리자는 유사한 다른 태그와 맞추기 위해 이러한 태그를 범주로 이동할 수 있습니다. |

## 태그 인벤토리

태그 인벤토리를 사용하는 태그 카테고리 및 태그 관리는 Experience Platform 및 Journey Optimizer 탐색 내에서 사용할 수 있습니다. 인벤토리의 태그 변경 사항은 태그를 지원하는 모든 오브젝트에 반영됩니다. 모든 사용자는 태그 인벤토리에 액세스하고 검색할 수 있지만 태그 관리는 시스템 및 제품 관리자로 제한됩니다.

태그 인벤토리에는 세 가지 수준의 계층 구조가 있으므로 사용자가 태그 범주, 범주 내의 태그 및 개별 태그를 관리할 수 있습니다. 개별 태그를 관리할 때 사용자는 현재 해당 태그가 적용된 오브젝트를 보고 이동할 수 있습니다.

### 태그 카테고리

범주는 태그를 의미 있는 세트로 그룹화하여 더 큰 컨텍스트를 제공하거나 태그의 목적을 설명합니다. 범주가 있는 태그에서 태그 이름 앞에 카테고리 이름 뒤에 콜론이 옵니다.

태그 카테고리를 사용할 때는 다음 작업을 수행할 수 있습니다.

* [태그 범주 만들기](./ui/tags-categories.md#create-tag-category)
* [태그 범주 편집](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [태그 범주 삭제](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 범주 내 태그 관리

>[!NOTE]
>
>Experience Cloud에 대한 태그를 관리하려면 Experience Cloud에 대한 구독이 있는 조직의 Adobe Experience Platform에 대한 시스템 관리자 또는 제품 관리자여야 합니다.

범주(또는 기본 &quot;분류되지 않은&quot; 그룹) 내에서 태그를 만들고 관리할 수 있습니다. 태그를 관리할 때는 다음 작업을 수행할 수 있습니다.

* [태그 만들기](./ui/managing-tags.md#create-a-tag-create-tag)
* [태그 편집](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [범주 간에 태그 이동](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [태그 보관](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [보관된 태그 복원](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [태그 삭제](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [태그가 지정된 오브젝트 보기](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
