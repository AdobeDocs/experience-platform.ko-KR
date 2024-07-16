---
title: 데이터 세트 샘플
description: 쿼리 서비스 샘플 데이터 세트를 사용하면 쿼리 정확도 비용으로 처리 시간을 크게 단축하면서 빅 데이터에 대한 탐색 쿼리를 수행할 수 있습니다. 이 안내서에서는 대략적인 쿼리 처리를 위해 샘플을 관리하는 방법에 대한 정보를 제공합니다
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# 데이터 세트 샘플

Adobe Experience Platform 쿼리 서비스는 대략적인 쿼리 처리 기능의 일부로 샘플 데이터 세트를 제공합니다. 샘플 데이터 세트는 원본의 레코드 비율만 사용하여 기존 [!DNL Azure Data Lake Storage](ADLS) 데이터 세트의 균일한 무작위 샘플로 만들어집니다. 이 백분율을 샘플링 속도라고 합니다. 샘플링 속도를 조정하여 정확도와 처리 시간의 균형을 제어하면 쿼리 정확도 비용으로 처리 시간을 크게 단축하면서 빅 데이터에 대한 탐색적 쿼리를 수행할 수 있습니다.

많은 사용자가 데이터 세트에 대한 집계 작업에 대해 정확한 답변이 필요하지 않으므로 대량의 데이터 세트에 대한 탐색적 쿼리에 대해서는 대략적인 답변을 반환하기 위해 대략적인 쿼리를 발행하는 것이 더 효율적입니다. 샘플 데이터 세트에는 원래 데이터 세트의 데이터 비율만 포함되어 있으므로 쿼리 정확도를 트레이드하여 응답 시간을 향상시킬 수 있습니다. 읽기 시 쿼리 서비스는 전체 데이터 세트를 쿼리하는 경우보다 결과를 빠르게 생성하는 행 수를 적게 스캔해야 합니다.

대략적인 쿼리 처리를 위한 샘플을 관리할 수 있도록 쿼리 서비스는 데이터 세트 샘플에 대해 다음 작업을 지원합니다.

- [균일한 무작위 데이터 세트 샘플을 만듭니다.](#create-a-sample)
- [선택적으로 필터 조건 지정](##optional-filter-criteria)
- [ADLS 테이블에 대한 샘플 목록을 봅니다.](#view-list-of-samples)
- [샘플 데이터 세트를 직접 쿼리합니다.](#query-sample-datasets)
- [샘플을 삭제합니다.](#delete-a-sample)
- 원래 ADLS 테이블을 삭제하면 연결된 샘플이 삭제됩니다.

## 시작하기 {#get-started}

이 문서에 자세히 설명된 대략적인 쿼리 처리 기능을 만들고 삭제하려면 세션 플래그를 `true`(으)로 설정해야 합니다. 쿼리 편집기 또는 PSQL 클라이언트의 명령줄에서 `SET aqp=true;` 명령을 입력합니다.

>[!NOTE]
>
>Platform에 로그인할 때마다 세션 플래그를 활성화해야 합니다.

![SET aqp=true;&#39; 명령이 강조 표시된 쿼리 편집기입니다.](../images/essential-concepts/set-session-flag.png)

## 균일한 무작위 데이터 세트 샘플 만들기 {#create-a-sample}

데이터 집합 이름과 함께 `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` 명령을 사용하여 해당 데이터 집합에서 균일한 무작위 샘플을 만드십시오.

샘플 비율은 원본 데이터 세트에서 가져온 레코드의 백분율입니다. `TABLESAMPLE SAMPLERATE` 키워드를 사용하여 샘플 속도를 제어할 수 있습니다. 이 예에서, 5.0의 값은 50%의 표본 속도와 같다. 2.5 값은 25% 등과 같습니다.

>[!IMPORTANT]
>
>시스템은 각 데이터 세트에 대해 최대 5개의 샘플을 허용합니다. 여섯 번째 샘플 데이터 세트를 만들려고 하면 샘플 제한에 도달했다는 오류 메시지가 화면에 표시됩니다.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## 선택적으로 필터 조건 지정 {#optional-filter-criteria}

균일 무작위 샘플에 대한 필터 기준을 지정하도록 선택할 수 있습니다. 이렇게 하면 분석된 테이블의 필터링된 하위 집합을 기반으로 샘플을 만들 수 있습니다.

샘플을 만들 때 선택 사항인 필터가 먼저 적용된 다음 데이터 세트의 필터링된 보기에서 샘플이 만들어집니다. 필터가 적용된 데이터 세트 샘플은 다음 쿼리 형식을 따릅니다.

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

이러한 유형의 필터링된 샘플 데이터 세트의 실제 예는 다음과 같습니다.

```sql
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

제공된 예제에서 테이블 이름은 `large_table`이고, 원래 테이블의 필터 조건은 `month(to_timestamp(timestamp)) in ('8', '9')`이며, 샘플링 속도는 (필터링된 데이터의 X%)입니다. 이 경우 `10`입니다.

## 샘플 목록 보기 {#view-list-of-samples}

ADLS 테이블과 연결된 샘플 목록을 보려면 `sample_meta()` 함수를 사용하십시오.

```sql
SELECT sample_meta('example_dataset_name')
```

데이터 세트 샘플 목록은 아래 예제의 형식으로 표시됩니다.

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## 샘플 데이터 세트 쿼리 {#query-sample-datasets}

`{EXAMPLE_DATASET_NAME}`을(를) 사용하여 샘플 테이블을 직접 쿼리합니다. 또는 쿼리 끝에 `WITHAPPROXIMATE` 키워드를 추가하면 쿼리 서비스에서 가장 최근에 만든 샘플을 자동으로 사용합니다.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## 데이터 세트 샘플 삭제 {#delete-a-sample}

삭제 작업을 사용하면 최대 5개의 데이터 세트 샘플 제한에 도달한 후 새 샘플을 만들 수 있습니다.

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>원본 ADLS 데이터 세트에서 파생된 샘플 데이터 세트가 여러 개 있는 경우 원본을 삭제하면 연결된 모든 샘플도 삭제됩니다.
