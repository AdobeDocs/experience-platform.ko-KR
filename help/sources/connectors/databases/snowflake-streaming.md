---
title: Snowflake 스트리밍 Source 커넥터 개요
description: 소스 연결 및 데이터 흐름을 만들어 Snowflake 인스턴스에서 Adobe Experience Platform으로 스트리밍 데이터를 수집하는 방법을 알아봅니다
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 3%

---

# [!DNL Snowflake] 스트리밍 원본

>[!IMPORTANT]
>
>* [!DNL Snowflake] 스트리밍 소스는 Real-Time CDP Ultimate을 구매한 사용자에게 API에서 사용할 수 있습니다.
>
>* 이제 Amazon Web Services(AWS)에서 Adobe Experience Platform을 실행할 때 [!DNL Snowflake] 스트리밍 소스를 사용할 수 있습니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../landing/multi-cloud.md)를 참조하세요.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집하는 동시에 Experience Platform 서비스를 사용하여 수신 데이터를 구조화하고 레이블을 지정하며 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform에서는 [!DNL Snowflake] 데이터베이스에서 데이터를 스트리밍할 수 있습니다.

## [!DNL Snowflake] 스트리밍 원본 이해

[!DNL Snowflake] 스트리밍 원본은 SQL 쿼리를 주기적으로 실행하고 결과 집합에서 각 행에 대한 출력 레코드를 만들어 데이터를 로드하여 작동합니다.

[!DNL Kafka Connect]을(를) 사용하여 [!DNL Snowflake] 스트리밍 소스는 다음 반복에 대한 올바른 위치에서 시작할 수 있도록 각 테이블에서 받은 최신 레코드를 추적합니다. 소스는 이 기능을 사용하여 데이터를 필터링하고 각 반복의 테이블에서 업데이트된 행만 가져옵니다.

## 전제 조건

다음 섹션에서는 [!DNL Snowflake] 데이터베이스에서 Experience Platform으로 데이터를 스트리밍하기 전에 완료해야 하는 필수 조건 단계에 대해 설명합니다.

