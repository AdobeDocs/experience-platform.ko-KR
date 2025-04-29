---
keywords: Experience Platform;홈;자주 찾는 항목;PSQL;쿼리 서비스에 psqlconnect;쿼리 서비스;쿼리 서비스;
solution: Experience Platform
title: PSQL을 쿼리 서비스에 연결
description: 지원되는 PostgreSQL 버전 및 설치 지침을 포함하여 PSQL 클라이언트를 Adobe Experience Platform 쿼리 서비스에 연결하는 방법에 대해 알아봅니다.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 74f4ac5a3ca4c06e81111ef453ae0effd21b3f16
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# PSQL을 쿼리 서비스에 연결

PSQL은 시스템에 PostgreSQL과 함께 설치되는 명령줄 인터페이스입니다. 이 문서에서는 PSQL을 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 다룹니다.

>[!IMPORTANT]
>
>쿼리 서비스는 PSQL 버전 14.x로만 연결을 지원합니다. 14.x 이전 버전(예: 10.x부터 13.x까지) 및 이후 버전(15.x 이상)은 공식적으로 지원되지 않습니다. 호환되는 클라이언트 버전을 설치했는지 확인하십시오. 자세한 내용은 [PostgreSQL 서비스 종료 날짜](https://endoflife.date/postgresql)를 참조하세요.

시작하기 전에 PSQL에 대한 액세스 권한이 있고 클라이언트 사용에 대한 기본 지식이 있는지 확인하십시오. PSQL에 대한 자세한 내용은 [공식 PSQL 설명서](https://www.postgresql.org/docs/current/app-psql.html)를 참조하십시오.

>[!IMPORTANT]
>
>PostgreSQL을 다운로드할 때 버전 14.x를 선택해야 합니다. 기본적으로 PostgreSQL 웹 사이트는 쿼리 서비스와 호환되지 않을 수 있는 최신 버전을 제공합니다.

PSQL이 설치되면 쿼리 서비스에 연결할 수 있습니다. Experience Platform UI로 돌아간 다음 **[!UICONTROL 쿼리]**, **[!UICONTROL 자격 증명]**&#x200B;을 차례로 선택합니다.

**[!UICONTROL PSQL 명령]** 섹션에서 **[!UICONTROL 클립보드에 복사]** 아이콘(![복사 아이콘](/help/images/icons/copy.png))을 선택하여 명령 문자열을 복사합니다.

![복사 아이콘이 강조 표시된 쿼리 대시보드 자격 증명 탭입니다.](../images/clients/psql/connect-bi.png)

명령 문자열을 터미널에 붙여 넣고 키보드에서 **Enter**&#x200B;를 누릅니다.

>[!IMPORTANT]
>
>PC를 사용하는 경우 텍스트 편집기를 사용하여 명령 문자열에서 줄바꿈을 제거한 다음 문자열을 복사합니다. 버전 12.0 이상을 사용하는 경우 연결 문자열에 `PGGSSENCMODE=disable`을(를) 추가해야 합니다. 이 설정은 GSSAPI 암호화를 사용하지 않도록 설정합니다. 이 암호는 쿼리 서비스 연결에 필요하지 않으며 연결 오류가 발생할 수 있습니다.<br>또한 만료되지 않는 자격 증명을 사용하는 경우 암호 필드를 만료되지 않는 자격 증명 암호로 바꾸십시오. 만료되지 않는 자격 증명에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오.

다음과 같은 결과가 표시됩니다.

```shell
psql (14.4, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

버전 14.x가 표시되지 않으면 [공식 PostgreSQL 다운로드 페이지](https://www.postgresql.org/download/)에서 지원되는 14.x 버전의 PSQL을 다운로드하여 설치하십시오.

>[!NOTE]
>
>운영 체제에 대한 설치 지침을 따른 다음 터미널에서 `psql --version`을(를) 실행하여 설치된 PSQL 버전을 확인합니다.

## 다음 단계

쿼리 서비스에 연결했으므로 PSQL을 사용하여 쿼리를 작성할 수 있습니다. 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md)에 대한 안내서를 참조하십시오.
