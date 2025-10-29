---
title: SQL을 사용하여 파생 데이터 세트 만들기
description: SQL을 사용하여 프로필에 대해 활성화된 파생된 데이터 세트를 만드는 방법과 실시간 고객 프로필 및 세분화 서비스에 대한 데이터 세트를 사용하는 방법에 대해 알아봅니다.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# SQL을 사용하여 파생 데이터 세트 만들기

SQL 쿼리를 사용하여 기존 데이터 세트에서 데이터를 조작하고 변형하여 프로필에 대해 활성화된 파생 데이터 세트를 만드는 방법을 알아봅니다. 이 워크플로우는 실시간 고객 프로필 비즈니스 사용 사례에 대해 파생된 데이터 세트를 만드는 효율적이고 대안적인 방법을 제공합니다.

이 문서에서는 실시간 고객 프로필과 함께 사용할 파생 데이터 세트를 생성하는 편리한 다양한 SQL 확장에 대해 설명합니다. 워크플로우는 다양한 API 호출 또는 Experience Platform UI 상호 작용을 통해 완료해야 하는 프로세스를 간소화합니다.

일반적으로 실시간 고객 프로필에 대해 파생된 데이터 세트를 생성하고 게시하는 절차는 다음과 같습니다.

* ID 네임스페이스가 없는 경우 만듭니다.
* 필요한 경우 파생된 데이터 세트를 저장할 데이터 유형을 만듭니다.
* 해당 데이터 유형으로 필드 그룹을 만들어 파생된 데이터 세트 정보를 저장합니다.
* 이전에 만든 네임스페이스로 기본 ID 열을 만들거나 할당합니다.
* 이전에 만든 필드 그룹 및 데이터 유형을 사용하여 스키마를 만듭니다.
* 스키마를 사용하여 새 데이터 세트를 만들고 필요한 경우 프로필에 대해 활성화합니다.
* 선택적으로 데이터 세트를 프로필이 활성화된 것으로 표시합니다.

위에 언급된 단계를 완료하면 데이터 세트를 채울 수 있습니다. 프로필에 대한 데이터 세트를 활성화한 경우 새 데이터 세트를 참조하는 세그먼트를 만들고 인사이트 생성을 시작할 수도 있습니다.

쿼리 서비스를 사용하면 SQL 쿼리를 사용하여 위에 나열된 모든 작업을 수행할 수 있습니다. 여기에는 필요한 경우 데이터 세트 및 필드 그룹을 변경하는 작업이 포함됩니다.

## 프로필에 대해 활성화할 수 있는 옵션이 있는 표 만들기 {#enable-dataset-for-profile}

>[!NOTE]
>
>아래에 제공된 SQL 쿼리는 기존 네임스페이스의 사용을 가정합니다.

CTAS(Create Table as Select) 쿼리를 사용하여 데이터 세트를 만들고, 데이터 형식을 할당하고, 기본 ID를 설정하고, 스키마를 만들고, 프로필이 활성화된 것으로 표시합니다. 아래의 예제 SQL 문은 데이터 세트를 만들어 Real-Time Customer Data Platform(Real-Time CDP)에서 사용할 수 있도록 합니다. SQL 쿼리는 아래 예에 표시된 형식을 따릅니다.

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

지원되는 데이터 유형은 부울, 날짜, 날짜, 시간, 텍스트, 부동 소수점, bigint, 정수, 맵, 배열 및 구조체/행입니다.

아래의 SQl 코드 블록은 구조/행, 맵 및 배열 데이터 형식을 정의하는 예를 제공합니다. 1행은 행 구문을 보여 줍니다. 2행은 맵 구문을, 3행은 배열 구문을 보여 줍니다.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

