---
keywords: Experience Platform;홈;인기 있는 주제;통합 태그;태그;
title: 통합 태그 개요
description: 이 문서는 Adobe Experience Platform의 통합 태그에 대한 정보를 제공합니다.
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 6977438d57dc8e1390812e58bf039ebc60cb830d
workflow-type: ht
source-wordcount: '578'
ht-degree: 100%

---

# 통합 태그 개요

태그는 Adobe Experience Platform의 기능으로, 관리자가 비즈니스 오브젝트를 분류하도록 메타데이터 분류를 관리하여 더 쉽게 검색하고 분류할 수 있습니다. 태그는 검색에서 해당 오브젝트 및 관련 오브젝트를 찾을 수 있도록 세그먼트, 데이터 세트, 여정 또는 기타 오브젝트에 연결할 수 있는 키워드로 생각할 수 있는 메타데이터입니다. 태그는 두 가지 유형(분류 및 미분류)으로 분류됩니다.

더 많은 컨텍스트를 제공하고 태그 목적을 정의하기 위해 카테고리는 태그를 유용한 세트로 구성합니다. 관리자는 사용자가 오브젝트에 추가할 수 있는 분류된 태그를 정의합니다. 카테고리를 포함하지 않는 새 태그는 태그가 적용되는 워크플로에서 인라인으로 만들 수도 있습니다. 이 태그는 태그 인벤토리의 분류되지 않은 섹션에 표시됩니다. 태그는 만든 사람과 상관없이 관리자와 사용자가 모두 적용할 수 있습니다. 오브젝트, 검색 또는 필터링에 할당할 때 모든 유형의 태그를 선택할 수 있습니다.

## 태그 용어

태그 지정 시 다음 구성 요소가 포함됩니다.

| 용어 | 정의 |
| --- | --- |
| 보관 | 오브젝트와의 현재 연결을 유지하지만 태그가 추가 오브젝트에 적용되지 않도록 제한하는 태그 상태입니다.  보관된 태그는 태그 선택기에서 숨겨집니다. |
| 오브젝트 | 태그를 적용할 수 있는 Experience Cloud 항목입니다.  예: 세그먼트, 여정, 데이터 세트. |
| 태그 | 태그는 메타데이터로, 검색에서 해당 오브젝트 및 관련 오브젝트를 찾을 수 있도록 세그먼트, 데이터 세트, 여정 또는 기타 오브젝트에 연결할 수 있는 키워드로 생각할 수 있습니다. |
| 태그 카테고리 | 태그 카테고리는 태그를 의미 있는 집합으로 그룹화하여 더 많은 컨텍스트를 제공하거나 태그 목적을 설명합니다.  관리자는 태그 카테고리와 카테고리 내의 태그를 관리합니다. |
| 미분류 태그 | 태그가 적용된 인라인으로 생성되는 새 태그입니다. 이러한 태그는 모든 사용자가 만들고 적용할 수 있지만 카테고리에 바인딩되지는 않습니다.  관리자는 이러한 태그를 카테고리로 이동하여 다른 유사한 태그와 정렬할 수 있습니다. |

## 태그 인벤토리

태그 인벤토리를 사용한 태그 카테고리 및 태그 관리는 Experience Platform 및 Journey Optimizer 탐색 내에서 사용할 수 있습니다. 인벤토리의 태그 변경 사항은 태그를 지원하는 모든 오브젝트에 반영됩니다. 모든 사용자는 태그 인벤토리에 액세스하고 검색할 수 있지만, 태그 관리는 시스템 및 제품 관리자로 제한됩니다.

태그 인벤토리에는 세 가지 수준의 계층 구조가 있어 사용자가 태그 카테고리, 카테고리 내의 태그 및 개별 태그를 관리할 수 있습니다. 개별 태그를 관리할 때 사용자는 해당 태그가 현재 적용된 모든 오브젝트를 보고 탐색할 수 있습니다.

### 태그 카테고리

카테고리는 태그를 의미 있는 집합으로 그룹화하여 더 많은 컨텍스트를 제공하거나 태그 목적을 설명합니다. 카테고리가 있는 모든 태그에서 카테고리 이름 다음에 콜론이 이어지고 태그 이름이 뒤에 옵니다.

태그 카테고리를 사용할 때 다음 작업이 가능합니다.

* [태그 카테고리 생성](./ui/tags-categories.md#create-tag-category)
* [태그 카테고리 편집](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [태그 카테고리 삭제](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### 카테고리 내 태그 관리

>[!NOTE]
>
>Experience Cloud에 대한 태그를 관리하려면 Experience Cloud를 구독하는 조직의 Adobe Experience Platform에 대한 시스템 관리자 또는 제품 관리자여야 합니다.

카테고리(또는 기본 “미분류” 그룹) 내에서 태그를 만들고 관리할 수 있습니다. 태그를 관리할 때 다음 작업이 가능합니다.

* [태그 만들기](./ui/managing-tags.md#create-a-tag-create-tag)
* [태그 편집](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [카테고리 간 태그 이동](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [태그 보관](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [보관된 태그 복원](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [태그 삭제](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [태그 지정된 오브젝트 보기](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
