---
keywords: Experience Platform;홈;자주 찾는 항목;tableau;Tableau;쿼리 서비스;쿼리 서비스;쿼리 서비스에 연결;
solution: Experience Platform
title: 쿼리 서비스에 타블로 연결
description: 이 문서에서는 Tableau를 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 안내합니다.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL Tableau] 연결

이 문서에서는 [!DNL Tableau]을(를) Adobe Experience Platform [!DNL Query Service]과(와) 연결하는 방법에 대한 정보를 제공합니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Tableau]에 액세스할 수 있고 해당 인터페이스를 탐색하는 방법을 잘 알고 있다고 가정합니다. [!DNL Tableau]에 대한 자세한 내용은 [공식 [!DNL Tableau] 설명서](https://help.tableau.com/current/pro/desktop/en-us/default.htm)에서 확인할 수 있습니다.

[Tableau를 사용하여 PostgreSQL 서버에 연결](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm)하는 방법에 대한 지침은 공식 Tableau 웹 사이트에서 제공됩니다. 연결 설정 대화 상자가 나타나면 매개 변수 필드에 Experience Platform 자격 증명을 입력하여 Adobe Experience Platform에 연결합니다. 필수 연결 매개 변수 목록이 아래에 나와 있습니다.

| 연결 매개 변수 | 설명 |
|---|---|
| **[!DNL Server]** | SFTP 저장소 위치의 주소입니다. Experience Platform **[!UICONTROL Host]** 자격 증명의 값을 사용하십시오. |
| **[!DNL Port]:** | [!DNL Query Service]에 대한 포트입니다. [!DNL Query Service]에 연결하려면 **80** 또는 **5432** 포트를 사용해야 합니다. |
| **[!DNL Database]** | 액세스하려는 데이터베이스입니다. Experience Platform **[!UICONTROL 데이터베이스]** 자격 증명의 값을 사용합니다. `prod:all`. |
| **[!DNL Authentication]:** | 사용자 ID를 증명하는 선택한 방법입니다. 드롭다운 메뉴의 사용 가능한 옵션에서 [!DNL Username and Password]을(를) 선택하는 것이 좋습니다. |
| **[!DNL Username]** | Experience Platform 조직 ID입니다. Experience Platform **[!UICONTROL 사용자 이름]** 자격 증명의 값을 사용하십시오. ID는 `ORG_ID@AdobeOrg` 형식입니다. |
| **[!DNL Password]** | 이 영숫자 문자열은 Experience Platform **[!UICONTROL 암호]** 자격 증명입니다. 만료되지 않는 자격 증명을 사용하려면 이 값은 구성 JSON 파일에서 다운로드한 `technicalAccountID` 및 `credential`에서 연결된 인수입니다. 암호 값은 {technicalAccountId}:{credential} 형식을 사용합니다. 만료되지 않는 자격 증명에 대한 구성 JSON 파일은 초기화 중에 Adobe이 복사본을 보관하지 않는 한 번 다운로드됩니다. |

사용자 이름, 암호 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오. 자격 증명을 찾으려면 [!DNL Experience Platform]에 로그인한 다음 **[!UICONTROL 쿼리]**, **[!UICONTROL 자격 증명]**&#x200B;을 선택하십시오.

>[!IMPORTANT]
>
>Tableau 또는 Power BI 사용자는 쿼리 서비스 자격 증명 탭에서 Customer Journey Analytics을 BI 도구에 연결할 수 있습니다. [BI 도구를 Customer Journey Analytics에 연결](../ui/credentials.md#connect-to-customer-journey-analytics)하는 방법에 대한 지침은 자격 증명 설명서를 참조하세요.

연결을 시도하기 전에 **[!UICONTROL SSL 필요]** 상자를 선택했는지 확인하십시오. Adobe Experience Platform 쿼리 서비스에 대한 서드파티 연결에 대한 SSL 지원에 대한 자세한 내용은 [SSL 모드 설명서](./ssl-modes.md)를 참조하세요.

>[!IMPORTANT]
>
>타사 BI 도구의 중첩된 데이터 구조를 병합하여 사용성을 개선하고 데이터를 검색, 분석, 변환 및 보고하는 데 필요한 워크로드를 줄일 수 있습니다. 데이터베이스에 연결할 때 이 설정을 활성화하는 방법에 대한 지침은 [`FLATTEN` 기능](../key-concepts/flatten-nested-data.md)에 대한 설명서를 참조하십시오.

모든 자격 증명을 입력한 후 설정을 확인하여 계속하십시오. 이제 Adobe Experience Platform에 연결되었습니다.

## 다음 단계

[!DNL Query Service]에 연결되었으므로 [!DNL Tableau]을(를) 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md)에 대한 안내서를 참조하십시오.
