---
title: Snowflake Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Snowflake을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 573691db9f71fcbe8b5edd4ea647d718ab3784e4
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# [!DNL Snowflake] 원본

>[!IMPORTANT]
>
>* [!DNL Snowflake] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.
>* 기본적으로 [!DNL Snowflake] 원본은 `null`을(를) 빈 문자열로 해석합니다. Adobe 담당자에게 문의하여 `null` 값이 Adobe Experience Platform에서 `null`(으)로 올바르게 기록되었는지 확인하십시오.
>* Experience Platform이 데이터를 수집하려면 모든 테이블 기반 배치 소스의 시간대를 UTC로 구성해야 합니다. [!DNL Snowflake] 소스에 대해 지원되는 타임스탬프는 UTC 시간이 있는 TIMESTAMP_NTZ뿐입니다.

>[!WARNING]
>
>[!DNL Snowflake] 원본에 대한 기본 인증(또는 계정 키 인증)은 2025년 11월에 더 이상 사용되지 않습니다. 소스를 계속 사용하고 데이터베이스에서 Experience Platform으로 데이터를 수집하려면 키 쌍 기반 인증으로 이동해야 합니다. 사용 중단에 대한 자세한 내용은 [[!DNL Snowflake] 자격 증명 손상 위험 완화에 대한 모범 사례 가이드](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/)를 참조하세요.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 데이터베이스에서 데이터를 수집하는 기능을 지원합니다. Experience Platform은 관계형, NoSQL 또는 데이터 웨어하우스와 같은 다양한 유형의 데이터베이스에 연결할 수 있습니다. 데이터베이스 공급자에 대한 지원에는 [!DNL Snowflake]이(가) 포함됩니다.

## 전제 조건 {#prerequisites}

이 섹션에서는 [!DNL Snowflake] 소스를 Experience Platform에 연결하기 전에 완료해야 하는 설정 작업에 대해 설명합니다.

### 계정 식별자 검색 {#retrieve-your-account-identifier}

Experience Platform에서 계정 식별자를 사용하여 [!DNL Snowflake] 인스턴스를 인증하게 되므로 [!DNL Snowflake] UI 대시보드에서 계정 식별자를 검색해야 합니다.

계정 식별자를 검색하려면:

* [[!DNL Snowflake] 응용 프로그램 UI 대시보드](https://app.snowflake.com/)에서 내 계정으로 이동합니다.
* 왼쪽 탐색에서 **[!DNL Accounts]**&#x200B;을(를) 선택한 후 헤더에서 **[!DNL Active Accounts]**&#x200B;을(를) 선택합니다.
* 그런 다음 정보 아이콘을 선택하고 을(를) 선택한 다음 현재 URL의 도메인 이름을 복사합니다.

![도메인 이름이 선택된 Snowflake UI 대시보드입니다.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### 개인 키 검색 {#retrieve-your-private-key}

[!DNL Snowflake] 연결에 키 쌍 인증을 사용하는 경우 Experience Platform에 연결하기 전에 개인 키도 생성해야 합니다.

>[!BEGINTABS]

>[!TAB 암호화된 개인 키를 만듭니다]

암호화된 [!DNL Snowflake] 개인 키를 생성하려면 터미널에서 다음 명령을 실행하십시오.

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

성공하면 개인 키를 PEM 형식으로 받아야 합니다.

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB 암호화되지 않은 개인 키를 만듭니다]

암호화되지 않은 [!DNL Snowflake] 개인 키를 생성하려면 터미널에서 다음 명령을 실행하십시오.

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

성공하면 개인 키를 PEM 형식으로 받아야 합니다.

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

그런 다음 개인 키를 가져와서 [!DNL Base64]에서 인코딩하십시오. [!DNL Snowflake] 개인 키에 대해 변환이나 형식 변환을 수행하지 않도록 하십시오. 또한 [!DNL Base64]에서 인코딩하기 전에 개인 키 끝에 후행 줄바꿈 문자가 없는지 확인해야 합니다.

### 구성 확인

[!DNL Snowflake] 데이터에 대한 원본 연결을 만들려면 먼저 다음 구성도 충족하는지 확인해야 합니다.

* 주어진 사용자에게 할당된 기본 웨어하우스는 Experience Platform에 인증할 때 입력하는 웨어하우스와 동일해야 합니다.
* 지정된 사용자에게 할당된 기본 역할은 Experience Platform 인증 시 입력한 것과 동일한 데이터베이스에 대한 액세스 권한이 있어야 합니다.

역할 및 웨어하우스를 확인하려면:

* 왼쪽 탐색에서 **[!DNL Admin]**&#x200B;을(를) 선택한 다음 **[!DNL Users & Roles]**&#x200B;을(를) 선택합니다.
* 적절한 사용자를 선택한 다음 오른쪽 상단 모서리에서 줄임표(`...`)를 선택합니다.
* 표시되는 [!DNL Edit user] 창에서 [!DNL Default Role]&#x200B;(으)로 이동하여 지정된 사용자와 연결된 역할을 봅니다.
* 같은 창에서 [!DNL Default Warehouse]&#x200B;(으)로 이동하여 지정된 사용자와 연결된 웨어하우스를 봅니다.

![역할과 웨어하우스를 확인할 수 있는 Snowflake UI입니다.](../../images/tutorials/create/snowflake/snowflake-configs.png)

인코딩이 완료되면 Experience Platform에서 [!DNL Base64] 인코딩된 개인 키를 사용하여 [!DNL Snowflake] 계정을 인증할 수 있습니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Snowflake]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

## API를 사용하여 [!DNL Snowflake]을(를) Experience Platform에 연결

* [흐름 서비스 API를 사용하여 Snowflake 기본 연결 만들기](../../tutorials/api/create/databases/snowflake.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 [!DNL Snowflake]을(를) Experience Platform에 연결

* [UI에서 Snowflake 소스 연결 만들기](../../tutorials/ui/create/databases/snowflake.md)
* [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
