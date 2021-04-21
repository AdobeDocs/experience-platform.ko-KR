---
keywords: Experience Platform;home;popular topics;PSQL;쿼리 서비스에 대한 psqlconnect;쿼리 서비스;쿼리 서비스;
solution: Experience Platform
title: 쿼리 서비스에 PSQL 연결
topic-legacy: connect
description: PSQL은 컴퓨터에 PostgreSQL을 설치할 때 제공되는 명령줄 인터페이스입니다. 다음 지침에 따라 설치할 수 있습니다.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---

# 쿼리 서비스에 PSQL 연결

PSQL은 컴퓨터에 [!DNL PostgreSQL]을(를) 설치할 때 설치되는 명령줄 인터페이스입니다. 이 문서에서는 Adobe Experience Platform [!DNL Query Service]에 PSQL을 연결하는 단계를 설명합니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL PSQL]에 액세스할 수 있으며 이 기능을 사용하는 방법에 익숙하다고 가정합니다. [!DNL PSQL]에 대한 자세한 내용은 [공식 [!DNL PSQL] 설명서](https://www.postgresql.org/docs/current/app-psql.html)을 참조하십시오.

컴퓨터에 PSQL을 설치한 후 쿼리 서비스에 PSQL을 연결할 준비가 되었습니다. [!DNL Platform] UI로 돌아간 다음 **[!UICONTROL Queries]**, **[!UICONTROL Credentials]** 순으로 선택합니다.

![이미지](../images/clients/psql/connect-bi.png)

**[!UICONTROL PSQL Command]** 레이블이 있는 섹션을 복사할 아이콘을 선택한 다음 Enter 키를 누르기 전에 명령 문자열을 터미널 또는 명령줄 창에 붙여넣습니다.

>[!IMPORTANT]
>
>PC를 사용하는 경우 텍스트 편집기를 사용하여 명령 문자열에서 줄 바꿈을 제거한 다음 문자열을 복사합니다. 또한 버전 12.0 이상을 사용하는 경우 연결 문자열에 `PGGSSENCMODE=disable`을 추가해야 합니다.

다음과 같은 결과가 표시됩니다.

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

버전 10.5 이상이 표시되지 않으면 해당 버전 이상을 다운로드해야 합니다.

## 다음 단계

이제 [!DNL Query Service]에 연결되었으므로 PSQL을 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md)에 대한 안내서를 참조하십시오.
