---
title: API에서 소스 연결에 대한 변경 데이터 캡처 활성화
description: API에서 소스 연결에 변경 데이터 캡처를 활성화하는 방법을 알아봅니다
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# API에서 소스 연결에 대한 변경 데이터 캡처 활성화

Adobe Experience Platform 소스의 변경 데이터 캡처는 소스와 대상 시스템 간의 실시간 데이터 동기화를 유지 관리하는 데 사용할 수 있는 기능입니다.

현재 Experience Platform에서는 **증분 데이터 복사**&#x200B;를 지원하므로 소스 시스템에서 새로 생성되거나 업데이트된 레코드가 수집된 데이터 세트에 정기적으로 복사됩니다. 이 프로세스는 변경 사항을 추적하고 **새로 삽입되거나 업데이트된 데이터만**&#x200B;을(를) 캡처하기 위해 `LastModified`타임스탬프 열&#x200B;**(예:**)을 사용합니다. 그러나 이 방법은 삭제된 레코드를 고려하지 않으므로 시간이 지남에 따라 데이터 불일치가 발생할 수 있습니다.

변경 데이터 캡처를 사용하면 지정된 흐름이 삽입, 업데이트 및 삭제를 포함하여 모든 변경 사항을 캡처하고 적용합니다. 마찬가지로 Experience Platform 데이터 세트는 소스 시스템과 완전히 동기화된 상태로 유지됩니다.

다음 소스에 대해 변경 데이터 캡처를 사용할 수 있습니다.

## [!DNL Amazon S3]

Experience Platform으로 수집할 `_change_request_type` 파일에 [!DNL Amazon S3]이(가) 있는지 확인하십시오. 또한 파일에 다음 유효한 값이 포함되어 있는지 확인해야 합니다.

* `u`: 삽입 및 업데이트용
* `d`: 삭제용.

`_change_request_type`이(가) 파일에 없으면 `u`의 기본값이 사용됩니다.

[!DNL Amazon S3] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Amazon S3] 기본 연결 만들기](../api/create/cloud-storage/s3.md).
* [클라우드 저장소에 대한 원본 연결을 만듭니다](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Blob]

Experience Platform으로 수집할 `_change_request_type` 파일에 [!DNL Azure Blob]이(가) 있는지 확인하십시오. 또한 파일에 다음 유효한 값이 포함되어 있는지 확인해야 합니다.

* `u`: 삽입 및 업데이트용
* `d`: 삭제용.

`_change_request_type`이(가) 파일에 없으면 `u`의 기본값이 사용됩니다.

[!DNL Azure Blob] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Azure Blob] 기본 연결 만들기](../api/create/cloud-storage/blob.md).
* [클라우드 저장소에 대한 원본 연결을 만듭니다](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Azure Databricks]

원본 연결에서 변경 데이터 캡처를 사용하려면 **테이블에서**&#x200B;변경 데이터 피드[!DNL Azure Databricks]를 사용하도록 설정해야 합니다.

다음 명령을 사용하여 [!DNL Azure Databricks]에서 데이터 피드 변경 옵션을 명시적으로 사용하도록 설정하십시오.

**새 테이블**

변경 데이터 피드를 새 테이블에 적용하려면 `delta.enableChangeDataFeed` 명령에서 테이블 속성 `TRUE`을(를) `CREATE TABLE`(으)로 설정해야 합니다.

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**기존 테이블**

기존 테이블에 변경 데이터 피드를 적용하려면 `delta.enableChangeDataFeed` 명령에서 테이블 속성 `TRUE`을(를) `ALTER TABLE`(으)로 설정해야 합니다.

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**새 테이블 모두**

모든 새 테이블에 변경 데이터 피드를 적용하려면 기본 속성을 `TRUE`(으)로 설정해야 합니다.

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

자세한 내용은 변경 데이터 피드를 사용하는 방법에 대한 [[!DNL Azure Databricks] 안내서](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed)를 참조하세요.

