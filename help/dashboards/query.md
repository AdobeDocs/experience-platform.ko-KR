---
solution: Experience Platform
title: Query Service를 사용하여 대시보드 데이터 세트를 탐색, 확인 및 처리합니다.
type: Documentation
description: Query Service를 사용하여 Experience Platform에서 프로필, 세그먼트 및 대상 대시보드에 적용되는 원시 데이터 세트를 탐색하고 처리하는 방법을 알아봅니다.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---

# 을 사용하여 대시보드 데이터 세트를 탐색, 확인 및 처리합니다 [!DNL Query Service]

Adobe Experience Platform은 Experience Platform UI에서 사용할 수 있는 대시보드를 통해 조직의 프로필, 세그먼트 및 대상 데이터에 대한 중요한 정보를 제공합니다. 그런 다음 Adobe Experience Platform을 사용할 수 있습니다 [!DNL Query Service] 데이터 레이크에서 이러한 대시보드를 제공하는 원시 데이터 세트를 탐색, 확인 및 처리합니다.

## 시작하기 [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 에서는 마케터가 표준 SQL을 사용하여 데이터 레이크에서 데이터를 쿼리할 수 있도록 하여 데이터로부터 통찰력을 얻을 수 있도록 지원합니다. [!DNL Query Service] 에서는 데이터 레이크에서 데이터 집합에 참여하고 쿼리 결과를 보고, 기계 학습 또는 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처하는 데 사용할 수 있는 사용자 인터페이스 및 API를 제공합니다.

에 대해 자세히 알아보려면 [!DNL Query Service] 그리고 Experience Platform 내에서 그 역할을 읽으세요 [[!DNL Query Service] 개요](../query-service/home.md).

## 사용 가능한 데이터 세트에 액세스

다음을 사용할 수 있습니다 [!DNL Query Service] 프로필, 세그먼트 및 대상 대시보드에 대한 원시 데이터 세트를 쿼리하려면 다음을 수행하십시오. 사용 가능한 데이터 세트를 보려면 Experience Platform UI에서 **데이터 세트** 왼쪽 탐색에서 데이터 세트 대시보드를 엽니다. 대시보드는 조직에 대해 사용 가능한 모든 데이터 세트를 나열합니다. 세부 사항은 해당 이름, 데이터 세트가 준수하는 스키마 및 가장 최근 수집 실행 상태를 포함하여 나열된 각 데이터 세트에 대해 표시됩니다.

![왼쪽 탐색 영역에 데이터 세트 탭이 강조 표시된 데이터 세트 찾아보기 대시보드입니다.](./images/query/browse-datasets.png)

### 시스템 생성 데이터 세트

>[!IMPORTANT]
>
>시스템 생성 데이터 세트는 기본적으로 숨겨져 있습니다. 기본적으로 [!UICONTROL 찾아보기] 탭에는 데이터를 수집한 데이터 세트만 표시됩니다.

시스템에서 생성한 데이터 세트를 보려면 필터 아이콘(![필터 아이콘.](./images/query/filter.png))을 클릭합니다.

![필터 아이콘이 강조 표시된 데이터 세트 찾아보기 탭입니다.](./images/query/filter-datasets.png)

두 개의 토글이 포함된 사이드바가 나타납니다. [!UICONTROL 프로필에 포함됨] 및 [!UICONTROL 시스템 데이터 세트 표시]. 에 대한 토글을 선택합니다 [!UICONTROL 시스템 데이터 세트 표시] 찾아보기 가능한 데이터 세트 목록 내에 시스템 생성 데이터 세트를 포함합니다.

![시스템 데이터 세트 표시 토글이 강조 표시된 데이터 세트 찾아보기 탭입니다.](./images/query/show-system-datasets.png)

### 프로필 속성 데이터 세트

프로필 대시보드 인사이트는 조직에서 정의한 병합 정책에 연결됩니다. 모든 활성 병합 정책에 대해 데이터 레이크에서 사용할 수 있는 프로필 속성 데이터 세트가 있습니다.

이러한 데이터 세트의 이름 지정 규칙은 다음과 같습니다 **Profile-Snapshot-Export** 시스템에서 생성된 임의의 영숫자 값이 뒤에 옵니다. 예: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

각 프로필 스냅샷 내보내기 데이터 세트의 전체 스키마를 이해하려면 데이터 세트를 미리 보고 탐색할 수 있습니다 [데이터 집합 뷰어 사용](../catalog/datasets/user-guide.md) Experience Platform UI에서 클릭합니다.

![프로필 스냅샷 내보내기 데이터 집합의 미리 보기입니다.](images/query/profile-attribute.png)

#### 프로필 속성 데이터 세트를 병합 정책 ID에 매핑

