---
title: API에서 소스 연결에 대한 변경 데이터 캡처 활성화
description: API에서 소스 연결에 변경 데이터 캡처를 활성화하는 방법을 알아봅니다
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: 2ad0ffba128e8c51f173d24d4dd2404b9cbbb59a
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# API에서 소스 연결에 대한 변경 데이터 캡처 활성화

Adobe Experience Platform 소스의 변경 데이터 캡처를 사용하여 소스 및 대상 시스템을 거의 실시간으로 동기화합니다.

Experience Platform은 현재 새로 생성되거나 업데이트된 레코드를 소스 시스템에서 수집된 데이터 세트로 정기적으로 전송하는 **증분 데이터 복사**&#x200B;를 지원합니다. 이 방법은 **timestamp 열**&#x200B;을 사용하여 변경 내용을 추적하지만 삭제를 감지하지 않으므로 시간이 지남에 따라 데이터가 일치하지 않을 수 있습니다.

반면 변경 데이터 캡처는 거의 실시간으로 삽입, 업데이트 및 삭제를 캡처하고 적용합니다. 이러한 포괄적인 변경 사항 추적을 통해 데이터 세트를 소스 시스템과 완벽하게 연계하고 변동분 복제본이 지원하는 것 이상의 완벽한 변경 내역을 제공할 수 있습니다. 그러나 삭제 작업은 대상 데이터 세트를 사용하는 모든 애플리케이션에 영향을 미치므로 특별히 고려해야 합니다.

Experience Platform에서 데이터 캡처를 변경하려면 **[관계형 스키마](../../../xdm/data-mirror/overview.md)**&#x200B;가 있는 [Data Mirror](../../../xdm/schema/relational.md)이(가) 필요합니다. 다음 두 가지 방법으로 Data Mirror에 변경 데이터를 제공할 수 있습니다.

