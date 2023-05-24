---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;Aqua Data Studio;Aqua Data Studio;쿼리 서비스에 연결;
solution: Experience Platform
title: Aqua Data Studio를 쿼리 서비스에 연결
description: 이 문서에서는 Aqua Data Studio를 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 안내합니다.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# 연결 [!DNL Aqua Data Studio] 쿼리 서비스

이 문서에서는 다음 연결 단계를 다룹니다 [!DNL Aqua Data Studio] Adobe Experience Platform 사용 [!DNL Query Service].

## 시작하기

이 안내서를 사용하려면 액세스 권한이 있어야 합니다. [!DNL Aqua Data Studio] 인터페이스를 탐색하는 방법을 숙지하십시오. 다음에 대한 추가 정보: [!DNL Aqua Data Studio] 에서 찾을 수 있음 [공식 [!DNL Aqua Data Studio] 설명서](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>다음 항목이 있습니다. [!DNL Windows] 및 [!DNL macOS] 버전 [!DNL Aqua Data Studio]. 이 안내서의 스크린샷은 [!DNL macOS] 데스크탑 앱입니다. 버전 간에 UI에 사소한 불일치가 있을 수 있습니다.

연결에 필요한 자격 증명을 획득하려면 [!DNL Aqua Data Studio] 을(를) Experience Platform 하려면 다음에 대한 액세스 권한이 있어야 합니다. [!UICONTROL 쿼리] Platform UI의 작업 공간 현재 다음에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오. [!UICONTROL 쿼리] 작업 영역.

## 서버 등록 {#register-server}

설치 후 [!DNL Aqua Data Studio]를 설치한 후 먼저 서버를 등록해야 합니다. 방법에 대한 지침은 공식 Aqua Data Studio 설명서 를 참조하십시오. [를 실행합니다. [!DNL Register Server] 대화 상자](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) 및 [서버 등록](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

한 번 **[!DNL Register Server]** postgresSQL 서버에 대한 대화 상자가 나타납니다. 서버 설정에 대한 다음 세부 정보를 제공합니다.

- **[!DNL Name]**: 연결의 이름입니다. 연결을 인식하기 위해 친숙한 이름을 제공하는 것이 좋습니다.
- **[!DNL Login Name]**: 로그인 이름은 Platform 조직 ID입니다. 형식은 다음과 같습니다. `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: 다음에 있는 영숫자 문자열입니다. [!DNL Query Service] 자격 증명 대시보드.
- **[!DNL Host and Port]**: 호스트 끝점 및 의 해당 포트 [!DNL Query Service]. 연결하려면 포트 80을 사용해야 합니다. [!DNL Query Service].
- **[!DNL Database]:** 사용할 데이터베이스입니다. Platform UI 자격 증명에 대한 값 사용 `dbname`: `prod:all`.

### [!DNL Query Service] 자격 증명

자격 증명을 찾으려면 [!DNL Platform] UI 및 선택 **[!UICONTROL 쿼리]** 왼쪽 탐색 후 **[!UICONTROL 자격 증명]**. 로그인 자격 증명, 호스트, 포트 및 데이터베이스 이름을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md).

[!DNL Query Service] 또한 타사 클라이언트와의 1회 설정을 허용하는 만료되지 않는 자격 증명을 제공합니다. 다음 설명서를 참조하십시오. [만료되지 않는 자격 증명을 생성하고 사용하는 방법에 대한 전체 지침](../ui/credentials.md#non-expiring-credentials).

### SSL 모드 설정

다음으로, SSL 모드 값을 로 설정해야 합니다. `?sslmode=require`. 이 작업은 다음에서 수행됩니다. [!DNL Driver] 의 탭 [!DNL Edit Server Properties] 대화 상자. 방법에 대한 지침은 공식 Aqua Data Studio 설명서 를 참조하십시오. [드라이버 속성 편집](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) 및 [다음에 대한 SSL 구성 [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). 검색 창을 사용하여 `sslmode` 속성.

>[!IMPORTANT]
>
>다음을 참조하십시오. [[!DNL Query Service] SSL 설명서](./ssl-modes.md) Adobe Experience Platform 쿼리 서비스에 대한 서드파티 연결에 대한 SSL 지원 및 을 사용하여 연결하는 방법에 대해 알아봅니다. `verify-full` SSL 모드.

연결 세부 정보를 입력한 후 동일한 탭에서 을 선택합니다. **[!DNL Test Connection]** 자격 증명이 제대로 작동하는지 확인합니다. 연결 테스트가 성공하면 을 선택합니다. **[!DNL Save]** 서버를 등록합니다. 연결을 확인하는 대화 상자가 나타나고 연결 아이콘이 대시보드에 나타납니다. 이제 서버에 연결하고 해당 스키마 개체를 볼 수 있습니다.

## 다음 단계

에 연결했으므로 [!DNL Query Service], 다음을 사용할 수 있습니다. **[!DNL Query Analyzer]** 다음 범위 내 [!DNL Aqua Data Studio] SQL 문을 실행하고 편집합니다. 쿼리 작성 및 실행 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
