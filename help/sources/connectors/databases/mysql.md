---
title: MySQL Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 MySQL을 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다.
last-substantial-update: 2025-05-17T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: f758479c37b72752bbb8a371de88bf653b2e6030
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# [!DNL MySQL]

[!DNL MySQL]은(는) 구조화된 데이터를 저장하고 관리하는 데 사용되는 오픈 소스 관계형 데이터베이스 관리 시스템입니다. 데이터를 표로 구성하고 SQL(Structured Query Language)을 사용하여 정보를 쿼리하고 업데이트합니다. [!DNL MySQL]은(는) 웹 응용 프로그램에서 널리 사용되며 여러 플랫폼을 지원하며 속도, 안정성 및 사용 편의성으로 알려져 있습니다.

[!DNL MySQL] 원본을 사용하여 계정을 연결하고 [!DNL MySQL] 데이터베이스에서 Adobe Experience Platform으로 데이터를 수집할 수 있습니다.

## 전제 조건 {#prerequisites}

[!DNL MySQl] 계정을 Experience Platform에 연결하기 전에 필수 구성 요소 설정을 완료하려면 다음 섹션을 참조하십시오.

### 허용 목록에 추가하다 IP 주소

Azure 또는 Amazon Web Services(AWS)에서 Experience Platform에 소스를 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Azure 및 AWS의 Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

### Azure에서 Experience Platform 인증 {#azure}

계정 키 인증 또는 기본 인증을 사용하여 [!DNL MySQL] 데이터베이스를 Azure의 Experience Platform에 연결할 수 있습니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하여 [!DNL MySQL] 데이터베이스를 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `connectionString` | 계정과 연결된 [!DNL MySQL] 연결 문자열입니다. [!DNL MySQL] 연결 문자열 패턴은 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL MySQL]의 연결 사양 ID는 `26d738e0-8963-47ea-aadf-c60de735468a`입니다. |

자세한 내용은 연결 문자열에 대한 [[!DNL MySQL] 설명서를 읽어보세요](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

>[!TAB 기본 인증]

기본 인증을 사용하여 [!DNL MySQL] 데이터베이스를 Experience Platform에 연결하려면 다음 자격 증명의 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `server` | [!DNL MySQL] 데이터베이스의 이름 또는 IP 주소입니다. |
| `username` | [!DNL MySQL] 데이터베이스 인증과 연결된 사용자 이름입니다. |
| `password` | [!DNL MySQL] 데이터베이스 인증과 연결된 암호입니다. |
| `database` | 연결할 [!DNL MySQL] 데이터베이스의 이름입니다. |
| `sslMode` | 연결에 적용할 [!DNL Secure Sockets Layer]&#x200B;(SSL) 방법입니다. 사용 가능한 값은 다음과 같습니다. <ul><li>`DISABLED`: SSL을 비활성화하려면 이 옵션을 사용합니다. 서버에 SSL 구성이 필요한 경우 연결이 실패합니다</li><li>`PREFERRED`: 서버에서 지원하는 SSL 연결을 선호하려면 이 옵션을 사용합니다. 이 옵션을 사용하면 SSL이 아닌 연결도 허용됩니다.</li><li>`REQUIRED`: SSL 연결을 필수로 설정하려면 이 옵션을 사용합니다. 서버가 SSL을 지원하지 않으면 연결이 실패합니다.</li><li>`Verify-Ca`: 서버에서 SSL을 지원하지 않는 경우 연결 실패 시 서버 인증서를 확인하려면 이 옵션을 사용합니다.</li><li>`Verify Identity`: 서버에서 SSL을 지원하지 않는 경우 연결 실패 시 이 옵션을 사용하여 호스트 이름이 있는 서버 인증서를 확인합니다.</li></ul> |

>[!ENDTABS]

### Amazon Web Services(AWS)에서 Experience Platform 인증 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../landing/multi-cloud.md)를 참조하세요.

AWS에서 Experience Platform에 [!DNL MySQL]을(를) 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `server` | [!DNL MySQL] 데이터베이스의 이름 또는 IP. |
| `username` | 데이터베이스의 이름입니다. |
| `password` | 데이터베이스에 해당하는 사용자 이름입니다. |
| `database` | 데이터베이스에 해당하는 암호입니다. |
| `sslMode` | 연결에 적용할 [!DNL Secure Sockets Layer]&#x200B;(SSL) 방법입니다. 사용 가능한 값은 다음과 같습니다. <ul><li>`DISABLED`: SSL을 비활성화하려면 이 옵션을 사용합니다. 서버에 SSL 구성이 필요한 경우 연결이 실패합니다</li><li>`PREFERRED`: 서버에서 지원하는 SSL 연결을 선호하려면 이 옵션을 사용합니다. 이 옵션을 사용하면 SSL이 아닌 연결도 허용됩니다.</li><li>`REQUIRED`: SSL 연결을 필수로 설정하려면 이 옵션을 사용합니다. 서버가 SSL을 지원하지 않으면 연결이 실패합니다.</li><li>`Verify-Ca`: 서버에서 SSL을 지원하지 않는 경우 연결 실패 시 서버 인증서를 확인하려면 이 옵션을 사용합니다.</li><li>`Verify Identity`: 서버에서 SSL을 지원하지 않는 경우 연결 실패 시 이 옵션을 사용하여 호스트 이름이 있는 서버 인증서를 확인합니다.</li></ul> |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL MySQL]의 연결 사양 ID는 `26d738e0-8963-47ea-aadf-c60de735468a`입니다. **참고**: 이 자격 증명은 [!DNL Flow Service] API를 통해 연결할 때만 필요합니다. |

## API를 사용하여 [!DNL MySQL]을(를) Experience Platform에 연결

- [흐름 서비스 API를 사용하여  [!DNL MySQL] 데이터베이스 연결](../../tutorials/api/create/databases/mysql.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 MySQL을 Experience Platform에 연결

- [UI를 사용하여  [!DNL MySQL] 데이터베이스를 Experience Platform에 연결](../../tutorials/ui/create/databases/mysql.md)
- [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
