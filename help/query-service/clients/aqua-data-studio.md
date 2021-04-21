---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;아쿠아 데이터 스튜디오;쿼리 서비스에 연결;;home;popular topics service;query service;
solution: Experience Platform
title: Aqua Data Studio를 쿼리 서비스에 연결
topic-legacy: connect
description: 이 문서에서는 Aqua Data Studio와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 안내합니다.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# 쿼리 서비스에 [!DNL Aqua Data Studio] 연결

이 문서에서는 [!DNL Aqua Data Studio]과(와) Adobe Experience Platform [!DNL Query Service]을(를) 연결하는 단계를 다룹니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Aqua Data Studio]에 액세스할 수 있으며 인터페이스를 탐색하는 방법에 익숙하다고 가정합니다. [!DNL Aqua Data Studio]에 대한 자세한 내용은 [공식 [!DNL Aqua Data Studio] 설명서](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1)에서 확인할 수 있습니다.

[!DNL Aqua Data Studio]을(를) 설치한 후 먼저 서버를 등록해야 합니다. 주 메뉴에서 **[!DNL Server]**, **[!DNL Register Server]** 순으로 선택합니다.

![](../images/clients/aqua-data-studio/register-server.png)

**[!DNL Register Server]** 대화 상자가 나타납니다. **[!DNL General]** 탭의 왼쪽 목록에서 **[!DNL PostgreSQL]**&#x200B;을 선택합니다. 나타나는 대화 상자에서 서버 설정에 대해 다음 세부 정보를 제공합니다.

- **[!DNL Name]**:연결 이름입니다.
- **[!DNL Login Name and Password]**:사용할 로그인 자격 증명입니다. 사용자 이름은 `ORG_ID@AdobeOrg` 형식을 사용합니다.
- **[!DNL Host and Port]**:호스트 끝점 및 해당 포트 [!DNL Query Service]입니다. [!DNL Query Service]에 연결하려면 포트 80을 사용해야 합니다.
- **[!DNL Database]** : 사용할 데이터베이스입니다.

>[!NOTE]
>
>로그인 자격 증명, 호스트, 포트 및 데이터베이스 이름을 찾는 방법에 대한 자세한 내용은 플랫폼](https://platform.adobe.com/query/configuration)의 [자격 증명 페이지를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인한 다음 **[!UICONTROL Queries]** 뒤에 **[!UICONTROL Credentials]**&#x200B;를 선택합니다.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

**[!DNL Driver]** 탭을 선택합니다. **[!DNL Parameters]** 아래에서 값을 `?sslmode=require`(으)로 설정합니다.

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

연결 세부 사항을 입력한 후 자격 증명이 제대로 작동하는지 확인하려면 **[!DNL Test Connection]**&#x200B;을 선택합니다. 연결이 성공하면 **[!DNL Save]**&#x200B;을 선택하여 서버를 등록합니다. 등록이 완료되면 대시보드에 연결이 나타나 서버에 연결하고 해당 스키마 객체를 볼 수 있음을 확인합니다.

## 다음 단계

[!DNL Query Service]에 연결되었으므로 [!DNL Aqua Data Studio] 내의 **[!DNL Query Analyzer]**&#x200B;을 사용하여 SQL 문을 실행하고 편집할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md)를 참조하십시오.
