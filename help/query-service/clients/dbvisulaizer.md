---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;DB 시각화 도우미;DB 시각화 도우미;DB 시각화 도우미;쿼리 서비스에 연결;
solution: Experience Platform
title: DbVisualizer를 쿼리 서비스에 연결
description: 이 문서에서는 DbVisualizer를 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 안내합니다.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---

# [!DNL DbVisualizer]을(를) [!DNL Query Service]에 연결 {#connect-dbvisualizer}

이 문서에서는 [!DNL DbVisualizer] 데이터베이스 도구를 Adobe Experience Platform [!DNL Query Service]과(와) 연결하는 단계를 다룹니다.

## 시작하기

이 안내서를 사용하려면 이미 [!DNL DbVisualizer] 데스크톱 앱에 액세스할 수 있어야 하며 해당 인터페이스를 탐색하는 방법에 익숙해야 합니다. [!DNL DbVisualizer] 데스크톱 앱을 다운로드하거나 자세한 내용은 [공식 [!DNL DbVisualizer] 설명서](https://www.dbvis.com/download/)를 참조하세요.

[!DNL  DbVisualizer]을(를) Experience Platform에 연결하는 데 필요한 자격 증명을 획득하려면 Experience Platform UI에서 쿼리 작업 영역에 액세스할 수 있어야 합니다. 현재 쿼리 작업 영역에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오.

## 데이터베이스 연결 만들기 {#connect-database}

로컬 컴퓨터에 데스크톱 앱을 설치했으면 공식 BDVisualizer 지침에 따라 [새 데이터베이스 연결을 만듭니다](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

[!DNL Connections] 목록에서 **[!DNL PostgreSQL]**&#x200B;을(를) 선택하면 새 [!DNL PostgreSQL] 연결에 대한 [!DNL Object View] 탭이 나타납니다.

### 연결에 대한 드라이버 속성 설정 {#properties}

[!DNL PostgreSQL] 개체 보기 탭에서 **[!DNL Properties]** 탭을 선택한 후 탐색 사이드바에서 **[!DNL Driver Properties]**&#x200B;을(를) 선택합니다. [드라이버 속성](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties)에 대한 자세한 내용은 공식 문서에서 확인할 수 있습니다.

그런 다음 아래 표에 설명된 드라이버 속성을 입력합니다.

>[!IMPORTANT]
>
>DBVisualizer를 Adobe Experience Platform과 연결하려면 SSL을 사용하도록 설정해야 합니다. Adobe Experience Platform 쿼리 서비스에 대한 서드파티 연결에 대한 SSL 지원 및 `verify-full` SSL 모드를 사용하여 연결하는 방법에 대한 자세한 내용은 [SSL 모드 설명서](./ssl-modes.md)를 참조하세요.

| 속성 | 설명 |
| ------ | ------ |
| `PGHOST` | [!DNL PostgreSQL] 서버의 호스트 이름입니다. 이 값은 Experience Platform **[!UICONTROL 호스트] 자격 증명**&#x200B;입니다. |
| `ssl` | SSL 사용을 활성화하려면 SSL 값 `1`을(를) 정의합니다. |
| `sslmode` | SSL 보호 수준을 제어합니다. Adobe Experience Platform에 타사 클라이언트를 연결할 때는 `require` SSL 모드를 사용하는 것이 좋습니다. `require` 모드를 사용하면 모든 통신에 암호화가 필요하며 네트워크가 올바른 서버에 연결할 수 있도록 신뢰할 수 있습니다. 서버 SSL 인증서 유효성 검사가 필요하지 않습니다. |
| `user` | 데이터베이스에 연결된 사용자 이름은 조직 ID입니다. `@Adobe.Org`(으)로 끝나는 영숫자 문자열입니다. 이 값은 Experience Platform **[!UICONTROL 사용자 이름] 자격 증명**&#x200B;입니다. |

검색 창을 사용하여 각 속성을 찾은 다음 매개 변수 값에 해당하는 셀을 선택합니다. 셀이 파란색으로 강조 표시됩니다. 값 필드에 Experience Platform 자격 증명을 입력하고 **[!DNL Apply]**&#x200B;을(를) 선택하여 드라이버 속성을 추가합니다.

>[!NOTE]
>
>두 번째 `user` 프로필을 추가하려면 매개 변수 열에서 `user`을(를) 선택한 다음 파란색 + (더하기) 아이콘을 선택하여 각 사용자의 자격 증명을 추가합니다. 드라이버 속성을 추가하려면 **[!DNL Apply]**&#x200B;을(를) 선택하십시오.

[!DNL Edited] 열에는 매개 변수 값이 업데이트되었음을 나타내는 확인 표시가 표시됩니다.

### 쿼리 서비스 자격 증명 입력 {#query-service-credentials}

쿼리 서비스에 BBVisualizer를 연결하는 데 필요한 자격 증명을 찾으려면 Experience Platform UI에 로그인하고 왼쪽 탐색에서 **[!UICONTROL 쿼리]**&#x200B;를 선택한 다음 **[!UICONTROL 자격 증명]**&#x200B;을 선택하십시오. **호스트**, **포트**, **데이터베이스**, **사용자 이름** 및 **암호** 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오.

![자격 증명과 만료 자격 증명이 강조 표시된 Experience Platform 쿼리 작업 영역의 자격 증명 페이지입니다.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service]은(는) 타사 클라이언트와의 일회성 설정을 허용하기 위해 만료되지 않는 자격 증명도 제공합니다. 만료되지 않는 자격 증명을 생성하고 사용하는 방법에 대한 [전체 지침](../ui/credentials.md#non-expiring-credentials)에 대해서는 설명서를 참조하십시오. BDVisualizer를 1회 설정으로 연결하려면 이 프로세스를 완료해야 합니다. 획득한 `credential` 및 `technicalAccountId` 값은 DBVisualizer `password` 매개 변수의 값을 구성합니다.

## 인증 {#authentication}

연결을 설정할 때마다 사용자 ID 및 암호 기반 인증을 요구하려면 [!DNL Properties] 탭으로 이동하여 [!DNL PostgreSQL] 아래의 탐색 사이드바에서 **[!DNL Authentication]**&#x200B;을(를) 선택하십시오.

연결 인증 패널에서 **[!DNL Require Userid]** 및 **[!DNL Require Password]** 확인란을 모두 선택한 다음 **[!DNL Apply]**&#x200B;을(를) 선택합니다. [인증 옵션 설정](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options)에 대한 자세한 내용은 공식 문서에서 확인할 수 있습니다.

## Experience Platform에 연결

만료되거나 만료되지 않는 자격 증명을 사용하여 연결할 수 있습니다. 연결하려면 [!DNL PostgreSQL] 개체 보기 탭에서 **[!DNL Connection]** 탭을 선택하고 다음 설정에 대한 Experience Platform 자격 증명을 입력하십시오. [수동 연결 설정](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually)에 대한 보완 지침은 공식 DBVisualizer 웹 사이트에서 사용할 수 있습니다.

>[!NOTE]
>
>아래 표에서 BDVisualizer에 필요한 모든 자격 증명은 매개 변수 설명에 명시되지 않는 한 만료 자격 증명과 만료되지 않는 자격 증명에 대해 동일합니다.

| 연결 매개 변수 | 설명 |
|---|---|
| **[!UICONTROL 이름]** | 연결의 이름을 만듭니다. 연결을 인식하기 위해 친숙한 이름을 제공하는 것이 좋습니다. |
| **[!UICONTROL 데이터베이스 서버]** | Experience Platform **[!UICONTROL 호스트]** 자격 증명입니다. |
| **[!UICONTROL 데이터베이스 포트]** | [!DNL Query Service]에 대한 포트입니다. [!DNL Query Service]에 연결하려면 **80** 또는 **5432** 포트를 사용해야 합니다. |
| **[!UICONTROL 데이터베이스]** | Experience Platform **[!UICONTROL 데이터베이스]** 자격 증명 값 사용: `prod:all`. |
| **[!UICONTROL 데이터베이스 사용자 ID]** | Experience Platform 조직 ID입니다. Experience Platform **[!UICONTROL 사용자 이름]** 자격 증명 값을 사용하십시오. ID는 `ORG_ID@AdobeOrg` 형식입니다. |
| **[!UICONTROL 데이터베이스 암호]** | 이 영숫자 문자열은 Experience Platform **[!UICONTROL 암호]** 자격 증명입니다. 만료되지 않는 자격 증명을 사용하려면 이 값은 구성 JSON 파일에서 다운로드한 `technicalAccountID` 및 `credential`에서 연결된 인수입니다. 암호 값은 {technicalAccountId}:{credential} 형식을 사용합니다. 만료되지 않는 자격 증명에 대한 구성 JSON 파일은 초기화 중에 Adobe이 복사본을 보관하지 않는 한 번 다운로드됩니다. |

모든 관련 자격 증명을 입력한 후 **[!DNL Connect]**&#x200B;을(를) 선택합니다.

[!DNL Connect] 대화 상자가 첫 번째 세션에 나타납니다. 사용자 ID와 암호를 입력하고 **[!DNL Connect]**&#x200B;을(를) 선택하십시오. 성공적인 연결을 확인하는 메시지가 로그에 나타납니다.

## 다음 단계

[!DNL DbVisualizer]을(를) [!DNL Query Service]과(와) 연결했으므로 [!DNL DbVisualizer]을(를) 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행에 대한 안내서](../best-practices/writing-queries.md)를 참조하십시오.
