---
keywords: Experience Platform;홈;자주 찾는 항목;타블로;타블로;쿼리 서비스;쿼리 서비스;쿼리 서비스에 연결;
solution: Experience Platform
title: 쿼리 서비스에 타블로 연결
description: 이 문서에서는 Tableau를 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 안내합니다.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# 연결 [!DNL Tableau] 쿼리 서비스

이 문서에서는 연결에 대한 정보를 제공합니다. [!DNL Tableau] Adobe Experience Platform 사용 [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 이미 다음에 대한 액세스 권한이 있다고 가정합니다. [!DNL Tableau] 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 다음에 대한 추가 정보: [!DNL Tableau] 에서 찾을 수 있음 [공식 [!DNL Tableau] 설명서](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

방법 지침 [tableau를 사용하여 PostgreSQL 서버에 연결](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) 공식 Tableau 웹 사이트에서 다운로드할 수 있습니다. 연결 설정 대화 상자가 나타나면 매개 변수 필드에 플랫폼 자격 증명을 입력하여 Adobe Experience Platform에 연결합니다. 필수 연결 매개 변수 목록이 아래에 나와 있습니다.

| 연결 매개 변수 | 설명 |
|---|---|
| **[!DNL Server]** | SFTP 저장소 위치의 주소입니다. Experience Platform 값 사용 **[!UICONTROL 호스트]** 자격 증명. |
| **[!DNL Port]:** | 의 포트 [!DNL Query Service]. 포트를 사용해야 합니다. **80** 또는 **5432** 연결 대상 [!DNL Query Service]. |
| **[!DNL Database]** | 액세스하려는 데이터베이스입니다. Experience Platform 값 사용 **[!UICONTROL 데이터베이스]** 자격 증명: `prod:all`. |
| **[!DNL Authentication]:** | 사용자 ID를 증명하는 선택한 방법입니다. 다음을 선택하는 것이 좋습니다. [!DNL Username and Password] 드롭다운 메뉴의 사용 가능한 옵션 |
| **[!DNL Username]** | Platform 조직 ID입니다. Experience Platform 값 사용 **[!UICONTROL 사용자 이름]** 자격 증명. ID는 다음과 같은 형식이어야 합니다. `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | 이 영숫자 문자열은 Experience Platform입니다. **[!UICONTROL 암호]** 자격 증명. 만료되지 않는 자격 증명을 사용하려는 경우 이 값은 `technicalAccountID` 및 `credential` 구성 JSON 파일에서 다운로드되었습니다. 암호 값은 다음 형식을 사용합니다. {technicalAccountId}:{credential}. 만료되지 않는 자격 증명에 대한 구성 JSON 파일은 초기화 중에 Adobe이 복사본을 보관하지 않는 한 번 다운로드됩니다. |

사용자 이름, 암호 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md). 자격 증명을 찾으려면 다음 위치에 로그인합니다. [!DNL Platform]을 선택한 다음 을 선택합니다. **[!UICONTROL 쿼리]**, 그 다음 **[!UICONTROL 자격 증명]**.

다음을 확인했는지 확인합니다. **[!UICONTROL SSL 필요]** 상자에 넣은 다음 연결합니다. 다음을 참조하십시오. [SSL 모드 설명서](./ssl-modes.md) Adobe Experience Platform 쿼리 서비스에 대한 서드파티 연결에 대한 SSL 지원에 대해 알아봅니다.

>[!IMPORTANT]
>
>타사 BI 도구의 중첩된 데이터 구조를 병합하여 사용성을 개선하고 데이터를 검색, 분석, 변환 및 보고하는 데 필요한 워크로드를 줄일 수 있습니다. 다음에서 설명서를 참조하십시오.[`FLATTEN` 기능](../key-concepts/flatten-nested-data.md) 데이터베이스에 연결할 때 이 설정을 활성화하는 방법에 대한 지침입니다.

모든 자격 증명을 입력한 후 설정을 확인하여 계속하십시오. 이제 Adobe Experience Platform에 연결되었습니다.

## 다음 단계

이제 을(를) 연결했습니다. [!DNL Query Service], 다음을 사용할 수 있습니다 [!DNL Tableau] 쿼리를 작성합니다. 쿼리 작성 및 실행 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [쿼리 실행 중](../best-practices/writing-queries.md).
