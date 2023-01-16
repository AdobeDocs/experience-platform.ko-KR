---
keywords: Experience Platform;홈;인기 항목;타블로;쿼리 서비스;쿼리 서비스;쿼리 서비스에 연결;
solution: Experience Platform
title: 쿼리 서비스에 타블로 연결
description: 이 문서에서는 Tableau와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 설명합니다.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 1d71cc4336747eb258ec2d8dcdc545cb2233692d
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Connect [!DNL Tableau] 쿼리 서비스

이 문서에서는 연결에 대한 정보를 제공합니다 [!DNL Tableau] Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Tableau] 및 은 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 에 대한 추가 정보 [!DNL Tableau] 은 [공식 [!DNL Tableau] 설명서](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

방법에 대한 지침 [타블로와 함께 PostgreSQL 서버에 연결](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) 공식 타블로 웹 사이트에서 이용할 수 있습니다. 연결 설정에 대한 대화 상자가 표시되면 매개 변수 필드에 Platform 자격 증명을 입력하여 Adobe Experience Platform과 연결합니다. 필요한 연결 매개 변수 목록은 아래에 나와 있습니다.

| 연결 매개 변수 | 설명 |
|---|---|
| **[!DNL Server]** | SFTP 저장소 위치의 주소입니다. Experience Platform 값 사용 **[!UICONTROL 호스트]** 자격 증명. |
| **[!DNL Port]:** | 포트 [!DNL Query Service]. 포트를 사용해야 합니다. **80** 또는 **5432년** 연결 [!DNL Query Service]. |
| **[!DNL Database]** | 액세스할 데이터베이스입니다. Experience Platform 값 사용 **[!UICONTROL 데이터베이스]** 자격 증명: `prod:all`. |
| **[!DNL Authentication]:** | 선택한 사용자 ID 인증 방법 선택하는 것이 좋습니다 [!DNL Username and Password] 드롭다운 메뉴의 사용 가능한 옵션에서 |
| **[!DNL Username]** | 플랫폼 조직 ID입니다. Experience Platform 값 사용 **[!UICONTROL 사용자 이름]** 자격 증명. ID는 `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | 이 영숫자 문자열은 Experience Platform입니다 **[!UICONTROL 암호]** 자격 증명. 만료되지 않은 자격 증명을 사용하려면 이 값이 `technicalAccountID` 그리고 `credential` 구성 JSON 파일에서 다운로드되었습니다. 암호 값은 다음 형식을 사용합니다. {technicalAccountId}:{credential}. 만료되지 않은 자격 증명을 위한 구성 JSON 파일은 Adobe이 복사본을 보존하지 않는 초기화 중에 일회성 다운로드입니다. |

사용자 이름, 암호 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md). 자격 증명을 찾으려면 [!DNL Platform]를 선택하고 을 선택합니다. **[!UICONTROL 쿼리]**, 그 다음 **[!UICONTROL 자격 증명]**.

을(를) 선택했는지 확인합니다. **[!UICONTROL SSL 필요]** 연결하기 전에 상자를 엽니다. 자세한 내용은 [SSL 모드 설명서](./ssl-modes.md) Adobe Experience Platform Query Service에 대한 타사 연결에 대한 SSL 지원에 대해 알아보십시오.

>[!IMPORTANT]
>
>타사 BI 도구의 중첩된 데이터 구조를 병합하여 사용 편의성을 향상시키고 데이터를 검색, 분석, 변환 및 보고하는 데 필요한 작업 로드를 줄일 수 있습니다. 다음 항목에 대한 설명서를 참조하십시오.[`FLATTEN` 기능](../best-practices/flatten-nested-data.md) 데이터베이스에 연결할 때 이 설정을 활성화하는 방법에 대한 지침

모든 자격 증명을 입력한 후 설정을 확인하여 계속 진행합니다. 이제 Adobe Experience Platform과 연결되었습니다.

## 다음 단계

이제 [!DNL Query Service], 다음 사용 가능 [!DNL Tableau] 쿼리를 작성하려면 다음을 수행하십시오. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md).
