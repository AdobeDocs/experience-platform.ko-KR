---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;DB 시각화 도우미;DB 시각화 도우미;DB 시각화 도우미;쿼리 서비스에 연결;
solution: Experience Platform
title: DbVisualizer를 쿼리 서비스에 연결
description: 이 문서에서는 DbVisualizer를 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 안내합니다.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# 연결 [!DNL DbVisualizer] 끝 [!DNL Query Service] {#connect-dbvisualizer}

이 문서에서는 [!DNL DbVisualizer] Adobe Experience Platform을 사용한 데이터베이스 도구 [!DNL Query Service].

## 시작하기

이 안내서를 사용하려면 이미 다음 항목에 대한 액세스 권한이 있어야 합니다. [!DNL DbVisualizer] 데스크탑 앱으로 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 다운로드하려면 [!DNL DbVisualizer] 데스크탑 앱 또는 자세한 내용은 [공식 [!DNL DbVisualizer] 설명서](https://www.dbvis.com/download/).

연결에 필요한 자격 증명을 획득하려면 [!DNL  DbVisualizer] Experience Platform을 수행하려면 Platform UI에서 쿼리 작업 영역에 액세스할 수 있어야 합니다. 현재 쿼리 작업 영역에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오.

## 데이터베이스 연결 만들기 {#connect-database}

로컬 컴퓨터에 데스크탑 앱을 설치했으면 공식 BDVisualizer 지침을 따라 다음을 수행합니다. [새 데이터베이스 연결 만들기](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

을(를) 선택하면 **[!DNL PostgreSQL]** 다음에서 [!DNL Connections] list, an [!DNL Object View] 새 항목 탭 [!DNL PostgreSQL] 연결이 나타납니다.

### 연결에 대한 드라이버 속성 설정 {#properties}

다음에서 [!DNL PostgreSQL] 개체 보기 탭에서 **[!DNL Properties]** 탭, 다음 **[!DNL Driver Properties]** 를 클릭합니다. 다음에 대한 추가 정보: [드라이버 속성](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) 공식 문서에서 확인할 수 있습니다.

그런 다음 아래 표에 설명된 드라이버 속성을 입력합니다.

>[!IMPORTANT]
>
>DBVisualizer를 Adobe Experience Platform과 연결하려면 SSL을 사용하도록 설정해야 합니다. 다음을 참조하십시오. [SSL 모드 설명서](./ssl-modes.md) Adobe Experience Platform 쿼리 서비스에 대한 서드파티 연결에 대한 SSL 지원 및 을 사용하여 연결하는 방법에 대해 알아봅니다. `verify-full` SSL 모드.

| 속성 | 설명 |
| ------ | ------ |
| `PGHOST` | 에 대한 호스트 이름 [!DNL PostgreSQL] 서버입니다. 이 값은 내 Experience Platform **[!UICONTROL 호스트] 자격 증명**. |
| `ssl` | SSL 값 정의 `1` SSL 사용을 활성화합니다. |
| `sslmode` | SSL 보호 수준을 제어합니다. 다음을 사용하는 것이 좋습니다. `require` Adobe Experience Platform에 타사 클라이언트를 연결할 때의 SSL 모드입니다. 다음 `require` 모드는 모든 통신에 암호화가 필요하며 네트워크를 신뢰할 수 있도록 하여 올바른 서버에 연결할 수 있도록 합니다. 서버 SSL 인증서 유효성 검사가 필요하지 않습니다. |
| `user` | 데이터베이스에 연결된 사용자 이름은 조직 ID입니다. 다음으로 끝나는 영숫자 문자열입니다. `@Adobe.Org`. 이 값은 내 Experience Platform **[!UICONTROL 사용자 이름] 자격 증명**. |

검색 창을 사용하여 각 속성을 찾은 다음 매개 변수 값에 해당하는 셀을 선택합니다. 셀이 파란색으로 강조 표시됩니다. 값 필드에 플랫폼 자격 증명을 입력하고 다음을 선택합니다. **[!DNL Apply]** 드라이버 속성을 추가합니다.

>[!NOTE]
>
>두 번째 추가 `user` 프로필, 선택 `user` 매개변수 열에서 파란색 + (더하기) 아이콘을 선택하여 각 사용자에 대한 자격 증명을 추가합니다. 선택 **[!DNL Apply]** 드라이버 속성을 추가합니다.

다음 [!DNL Edited] 열에는 매개 변수 값이 업데이트되었음을 나타내는 확인 표시가 표시됩니다.

### 쿼리 서비스 자격 증명 입력 {#query-service-credentials}

BBVisualizer를 쿼리 서비스와 연결하는 데 필요한 자격 증명을 찾으려면 플랫폼 UI에 로그인하고 를 선택합니다. **[!UICONTROL 쿼리]** 왼쪽 탐색 후 **[!UICONTROL 자격 증명]**. 을(를) 찾는 방법에 대한 자세한 내용은 **호스트**, **포트**, **데이터베이스**, **사용자 이름**, 및 **암호** 자격 증명, 다음을 읽으십시오. [자격 증명 안내서](../ui/credentials.md).

![[인증서] 및 [만료 인증서]가 강조 표시된 Experience Platform 쿼리 작업 영역의 [인증서] 페이지](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 또한 타사 클라이언트와의 1회 설정을 허용하는 만료되지 않는 자격 증명을 제공합니다. 다음 설명서를 참조하십시오. [만료되지 않는 자격 증명을 생성하고 사용하는 방법에 대한 전체 지침](../ui/credentials.md#non-expiring-credentials). BDVisualizer를 1회 설정으로 연결하려면 이 프로세스를 완료해야 합니다. 다음 `credential` 및 `technicalAccountId` 획득한 값은 DBVisualizer에 대한 값을 구성합니다. `password` 매개 변수.

## 인증 {#authentication}

연결이 설정될 때마다 사용자 ID 및 암호 기반 인증을 요구하려면 [!DNL Properties] 탭하고 선택 **[!DNL Authentication]** 탐색 사이드바에서 [!DNL PostgreSQL].

연결 인증 패널에서 **[!DNL Require Userid]** 및 **[!DNL Require Password]** 확인란을 선택한 다음 을 선택합니다 **[!DNL Apply]**. 다음에 대한 추가 정보: [인증 옵션 설정](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) 공식 문서에서 찾을 수 있습니다.

## 플랫폼에 연결

만료되거나 만료되지 않는 자격 증명을 사용하여 연결할 수 있습니다. 연결하려면 **[!DNL Connection]** 의 탭 [!DNL PostgreSQL] [개체 보기] 탭을 클릭하고 다음 설정에 대한 Experience Platform 자격 증명을 입력합니다. 에 대한 보완 지침 [수동 연결 설정](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) 는 공식 DBVisualizer 웹 사이트에서 사용할 수 있습니다.

>[!NOTE]
>
>아래 표에서 BDVisualizer에 필요한 모든 자격 증명은 매개 변수 설명에 명시되지 않는 한 만료 자격 증명과 만료되지 않는 자격 증명에 대해 동일합니다.

| 연결 매개 변수 | 설명 |
|---|---|
| **[!UICONTROL 이름]** | 연결의 이름을 만듭니다. 연결을 인식하기 위해 친숙한 이름을 제공하는 것이 좋습니다. |
| **[!UICONTROL 데이터베이스 서버]** | Experience Platform **[!UICONTROL 호스트]** 자격 증명. |
| **[!UICONTROL 데이터베이스 포트]** | 의 포트 [!DNL Query Service]. 포트를 사용해야 합니다. **80** 또는 **5432** 연결 대상 [!DNL Query Service]. |
| **[!UICONTROL 데이터베이스]** | Experience Platform 사용 **[!UICONTROL 데이터베이스]** 자격 증명 값: `prod:all`. |
| **[!UICONTROL 데이터베이스 사용자 ID]** | Platform 조직 ID입니다. Experience Platform 사용 **[!UICONTROL 사용자 이름]** 자격 증명 값. ID는 다음과 같은 형식이어야 합니다. `ORG_ID@AdobeOrg`. |
| **[!UICONTROL 데이터베이스 암호]** | 이 영숫자 문자열은 Experience Platform입니다. **[!UICONTROL 암호]** 자격 증명. 만료되지 않는 자격 증명을 사용하려는 경우 이 값은 `technicalAccountID` 및 `credential` 구성 JSON 파일에서 다운로드되었습니다. 암호 값은 {technicalAccountId}:{credential} 형식을 사용합니다. 만료되지 않는 자격 증명에 대한 구성 JSON 파일은 초기화 중에 Adobe이 복사본을 보관하지 않는 한 번 다운로드됩니다. |

모든 관련 자격 증명을 입력한 후 을(를) 선택합니다 **[!DNL Connect]**.

다음 [!DNL Connect] 대화는 세션의 첫 번째 경우에 나타납니다. 사용자 ID 및 암호를 입력하고 **[!DNL Connect]**. 성공적인 연결을 확인하는 메시지가 로그에 나타납니다.

## 다음 단계

연결했으므로 [!DNL DbVisualizer] 포함 [!DNL Query Service], 다음을 사용할 수 있습니다 [!DNL DbVisualizer] 쿼리를 작성합니다. 쿼리 작성 및 실행 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
