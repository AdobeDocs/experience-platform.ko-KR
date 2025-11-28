---
title: Snowflake Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Snowflake을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 1%

---

# [!DNL Snowflake] 원본

>[!IMPORTANT]
>
>* [!DNL Snowflake] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.
>* 기본적으로 [!DNL Snowflake] 원본은 `null`을(를) 빈 문자열로 해석합니다. Adobe 담당자에게 문의하여 `null` 값이 Adobe Experience Platform에서 `null`(으)로 올바르게 기록되었는지 확인하십시오.
>* Experience Platform이 데이터를 수집하려면 모든 테이블 기반 배치 소스의 시간대를 UTC로 구성해야 합니다. [!DNL Snowflake] 소스에 대해 지원되는 타임스탬프는 UTC 시간이 있는 TIMESTAMP_NTZ뿐입니다.

[!DNL Snowflake]은(는) 조직에서 대량의 데이터를 효율적으로 저장, 처리 및 분석할 수 있도록 설계된 클라우드 기반의 데이터 웨어하우스 플랫폼입니다. 클라우드의 확장성과 유연성을 활용하도록 빌드된 [!DNL Snowflake]은(는) 데이터 통합, 고급 분석 및 팀 간의 원활한 공유를 지원합니다. [!DNL Snowflake]은(는) 완전 관리 서비스로서 기존 데이터베이스에 공통되는 유지 관리의 복잡성을 제거하여 데이터에서 통찰력과 가치를 도출하는 데 집중할 수 있도록 합니다.

[!DNL Snowflake] 원본을 사용하여 [!DNL Snowflake]에서 Adobe Experience Platform으로 데이터를 연결하고 가져올 수 있습니다. [!DNL Snowflake] 소스를 설정하고 Experience Platform에 연결하는 방법에 대해 알아보려면 아래 설명서를 읽어 보십시오.

## 전제 조건 {#prerequisites}

이 섹션에서는 [!DNL Snowflake] 소스를 Experience Platform에 연결하기 전에 완료해야 하는 설정 작업에 대해 설명합니다.

### 허용 목록에 추가하다 IP 주소

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

### 필요한 자격 증명 수집

[!DNL Snowflake] 원본을 인증하려면 다음 자격 증명 속성에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증(Azure)]

