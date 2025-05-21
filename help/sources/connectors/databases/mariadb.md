---
title: MariaDB Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 MariaDB를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# [!DNL MariaDB]

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 데이터베이스에서 데이터를 수집하는 기능을 지원합니다. [!DNL Experience Platform]은(는) 관계형, NoSQL 또는 데이터 웨어하우스와 같은 다양한 유형의 데이터베이스에 연결할 수 있습니다. 데이터베이스 공급자에 대한 지원에는 [!DNL MariaDB]이(가) 포함됩니다.

## 전제 조건 {#prerequisites}

[!DNL MariaDB] 계정을 Experience Platform에 연결하기 전에 필수 구성 요소 설정을 완료하려면 다음 섹션을 참조하십시오.

### 허용 목록에 추가하다 IP 주소

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

### Experience Platform 인증

[!DNL MariaDB]을(를) Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하려면 다음 자격 증명에 적절한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `connectionString` | [!DNL MariaDB] 인증과 연결된 연결 문자열입니다. [!DNL MariaDB] 연결 문자열 패턴은 `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL MariaDB]의 연결 사양 ID는 `3000eb99-cd47-43f3-827c-43caf170f015`입니다. **참고**: 이 자격 증명은 [!DNL Flow Service] API를 통해 연결할 때만 필요합니다. |

연결 문자열을 가져오는 방법에 대한 자세한 내용은 이 [[!DNL MariaDB] 문서](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)를 참조하세요.

>[!TAB 기본 인증]

기본 인증을 사용하려면 다음 자격 증명에 적절한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `server` | [!DNL MariaDB] 데이터베이스의 이름 또는 IP. |
| `username` | 데이터베이스의 이름입니다. |
| `port` | 연결 중인 통신 끝점의 포트 번호입니다. |
| `password` | 데이터베이스에 해당하는 사용자 이름입니다. |
| `database` | 데이터베이스에 해당하는 암호입니다. |
| `sslMode` | 데이터를 전송하는 동안 데이터를 암호화하는 방법입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL MariaDB]의 연결 사양 ID는 `3000eb99-cd47-43f3-827c-43caf170f015`입니다. **참고**: 이 자격 증명은 [!DNL Flow Service] API를 통해 연결할 때만 필요합니다. |

연결 문자열을 가져오는 방법에 대한 자세한 내용은 이 [[!DNL MariaDB] 문서](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)를 참조하세요.

>[!ENDTABS]

## API를 사용하여 [!DNL MariaDB]을(를) Experience Platform에 연결

- [흐름 서비스 API를 사용하여 MariaDB 기본 연결 만들기](../../tutorials/api/create/databases/mariadb.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 [!DNL MariaDB]을(를) Experience Platform에 연결

- [UI에서 MariaDB 소스 연결 만들기](../../tutorials/ui/create/databases/mariadb.md)
- [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
