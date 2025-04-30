---
title: PostgreSQL Source 커넥터 개요
description: Adobe Experience Platform의 PostgreSQL 소스에 대해 알아봅니다.
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: 04634c6edc13d8b8da01a01077161866235c61b1
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL PostgreSQL]

[!DNL PostgreSQL] 데이터베이스를 Adobe Experience Platform에 연결하기 전에 완료해야 하는 필수 구성 요소 단계에 대해 알아보려면 이 문서를 참조하십시오.

## 전제 조건 {#prerequisites}

[!DNL PostgreSQL] 데이터베이스를 Experience Platform에 연결하기 전에 필수 구성 요소 설정을 완료하려면 다음 섹션을 참조하십시오.

### 허용 목록에 추가하다 IP 주소

Azure 또는 Amazon Web Services(AWS)에서 Experience Platform에 소스를 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Azure 및 AWS의 Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

### Azure에서 Experience Platform 인증 {#azure}

[!DNL PostgreSQL]을(를) Azure의 Experience Platform에 연결하려면 다음 인증 자격 증명에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하여 [!DNL PostgreSQL] 데이터베이스를 Azure의 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `connectionString` | [!DNL PostgreSQL] 계정과 연결된 연결 문자열입니다. [!DNL PostgreSQL] 연결 문자열 패턴은 `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL PostgreSQL]의 연결 사양 ID는 `74a1c565-4e59-48d7-9d67-7c03b8a13137`입니다. |

자세한 내용은 [[!DNL PostgreSQL] 설명서](https://www.postgresql.org/docs/current/)를 참조하세요.

>[!TAB 기본 인증]

기본 인증을 사용하여 [!DNL PostgreSQL] 데이터베이스를 Azure의 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `server` | [!DNL PostgreSQL] 데이터베이스의 이름 또는 IP 주소입니다. |
| `port` | [!DNL PostgreSQL] 서버의 TCP 포트입니다. |
| `username` | [!DNL PostgreSQL] 데이터베이스 인증과 연결된 사용자 이름입니다. |
| `password` | [!DNL PostgreSQL] 데이터베이스 인증과 연결된 암호입니다. |
| `database` | 연결할 [!DNL PostgreSQL] 데이터베이스의 이름입니다. |
| `sslMode` | 연결에 적용할 [!DNL Secure Sockets Layer]&#x200B;(SSL) 방법입니다. 사용 가능한 값은 다음과 같습니다. <ul><li>`Disable`: SSL을 비활성화하려면 이 옵션을 사용합니다. 서버에 SSL 구성이 필요한 경우 연결이 실패합니다.</li><li>`Allow`: SSL 연결을 허용하려면 이 옵션을 사용합니다. 서버가 비SSL 연결을 지원하는 경우에도 계속 사용할 수 있습니다.</li><li>`Prefer`: 서버에서 지원하는 SSL 연결을 선호하려면 이 옵션을 사용합니다. 이 옵션을 사용하면 SSL이 아닌 연결도 허용됩니다.</li><li>`Require`: SSL 연결을 필수로 설정하려면 이 옵션을 사용합니다. 서버가 SSL을 지원하지 않으면 연결이 실패합니다.</li><li>`Verify-Ca`: 서버에서 SSL을 지원하지 않는 경우 연결 실패 시 서버 인증서를 확인하려면 이 옵션을 사용합니다.</li><li>`Verify-Full`: 서버에서 SSL을 지원하지 않는 경우 연결 실패 시 이 옵션을 사용하여 호스트 이름이 있는 서버 인증서를 확인합니다.</li></ul> |

자세한 내용은 [[!DNL PostgreSQL] 설명서](https://www.postgresql.org/docs/current/)를 참조하세요.

>[!ENDTABS]

### Amazon Web Services(AWS)에서 Experience Platform 인증 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../landing/multi-cloud.md)를 참조하세요.

기본 인증을 사용하여 [!DNL PostgreSQL] 데이터베이스를 AWS의 Experience Platform에 연결하려면 다음 자격 증명의 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `server` | [!DNL PostgreSQL] 데이터베이스의 이름 또는 IP 주소입니다. |
| `port` | [!DNL PostgreSQL] 서버의 TCP 포트입니다. |
| `username` | [!DNL PostgreSQL] 데이터베이스 인증과 연결된 사용자 이름입니다. |
| `password` | [!DNL PostgreSQL] 데이터베이스 인증과 연결된 암호입니다. |
| `database` | 연결할 [!DNL PostgreSQL] 데이터베이스의 이름입니다. |
| `sslMode` | 연결에 적용할 [!DNL Secure Sockets Layer]&#x200B;(SSL) 방법입니다. 사용 가능한 값은 다음과 같습니다. <ul><li>`Disable`: SSL을 비활성화하려면 이 옵션을 사용합니다. 서버에 SSL 구성이 필요한 경우 연결이 실패합니다.</li><li>`Allow`: SSL 연결을 허용하려면 이 옵션을 사용합니다. 서버가 비SSL 연결을 지원하는 경우에도 계속 사용할 수 있습니다.</li><li>`Prefer`: 서버에서 지원하는 SSL 연결을 선호하려면 이 옵션을 사용합니다. 이 옵션을 사용하면 SSL이 아닌 연결도 허용됩니다.</li><li>`Require`: SSL 연결을 필수로 설정하려면 이 옵션을 사용합니다. 서버가 SSL을 지원하지 않으면 연결이 실패합니다.</li><li>`Verify-Ca`: 서버에서 SSL을 지원하지 않는 경우 연결 실패 시 서버 인증서를 확인하려면 이 옵션을 사용합니다.</li><li>`Verify-Full`: 서버에서 SSL을 지원하지 않는 경우 연결 실패 시 이 옵션을 사용하여 호스트 이름이 있는 서버 인증서를 확인합니다.</li></ul> |

자세한 내용은 [[!DNL PostgreSQL] 설명서](https://www.postgresql.org/docs/current/)를 참조하세요.

## API를 사용하여 [!DNL PostgreSQL]을(를) Experience Platform에 연결

* [흐름 서비스 API를 사용하여  [!DNL PostgreSQL] 기본 연결 만들기](../../tutorials/api/create/databases/postgres.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 [!DNL PostgreSQL]을(를) Experience Platform에 연결

* [UI에서  [!DNL PostgreSQL] 소스 연결 만들기](../../tutorials/ui/create/databases/postgres.md)
* [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
