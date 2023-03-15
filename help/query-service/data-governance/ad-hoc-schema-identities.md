---
title: Ad Hoc 데이터 세트에서 기본 Id 설정
description: Adobe Experience Platform Query Service를 사용하면 SQL ALTER TABLE 명령을 통해 직접 임시 스키마 데이터 세트 필드에 ID 또는 기본 ID를 설정할 수 있습니다. 이 문서에서는 ALTER TABLE 명령을 사용하여 기본 ID 또는 보조 ID를 설정하는 방법에 대해 설명합니다.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# 임시 데이터 세트에서 기본 ID 설정

Adobe Experience Platform Query Service를 사용하면 SQL에 대한 제약 조건을 사용하여 데이터 세트 열을 기본 또는 보조 ID로 표시할 수 있습니다 `ALTER TABLE` 명령입니다. 이 기능을 사용하여 플래그가 지정된 필드가 데이터 개인 정보 보호 요구 사항과 일치하도록 할 수 있습니다. 이 명령을 사용하면 SQL을 통해 직접 기본 및 보조 ID 테이블 열에 대한 제약 조건을 추가하거나 삭제할 수 있습니다.

## 시작하기

데이터 세트 열에 기본 또는 보조 ID로 레이블을 지정하려면 다음을 이해해야 합니다. `ALTER TABLE` SQL 명령 및 데이터 개인 정보 보호 요구 사항에 대한 올바른 이해. 이 문서를 계속하기 전에 다음 설명서를 검토하십시오.

* [다음에 대한 SQL 구문 안내서 `ALTER TABLE` 명령](../sql/syntax.md).
* [데이터 거버넌스 개요](../../data-governance/home.md) 추가 정보.

## 제한 추가 {#add-constraints}

다음 `ALTER TABLE` 명령을 사용하면 데이터 세트 열에 레이블을 개인의 id로 지정한 다음 SQL을 사용하여 관련 메타데이터를 업데이트하여 해당 레이블을 기본 id로 사용할 수 있습니다. 이 기능은 Platform UI를 통해 스키마에서 직접 가져오는 대신 SQL을 통해 데이터 세트를 만들 때 특히 유용합니다. 이 명령은 플랫폼 내의 데이터 작업이 데이터 사용 정책을 준수하는지 확인하는 데 사용할 수 있습니다.

**예**

다음 예제에서는 기존 파일에 제약 조건을 추가합니다 `t1` 테이블. 의 값 `id` 열은 이제 아래의 기본 ID로 표시됩니다. `IDFA` 네임스페이스입니다. ID 네임스페이스는 필드가 나타내는 ID 데이터 유형을 선언하는 키워드입니다.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

두 번째 예에서는 `id` 열이 보조 ID로 표시됩니다.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## 드롭 제한 {#drop-constraints}

테이블 열에서 제약 조건을 제거할 수도 있습니다. `ALTER TABLE` 명령입니다.

**예**

다음 예제에서는 `c1` 열은 기존 ID에서 기본 ID로 레이블이 지정됨 `t1` 테이블.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

아래에서 보듯이 ID 제약 조건을 제거할 때와 동일한 구문이 사용됩니다.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## ID 표시

metadata 명령 사용 `show identities` 를 사용하여 id로 지정된 모든 특성이 있는 테이블을 표시할 수 있습니다.

```shell
> show identities;
```

반환된 테이블의 예가 아래에 표시됩니다.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM 제한 사항 {#limitations}

다음 목록은 XDM을 사용할 때 기존 데이터 세트에서 ID를 업데이트할 때 고려해야 할 중요한 사항을 설명합니다.

* 열을 ID로 지정하려면 다음을 수행합니다 **필수** 또한 열의 메타데이터로 유지할 네임스페이스를 정의합니다.
* XDM은 네임스페이스 특성에서 열 이름 지정을 지원하지 않습니다.
* 스키마에서 `identityMap` 루트 또는 최상위 수준인 XDM 필드 `identityMap` 오브젝트 **필수** id 또는 기본 id로 레이블이 지정됩니다.
