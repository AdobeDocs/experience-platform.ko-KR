---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;Aqua Data Studio;Aqua Data Studio;쿼리 서비스에 연결;
solution: Experience Platform
title: Aqua Data Studio를 쿼리 서비스에 연결
description: 이 문서에서는 Aqua Data Studio를 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 안내합니다.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL Aqua Data Studio] 연결

이 문서에서는 [!DNL Aqua Data Studio]을(를) Adobe Experience Platform [!DNL Query Service]과(와) 연결하는 단계를 다룹니다.

## 시작하기

이 안내서를 사용하려면 이미 [!DNL Aqua Data Studio]에 액세스할 수 있어야 하며 해당 인터페이스를 탐색하는 방법에 익숙해야 합니다. [!DNL Aqua Data Studio]에 대한 자세한 내용은 [공식 [!DNL Aqua Data Studio] 설명서](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1)에서 확인할 수 있습니다.

>[!NOTE]
>
>[!DNL Aqua Data Studio]의 [!DNL Windows] 및 [!DNL macOS] 버전이 있습니다. 이 안내서의 스크린샷은 [!DNL macOS] 데스크톱 앱을 사용하여 찍은 것입니다. 버전 간에 UI에 사소한 불일치가 있을 수 있습니다.

[!DNL Aqua Data Studio]을(를) Experience Platform에 연결하는 데 필요한 자격 증명을 획득하려면 Platform UI에서 [!UICONTROL 쿼리] 작업 영역에 액세스할 수 있어야 합니다. 현재 [!UICONTROL 쿼리] 작업 영역에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오.

## 서버 등록 {#register-server}

[!DNL Aqua Data Studio]을(를) 설치한 후 먼저 서버를 등록해야 합니다. [대화 상자  [!DNL Register Server] 시작](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) 및 [서버 등록](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio)하는 방법에 대한 지침은 공식 Aqua Data Studio 설명서를 참조하세요.

PostgresSQL 서버에 대한 **[!DNL Register Server]** 대화 상자가 나타나면 서버 설정에 대해 다음 세부 정보를 제공합니다.

- **[!DNL Name]**: 연결의 이름입니다. 연결을 인식하기 위해 친숙한 이름을 제공하는 것이 좋습니다.
- **[!DNL Login Name]**: 로그인 이름은 플랫폼 조직 ID입니다. `ORG_ID@AdobeOrg` 형식을 사용합니다.
- **[!DNL Password]**: [!DNL Query Service] 자격 증명 대시보드에 있는 영숫자 문자열입니다.
- **[!DNL Host and Port]**: [!DNL Query Service]에 대한 호스트 끝점 및 해당 포트입니다. [!DNL Query Service]에 연결하려면 포트 80을 사용해야 합니다.
- **[!DNL Database]:** 사용할 데이터베이스입니다. 플랫폼 UI 자격 증명 `dbname`에 대한 값을 사용합니다. `prod:all`.

### [!DNL Query Service] 자격 증명

자격 증명을 찾으려면 [!DNL Platform] UI에 로그인하고 왼쪽 탐색에서 **[!UICONTROL 쿼리]**&#x200B;를 선택한 다음 **[!UICONTROL 자격 증명]**&#x200B;을 선택하십시오. 로그인 자격 증명, 호스트, 포트 및 데이터베이스 이름을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오.

[!DNL Query Service]은(는) 타사 클라이언트와의 일회성 설정을 허용하기 위해 만료되지 않는 자격 증명도 제공합니다. 만료되지 않는 자격 증명을 생성하고 사용하는 방법에 대한 [전체 지침](../ui/credentials.md#non-expiring-credentials)에 대해서는 설명서를 참조하십시오.

### SSL 모드 설정

그런 다음 SSL 모드 값을 `?sslmode=require`(으)로 설정해야 합니다. 이 작업은 [!DNL Edit Server Properties] 대화 상자의 [!DNL Driver] 탭에서 수행됩니다. [드라이버 속성 편집](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) 및 [SSL을 구성 [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration)하는 방법에 대한 지침은 공식 Aqua Data Studio 설명서를 참조하십시오. 검색 창을 사용하여 `sslmode` 속성을 찾으십시오.

>[!IMPORTANT]
>
>Adobe Experience Platform 쿼리 서비스에 대한 서드파티 연결에 대한 SSL 지원 및 `verify-full` SSL 모드를 사용하여 연결하는 방법에 대한 자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md)를 참조하세요.

연결 세부 정보를 입력한 후 같은 탭에서 **[!DNL Test Connection]**&#x200B;을(를) 선택하여 자격 증명이 제대로 작동하는지 확인합니다. 연결 테스트가 성공하면 **[!DNL Save]**&#x200B;을(를) 선택하여 서버를 등록합니다. 연결을 확인하는 대화 상자가 나타나고 연결 아이콘이 대시보드에 나타납니다. 이제 서버에 연결하고 해당 스키마 개체를 볼 수 있습니다.

## 다음 단계

[!DNL Query Service]에 연결되었으므로 [!DNL Aqua Data Studio] 내의 **[!DNL Query Analyzer]**&#x200B;을(를) 사용하여 SQL 문을 실행하고 편집할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 가이드](../best-practices/writing-queries.md)를 참조하십시오.
