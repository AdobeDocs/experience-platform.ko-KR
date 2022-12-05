---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;Db 시각화 도우미;Db 시각화 도우미;쿼리 서비스에 연결
solution: Experience Platform
title: DbVisualizer를 Query Service에 연결
topic-legacy: connect
description: 이 문서에서는 DbVisualizer와 Adobe Experience Platform Query Service를 연결하는 단계를 설명합니다.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 640a89231abf96a966f55dce2e3a7242c739538f
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Connect [!DNL DbVisualizer] to [!DNL Query Service] {#connect-dbvisualizer}

이 문서에서는 [!DNL DbVisualizer] Adobe Experience Platform을 사용한 데이터베이스 도구 [!DNL Query Service].

## 시작하기

이 안내서에서는 이미 [!DNL DbVisualizer] 데스크탑 앱과 는 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 를 다운로드하려면 [!DNL DbVisualizer] 자세한 내용은 데스크탑 앱 또는 [공식 [!DNL DbVisualizer] 설명서](https://www.dbvis.com/download/).

>[!NOTE]
>
>있습니다 [!DNL Windows], [!DNL macOS], 및 [!DNL Linux] 버전 [!DNL DbVisualizer]. 이 안내서의 스크린샷은 [!DNL macOS] 데스크탑 앱. 버전 간의 UI에 약간의 불일치가 있을 수 있습니다.

연결에 필요한 자격 증명을 획득하려면 [!DNL  DbVisualizer] Experience Platform을 수행하려면 플랫폼 UI의 쿼리 작업 영역에 액세스할 수 있어야 합니다. 현재 쿼리 작업 영역에 대한 액세스 권한이 없는 경우 IMS 조직 관리자에게 문의하십시오.

## 데이터베이스 연결 만들기 {#connect-database}

로컬 컴퓨터에 데스크탑 앱을 설치하면 앱을 시작하고 을(를) 선택합니다 **[!DNL Create a Database Connection]** 처음 [!DNL DbVisualizer] 메뉴 아래의 제품에서 사용할 수 있습니다. 그런 다음 을(를) 선택합니다 **[!DNL Create a Connection]** 오른쪽 패널에 있는 를 클릭합니다.

![다음 [!DNL DbVisualizer] &quot;데이터베이스 연결 만들기&quot;가 강조 표시된 기본 메뉴](../images/clients/dbvisualizer/create-db-connection.png)

검색 창을 사용하거나 [!DNL PostgreSQL] 드라이버 이름 드롭다운 목록에서 삭제할 수 있습니다. 데이터베이스 연결 작업 영역이 나타납니다.

![드라이버 이름 드롭다운 메뉴에서 [!DNL PostgreSQL] 강조 표시되어 있습니다.](../images/clients/dbvisualizer/driver-name.png)

데이터베이스 연결 작업 영역에서 **[!DNL Properties]** 탭, 그 다음에 **[!DNL Driver Properties]** 탐색 사이드바에서 참조할 수 있습니다.

![속성 및 드라이버 속성이 강조 표시된 데이터베이스 연결 작업 영역입니다.](../images/clients/dbvisualizer/driver-properties.png)

아래 표에 표시된 드라이버 속성은 DBVisualizer에서 SSL을 사용할 수 있도록 설정하는 것이 좋습니다.

| 속성 | 설명 |
| ------ | ------ |
| `PGHOST` | 의 호스트 이름 [!DNL PostgreSQL] server. 이 값은 Experience Platform입니다 [!UICONTROL 호스트] 자격 증명. |
| `ssl` | SSL 값 정의 `1` 를 ssl을 사용하도록 설정합니다. |
| `sslmode` | 이는 SSL 보호 수준을 제어합니다. 을 사용하는 것이 좋습니다 `require` 타사 클라이언트를 Adobe Experience Platform에 연결할 때 SSL 모드. 다음 `require` 모드에서는 모든 통신에서 암호화가 필요하며 올바른 서버에 연결하기 위해 네트워크를 신뢰할 수 있습니다. 서버 SSL 인증서 유효성 검사가 필요하지 않습니다. 자세한 내용은 [타사 클라이언트 연결을 위한 SSL 옵션](./ssl-modes.md) to [!DNL Query Service]. |
| `user` | 데이터베이스에 연결된 사용자 이름은 조직 ID입니다. 로 끝나는 영숫자 문자열입니다 `@adobe.org` |

>[!IMPORTANT]
>
>자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md) Adobe Experience Platform Query Service에 대한 타사 연결에 대한 SSL 지원 및 `verify-full` SSL 모드.

### [!DNL Query Service] 자격 증명

다음 `PGHOST` 및 `user` 값은 Adobe Experience Platform 자격 증명에서 가져옵니다. 자격 증명을 찾으려면 Platform UI에 로그인하고 를 선택합니다 **[!UICONTROL 쿼리]** 왼쪽 탐색에서 다음을 차례로 수행합니다 **[!UICONTROL 자격 증명]**. 데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md).

