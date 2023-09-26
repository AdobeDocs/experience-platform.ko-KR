---
title: Snowflake 스트리밍 소스 커넥터 개요
description: 소스 연결 및 데이터 흐름을 만들어 Snowflake 인스턴스에서 Adobe Experience Platform으로 스트리밍 데이터를 수집하는 방법을 알아봅니다
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: 054175bd3f3aaab73c8cca249eaf1a9cdbc8deab
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 1%

---

# [!DNL Snowflake] 스트리밍 소스

>[!IMPORTANT]
>
>* 다음 [!DNL Snowflake] 스트리밍 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.
>* 다음 [!DNL Snowflake] 스트리밍 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 API에서 사용할 수 있습니다.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 의 데이터 스트리밍을 지원합니다. [!DNL Snowflake] 데이터베이스.

## 이해 [!DNL Snowflake] 스트리밍 소스

다음 [!DNL Snowflake] 스트리밍 소스는 주기적으로 SQL 쿼리를 실행하고 결과 집합의 각 행에 대한 출력 레코드를 만들어 데이터를 로드함으로써 작동합니다.

사용 [!DNL Kafka Connect], [!DNL Snowflake] 스트리밍 소스는 각 테이블에서 받은 최신 레코드를 추적하므로 다음 반복의 올바른 위치에서 시작할 수 있습니다. 소스는 이 기능을 사용하여 데이터를 필터링하고 각 반복의 테이블에서 업데이트된 행만 가져옵니다.

## 전제 조건

다음 섹션에서는 의 데이터를 스트리밍하기 전에 완료해야 하는 사전 요구 사항에 대해 설명합니다. [!DNL Snowflake] Experience Platform 대상 데이터베이스:

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 연결 대상 [!DNL Snowflake], 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `account` | 와(과) 연결된 전체 계정 이름 [!DNL Snowflake] 계정입니다. 완전한 자격을 갖춘 [!DNL Snowflake] 계정 이름에는 계정 이름, 지역 및 클라우드 플랫폼이 포함됩니다. 예, `cj12345.east-us-2.azure`. 계정 이름에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | 다음 [!DNL Snowflake] warehouse는 애플리케이션의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] warehouse는 서로 독립적이며 데이터를 Platform으로 가져올 때 개별적으로 액세스해야 합니다. |
| `database` | 다음 [!DNL Snowflake] 데이터베이스에는 플랫폼으로 가져올 데이터가 포함되어 있습니다. |
| `username` | 의 사용자 이름 [!DNL Snowflake] 계정입니다. |
| `password` | 에 대한 암호 [!DNL Snowflake] 사용자 계정입니다. |
| `role` | (선택 사항) 지정된 연결에 대해 사용자에게 제공할 수 있는 사용자 정의 역할입니다. 제공되지 않은 경우 이 값의 기본값은 입니다. `public`. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 에 대한 연결 사양 ID [!DNL Snowflake] 은(는) `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

인증에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL Snowflake] 문서](<https://docs.snowflake.com/en/user-guide/key-pair-auth.html>).

### 역할 설정 구성 {#configure-role-settings}

기본 공용 역할이 지정된 경우에도 소스 연결이 관련 역할에 액세스할 수 있도록 하려면 역할에 대한 권한을 구성해야 합니다 [!DNL Snowflake] 데이터베이스, 스키마 및 테이블입니다. 다양한 권한을 사용할 수 있습니다 [!DNL Snowflake] 엔티티는 다음과 같습니다.

| [!DNL Snowflake] 엔티티 | 역할 권한 필요 |
| --- | --- |
| 웨어하우스 | 운영, 사용 |
| 데이터베이스 | 사용 |
| 스키마 | 사용 |
| 표 | 선택 |

>[!NOTE]
>
>창고의 고급 설정 구성에서 자동 재개 및 자동 일시 중지를 활성화해야 합니다.

롤 및 권한 관리에 대한 자세한 내용은 [[!DNL Snowflake] API 참조](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## 제한 사항 및 FAQ {#limitations-and-frequently-asked-questions}

* 다음에 대한 데이터 처리량 [!DNL Snowflake] 소스는 초당 2000개의 레코드입니다.
* 창고가 활성화된 시간과 창고 크기에 따라 가격 책정이 달라질 수 있다. 의 경우 [!DNL Snowflake] 소스 통합, 가장 작은 크기, x-small warehouse로 충분합니다. 자동 중지를 가능하게 하여 창고가 미사용 시 자체적으로 중지를 할 수 있도록 할 것을 제안한다.
* 다음 [!DNL Snowflake] 소스는 10초마다 새 데이터에 대해 데이터베이스를 폴링합니다.
* 구성 옵션:
   * 다음을 활성화할 수 있습니다. `backfill` 에 대한 부울 플래그 [!DNL Snowflake] 소스 연결을 만들 때 소스.
      * backfill 이 true 로 설정되면 timestamp.initial 의 값이 0으로 설정됩니다. 즉, 타임스탬프 열이 0 epoch 시간보다 큰 데이터를 가져옵니다.
      * backfill 이 false 로 설정되어 있으면 timestamp.initial 의 값이 -1 로 설정됩니다. 즉, 타임스탬프 열이 현재 시간(소스가 수집을 시작하는 시간)보다 큰 데이터를 가져옵니다.
   * 타임스탬프 열의 형식은 다음과 같아야 합니다. `TIMESTAMP_LTZ` 또는 `TIMESTAMP_NTZ`. 타임스탬프 열이 로 설정된 경우 `TIMESTAMP_NTZ`를 설치한 다음 값이 저장된 해당 시간대를 `timezoneValue` 매개 변수. 제공되지 않는 경우 값은 기본적으로 UTC로 설정됩니다.
      * `TIMESTAMP_TZ` 타임스탬프 열 또는 매핑에서 사용할 수 없습니다.

## 다음 단계

다음 튜토리얼에서는 를 연결하는 방법에 대한 단계를 제공합니다. [!DNL Snowflake] API를 사용하여 스트리밍 소스에서 Experience Platform:

* [에서 데이터 스트리밍 [!DNL Snowflake] 흐름 서비스 API를 사용하여 Experience Platform 할 데이터베이스](../../tutorials/api/create/databases/snowflake-streaming.md)