각 시스템 생성 프로필 속성 데이터 세트에 할당된 영숫자 값은 조직이 만든 병합 정책 중 하나의 병합 정책 ID에 매핑되는 임의의 문자열입니다. 각 병합 정책 ID를 관련 프로필 속성 데이터 세트 문자열에 매핑하는 작업은 `adwh_dim_merge_policies` 데이터 세트.

다음 `adwh_dim_merge_policies` 데이터 세트에는 다음 필드가 포함되어 있습니다.

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

이 데이터 집합은 Experience Platform의 쿼리 편집기 UI를 사용하여 탐색할 수 있습니다. 쿼리 편집기 사용에 대한 자세한 내용은 [쿼리 편집기 UI 안내서](../query-service/ui/user-guide.md).

### 세그먼트 메타데이터 데이터 세트

각 조직의 세그먼트에 대한 메타데이터가 포함된 데이터 레이크에서 사용할 수 있는 세그먼트 메타데이터 데이터 세트가 있습니다.

이 데이터 세트의 이름 지정 규칙은 다음과 같습니다 **Segmentdefinition-Snapshot-Export** 뒤에 영숫자 값이 옵니다. 예: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

각 세그먼트 정의 스냅샷 내보내기 데이터 세트의 전체 스키마를 이해하려면 데이터 세트를 미리 보고 탐색할 수 있습니다 [데이터 집합 뷰어 사용](../catalog/datasets/user-guide.md) Experience Platform UI에서 클릭합니다.

![Segmentdefinition-Snapshot-Export 데이터 세트의 미리 보기입니다.](images/query/segment-metadata.png)

### 대상 메타데이터 데이터 세트

조직의 활성화된 모든 대상에 대한 메타데이터는 데이터 레이크에서 원시 데이터 세트로 사용할 수 있습니다.

이 데이터 세트의 이름 지정 규칙은 다음과 같습니다 **DIM_Destination**.

DIM 대상 데이터 집합의 전체 스키마를 이해하기 위해 데이터 집합을 미리 보고 탐색할 수 있습니다 [데이터 집합 뷰어 사용](../catalog/datasets/user-guide.md) Experience Platform UI에서 클릭합니다.

![DIM_Destination 데이터 세트의 미리 보기입니다.](images/query/destinations-metadata.png)

## (베타) CDP(고객 데이터 플랫폼) 통찰력 보고서

>[!IMPORTANT]
>
>CDP 통찰력 데이터 모델 기능은 베타에 있습니다. 해당 기능과 설명서는 변경될 수 있습니다.

CDP 통찰력 데이터 모델 기능은 다양한 프로필, 대상 및 세그멘테이션 위젯에 대한 통찰력을 제공하는 SQL을 표시합니다. 이러한 SQl 쿼리 템플릿을 사용자 지정하여 마케팅 및 KPI 사용 사례를 위한 CDP 보고서를 만들 수 있습니다.

CDP 보고에서는 프로필 데이터와 세그먼트 및 대상과의 관계에 대한 통찰력을 제공합니다. 방법에 대한 자세한 내용은 CDP 통찰력 데이터 모델 설명서 를 참조하십시오 [특정 KPI 사용 사례에 CDP 통찰력 데이터 모델 적용](./cdp-insights-data-model.md).

## 쿼리 예

다음 예제 쿼리에는 [!DNL Query Service] 대시보드 전원을 지원하는 원시 데이터 세트를 탐색, 확인 및 처리합니다.

### ID별 프로필 수

이 프로필 인사이트는 데이터 집합에 있는 모든 병합된 프로필에서 ID의 분류를 제공합니다.

>[!NOTE]
>
>한 프로필에는 여러 네임스페이스가 연결되어 있을 수 있으므로 ID별 총 프로필 수(즉, 각 네임스페이스에 대해 표시된 값을 함께 추가)는 병합된 총 프로필 수보다 높을 수 있습니다. 예를 들어 고객이 둘 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다.

**쿼리**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
        )
     group by
        namespace;
```

### 세그먼트별 프로필 수

이 대상 인사이트는 데이터 집합에 있는 각 세그먼트 내의 병합된 총 프로필 수를 제공합니다. 이 숫자는 프로필 조각을 함께 병합하여 세그먼트의 각 개인을 위한 단일 프로필을 구성하기 위해 프로필 데이터에 세그먼트 병합 정책을 적용한 결과입니다.

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## 다음 단계

이제 이 안내서를 읽으면 다음 작업을 수행할 수 있습니다 [!DNL Query Service] 몇 가지 쿼리를 수행하여 프로필, 세그먼트 및 대상 대시보드에 적용되는 원시 데이터 세트를 탐색하고 처리합니다.

각 대시보드 및 해당 지표에 대한 자세한 내용을 보려면 설명서 탐색의 사용 가능한 대시보드 목록에서 대시보드를 선택하십시오.
