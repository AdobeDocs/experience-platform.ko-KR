---
solution: Experience Platform
title: 원시 데이터 세트 탐색 및 처리 Experience Platform 기반 대시보드
type: Documentation
description: Query Service를 사용하여 Experience Platform에서 프로필, 세그먼트 및 대상 대시보드에 적용되는 원시 데이터 세트를 탐색하고 처리하는 방법을 알아봅니다.
source-git-commit: 743367431144e9714a967b0340c755bf2120559c
workflow-type: tm+mt
source-wordcount: '592'
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

실시간 고객 프로필의 모든 활성 병합 정책에 대해 데이터 레이크에서 사용할 수 있는 프로필 속성 데이터 세트가 있습니다.

이 데이터 집합의 이름 지정 규칙은 **프로필 속성**&#x200B;에 영숫자 값이 옵니다. 예: `Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

데이터 세트의 전체 스키마를 이해하려면 Experience Platform UI에서 데이터 세트 뷰어를 사용하여 스키마를 미리 보고 탐색할 수 있습니다.

### 세그먼트 메타데이터 데이터 세트

각 조직의 세그먼트에 대해 데이터 레이크에서 사용할 수 있는 세그먼트 메타데이터 데이터 세트가 있습니다.

이 데이터 집합의 이름 지정 규칙은 **프로필 세그먼트 정의**&#x200B;에 영숫자 값이 옵니다. 예: `Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

다음 이미지는 세그먼트 메타데이터 데이터 세트의 스키마를 보여줍니다.

![](images/query/segment-metadata.png)

### 대상 메타데이터 데이터 세트

활성화된 대상에 대한 메타데이터는 데이터 레이크에서 원시 데이터 세트로 사용할 수 있습니다.

이 데이터 집합의 이름 지정 규칙은 **DIM_Destination**&#x200B;입니다.

다음 이미지는 대상 메타데이터 데이터 집합의 스키마를 보여줍니다.

![](images/query/destinations-metadata.png)

## 쿼리 예

다음 예제 쿼리는 Query Service에서 대시보드를 구동하는 원시 데이터 세트를 탐색, 확인 및 처리하는 데 사용할 수 있는 샘플 SQL을 포함합니다.

### ID별 프로필 수

이 프로필 인사이트는 데이터 집합에 있는 모든 병합된 프로필에서 ID의 분류를 제공합니다. 한 프로필에는 여러 네임스페이스가 연결되어 있을 수 있으므로 ID별 총 프로필 수(즉, 각 네임스페이스에 대해 표시된 값을 함께 추가)는 병합된 총 프로필 수보다 높을 수 있습니다. 예를 들어 고객이 둘 이상의 채널에서 브랜드와 상호 작용하는 경우 여러 네임스페이스가 해당 개별 고객과 연결됩니다.

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
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
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
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

### 모든 대상에 대해 대상당 활성화된 세그먼트 수

## 다음 단계

이제 이 안내서를 읽으면 Query Service를 사용하여 프로필, 세그먼트 및 대상 대시보드에 적용되는 원시 데이터 세트를 탐색하고 처리할 수 있습니다.

각 대시보드 및 해당 지표에 대한 자세한 내용을 보려면 설명서 탐색의 사용 가능한 대시보드 목록에서 대시보드를 선택하십시오.