### 허용 목록에 추가하다 IP 주소

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Amazon Redshift]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Snowflake]과(와) 연결하려면 다음 연결 속성을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `account` | [!DNL Snowflake] 접미사가 추가된 `snowflakecomputing.com` 계정의 전체 계정 식별자(계정 이름 또는 계정 로케이터)입니다. 계정 식별자는 다양한 형식일 수 있습니다. <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com(예: `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (예: `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (예: `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> 자세한 내용은 [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>)을(를) 참조하십시오. |
| `warehouse` | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이므로 Experience Platform으로 데이터를 가져올 때 개별적으로 액세스해야 합니다. |
| `database` | [!DNL Snowflake] 데이터베이스에 Experience Platform으로 가져올 데이터가 있습니다. |
| `username` | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| `password` | [!DNL Snowflake] 사용자 계정의 암호입니다. |
| `role` | (선택 사항) 지정된 연결에 대해 사용자에게 제공할 수 있는 사용자 정의 역할입니다. 지정하지 않으면 이 값은 기본적으로 `public`(으)로 설정됩니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Snowflake]의 연결 사양 ID는 `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`입니다. |

>[!TAB 키 쌍 인증]

키 쌍 인증을 사용하려면 2048비트 RSA 키 쌍을 생성한 다음 [!DNL Snowflake] 소스에 대한 계정을 만들 때 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `account` | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 [!DNL Snowflake] 조직에서 계정을 고유하게 식별해야 합니다. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `orgname-account_name`. 추가 지침은 [계정 식별자 검색 [!DNL Snowflake] 에 대한 안내서를 참조하십시오](./snowflake.md#retrieve-your-account-identifier). 자세한 내용은 [[!DNL Snowflake] 설명서](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)를 참조하세요. |
| `username` | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| `privateKey` | [!DNL Base64-] 계정의 [!DNL Snowflake]인코딩된 개인 키입니다. 암호화되거나 암호화되지 않은 개인 키를 생성할 수 있습니다. 암호화된 개인 키를 사용하는 경우 Experience Platform에 대해 인증할 때 개인 키 암호도 제공해야 합니다. 자세한 내용은 [개인 키 검색 [!DNL Snowflake] 2&rbrace;에 대한 안내서를 참조하십시오.](./snowflake.md) |
| `passphrase` | 암호는 암호화된 개인 키로 인증할 때 사용해야 하는 추가 보안 계층입니다. 암호화되지 않은 개인 키를 사용하는 경우에는 암호를 제공할 필요가 없습니다. |
| `database` | Experience Platform으로 수집할 데이터가 포함된 [!DNL Snowflake] 데이터베이스입니다. |
| `warehouse` | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이므로 Experience Platform으로 데이터를 가져올 때 개별적으로 액세스해야 합니다. |

이러한 값에 대한 자세한 내용은 [[!DNL Snowflake] 키 쌍 인증 가이드](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)를 참조하십시오.

>[!ENDTABS]

### 계정 식별자 검색 {#retrieve-your-account-identifier}

Experience Platform을 사용하여 [!DNL Snowflake] 인스턴스를 인증하려면 [!DNL Snowflake] UI 대시보드에서 계정 식별자를 가져와야 합니다.

계정 식별자를 찾으려면 다음 단계를 따르십시오.

* [[!DNL Snowflake] 응용 프로그램 UI 대시보드](https://app.snowflake.com/)에서 내 계정으로 이동합니다.
* 왼쪽 탐색에서 **[!DNL Accounts]**&#x200B;을(를) 선택한 후 헤더에서 **[!DNL Active Accounts]**&#x200B;을(를) 선택합니다.
* 그런 다음 정보 아이콘을 선택하고 을(를) 선택한 다음 현재 URL의 도메인 이름을 복사합니다.

### 개인 키 검색 {#retrieve-your-private-key}

[!DNL Snowflake] 연결에 키 쌍 인증을 사용할 계획이라면 Experience Platform에 연결하기 전에 개인 키를 생성해야 합니다.

>[!BEGINTABS]

>[!TAB 암호화된 개인 키를 만듭니다]

암호화된 [!DNL Snowflake] 개인 키를 생성하려면 터미널에서 다음 명령을 실행하십시오.

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

성공하면 개인 키를 PEM 형식으로 받아야 합니다.

```shell
|-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
|-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB 암호화되지 않은 개인 키를 만듭니다]

암호화되지 않은 [!DNL Snowflake] 개인 키를 생성하려면 터미널에서 다음 명령을 실행하십시오.

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

성공하면 개인 키를 PEM 형식으로 받아야 합니다.

```shell
|-----BEGIN PRIVATE KEY-----
MIIE6T...
|-----END PRIVATE KEY-----
```

>[!ENDTABS]

개인 키를 생성한 후 형식 또는 콘텐츠를 변경하지 않고 [!DNL Base64]에서 직접 인코딩하십시오. 인코딩을 수행하기 전에 개인 키 끝에 공백이나 빈 줄(후행 줄바꿈 포함)이 없는지 확인합니다.

### 구성 확인

[!DNL Snowflake] 데이터에 대한 원본 연결을 만들려면 먼저 다음 구성도 충족하는지 확인해야 합니다.

* 주어진 사용자에게 할당된 기본 웨어하우스는 Experience Platform에 인증할 때 입력하는 웨어하우스와 동일해야 합니다.
* 지정된 사용자에게 할당된 기본 역할은 Experience Platform 인증 시 입력한 것과 동일한 데이터베이스에 대한 액세스 권한이 있어야 합니다.

역할 및 웨어하우스를 확인하려면:

* 왼쪽 탐색에서 **[!DNL Admin]**&#x200B;을(를) 선택한 다음 **[!DNL Users & Roles]**&#x200B;을(를) 선택합니다.
* 적절한 사용자를 선택한 다음 오른쪽 상단 모서리에서 줄임표(`...`)를 선택합니다.
* 표시되는 [!DNL Edit user] 창에서 [!DNL Default Role]&#x200B;(으)로 이동하여 지정된 사용자와 연결된 역할을 봅니다.
* 같은 창에서 [!DNL Default Warehouse]&#x200B;(으)로 이동하여 지정된 사용자와 연결된 웨어하우스를 봅니다.

인코딩이 완료되면 Experience Platform에서 [!DNL Base64] 인코딩된 개인 키를 사용하여 [!DNL Snowflake] 계정을 인증할 수 있습니다.

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

## Unix 시간 필드를 날짜 필드로 변환

[!DNL Snowflake Streaming]은(는) Unix Epoch(1970-01-01) 이후의 일 수로 ` DATE` 필드를 구문 분석하고 기록합니다. 예를 들어, `DATE` 값이 0이면 1970년 1월 1일을 의미하며, 1이면 1970년 1월 2일을 의미합니다. 따라서 [!DNL Snowflake Streaming] 원본에서 매핑을 만들 파일을 준비할 때는 `DATE` 열이 정수로 표시되었는지 확인하십시오.

[데이터 준비 데이터 및 시간 함수](../../../data-prep/functions.md#date-and-time-functions)를 사용하여 Unix 시간을 Experience Platform에 수집할 수 있는 날짜 필드로 변환할 수 있습니다. 예:

```shell
dformat({DATE_COLUMN} * 86400000, "yyyy-MM-dd")
```

이 함수에서:

* `{DATE_COLUMN}`은(는) epoch 일 정수를 포함하는 날짜 열입니다.
* 에포크86400000 곱하면 에포크 일수가 밀리초로 변환됩니다.
* &#39;yyyy-MM-dd&#39;는 원하는 날짜 형식을 지정합니다.

이렇게 변환하면 날짜가 데이터 세트에 올바르게 표시됩니다.


## 제한 사항 및 FAQ {#limitations-and-frequently-asked-questions}

* [!DNL Snowflake] 원본의 데이터 처리량은 초당 레코드 2000개입니다.
* 창고가 활성화된 시간과 창고 크기에 따라 가격 책정이 달라질 수 있다. [!DNL Snowflake] 소스 통합의 경우 가장 작은 크기의 x-small 웨어하우스로 충분합니다. 자동 중지를 가능하게 하여 창고가 미사용 시 자체적으로 중지를 할 수 있도록 할 것을 제안한다.
* [!DNL Snowflake] 원본은 10초마다 새 데이터를 위해 데이터베이스를 폴링합니다.
* 구성 옵션:
   * 소스 연결을 만들 때 `backfill` 소스에 대해 [!DNL Snowflake] 부울 플래그를 사용하도록 설정할 수 있습니다.
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
