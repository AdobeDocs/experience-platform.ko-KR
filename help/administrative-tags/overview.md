---
keywords: Experience Platform;홈;인기 항목;관리 태그;태그;
title: 관리 태그 개요
description: 이 문서에서는 Adobe Experience Platform의 관리 태그에 대한 정보를 제공합니다
hide: true
hidefromtoc: true
source-git-commit: 7f0572af2d582353a0dde12bdb6692f342463312
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# 태그 개요

태그는 관리자가 보다 쉽게 검색 및 분류할 수 있도록 비즈니스 객체를 분류하기 위해 메타데이터 분류법을 관리할 수 있는 Adobe Experience Platform 기능입니다. 태그는 검색 시 해당 개체 및 관련 개체를 찾을 수 있도록 세그먼트, 데이터 세트, 여정 또는 기타 개체에 첨부할 수 있는 키워드로 생각할 수 있는 메타데이터입니다. 태그는 다음 두 가지 유형으로 분류됩니다. 분류 및 분류되지 않았습니다.

더 많은 컨텍스트를 제공하고 태그의 목적을 정의하기 위해 카테고리는 태그를 유용한 세트로 구성합니다. 관리자는 사용자가 객체에 추가할 수 있는 분류 태그를 정의합니다. 카테고리가 포함되지 않은 새로운 태그는 태그가 적용되는 워크플로우에서 인라인 생성할 수도 있습니다. 이러한 태그는 태그 인벤토리의 조직되지 않은 섹션에 표시됩니다. 태그는 누가 태그를 만들었는지에 관계없이 관리자 및 사용자가 비슷하게 적용할 수 있습니다. 객체에 할당하거나 검색 또는 필터링할 때 모든 유형의 태그를 선택할 수 있습니다.

## 태그 용어

태깅에는 다음 구성 요소가 포함됩니다.

| 용어 | 정의 |
| --- | --- |
| 보관됨 | 현재 개체 연결을 유지하지만 태그가 추가 개체에 적용되지 않도록 제한하는 태그의 상태입니다.  보관된 태그는 태그 선택기에서 숨겨집니다. |
| 오브젝트 | 태그가 적용될 수 있는 Experience Cloud 항목입니다.  예: 세그먼트, 여정, 데이터 세트. |
| 태그 | 태그는 메타데이터이며 검색을 통해 해당 개체 및 관련 개체를 찾을 수 있도록 세그먼트, 데이터 세트, 여정 또는 기타 개체에 첨부할 수 있는 키워드로 생각할 수 있습니다. |
| 태그 범주 | 태그 카테고리는 태그를 의미 있는 세트로 그룹화하여 더 큰 컨텍스트를 제공하거나 태그의 목적을 설명합니다.  관리자는 카테고리 내의 태그 카테고리와 태그를 관리합니다. |
| 조직화되지 않은 태그 | 태그가 적용되는 인라인 태그입니다. 이러한 태그는 모든 사용자가 만들고 적용할 수 있지만 카테고리에 바인딩되어 있지 않습니다.  관리자는 이러한 태그를 다른 유사한 태그와 일치하도록 카테고리로 이동할 수 있습니다. |

## 태그 인벤토리

태그 인벤토리를 사용하는 태그 카테고리 및 태그 관리는 Experience Platform 및 Journey Optimizer 탐색 내에서 사용할 수 있습니다. 인벤토리에서 태그를 변경하면 태그를 지원하는 모든 객체에 반영됩니다. 모든 사용자는 태그 인벤토리에 액세스하고 검색할 수 있지만, 태그 관리는 시스템 및 제품 관리자로 제한됩니다.

태그 인벤토리는 세 가지 계층 구조를 가지므로, 태그 카테고리, 카테고리 내의 태그 및 개별 태그를 관리할 수 있습니다. 개별 태그를 관리할 때 사용자는 현재 해당 태그가 적용되는 개체를 보고 이동할 수 있습니다.

### 태그 카테고리

카테고리는 태그를 의미 있는 세트로 그룹화하여 더 큰 컨텍스트를 제공하거나 태그의 목적을 설명합니다. 카테고리가 있는 모든 태그에서는 카테고리 이름 뒤에 콜론이 옵니다.

태그 카테고리를 사용할 때는 다음 작업을 수행할 수 있습니다.

* [태그 카테고리 만들기](./ui/tags-categories.md#create-tag-category)
* [태그 범주 편집](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [태그 범주 삭제](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 카테고리 내 태그 관리

>[!NOTE]
>
>Experience Cloud에 대한 태그를 관리하려면 Experience Cloud에 대한 자격이 있는 조직의 Adobe Experience Platform에 대한 시스템 관리자 또는 제품 관리자여야 합니다.

카테고리(또는 기본 &quot;분류되지 않은&quot; 그룹) 내에서 태그를 만들고 관리할 수 있습니다. 태그를 관리할 때에는 다음 작업이 가능합니다.

* [태그 만들기](./ui/managing-tags.md#create-a-tag-create-tag)
* [태그 편집](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [카테고리 간에 태그 이동](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [태그 보관](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [보관된 태그 복원](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [태그 삭제](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [태그가 지정된 개체 보기](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