![자격 증명과 만료 자격 증명이 강조 표시된 Experience Platform 쿼리 작업 영역의 자격 증명 페이지.](../images/clients/dbvisualizer/query-service-credentials-page.png)

[!DNL Query Service] 또한 타사 클라이언트로 1회 설정할 수 있도록 만료되는 자격 증명을 제공합니다. 다음 문서를 참조하십시오. [만료되지 않은 자격 증명을 생성하고 사용하는 방법에 대한 전체 지침](../ui/credentials.md#non-expiring-credentials).

검색 막대를 사용하여 각 속성을 찾은 다음 매개 변수 값에 해당하는 셀을 선택합니다. 셀이 파란색으로 강조 표시됩니다. 값 필드에 Platform 자격 증명을 입력하고 을 선택합니다. **[!DNL Apply]** 드라이버 속성을 추가하려면

>[!NOTE]
>
>초 추가 `user` 프로필, 선택 `user` 매개 변수 열에서 파란색 + (더하기) 아이콘을 선택하여 각 사용자에 대한 자격 증명을 추가합니다. 선택 **[!DNL Apply]** 드라이버 속성을 추가하려면

다음 [!DNL Edited] 열에는 매개 변수 값이 업데이트되었음을 나타내는 확인 표시가 표시됩니다.

## 인증

연결이 설정될 때마다 사용자 ID 및 암호 기반 인증을 필요로 하려면 을 선택합니다 **[!DNL Authentication]** 아래의 탐색 사이드바에서 [!DNL PostgreSQL].

연결 인증 패널에서 **[!DNL Require Userid]** 및 **[!DNL Require Password]** 확인란을 선택한 다음 **[!DNL Apply]**.

![용 인증 패널 [!DNL PostgreSQL] 사용자 ID 및 암호 필요 확인란을 선택한 데이터베이스 연결](../images/clients/dbvisualizer/connection-authentication.png)

## 플랫폼에 연결

연결을 만들려면 **[!DNL Connection]** 데이터베이스 연결 작업 영역에서 탭을 선택하고 다음 설정에 대한 Experience Platform 인증서를 입력합니다.

- **이름**: 연결을 인식하려면 친숙한 이름을 제공하는 것이 좋습니다.
- **데이터베이스 서버**: Experience Platform [!UICONTROL 호스트] 자격 증명.
- **데이터베이스 포트**: 포트 [!DNL Query Service]. 연결할 포트 80을 사용해야 합니다. [!DNL Query Service].
- **데이터베이스**: 자격 증명 사용 `dbname` value `prod:all`.
- **데이터베이스 사용자 ID**: 플랫폼 조직 ID입니다. Userid는 `ORG_ID@AdobeOrg`.
- **데이터베이스 암호**: 이 문자열은 [!DNL Query Service] 자격 증명 대시보드.

관련 자격 증명을 모두 입력한 후 을 선택합니다 **[!DNL Connect]**.

![다음 [!DNL PostgreSQL] 연결 탭 및 연결 단추가 강조 표시된 데이터베이스 연결 작업 영역입니다.](../images/clients/dbvisualizer/connect.png)

다음 [!DNL Connect] 대화 상자가 세션의 첫 번째 사례에 나타납니다.

![연결: [!DNL PostgreSQL] 데이터베이스 사용자 id 및 데이터베이스 암호 텍스트 필드가 강조 표시된 대화 상자](../images/clients/dbvisualizer/connect-dialog.png)

사용자 ID와 암호를 입력하고 을(를) 선택합니다 **[!DNL Connect]**. 연결에 성공했는지 확인하는 메시지가 로그에 나타납니다.

## 다음 단계

이제 연결해서 [!DNL DbVisualizer] with [!DNL Query Service], 다음 사용 가능 [!DNL DbVisualizer] 쿼리를 작성하려면 다음을 수행하십시오. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
