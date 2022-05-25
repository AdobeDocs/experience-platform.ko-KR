---
title: Ad Hoc 데이터 세트에서 기본 ID 설정
description: Adobe Experience Platform 쿼리 서비스를 사용하면 SQL ALTER TABLE 명령을 통해 직접 임시 스키마 데이터 세트 필드의 ID 또는 기본 ID를 설정할 수 있습니다. 이 문서에서는 ALTER TABLE 명령을 사용하여 기본 ID 또는 보조 ID를 설정하는 방법을 설명합니다.
source-git-commit: bf51fc3e0c9635c0555f87f3389fb4a9542c092d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# 임시 데이터 세트에서 기본 ID 설정

Adobe Experience Platform Query Service를 사용하면 SQL에 대한 제약 조건을 사용하여 데이터 세트 열을 기본 또는 보조 ID로 표시할 수 있습니다 `ALTER TABLE` 명령. 이 기능을 사용하여 플래그가 지정된 필드가 데이터 개인 정보 보호 요구 사항과 일치하는지 확인할 수 있습니다. 이 명령을 사용하면 SQL을 통해 직접 주 ID 테이블 열과 보조 ID 테이블 열 모두에 대한 제약 조건을 추가하거나 삭제할 수 있습니다.

## 시작하기

데이터 세트 열을 기본 또는 보조 ID로 레이블링하려면 `ALTER TABLE` SQL 명령 및 데이터 개인 정보 보호 요구 사항을 잘 이해합니다. 이 문서를 계속하기 전에 다음 설명서를 검토하십시오.

* [에 대한 SQL 구문 안내서 `ALTER TABLE` 명령](../sql/syntax.md).
* [데이터 거버넌스 개요](../../data-governance/home.md) 추가 정보.

## 제한 추가 {#add-constraints}

다음 `ALTER TABLE` 명령을 사용하면 데이터 집합 열에 개인 ID로 레이블을 지정한 다음 SQL을 사용하여 연결된 메타데이터를 업데이트하여 해당 레이블을 기본 ID로 사용할 수 있습니다. 이 기능은 Platform UI를 통해 스키마에서 직접 생성되는 것이 아니라 SQL을 통해 데이터 세트를 만들 때 특히 유용합니다. 명령을 사용하여 플랫폼 내의 데이터 작업이 데이터 사용 정책을 준수하도록 할 수 있습니다.

**예**

다음 예제에서는 기존 `t1` 테이블. 의 값 `id` 이제 열은 `IDFA` 네임스페이스. ID 네임스페이스는 필드가 나타내는 ID 데이터 유형을 선언하는 키워드입니다.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

두 번째 예에서는 `id` 열은 보조 id로 표시됩니다.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## 드롭 제한 {#drop-constraints}

제약 조건은 `ALTER TABLE` 명령.

**예**

다음 예에서는 `c1` 열은 기존 `t1` 테이블.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

아래에서 보듯이 ID 제약 조건을 제거할 때도 동일한 구문을 사용합니다.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## ID 표시

메타데이터 명령 사용 `show identities` 명령줄 인터페이스에서 ID로 지정된 모든 특성이 있는 테이블을 표시합니다.

```shell
> show identities;
```

반환된 테이블의 예는 아래에 나와 있습니다.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM 제한 사항 {#limitations}

다음 목록에서는 XDM을 사용할 때 기존 데이터 세트에서 ID를 업데이트하는 데 중요한 고려 사항을 설명합니다.

* 열을 ID로 지정하려면 **반드시** 또한 열의 메타데이터로 유지할 네임스페이스를 정의합니다.
* XDM은 네임스페이스 속성에서 열 이름을 지정하는 것을 지원하지 않습니다.
* 스키마에 `identityMap` XDM 필드, 루트 또는 최상위 수준 `identityMap` 개체 **반드시** id 또는 기본 id로 레이블이 지정됩니다.