[!DNL Azure Databricks] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Azure Databricks] 기본 연결 만들기](../api/create/databases/databricks.md).
* [데이터베이스에 대한 원본 연결을 만듭니다](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Data Landing Zone]

원본 연결에서 변경 데이터 캡처를 사용하려면 **테이블에서**&#x200B;변경 데이터 피드[!DNL Data Landing Zone]를 사용하도록 설정해야 합니다.

[!DNL Data Landing Zone]에서 데이터 피드 변경 옵션을 명시적으로 활성화하려면 다음 명령을 사용하십시오.

[!DNL Data Landing Zone] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Data Landing Zone] 기본 연결 만들기](../api/create/cloud-storage/data-landing-zone.md).
* [클라우드 저장소에 대한 원본 연결을 만듭니다](../api/collect/cloud-storage.md#create-a-source-connection).

## [!DNL Google BigQuery]

[!DNL Google BigQuery] 원본 연결에서 변경 데이터 캡처를 사용하려면 [!DNL Google BigQuery] 콘솔에서 [!DNL Google Cloud] 페이지로 이동하여 `enable_change_history`을(를) `TRUE`(으)로 설정합니다. 이 속성을 사용하면 데이터 테이블에 대한 변경 내역을 사용할 수 있습니다.

자세한 내용은 [ [!DNL GoogleSQL]의 ](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list)데이터 정의 언어 구문에 대한 안내서를 참조하십시오.

[!DNL Google BigQuery] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Google BigQuery] 기본 연결 만들기](../api/create/databases/bigquery.md).
* [데이터베이스에 대한 원본 연결을 만듭니다](../api/collect/database-nosql.md#create-a-source-connection).

## [!DNL Google Cloud Storage]

Experience Platform으로 수집할 `_change_request_type` 파일에 [!DNL Google Cloud Storage]이(가) 있는지 확인하십시오. 또한 파일에 다음 유효한 값이 포함되어 있는지 확인해야 합니다.

* `u`: 삽입 및 업데이트용
* `d`: 삭제용.

`_change_request_type`이(가) 파일에 없으면 `u`의 기본값이 사용됩니다.

[!DNL Google Cloud Storage] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Google Cloud Storage] 기본 연결 만들기](../api/create/cloud-storage/google.md).
* [클라우드 저장소에 대한 원본 연결을 만듭니다](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL SFTP]

Experience Platform으로 수집할 `_change_request_type` 파일에 [!DNL SFTP]이(가) 있는지 확인하십시오. 또한 파일에 다음 유효한 값이 포함되어 있는지 확인해야 합니다.

* `u`: 삽입 및 업데이트용
* `d`: 삭제용.

`_change_request_type`이(가) 파일에 없으면 `u`의 기본값이 사용됩니다.

[!DNL SFTP] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL SFTP] 기본 연결 만들기](../api/create/cloud-storage/sftp.md).
* [클라우드 저장소에 대한 원본 연결을 만듭니다](../api/collect/cloud-storage.md#create-a-source-connection).


## [!DNL Snowflake]

원본 연결에서 변경 데이터 캡처를 사용하려면 **테이블에서**&#x200B;변경 내용 추적[!DNL Snowflake]을 사용하도록 설정해야 합니다.

[!DNL Snowflake]에서 `ALTER TABLE`을(를) 사용하고 `CHANGE_TRACKING`을(를) `TRUE`(으)로 설정하여 변경 내용 추적을 사용하도록 설정합니다.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

자세한 내용은 [[!DNL Snowflake] 변경 내용 절 사용 가이드](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes)를 참조하십시오.

[!DNL Snowflake] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Snowflake] 기본 연결 만들기](../api/create/databases/snowflake.md).
* [데이터베이스에 대한 원본 연결을 만듭니다](../api/collect/database-nosql.md#create-a-source-connection).

