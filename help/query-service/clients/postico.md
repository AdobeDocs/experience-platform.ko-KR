---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;리포티코;포스티코;쿼리 서비스에 연결
solution: Experience Platform
title: 쿼리 서비스에 Postico 연결
topic-legacy: connect
description: 이 문서에는 Adobe Experience Platform Query Service용 백업 클라이언트 Postico를 설치하기 위한 링크가 포함되어 있습니다.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Connect [!DNL Postico] to 쿼리 서비스(Mac)

이 문서에서는 연결 단계를 설명합니다 [!DNL Postico] Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Postico] 및 은 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 에 대한 추가 정보 [!DNL Postico] 은 [공식 [!DNL Postico] 설명서](https://eggerapps.at/postico/docs).
> 
> 또한, [!DNL Postico] is **전용** macOS 장치에서 사용할 수 있습니다.

연결하려면 [!DNL Postico] Query Service를 실행하려면 [!DNL Postico] 을(를) 선택합니다. **[!DNL New Favorite]**.

![다음 [!DNL Postico] 새 즐겨찾기 가 강조 표시된 UI](../images/clients/postico/open-postico.png)

이제 Adobe Experience Platform에 연결할 값을 입력할 수 있습니다.

데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md). 자격 증명을 찾으려면 [!DNL Platform]를 선택하고 을 선택합니다. **[!UICONTROL 쿼리]**, 그 다음 **[!UICONTROL 자격 증명]**.

자격 증명을 삽입한 후 **[!DNL Connect]** 쿼리 서비스와 연결하기 위해

![연결이 강조 표시된 새 즐겨찾기 대화 상자](../images/clients/postico/authentication-details.png)

Platform에 연결하면 Query Service에서 이전에 수행한 모든 관계 목록을 볼 수 있습니다.

![의 연결 목록 [!DNL Postico] UI.](../images/clients/postico/show-queries.png)

## SQL 문 만들기

새 SQL 쿼리를 만들려면 &quot;SQL 쿼리&quot;를 선택하고 엽니다.

![다음 [!DNL Postico] SQL 쿼리 바로 가기가 강조 표시된 UI](../images/clients/postico/create-query.png)

상자가 나타나고 여기에서 실행할 쿼리를 입력할 수 있습니다. 완료되면 을 선택합니다 **[!DNL Execute Statement]** 쿼리를 실행하려면

![실행 문이 강조 표시된 SQL 편집기](../images/clients/postico/run-statement.png)

완료된 쿼리 실행 결과를 보여주는 테이블이 나타납니다.

![예제 쿼리의 결과 테이블.](../images/clients/postico/query-results.png)

## 다음 단계

이제 [!DNL Query Service], 다음 사용 가능 [!DNL Postico] 쿼리를 작성하려면 다음을 수행하십시오. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
