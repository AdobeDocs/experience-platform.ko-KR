---
keywords: Experience Platform;홈;인기 항목;타블로;쿼리 서비스;쿼리 서비스;쿼리 서비스에 연결;
solution: Experience Platform
title: 쿼리 서비스에 타블로 연결
description: 이 문서에서는 Tableau와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 설명합니다.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 2%

---

# Connect [!DNL Tableau] 쿼리 서비스

이 문서에서는 연결 단계를 설명합니다 [!DNL Tableau] Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Tableau] 및 은 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 에 대한 추가 정보 [!DNL Tableau] 은 [공식 [!DNL Tableau] 설명서](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

연결하려면 [!DNL Tableau] to [!DNL Query Service], 열기 [!DNL Tableau], 및에서 **[!DNL To a Server]** 섹션 선택 **[!DNL More]** 후 **[!DNL PostgreSQL]**

![다음 [!DNL Tableau] 더 보기 및 [!DNL PostgreSQL] 강조 표시되어 있습니다.](../images/clients/tableau/open-connection.png)

이제 Adobe Experience Platform에 연결할 값을 입력할 수 있습니다. 데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md). 자격 증명을 찾으려면 [!DNL Platform]를 선택하고 을 선택합니다. **[!UICONTROL 쿼리]**, 그 다음 **[!UICONTROL 자격 증명]**.

을(를) 선택했는지 확인합니다. **[!UICONTROL SSL 필요]** 연결하기 전에 상자를 엽니다.

>[!IMPORTANT]
>
>자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md) Adobe Experience Platform Query Service에 대한 타사 연결에 대한 SSL 지원 및 `verify-full` SSL 모드.

![다음 [!DNL PostgreSQL] 연결 대화 상자에 연결 세부 정보가 완료되었습니다.](../images/clients/tableau/sign-in.png)

>[!IMPORTANT]
>
>타사 BI 도구의 중첩된 데이터 구조를 병합하여 사용 편의성을 향상시키고 데이터를 검색, 분석, 변환 및 보고하는 데 필요한 작업 로드를 줄일 수 있습니다. 다음 항목에 대한 설명서를 참조하십시오.[`FLATTEN` 기능](../best-practices/flatten-nested-data.md) 데이터베이스에 연결할 때 이 설정을 활성화하는 방법에 대한 지침

모든 자격 증명을 입력한 후 **[!DNL Sign In]** 계속하십시오.

이제 Adobe Experience Platform과 연결되었으며 테이블 목록이 측면에 표시됩니다.

![새로운 [!DNL Tableau] 왼쪽 패널에 Query Service 테이블이 강조 표시된 대시보드.](../images/clients/tableau/connected.png)

## 다음 단계

이제 [!DNL Query Service], 다음 사용 가능 [!DNL Tableau] 쿼리를 작성하려면 다음을 수행하십시오. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md).
