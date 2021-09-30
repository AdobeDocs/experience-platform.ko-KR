---
solution: Experience Platform
title: Platform 대시보드를 제공하는 원시 데이터 세트 탐색 및 처리
type: Documentation
description: Query Service를 사용하여 Experience Platform에서 프로필, 세그먼트 및 대상 대시보드에 적용되는 원시 데이터 세트를 탐색하고 처리하는 방법을 알아봅니다.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: b9dd7584acc43b5946f8c0669d7a81001e44e702
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%

---

# Query Service를 사용하여 대시보드 데이터 세트를 탐색, 확인 및 처리합니다

Adobe Experience Platform은 Experience Platform UI에서 사용할 수 있는 대시보드를 통해 조직의 프로필, 세그먼트 및 대상 데이터에 대한 중요한 정보를 제공합니다. 그런 다음 Adobe Experience Platform 쿼리 서비스 를 사용하여 데이터 레이크에서 이러한 대시보드를 제공하는 원시 데이터 세트를 탐색, 확인 및 처리할 수 있습니다.

## 쿼리 서비스 시작

Adobe Experience Platform Query Service는 표준 SQL을 사용하여 데이터 레이크에서 데이터를 쿼리할 수 있도록 하여 마케터가 데이터로부터 통찰력을 얻을 수 있도록 지원합니다. Query Service는 사용자 인터페이스와 API를 제공하여 데이터 레이크의 데이터 세트를 결합하고 쿼리 결과를 보고, 머신 러닝 또는 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

Query Service 및 Query Service 내의 역할에 대해 자세히 알아보려면 [Query Service 개요](../query-service/home.md)를 읽어 보십시오.

## 사용 가능한 데이터 세트

Query Service를 사용하여 프로필, 세그먼트 및 대상 대시보드에 대한 원시 데이터 세트를 쿼리할 수 있습니다. 다음 섹션에서는 데이터 레이크에서 찾을 수 있는 원시 데이터 세트에 대해 설명합니다.

### 프로필 속성 데이터 세트

프로필 대시보드 인사이트는 조직에서 정의한 병합 정책에 연결됩니다. 모든 활성 병합 정책에 대해 데이터 레이크에서 사용할 수 있는 프로필 속성 데이터 세트가 있습니다.

이러한 데이터 세트의 이름 지정 규칙은 **Profile-Snapshot-Export** 뒤에 시스템이 생성한 임의의 영숫자 값이 옵니다. 예: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

각 프로필 스냅샷 내보내기 데이터 세트의 전체 스키마를 이해하려면 Experience Platform UI에서 데이터 세트 뷰어](../catalog/datasets/user-guide.md)를 사용하여 데이터 세트 [을 미리 보고 탐색할 수 있습니다.

![](images/query/profile-attribute.png)

#### 프로필 속성 데이터 세트를 병합 정책 ID에 매핑

각 프로필 속성 데이터 세트에는 **프로필 스냅샷 내보내기** 뒤에 시스템이 생성한 임의 영숫자 값이 옵니다. 예: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

이 영숫자 값은 조직에서 만든 병합 정책 중 하나의 병합 정책 ID에 매핑되는 시스템에서 생성된 임의의 문자열입니다. 각 병합 정책 ID를 해당 관련 프로필 속성 데이터 세트 문자열에 대한 매핑은 `adwh_dim_merge_policies` 데이터 세트에서 유지됩니다.

`adwh_dim_merge_policies` 데이터 세트에 다음 필드가 포함되어 있습니다.

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

이 데이터 집합은 Experience Platform의 쿼리 편집기 UI를 사용하여 탐색할 수 있습니다. 쿼리 편집기 사용에 대한 자세한 내용은 [쿼리 편집기 UI 안내서](../query-service/ui/user-guide.md)를 참조하십시오.

### 세그먼트 메타데이터 데이터 세트

각 조직의 세그먼트에 대한 메타데이터가 포함된 데이터 레이크에서 사용할 수 있는 세그먼트 메타데이터 데이터 세트가 있습니다.

이 데이터 집합에 대한 이름 지정 규칙은 **Segmentdefinition-Snapshot-Export** 다음에 영숫자 값이 옵니다. 예: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

각 세그먼트 정의 스냅샷 내보내기 데이터 세트의 전체 스키마를 이해하려면 Experience Platform UI에서 데이터 세트 뷰어](../catalog/datasets/user-guide.md)를 사용하여 데이터 세트 [을(를) 미리 보고 탐색할 수 있습니다.

![](images/query/segment-metadata.png)

### 대상 메타데이터 데이터 세트

조직의 활성화된 모든 대상에 대한 메타데이터는 데이터 레이크에서 원시 데이터 세트로 사용할 수 있습니다.

이 데이터 집합의 이름 지정 규칙은 **DIM_Destination**&#x200B;입니다.

DIM 대상 데이터 집합의 전체 스키마를 이해하려면 Experience Platform UI에서 데이터 집합 뷰어](../catalog/datasets/user-guide.md)를 사용하여 데이터 집합 [을(를) 미리 보고 탐색할 수 있습니다.

![](images/query/destinations-metadata.png)

## 쿼리 예

다음 예제 쿼리는 Query Service에서 대시보드를 구동하는 원시 데이터 세트를 탐색, 확인 및 처리하는 데 사용할 수 있는 샘플 SQL을 포함합니다.

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

이제 이 안내서를 읽으면 Query Service를 사용하여 프로필, 세그먼트 및 대상 대시보드에 적용되는 원시 데이터 세트를 탐색하고 처리할 수 있습니다.

각 대시보드 및 해당 지표에 대한 자세한 내용을 보려면 설명서 탐색의 사용 가능한 대시보드 목록에서 대시보드를 선택하십시오.