* **[수동 변경 추적](#file-based-sources)**: 변경 데이터 캡처 레코드를 기본적으로 생성하지 않는 소스의 데이터 집합에 `_change_request_type` 열을 포함합니다
* **[기본 변경 데이터 캡처 내보내기](#database-sources)**: 소스 시스템에서 직접 내보낸 변경 데이터 캡처 레코드를 사용합니다.

두 가지 접근 방식 모두 관계를 유지하고 고유성을 적용하기 위해 Data Mirror에 관계형 스키마가 있어야 합니다.

## 관계형 스키마가 있는 Data Mirror

>[!AVAILABILITY]
>
>Adobe Journey Optimizer **오케스트레이션된 캠페인** 라이선스 소유자는 Data Mirror 및 관계형 스키마를 사용할 수 있습니다. 또한 라이선스 및 기능 활성화에 따라 Customer Journey Analytics 사용자를 위한 **제한된 릴리스**(으)로도 사용할 수 있습니다. 액세스하려면 Adobe 담당자에게 문의하십시오.

>[!NOTE]
>
>이전 버전의 Adobe Experience Platform 설명서에서는 관계형 스키마를 모델 기반 스키마라고 했습니다. 기능 및 변경 데이터 캡처 기능은 그대로 유지됩니다.

>[!NOTE]
>
>**오케스트레이션된 캠페인 사용자**: 이 문서에 설명된 Data Mirror 기능을 사용하여 참조 무결성을 유지하는 고객 데이터를 사용합니다. 소스에서 변경 데이터 캡처 형식을 사용하지 않더라도 Data Mirror에서는 기본 키 적용, 레코드 수준 업데이트 및 스키마 관계와 같은 관계형 기능을 지원합니다. 이러한 기능은 연결된 데이터 세트 간에 일관되고 안정적인 데이터 모델링을 보장합니다.

Data Mirror은 관계형 스키마를 사용하여 변경 데이터 캡처를 확장하고 고급 데이터베이스 동기화 기능을 활성화합니다. Data Mirror에 대한 개요는 [Data Mirror 개요](../../../xdm/data-mirror/overview.md)를 참조하십시오.

관계형 스키마는 Experience Platform을 확장하여 기본 키 고유성을 적용하고, 행 수준 변경 사항을 추적하고, 스키마 수준 관계를 정의합니다. 변경 데이터 캡처를 사용하면 데이터 레이크에서 직접 삽입, 업데이트 및 삭제를 적용하여 추출, 변환, 로드(ETL) 또는 수동 조정에 대한 필요성을 줄일 수 있습니다.

자세한 내용은 [관계형 스키마 개요](../../../xdm/schema/relational.md)를 참조하십시오.

### 변경 데이터 캡처를 위한 관계형 스키마 요구 사항

변경 데이터 캡처와 함께 관계형 스키마를 사용하기 전에 다음 식별자를 구성합니다.

* 기본 키로 각 레코드를 고유하게 식별합니다.
* 버전 식별자를 사용하여 업데이트를 순차적으로 적용합니다.
* 시계열 스키마의 경우 타임스탬프 식별자를 추가합니다.

### 컨트롤 열 처리 {#control-column-handling}

`_change_request_type` 열을 사용하여 각 행의 처리 방법을 지정하십시오.

* `u` — 업데이트(열이 없는 경우 기본값)
* `d` — 삭제

이 열은 수집 중에만 평가되며 XDM 필드에 저장되거나 매핑되지 않습니다.

### 워크플로 {#workflow}

관계형 스키마를 사용하여 변경 데이터 캡처를 활성화하려면 다음을 수행합니다.

1. 관계형 스키마를 만듭니다.
2. 필수 설명자를 추가합니다.
   * [기본 키 설명자](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [버전 설명자](../../../xdm/api/descriptors.md#version-descriptor)
   * [타임스탬프 설명자](../../../xdm/api/descriptors.md#timestamp-descriptor)(시계열만 해당)
3. 스키마에서 데이터 세트를 만들고 변경 데이터 캡처를 활성화합니다.
4. 파일 기반 수집에만 해당: 삭제 작업을 명시적으로 지정해야 하는 경우 `_change_request_type` 열을 소스 파일에 추가합니다. CDC 내보내기 구성은 데이터베이스 소스에 대해 이 작업을 자동으로 처리합니다.
5. 수집을 활성화하려면 소스 연결 설정을 완료하십시오.

>[!NOTE]
>
>행 수준 변경 동작을 명시적으로 제어하려는 경우 `_change_request_type` 열은 파일 기반 소스(Amazon S3, Azure Blob, Google Cloud Storage, SFTP)에만 필요합니다. 기본 CDC 기능이 있는 데이터베이스 소스의 경우 변경 작업은 CDC 내보내기 구성을 통해 자동으로 처리됩니다. 파일 기반 수집은 기본적으로 업데이트 작업을 가정합니다. 파일 업로드에서 삭제 작업을 지정하려면 이 열만 추가하면 됩니다.

>[!IMPORTANT]
>
>**데이터 삭제 계획이 필요합니다**. 관계형 스키마를 사용하는 모든 애플리케이션은 변경 데이터 캡처를 구현하기 전에 삭제 의미를 이해해야 합니다. 삭제 작업이 관련 데이터 세트, 규정 준수 요구 사항 및 다운스트림 프로세스에 미치는 영향에 대해 계획합니다. 지침은 [데이터 위생 고려 사항](../../../hygiene/ui/record-delete.md#relational-record-delete)을 참조하세요.

## 파일 기반 소스에 대한 변경 데이터 제공 {#file-based-sources}

>[!IMPORTANT]
>
>파일 기반 변경 데이터 캡처를 사용하려면 관계형 스키마가 있는 Data Mirror이 필요합니다. 아래 파일 서식 단계를 따르려면 먼저 이 문서의 앞부분에서 설명한 [Data Mirror 설치 워크플로](#workflow)를 완료하십시오. 아래 단계에서는 Data Mirror에서 처리할 변경 내용 추적 정보를 포함하도록 데이터 파일의 형식을 지정하는 방법을 설명합니다.

파일 기반 원본([!DNL Amazon S3], [!DNL Azure Blob], [!DNL Google Cloud Storage] 및 [!DNL SFTP])의 경우 파일에 `_change_request_type` 열을 포함하십시오.

위의 `_change_request_type`컨트롤 열 처리[ 섹션에 정의된 ](#control-column-handling) 값을 사용하십시오.

>[!IMPORTANT]
>
>**파일 기반 원본 전용**&#x200B;의 경우 변경 내용 추적 기능의 유효성을 검사하려면 특정 응용 프로그램에 `_change_request_type`(업데이트) 또는 `u`(삭제)이 포함된 `d` 열이 필요할 수 있습니다. 예를 들어 Adobe Journey Optimizer의 **오케스트레이션된 캠페인** 기능을 사용하려면 이 열이 &quot;오케스트레이션된 캠페인&quot; 전환을 활성화하고 타깃팅을 위한 데이터 세트 선택을 허용해야 합니다. 애플리케이션별 유효성 검사 요구 사항은 다를 수 있습니다.

아래의 소스별 단계를 따르십시오.

### 클라우드 스토리지 소스 {#cloud-storage-sources}

다음 단계를 수행하여 클라우드 스토리지 소스에 대한 변경 데이터 캡처를 활성화합니다.

1. 소스에 대한 기본 연결 만들기:

   | 소스 | Base 연결 안내서 |
   |---|---|
   | [!DNL Amazon S3] | [기본 연결 만들기 [!DNL Amazon S3] 기본 연결 만들기](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [기본 연결 만들기 [!DNL Azure Blob] 기본 연결 만들기](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [기본 연결 만들기 [!DNL Google Cloud Storage] 기본 연결 만들기](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [기본 연결 만들기 [!DNL SFTP] 기본 연결 만들기](../api/create/cloud-storage/sftp.md) |

2. [클라우드 저장소에 대한 원본 연결을 만듭니다](../api/collect/cloud-storage.md#create-a-source-connection).

모든 클라우드 저장소 원본은 위의 `_change_request_type`파일 기반 원본[ 섹션에서 설명한 것과 동일한 ](#file-based-sources) 열 형식을 사용합니다.

## 데이터베이스 소스 {#database-sources}

### [!DNL Azure Databricks]

[!DNL Azure Databricks]에서 변경 데이터 캡처를 사용하려면 소스 테이블에서 **변경 데이터 피드**&#x200B;를 사용하도록 설정하고 Experience Platform에서 관계형 스키마로 Data Mirror을 구성해야 합니다.

다음 명령을 사용하여 테이블에서 변경 데이터 피드를 활성화합니다.

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

### [!DNL Data Landing Zone]

[!DNL Data Landing Zone]에서 변경 데이터 캡처를 사용하려면 소스 테이블에서 **변경 데이터 피드**&#x200B;를 사용하도록 설정하고 Experience Platform에서 관계형 스키마로 Data Mirror을 구성해야 합니다.

[!DNL Data Landing Zone] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Data Landing Zone] 기본 연결 만들기](../api/create/cloud-storage/data-landing-zone.md).
* [클라우드 저장소에 대한 원본 연결을 만듭니다](../api/collect/cloud-storage.md#create-a-source-connection).

### [!DNL Google BigQuery]

[!DNL Google BigQuery]과(와) 함께 변경 데이터 캡처를 사용하려면 소스 테이블에서 변경 기록을 활성화하고 Experience Platform의 관계형 스키마로 Data Mirror을 구성해야 합니다.

[!DNL Google BigQuery] 원본 연결에서 변경 기록을 사용하려면 [!DNL Google BigQuery] 콘솔에서 [!DNL Google Cloud] 페이지로 이동하여 `enable_change_history`을(를) `TRUE`(으)로 설정하십시오. 이 속성을 사용하면 데이터 테이블에 대한 변경 내역을 사용할 수 있습니다.

자세한 내용은 [ [!DNL GoogleSQL]의 ](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list)데이터 정의 언어 구문에 대한 안내서를 참조하십시오.

[!DNL Google BigQuery] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Google BigQuery] 기본 연결 만들기](../api/create/databases/bigquery.md).
* [데이터베이스에 대한 원본 연결을 만듭니다](../api/collect/database-nosql.md#create-a-source-connection).

### [!DNL Snowflake]

[!DNL Snowflake]과(와) 함께 변경 데이터 캡처를 사용하려면 소스 테이블에서 **변경 추적**&#x200B;을 사용하도록 설정하고 Experience Platform의 관계형 스키마로 Data Mirror을 구성해야 합니다.

[!DNL Snowflake]에서 `ALTER TABLE`을(를) 사용하고 `CHANGE_TRACKING`을(를) `TRUE`(으)로 설정하여 변경 내용 추적을 사용하도록 설정합니다.

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

자세한 내용은 [[!DNL Snowflake] 변경 내용 절 사용 가이드](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes)를 참조하십시오.

[!DNL Snowflake] 소스 연결에 변경 데이터 캡처를 활성화하는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [기본 연결 만들기 [!DNL Snowflake] 기본 연결 만들기](../api/create/databases/snowflake.md).
* [데이터베이스에 대한 원본 연결을 만듭니다](../api/collect/database-nosql.md#create-a-source-connection).