계정 키 인증을 사용하여 Azure의 Experience Platform에 [!DNL Snowflake]을(를) 연결하려면 다음 자격 증명의 값을 제공하세요.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `account` | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 [!DNL Snowflake] 조직에서 계정을 고유하게 식별해야 합니다. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `myorg-myaccount.snowflakecomputing.com`. 추가 지침을 보려면 [계정 식별자 검색 [!DNL Snowflake] 의 섹션을 참조하십시오](#retrieve-your-account-identifier). 자세한 내용은 [[!DNL Snowflake] 설명서](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)를 참조하세요. |
| `warehouse` | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이므로 Experience Platform으로 데이터를 가져올 때 개별적으로 액세스해야 합니다. |
| `database` | [!DNL Snowflake] 데이터베이스에 Experience Platform으로 가져올 데이터가 있습니다. |
| `username` | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| `password` | [!DNL Snowflake] 사용자 계정의 암호입니다. |
| `role` | [!DNL Snowflake] 세션에서 사용할 기본 액세스 제어 역할입니다. 역할은 지정된 사용자에게 이미 할당된 기존 역할이어야 합니다. 기본 역할은 `PUBLIC`입니다. |
| `connectionString` | [!DNL Snowflake] 인스턴스에 연결하는 데 사용되는 연결 문자열입니다. [!DNL Snowflake]에 대한 연결 문자열 패턴은 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`입니다. |

>[!TAB 키 쌍 인증(Azure)]

키 쌍 인증을 사용하려면 먼저 2048비트 RSA 키 쌍을 생성합니다. 그런 다음 키 쌍 인증을 사용하여 Azure의 Experience Platform에 연결하기 위해 다음 자격 증명에 대한 값을 제공합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `account` | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 [!DNL Snowflake] 조직에서 계정을 고유하게 식별해야 합니다. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `myorg-myaccount.snowflakecomputing.com`. 추가 지침을 보려면 [계정 식별자 검색 [!DNL Snowflake] 의 섹션을 참조하십시오](#retrieve-your-account-identifier). 자세한 내용은 [[!DNL Snowflake] 설명서](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)를 참조하세요. |
| `username` | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| `privateKey` | [!DNL Base64-] 계정의 [!DNL Snowflake]인코딩된 개인 키입니다. 암호화되거나 암호화되지 않은 개인 키를 생성할 수 있습니다. 암호화된 개인 키를 사용하는 경우 Experience Platform에 대해 인증할 때 개인 키 암호도 제공해야 합니다. 자세한 내용은 [개인 키 검색](#retrieve-your-private-key)의 섹션을 참조하십시오. |
| `privateKeyPassphrase` | 개인 키 암호는 암호화된 개인 키로 인증할 때 사용해야 하는 추가 보안 계층입니다. 암호화되지 않은 개인 키를 사용하는 경우에는 암호를 제공할 필요가 없습니다. |
| `port` | [!DNL Snowflake]이(가) 인터넷을 통해 서버에 연결할 때 사용하는 포트 번호입니다. |
| `database` | Experience Platform으로 수집할 데이터가 포함된 [!DNL Snowflake] 데이터베이스입니다. |
| `warehouse` | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이므로 Experience Platform으로 데이터를 가져올 때 개별적으로 액세스해야 합니다. |

이러한 값에 대한 자세한 내용은 [[!DNL Snowflake] 키 쌍 인증 가이드](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)를 참조하십시오.

>[!TAB 기본 인증(AWS)]

기본 인증을 사용하여 AWS의 Experience Platform에 [!DNL Snowflake]을(를) 연결하려면 다음 자격 증명의 값을 제공하십시오.

>[!WARNING]
>
>[!DNL Snowflake] 원본에 대한 기본 인증(또는 계정 키 인증)은 2025년 11월에 더 이상 사용되지 않습니다. 소스를 계속 사용하고 데이터베이스에서 Experience Platform으로 데이터를 수집하려면 키 쌍 기반 인증으로 이동해야 합니다. 사용 중단에 대한 자세한 내용은 [[!DNL Snowflake] 자격 증명 손상 위험 완화에 대한 모범 사례 가이드](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/)를 참조하세요.

| 자격 증명 | 설명 |
| --- | --- |
| `host` | [!DNL Snowflake] 계정이 연결되는 호스트 URL입니다. |
| `port` | [!DNL Snowflake]이(가) 인터넷을 통해 서버에 연결할 때 사용하는 포트 번호입니다. |
| `username` | [!DNL Snowflake] 계정과 연결된 사용자 이름. |
| `password` | [!DNL Snowflake] 계정과 연결된 암호입니다. |
| `database` | 데이터를 가져올 위치의 [!DNL Snowflake] 데이터베이스입니다. |
| `schema` | [!DNL Snowflake] 데이터베이스와 연결된 스키마의 이름입니다. 데이터베이스 액세스 권한을 부여할 사용자도 이 스키마에 액세스할 수 있는지 확인해야 합니다. |
| `warehouse` | 사용 중인 [!DNL Snowflake] 웨어하우스입니다. |

>[!TAB 키 쌍 인증(AWS)]

키 쌍 인증을 사용하려면 먼저 2048비트 RSA 키 쌍을 생성합니다. 다음으로, 키 쌍 인증을 사용하여 AWS의 Experience Platform에 연결하기 위해 다음 자격 증명에 대한 값을 제공합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `account` | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 [!DNL Snowflake] 조직에서 계정을 고유하게 식별해야 합니다. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `http://myorg-myaccount.snowflakecomputing.com/`. 추가 지침은 [계정 식별자 검색 [!DNL Snowflake] 에 대한 안내서를 참조하십시오](#etrieve-your-account-identifier). 자세한 내용은 [[!DNL Snowflake] 설명서](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)를 참조하세요. |
| `username` | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| `privateKey` | 머리글이나 줄 바꿈이 없는 한 줄로 base64가 인코딩된 [!DNL Snowflake] 사용자의 개인 키입니다. 준비하려면 PEM 파일의 내용을 복사하고 `BEGIN`/`END` 줄과 모든 줄 바꿈을 제거한 다음 base64 인코딩하여 결과를 만듭니다. 자세한 내용은 [개인 키 검색](#retrieve-your-private-key)의 섹션을 참조하십시오. **참고:** 암호화된 개인 키는 현재 AWS 연결에 대해 지원되지 않습니다. |
| `port` | [!DNL Snowflake]이(가) 인터넷을 통해 서버에 연결할 때 사용하는 포트 번호입니다. |
| `database` | Experience Platform으로 수집할 데이터가 포함된 [!DNL Snowflake] 데이터베이스입니다. |
| `warehouse` | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이므로 Experience Platform으로 데이터를 가져올 때 개별적으로 액세스해야 합니다. |

이러한 값에 대한 자세한 내용은 [[!DNL Snowflake] 키 쌍 인증 가이드](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)를 참조하십시오.

>[!ENDTABS]

### 계정 식별자 검색 {#retrieve-your-account-identifier}

Experience Platform에서 [!DNL Snowflake] 인스턴스를 인증하기 위해 [!DNL Snowflake] UI 대시보드에서 계정 식별자를 검색해야 합니다.

계정 식별자를 검색하려면:

* [[!DNL Snowflake] 응용 프로그램 UI 대시보드](https://app.snowflake.com/)를 사용하여 계정에 액세스하세요.
* 왼쪽 탐색에서 **[!DNL Accounts]**&#x200B;을(를) 선택한 다음 헤더에서 **[!DNL Active Accounts]**&#x200B;을(를) 선택합니다.
* 그런 다음 정보 아이콘을 선택하고 을(를) 선택한 다음 현재 URL의 도메인 이름을 복사합니다.

![도메인 이름이 선택된 Snowflake UI 대시보드입니다.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### RSA 키 쌍 생성

명령줄 인터페이스에서 OpenSSL을 사용하여 PKCS#8 형식의 2048비트 RSA 키 쌍을 생성합니다. 보안을 위해 암호 암호가 필요한 암호화된 개인 키를 만드는 것이 좋습니다.

>[!BEGINTABS]

>[!TAB 암호화된 개인 키 생성]

암호화된 [!DNL Snowflake] 개인 키를 생성하려면 터미널에서 다음 명령을 실행하십시오.

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB 암호화되지 않은 개인 키 생성]

암호화되지 않은 [!DNL Snowflake] 개인 키를 생성하려면 터미널에서 다음 명령을 실행하십시오.

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### 개인 키에서 공개 키 생성

그런 다음 명령줄 인터페이스에서 다음 명령을 실행하여 개인 키를 기반으로 공개 키를 만듭니다.

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### [!DNL Snowflake] 사용자에게 공개 키 할당

생성된 공개 키를 Experience Platform에서 사용할 [!DNL Snowflake] 서비스 사용자와 연결하려면 **관리자 역할(예:** SECURITYADMIN[!DNL Snowflake])을 사용해야 합니다. 공개 키 콘텐츠를 검색하려면 `rsa_key.pub` 파일을 열고 `-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----` 줄을 제외한 전체 콘텐츠를 복사하십시오. 그런 다음 [!DNL Snowflake]에서 다음 SQL을 실행하십시오.

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### [!DNL Base64]의 개인 키 인코딩

Experience Platform에서는 연결을 설정하는 동안 개인 키를 [!DNL Base64] 인코딩하고 문자열로 제공해야 합니다. 적절한 도구 또는 스크립트를 사용하여 `rsa_key.p8` 파일의 내용을 단일 [!DNL Base64] 문자열로 인코딩하십시오.

>[!TIP]
>
>인코딩 프로세스 전이나 후에 인증 오류가 발생할 수 있으므로 머리글/바닥글 줄 `(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)`을(를) 포함하여 추가 공백이나 줄 바꿈이 없는지 확인하십시오.

### 구성 확인

Experience Platform에서 [!DNL Snowflake] 소스 연결을 만들기 전에 사용자의 **[!DNL Default Role]** 및 **[!DNL Default Warehouse]**&#x200B;이(가) Experience Platform에서 제공하는 값과 일치하는지 확인해야 합니다. [!DNL Snowflake] SQL 명령을 사용하여 `DESCRIBE USER {USERNAME}` UI에서 이러한 설정을 확인할 수 있습니다.

또는 아래 단계에 따라 설정을 확인할 수 있습니다.

* 왼쪽 탐색에서 **[!DNL Admin]**&#x200B;을(를) 선택한 다음 **[!DNL Users & Roles]**&#x200B;을(를) 선택합니다.
* 적절한 사용자를 선택한 다음 오른쪽 상단 모서리에서 줄임표(`...`)를 선택합니다.
* 표시되는 [!DNL Edit user] 창에서 [!DNL Default Role]&#x200B;(으)로 이동하여 지정된 사용자와 연결된 역할을 봅니다.
* 같은 창에서 [!DNL Default Warehouse]&#x200B;(으)로 이동하여 지정된 사용자와 연결된 웨어하우스를 봅니다.

![역할과 웨어하우스를 확인할 수 있는 Snowflake UI입니다.](../../images/tutorials/create/snowflake/snowflake-configs.png)

## 다음 단계

설정이 완료되면 이제 [!DNL Snowflake] 계정을 Experience Platform에 연결할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.

### API를 사용하여 [!DNL Snowflake]을(를) Experience Platform에 연결

* [API를 사용하여  [!DNL Snowflake] 을(를) Experience Platform에 연결](../../tutorials/api/create/databases/snowflake.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

### UI를 사용하여 [!DNL Snowflake]을(를) Experience Platform에 연결

* [UI를 사용하여  [!DNL Snowflake] 을(를) Experience Platform에 연결](../../tutorials/ui/create/databases/snowflake.md)
* [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
