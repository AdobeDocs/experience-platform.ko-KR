---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;리포티코;포스티코;쿼리 서비스에 연결
solution: Experience Platform
title: 쿼리 서비스에 Postico 연결
topic-legacy: connect
description: 이 문서에는 Adobe Experience Platform Query Service용 백업 클라이언트 Postico를 설치하기 위한 링크가 포함되어 있습니다.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# [!DNL Postico]을 쿼리 서비스에 연결(Mac)

이 문서에서는 [!DNL Postico]과 Adobe Experience Platform [!DNL Query Service]을 연결하는 단계를 설명합니다.

>[!NOTE]
>
> 이 안내서에서는 이미 [!DNL Postico]에 액세스할 수 있고 인터페이스를 탐색하는 방법을 잘 알고 있다고 가정합니다. [!DNL Postico]에 대한 자세한 내용은 [공식 [!DNL Postico] 설명서](https://eggerapps.at/postico/docs)에서 확인할 수 있습니다.
> 
> 또한 [!DNL Postico]은 **macOS 장치에서 사용할 수 있는**&#x200B;뿐입니다.

[!DNL Postico]을 쿼리 서비스에 연결하려면 [!DNL Postico]을(를) 열고 **[!DNL New Favorite]**&#x200B;를 선택합니다.

![](../images/clients/postico/open-postico.png)

이제 Adobe Experience Platform에 연결할 값을 입력할 수 있습니다.

데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인한 다음 **[!UICONTROL 쿼리]**, 자격 증명&#x200B;]**을 차례로 선택하십시오.**[!UICONTROL 

자격 증명을 삽입한 후 **[!DNL Connect]**&#x200B;을 선택하여 쿼리 서비스와 연결합니다.

![](../images/clients/postico/authentication-details.png)

Platform에 연결하면 Query Service에서 이전에 수행한 모든 관계 목록을 볼 수 있습니다.

![](../images/clients/postico/show-queries.png)

## SQL 문 만들기

새 SQL 쿼리를 만들려면 &quot;SQL 쿼리&quot;를 선택하고 엽니다.

![](../images/clients/postico/create-query.png)

상자가 나타나고 여기에서 실행할 쿼리를 입력할 수 있습니다. 완료되면 **[!DNL Execute Statement]** 을 선택하여 쿼리를 실행합니다.

![](../images/clients/postico/run-statement.png)

완료된 쿼리 실행 결과를 보여주는 테이블이 나타납니다.

![](../images/clients/postico/query-results.png)

## 다음 단계

이제 [!DNL Query Service]과 연결되었으므로 [!DNL Postico]을 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md)를 참조하십시오.
