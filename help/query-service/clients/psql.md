---
keywords: Experience Platform;홈;자주 찾는 항목;PSQL;쿼리 서비스에 psqlconnect;쿼리 서비스;쿼리 서비스;
solution: Experience Platform
title: PSQL을 쿼리 서비스에 연결
description: PSQL은 컴퓨터에 PostgreSQL을 설치할 때 제공되는 명령줄 인터페이스입니다. 다음 지침에 따라 설치할 수 있습니다.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# PSQL을 쿼리 서비스에 연결

PSQL은 컴퓨터에 [!DNL PostgreSQL]을(를) 설치할 때 설치되는 명령줄 인터페이스입니다. 이 문서에서는 PSQL을 Adobe Experience Platform [!DNL Query Service]과(와) 연결하는 단계를 다룹니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL PSQL]에 액세스할 수 있고 사용 방법을 잘 알고 있다고 가정합니다. [!DNL PSQL]에 대한 자세한 내용은 [공식 [!DNL PSQL] 설명서](https://www.postgresql.org/docs/current/app-psql.html)에서 확인할 수 있습니다.

컴퓨터에 PSQL을 설치한 후 쿼리 서비스와 PSQL을 연결할 준비가 되었습니다. [!DNL Experience Platform] UI로 돌아간 다음 **[!UICONTROL 쿼리]**, **[!UICONTROL 자격 증명]**&#x200B;을 차례로 선택합니다.

**[!UICONTROL PSQL 명령]** 섹션에서 **[!UICONTROL 클립보드에 복사]** 아이콘(![복사 아이콘](/help/images/icons/copy.png))을 선택하여 명령 문자열을 복사합니다.

![복사 아이콘이 강조 표시된 쿼리 대시보드 자격 증명 탭입니다.](../images/clients/psql/connect-bi.png)

터미널 또는 명령줄 창에 명령 문자열을 붙여 넣고 키보드에서 **Enter**&#x200B;를 누릅니다.

>[!IMPORTANT]
>
>PC를 사용하는 경우 텍스트 편집기를 사용하여 명령 문자열에서 줄바꿈을 제거한 다음 문자열을 복사합니다. 버전 12.0 이상을 사용하는 경우 연결 문자열에 `PGGSSENCMODE=disable`을(를) 추가해야 합니다. 또한 만료되지 않는 자격 증명을 사용하는 경우 암호 필드를 만료되지 않는 자격 증명 암호로 바꾸십시오. 만료되지 않는 자격 증명에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오.

다음과 같은 결과가 표시됩니다.

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

버전 10.5 이상이 표시되지 않으면 해당 버전 이상을 다운로드해야 합니다.

## 다음 단계

[!DNL Query Service]에 연결되었으므로 PSQL을 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md)에 대한 안내서를 참조하십시오.