또는 Experience Platform UI를 통해 프로필에 대해 데이터 세트를 활성화할 수도 있습니다. 프로필에 대해 활성화된 데이터 세트로 표시하는 방법에 대한 자세한 내용은 [실시간 고객 프로필에 데이터 세트 활성화](../../../catalog/datasets/user-guide.md#enable-profile)를 참조하십시오.

아래 예제 쿼리에서 `decile_table`을(를) 기본 ID 열로 사용하여 `id` 데이터 집합을 만들고 네임스페이스는 `IDFA`입니다. 맵 데이터 형식의 이름이 `decile1Month`인 필드도 있습니다. 만든 테이블(`decile_table`)이 프로필에 대해 활성화되어 있습니다.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

쿼리가 성공적으로 실행되면 아래 예에 표시된 대로 데이터 세트 ID가 콘솔로 반환됩니다.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

`label='PROFILE'` 명령에 `CREATE TABLE`을(를) 사용하여 프로필이 활성화된 데이터 세트를 만듭니다. `upsert` 기능은 기본적으로 켜져 있습니다. 아래 예제와 같이 `upsert` 명령을 사용하여 `ALTER` 기능을 덮어쓸 수 있습니다.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

[ALTER TABLE](../../sql/syntax.md#alter-table) 명령 및 [CTAS 쿼리의 일부로 레이블](../../sql/syntax.md#create-table-as-select)을 사용하는 방법에 대한 자세한 내용은 SQl 구문 설명서를 참조하십시오.

## SQL을 통해 파생 데이터 세트를 관리하는 데 도움이 되는 구문

아래에 설명된 기능은 SQL을 통해 파생 데이터 세트를 관리할 때 큰 도움이 됩니다.

### 프로필에 사용할 수 있도록 기존 데이터 세트 변경 {#enable-existing-dataset-for-profile}

ALTER TABLE SQL 구성을 사용하여 프로필에 대해 기존 데이터 세트를 활성화할 수 있습니다. 이를 위해서는 프로필 활성화 태그가 스키마와 해당 데이터 세트 모두에 추가되어야 합니다.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>`ALTER TABLE` 명령을 성공적으로 실행하면 콘솔이 `ALTER SUCCESS`을(를) 반환합니다.

### 기존 데이터 세트에 기본 ID 추가 {#add-primary-identity}

데이터 세트의 기존 열을 기본 ID 세트로 표시합니다. 그렇지 않으면 오류가 발생합니다. SQL을 사용하여 기본 ID를 설정하려면 아래에 표시된 쿼리 형식을 사용합니다.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

예:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

제공된 예에서 `id2`은(는) `test1_dataset`의 기존 열입니다.

### 프로필에 대한 데이터 세트 비활성화 {#disable-dataset-for-profile}

프로파일 사용에 대해 테이블을 비활성화하려면 DROP 명령을 사용해야 합니다. `DROP`을(를) 사용하는 SQL 문의 예는 아래에 나와 있습니다.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

예:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

이 SQL 문은 API 호출 사용에 대한 효율적인 대체 방법을 제공합니다. 자세한 내용은 [데이터 세트 API를 사용하여 Real-Time CDP에서 사용할 데이터 세트를 비활성화](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile)하는 방법에 대한 설명서를 참조하십시오.

### 데이터 세트에 대한 업데이트 및 삽입 기능 허용 {#enable-upsert-functionality-for-dataset}

UPDATE 명령을 사용하면 새 레코드를 삽입하거나 테이블의 기존 데이터를 업데이트할 수 있습니다. 특히, 지정된 값이 테이블에 이미 있는 경우 기존 행을 업데이트하거나 지정된 값이 없는 경우 새 행을 삽입할 수 있습니다.

올바른 형식을 사용하는 예제 문이 아래에 표시되어 있습니다.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

예:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

이 SQL 문은 API 호출 사용에 대한 효율적인 대체 방법을 제공합니다. 자세한 내용은 [데이터 세트 API를 사용하여 Real-Time CDP 및 업데이트에 사용할 데이터 세트를 활성화](../../../catalog/datasets/enable-upsert.md#enable-the-dataset)하는 방법에 대한 설명서를 참조하십시오.

### 데이터 세트에 대한 업데이트 및 삽입 기능 비활성화 {#disable-upsert-functionality-for-dataset}

이 명령은 데이터 세트에 행을 업데이트하고 삽입하는 기능을 비활성화합니다.

올바른 형식을 사용하는 예제 문이 아래에 표시되어 있습니다.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

예:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### 각 테이블과 연관된 추가 테이블 정보 표시 {#show-labels-for-tables}

프로필이 활성화된 데이터 세트에 대해 추가 메타데이터가 유지됩니다. `SHOW TABLES` 명령을 사용하여 테이블과 연결된 레이블에 대한 정보를 제공하는 추가 `labels` 열을 표시합니다.

이 명령의 출력 예는 다음과 같습니다.

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
|---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

앞에서 설명한 대로 `table_with_a_decile`이(가) 프로필에 대해 활성화되어 있고 [&#39; 업데이트&#39;](#enable-upsert-functionality-for-dataset), [&#39; 프로필&#39;](#enable-existing-dataset-for-profile) 등의 레이블이 적용된 것을 예제에서 확인할 수 있습니다.

### SQL로 필드 그룹 만들기

이제 SQL을 사용하여 필드 그룹을 만들 수 있습니다. Experience Platform UI 내에서 스키마 편집기를 사용하거나 스키마 레지스트리에 대한 API 호출을 수행하는 것에 대한 대안을 제공합니다.

필드 그룹을 만드는 예제 문은 아래에서 볼 수 있습니다.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>문에 `label` 플래그가 제공되지 않았거나 필드 그룹이 이미 있는 경우 SQL을 통한 필드 그룹 만들기가 실패합니다.
>&#x200B;>필드 그룹이 이미 있으므로 쿼리가 실패하는 것을 방지하기 위해 쿼리에 `IF NOT EXISTS` 절이 포함되어 있는지 확인하십시오.

실제 예는 아래에 표시된 것과 유사하게 나타날 수 있습니다.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

이 문이 성공적으로 실행되면 생성된 필드 그룹 ID가 반환됩니다. 예 `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

대체 메서드에 대한 자세한 내용은 [스키마 편집기에서 새 필드 그룹을 만드는 방법](../../../xdm/ui/resources/field-groups.md#create) 또는 [스키마 레지스트리 API](../../../xdm/api/field-groups.md#create)를 사용하는 방법에 대한 설명서를 참조하십시오.

### 필드 그룹 끌어 놓기

스키마 레지스트리에서 필드 그룹을 제거해야 하는 경우가 있습니다. 필드 그룹 ID로 `DROP FIELDGROUP` 명령을 실행하면 됩니다.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

예:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>필드 그룹이 없으면 SQL을 통해 필드 그룹을 삭제할 수 없습니다. 쿼리 실패를 방지하기 위해 문에 `IF EXISTS` 절이 포함되어 있는지 확인하십시오.

### 테이블의 필드 그룹 이름 및 ID 모두 표시

`SHOW FIELDGROUPS` 명령은 테이블의 이름, 필드 그룹 ID 및 소유자가 포함된 테이블을 반환합니다.

이 명령의 출력 예는 다음과 같습니다.

```sql
       name                      |        fieldgroupId                             |     owner      |
|---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## 다음 단계

이 문서를 읽은 후에는 SQL을 사용하여 파생된 데이터 세트를 기반으로 프로필 및 업데이트 사용 데이터 세트를 만드는 방법을 더 잘 이해할 수 있습니다. 이제 일괄 처리 수집 워크플로우로 이 데이터 세트를 사용하여 프로필 데이터를 업데이트할 준비가 되었습니다. Adobe Experience Platform으로 데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../../ingestion/home.md)를 읽는 것부터 시작해 보십시오.
