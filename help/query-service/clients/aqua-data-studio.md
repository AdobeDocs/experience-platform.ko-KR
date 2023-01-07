---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;Aqua Data Studio;Aqua data Studio;쿼리 서비스에 연결
solution: Experience Platform
title: Aqua Data Studio를 쿼리 서비스에 연결
description: 이 문서에서는 Aqua Data Studio와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 설명합니다.
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Connect [!DNL Aqua Data Studio] 쿼리 서비스

이 문서에서는 연결 단계를 설명합니다 [!DNL Aqua Data Studio] Adobe Experience Platform [!DNL Query Service].

## 시작하기

이 안내서에서는 다음에 이미 액세스할 수 있어야 합니다 [!DNL Aqua Data Studio] 인터페이스를 탐색하는 방법을 숙지하십시오. 에 대한 추가 정보 [!DNL Aqua Data Studio] 은 [공식 [!DNL Aqua Data Studio] 설명서](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>있습니다 [!DNL Windows] 및 [!DNL macOS] 버전 [!DNL Aqua Data Studio]. 이 안내서의 스크린샷은 [!DNL macOS] 데스크탑 앱. 버전 간의 UI에 약간의 불일치가 있을 수 있습니다.

연결에 필요한 자격 증명을 획득하려면 [!DNL Aqua Data Studio] Experience Platform을 사용하려면 [!UICONTROL 쿼리] 플랫폼 UI의 작업 영역입니다. 현재 액세스 권한이 없는 경우 IMS 조직 관리자에게 문의하십시오 [!UICONTROL 쿼리] 작업 공간.

## 서버 등록 {#register-server}

설치 후 [!DNL Aqua Data Studio]로 지정하는 경우 먼저 서버를 등록해야 합니다. 주 메뉴에서 을(를) 선택합니다 **[!DNL Server]**, 그 다음 **[!DNL Register Server]**.

![서버 등록 서버가 강조 표시된 서버 드롭다운 메뉴](../images/clients/aqua-data-studio/register-server.png)

다음 **[!DNL Register Server]** 대화 상자가 나타납니다. 아래에 **[!DNL General]** 탭, 선택 **[!DNL PostgreSQL]** 왼쪽에 있는 목록에서 대화 상자가 표시되면 서버 설정에 대해 다음 세부 정보를 제공합니다.

- **[!DNL Name]**: 연결의 이름입니다. 연결을 인식하려면 친숙한 이름을 제공하는 것이 좋습니다.
- **[!DNL Login Name]**: 로그인 이름은 플랫폼 조직 ID입니다. 이렇게 하려면 `ORG_ID@AdobeOrg`.
- **[!DNL Password]**: 이 문자열은 [!DNL Query Service] 자격 증명 대시보드.
- **[!DNL Host and Port]**: 호스트 끝점 및 해당 포트 [!DNL Query Service]. 연결할 포트 80을 사용해야 합니다. [!DNL Query Service].
- **[!DNL Database]:** 사용할 데이터베이스입니다. 플랫폼 UI 자격 증명에 대한 값 사용 `dbname`: `prod:all`.

![다음 [!DNL Aqua Data Studio] 필수 입력 필드가 강조 표시된 일반 탭](../images/clients/aqua-data-studio/register-server-general-tab.png)

### [!DNL Query Service] 자격 증명

자격 증명을 찾으려면 [!DNL Platform] UI 및 선택 **[!UICONTROL 쿼리]** 왼쪽 탐색에서 다음을 차례로 수행합니다 **[!UICONTROL 자격 증명]**. 로그인 자격 증명, 호스트, 포트 및 데이터베이스 이름을 찾는 전체 방법은 [자격 증명 안내서](../ui/credentials.md).

[!DNL Query Service] 또한 타사 클라이언트로 1회 설정할 수 있도록 만료되는 자격 증명을 제공합니다. 다음 문서를 참조하십시오. [만료되지 않은 자격 증명을 생성하고 사용하는 방법에 대한 전체 지침](../ui/credentials.md#non-expiring-credentials).

### SSL 모드 설정

다음으로, **[!DNL Driver]** 탭. 아래 **[!DNL Parameters]**&#x200B;를 사용하여 값을 로 설정합니다. `?sslmode=require`

>[!IMPORTANT]
>
>자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md) Adobe Experience Platform Query Service에 대한 타사 연결에 대한 SSL 지원 및 `verify-full` SSL 모드.

![다음 [!DNL Aqua Data Studio] 매개 변수 필드가 강조 표시된 드라이버 탭입니다.](../images/clients/aqua-data-studio/register-server-driver-tab.png)

연결 세부 정보를 입력한 후 을 선택합니다 **[!DNL Test Connection]** 자격 증명이 제대로 작동하는지 확인합니다. 연결 테스트가 성공하면 **[!DNL Save]** 서버를 등록하려면 연결을 확인하는 확인 대화 상자가 나타나고 대시보드에 연결이 나타납니다. 이제 서버에 연결하고 스키마 개체를 볼 수 있습니다.

## 다음 단계

이제 [!DNL Query Service]를 사용하여 다음을 수행할 수 있습니다. **[!DNL Query Analyzer]** within [!DNL Aqua Data Studio] SQL 문을 실행하고 편집할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
