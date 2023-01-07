---
keywords: Experience Platform;홈;인기 항목;PSQL;psqlconnect to query service;Query service;
solution: Experience Platform
title: PSQL을 Query Service에 연결
description: PSQL은 시스템에 PostgreSQL을 설치할 때 제공되는 명령줄 인터페이스입니다. 다음 지침에 따라 설치할 수 있습니다.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# PSQL을 Query Service에 연결

PSQL은 설치 시 설치되는 명령줄 인터페이스입니다 [!DNL PostgreSQL] 사용자 시스템에 있는 이 문서에서는 PSQL과 Adobe Experience Platform을 연결하는 단계를 설명합니다 [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL PSQL] 사용 방법도 잘 알고 있습니다. 에 대한 추가 정보 [!DNL PSQL] 은 [공식 [!DNL PSQL] 설명서](https://www.postgresql.org/docs/current/app-psql.html).

컴퓨터에 PSQL을 설치한 후 PSQL을 Query Service와 연결할 준비가 되었습니다. 로 돌아갑니다. [!DNL Platform] UI를 선택한 다음 **[!UICONTROL 쿼리]**, 그 다음 **[!UICONTROL 자격 증명]**.

아래에 **[!UICONTROL PSQL 명령]** 섹션에서 **[!UICONTROL 클립보드에 복사]** 아이콘 (![복사 아이콘](../images/clients/psql/copy-icon.png))를 클릭하여 명령 문자열을 복사합니다.

![복사 아이콘이 강조 표시된 쿼리 대시보드 자격 증명 탭.](../images/clients/psql/connect-bi.png)

명령 문자열을 터미널 또는 명령줄 창에 붙여 넣고 키를 누릅니다 **Enter 키** 클릭합니다.

>[!IMPORTANT]
>
>PC를 사용하는 경우 텍스트 편집기를 사용하여 명령 문자열의 줄 바꿈을 제거한 다음 문자열을 복사합니다. 버전 12.0 이상을 사용 중인 경우, 다음을 추가해야 합니다 `PGGSSENCMODE=disable` 연결 문자열에 연결할 수도 있습니다. 또한 만료되지 않은 자격 증명을 사용하는 경우 암호 필드를 만료되지 않은 자격 증명 암호로 바꾸십시오. 만료되지 않은 자격 증명에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md).

다음과 같은 결과가 표시됩니다.

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

버전 10.5 이상이 표시되지 않으면 해당 버전 이상을 다운로드해야 합니다.

## 다음 단계

이제 [!DNL Query Service]PSQL을 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md).
