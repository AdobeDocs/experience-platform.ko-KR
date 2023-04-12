---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;Aqua Data Studio;Aqua data Studio;쿼리 서비스에 연결
solution: Experience Platform
title: Aqua Data Studio를 쿼리 서비스에 연결
description: 이 문서에서는 Aqua Data Studio와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 설명합니다.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Connect [!DNL Aqua Data Studio] 쿼리 서비스

이 문서에서는 연결 단계를 설명합니다 [!DNL Aqua Data Studio] Adobe Experience Platform [!DNL Query Service].

## 시작하기

이 안내서에서는 다음에 이미 액세스할 수 있어야 합니다 [!DNL Aqua Data Studio] 인터페이스를 탐색하는 방법을 숙지하십시오. 에 대한 추가 정보 [!DNL Aqua Data Studio] 은 [공식 [!DNL Aqua Data Studio] 설명서](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>있습니다 [!DNL Windows] 및 [!DNL macOS] 버전 [!DNL Aqua Data Studio]. 이 안내서의 스크린샷은 [!DNL macOS] 데스크탑 앱. 버전 간의 UI에 약간의 불일치가 있을 수 있습니다.

연결에 필요한 자격 증명을 획득하려면 [!DNL Aqua Data Studio] Experience Platform을 사용하려면 [!UICONTROL 쿼리] 플랫폼 UI의 작업 영역입니다. 현재 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오 [!UICONTROL 쿼리] 작업 공간.

## 서버 등록 {#register-server}

설치 후 [!DNL Aqua Data Studio]로 지정하는 경우 먼저 서버를 등록해야 합니다. 방법에 대한 지침은 공식 Aqua Data Studio 설명서를 참조하십시오 [launch [!DNL Register Server] 대화 상자](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) 및 [서버 등록](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

한 번 **[!DNL Register Server]** PostgresSQL Server에 대한 대화 상자가 나타나고 서버 설정에 대해 다음 세부 정보를 제공합니다.

- **[!DNL Name]**: 연결의 이름입니다. 연결을 인식하려면 친숙한 이름을 제공하는 것이 좋습니다.
- **[!DNL Login Name]**: 로그인 이름은 플랫폼 조직 ID입니다. 이렇게 하려면 `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: 이 문자열은 [!DNL Query Service] 자격 증명 대시보드.
- **[!DNL Host and Port]**: 호스트 끝점 및 해당 포트 [!DNL Query Service]. 연결할 포트 80을 사용해야 합니다. [!DNL Query Service].
- **[!DNL Database]:** 사용할 데이터베이스입니다. 플랫폼 UI 자격 증명에 대한 값 사용 `dbname`: `prod:all`.

### [!DNL Query Service] 자격 증명

자격 증명을 찾으려면 [!DNL Platform] UI 및 선택 **[!UICONTROL 쿼리]** 왼쪽 탐색에서 다음을 차례로 수행합니다 **[!UICONTROL 자격 증명]**. 로그인 자격 증명, 호스트, 포트 및 데이터베이스 이름을 찾는 전체 방법은 [자격 증명 안내서](../ui/credentials.md).

[!DNL Query Service] 또한 타사 클라이언트로 1회 설정할 수 있도록 만료되는 자격 증명을 제공합니다. 다음 문서를 참조하십시오. [만료되지 않은 자격 증명을 생성하고 사용하는 방법에 대한 전체 지침](../ui/credentials.md#non-expiring-credentials).

### SSL 모드 설정

다음으로, SSL 모드 값을 `?sslmode=require`. 이 작업은 [!DNL Driver] 의 탭 [!DNL Edit Server Properties] 대화 상자. 방법에 대한 지침은 공식 Aqua Data Studio 설명서를 참조하십시오 [드라이버 속성 편집](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) 및 [에 대한 SSL 구성 [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). 검색 막대를 사용하여 `sslmode` 속성을 사용합니다.

>[!IMPORTANT]
>
>자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md) Adobe Experience Platform Query Service에 대한 타사 연결에 대한 SSL 지원 및 `verify-full` SSL 모드.

연결 세부 정보를 입력한 후 동일한 탭에서 을 선택합니다 **[!DNL Test Connection]** 자격 증명이 제대로 작동하는지 확인합니다. 연결 테스트가 성공하면 **[!DNL Save]** 서버를 등록하려면 연결을 확인하는 확인 대화 상자가 나타나고 연결 아이콘이 대시보드에 나타납니다. 이제 서버에 연결하고 스키마 개체를 볼 수 있습니다.

## 다음 단계

이제 [!DNL Query Service]를 사용하여 다음을 수행할 수 있습니다. **[!DNL Query Analyzer]** within [!DNL Aqua Data Studio] SQL 문을 실행하고 편집할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
