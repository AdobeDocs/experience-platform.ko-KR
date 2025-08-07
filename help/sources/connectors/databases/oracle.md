---
title: Oracle DB Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Oracle을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# [!DNL Oracle DB]

[!DNL Oracle DB]은(는) [!DNL Oracle Corporation]에서 개발한 강력한 관계형 데이터베이스 관리 시스템입니다. [!DNL Oracle DB]을(를) 사용하여 대량의 구조화된 데이터를 효율적이고 안전하게 저장, 관리 및 검색할 수 있습니다.

Adobe Experience Platform 소스 카탈로그의 [!DNL Oracle DB] 소스를 사용하여 데이터베이스를 연결하고 데이터를 Experience Platform에 수집합니다.

## 전제 조건 {#prerequisites}

[!DNL Oracle DB] 계정을 Experience Platform에 연결하기 전에 필수 구성 요소 설정을 완료하려면 다음 섹션을 참조하십시오.

### 허용 목록에 추가하다 IP 주소

Azure 또는 Amazon Web Services(AWS)에서 Experience Platform에 소스를 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Azure 및 AWS의 Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

### Azure에서 Experience Platform 인증 {#azure}

[!DNL Oracle DB] 계정을 인증하고 Azure의 Experience Platform에 연결하기 위한 연결 문자열을 제공합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 연결 문자열 | 연결 문자열은 응용 프로그램에서 데이터베이스에 연결하는 데 사용하는 텍스트 문자열입니다. [!DNL Oracle DB] 연결 문자열 패턴은 `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`입니다. |
| 연결 사양 ID | 연결 사양 ID는 기본 및 소스 연결 생성과 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Oracle]의 연결 사양 ID는 `d6b52d86-f0f8-475f-89d4-ce54c8527328`입니다. **참고**: 이 자격 증명은 [!DNL Flow Service] API를 통해 연결할 때만 필요합니다. |

### Amazon Web Services에서 Experience Platform 인증 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../landing/multi-cloud.md)를 참조하세요.

[!DNL Oracle DB] 계정을 인증하고 AWS의 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| 서버 | [!DNL Oracle DB] 서버의 IP 주소 또는 호스트 이름입니다. |
| 포트 | 데이터베이스 서버의 포트 번호입니다. 기본 포트 번호는 `1521`입니다. |
| 사용자 이름 | 데이터베이스를 인증하고 액세스하는 데 사용되는 [!DNL Oracle DB] 사용자 계정입니다. |
| 암호 | 인증에 사용되는 사용자 이름과 연결된 비밀 키입니다. |
| 데이터베이스 | 연결할 특정 [!DNL Oracle] 데이터베이스 인스턴스입니다. |
| 스키마 | 테이블, 뷰 또는 프로시저와 같은 데이터베이스 개체에 대한 컨테이너입니다. |
| SSL 모드 | SSL 적용 여부를 제어하는 부울 값. 이 구성은 서버 지원에 따라 다르며 기본값은 `false`입니다. |
| 연결 사양 ID | 연결 사양 ID는 기본 및 소스 연결 생성과 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Oracle]의 연결 사양 ID는 `d6b52d86-f0f8-475f-89d4-ce54c8527328`입니다. **참고**: 이 자격 증명은 [!DNL Flow Service] API를 통해 연결할 때만 필요합니다. |


## API를 사용하여 [!DNL Oracle]을(를) [!DNL Experience Platform]에 연결

- [흐름 서비스 API를 사용하여 Oracle DB 연결](../../tutorials/api/create/databases/oracle.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 [!DNL Oracle]을(를) [!DNL Experience Platform]에 연결

- [Experience Platform UI 작업 영역을 사용하여 Oracle DB를 연결합니다.](../../tutorials/ui/create/databases/oracle.md)
- [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
