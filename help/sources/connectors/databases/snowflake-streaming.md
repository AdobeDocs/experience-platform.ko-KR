---
title: Snowflake 스트리밍 Source 커넥터 개요
description: 소스 연결 및 데이터 흐름을 만들어 Snowflake 인스턴스에서 Adobe Experience Platform으로 스트리밍 데이터를 수집하는 방법을 알아봅니다
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-09-24T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 1%

---

# [!DNL Snowflake] 스트리밍 원본

>[!IMPORTANT]
>
>* [!DNL Snowflake] 스트리밍 소스는 Real-Time CDP Ultimate을 구매한 사용자에게 API에서 사용할 수 있습니다.
>
>* 이제 Amazon Web Services(AWS)에서 Adobe Experience Platform을 실행할 때 [!DNL Snowflake] 스트리밍 소스를 사용할 수 있습니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../landing/multi-cloud.md)를 참조하세요.


Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform에서는 [!DNL Snowflake] 데이터베이스에서 데이터를 스트리밍할 수 있습니다.

## [!DNL Snowflake] 스트리밍 원본 이해

[!DNL Snowflake] 스트리밍 원본은 SQL 쿼리를 주기적으로 실행하고 결과 집합에서 각 행에 대한 출력 레코드를 만들어 데이터를 로드하여 작동합니다.

[!DNL Kafka Connect]을(를) 사용하여 [!DNL Snowflake] 스트리밍 소스는 다음 반복에 대한 올바른 위치에서 시작할 수 있도록 각 테이블에서 받은 최신 레코드를 추적합니다. 소스는 이 기능을 사용하여 데이터를 필터링하고 각 반복의 테이블에서 업데이트된 행만 가져옵니다.

## 전제 조건

다음 섹션에서는 [!DNL Snowflake] 데이터베이스에서 Experience Platform으로 데이터를 스트리밍하기 전에 완료해야 하는 필수 조건 단계에 대해 설명합니다.

### IP 주소 허용 목록 업데이트

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources) 페이지를 참조하세요.

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Amazon Redshift]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Snowflake]과(와) 연결하려면 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `account` | `snowflakecomputing.com` 접미사가 추가된 [!DNL Snowflake] 계정의 전체 계정 식별자(계정 이름 또는 계정 로케이터)입니다. 계정 식별자는 다양한 형식일 수 있습니다. <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com(예: `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (예: `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (예: `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> 자세한 내용은 [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>)을(를) 참조하십시오. |
| `warehouse` | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이므로 Experience Platform으로 데이터를 가져올 때 개별적으로 액세스해야 합니다. |
| `database` | [!DNL Snowflake] 데이터베이스에 Experience Platform으로 가져올 데이터가 있습니다. |
| `username` | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| `password` | [!DNL Snowflake] 사용자 계정의 암호입니다. |
| `role` | (선택 사항) 지정된 연결에 대해 사용자에게 제공할 수 있는 사용자 정의 역할입니다. 지정하지 않으면 이 값은 기본적으로 `public`(으)로 설정됩니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Snowflake]의 연결 사양 ID는 `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`입니다. |

{style="table-layout:auto"}

### 역할 설정 구성 {#configure-role-settings}

기본 공용 역할이 할당되었더라도 소스 연결이 관련 [!DNL Snowflake] 데이터베이스, 스키마 및 테이블에 액세스할 수 있도록 역할에 대한 권한을 구성해야 합니다. 서로 다른 [!DNL Snowflake] 엔터티에 대한 다양한 권한은 다음과 같습니다.

| [!DNL Snowflake] 엔터티 | 역할 권한 필요 |
| --- | --- |
| 웨어하우스 | 운영, 사용 |
| 데이터베이스 | 사용 |
| 스키마 | 사용 |
| 테이블 | 선택 |

>[!NOTE]
>
>창고의 고급 설정 구성에서 자동 재개 및 자동 일시 중지를 활성화해야 합니다.

역할 및 권한 관리에 대한 자세한 내용은 [[!DNL Snowflake] API 참조](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>)를 참조하세요.

## 제한 사항 및 FAQ {#limitations-and-frequently-asked-questions}

* [!DNL Snowflake] 원본의 데이터 처리량은 초당 레코드 2000개입니다.
* 창고가 활성화된 시간과 창고 크기에 따라 가격 책정이 달라질 수 있다. [!DNL Snowflake] 소스 통합의 경우 가장 작은 크기의 x-small 웨어하우스로 충분합니다. 자동 중지를 가능하게 하여 창고가 미사용 시 자체적으로 중지를 할 수 있도록 할 것을 제안한다.
* [!DNL Snowflake] 원본은 10초마다 새 데이터를 위해 데이터베이스를 폴링합니다.
* 구성 옵션:
   * 소스 연결을 만들 때 [!DNL Snowflake] 소스에 대해 `backfill` 부울 플래그를 사용하도록 설정할 수 있습니다.
      * backfill 이 true 로 설정되면 timestamp.initial 의 값이 0으로 설정됩니다. 즉, 타임스탬프 열이 0 epoch 시간보다 큰 데이터를 가져옵니다.
      * backfill 이 false 로 설정되어 있으면 timestamp.initial 의 값이 -1 로 설정됩니다. 즉, 타임스탬프 열이 현재 시간(소스가 수집을 시작하는 시간)보다 큰 데이터를 가져옵니다.
   * 타임스탬프 열의 형식은 `TIMESTAMP_LTZ` 또는 `TIMESTAMP_NTZ` 형식으로 지정해야 합니다. 타임스탬프 열이 `TIMESTAMP_NTZ`(으)로 설정된 경우 값이 저장된 해당 시간대가 `timezoneValue` 매개 변수를 통해 전달되어야 합니다. 제공되지 않는 경우 값은 기본적으로 UTC로 설정됩니다.
      * `TIMESTAMP_TZ`은(는) 타임스탬프 열 또는 매핑에서 사용할 수 없습니다.

## 다음 단계

>[!NOTE]
>
>스트리밍 데이터 흐름을 만들거나 업데이트한 후 데이터 손실 또는 데이터 감소의 잠재적 인스턴스를 방지하기 위해 데이터 수집에서 5분 정도의 짧은 일시 중지가 필요합니다.

다음 자습서에서는 API를 사용하여 [!DNL Snowflake] 스트리밍 소스를 Experience Platform에 연결하는 방법에 대한 단계를 제공합니다.

* [흐름 서비스 API를 사용하여  [!DNL Snowflake] 데이터베이스에서 Experience Platform으로 데이터 스트리밍](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Experience Platform 사용자 인터페이스의 소스 작업 영역을 사용하여  [!DNL Snowflake] 데이터베이스에서 Experience Platform으로 데이터 스트리밍](../../tutorials/ui/create/databases/snowflake-streaming.md)
