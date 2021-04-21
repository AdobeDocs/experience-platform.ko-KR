---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;포스트티코;쿼리 서비스에 연결;;home;popular topics service;query service;positico;connect to query service;
solution: Experience Platform
title: 쿼리 서비스에 보스티코 연결
topic-legacy: connect
description: 이 문서에는 Adobe Experience Platform Query Service용 백업 클라이언트 포스트티코를 설치하는 링크가 포함되어 있습니다.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL Postico] 연결(Mac)

이 문서에서는 [!DNL Postico]과(와) Adobe Experience Platform [!DNL Query Service]을(를) 연결하는 단계를 다룹니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Postico]에 액세스할 수 있으며 인터페이스를 탐색하는 방법에 익숙하다고 가정합니다. [!DNL Postico]에 대한 자세한 내용은 [공식 [!DNL Postico] 설명서](https://eggerapps.at/postico/docs)에서 확인할 수 있습니다.
> 
> 또한 [!DNL Postico]은(는) macOS 장치에서 **만 사용할 수 있습니다.**

[!DNL Postico]을(를) 쿼리 서비스에 연결하려면 [!DNL Postico]을(를) 열고 **[!DNL New Favorite]**&#x200B;를 선택합니다.

![](../images/clients/postico/open-postico.png)

이제 Adobe Experience Platform에 연결할 값을 입력할 수 있습니다.

데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 플랫폼](https://platform.adobe.com/query/configuration)의 [자격 증명 페이지를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인한 다음 **[!UICONTROL Queries]** 뒤에 **[!UICONTROL Credentials]**&#x200B;를 선택합니다.

자격 증명을 삽입한 후 **[!DNL Connect]**&#x200B;을 선택하여 쿼리 서비스에 연결합니다.

![](../images/clients/postico/authentication-details.png)

플랫폼에 연결한 후에는 쿼리 서비스로 이전에 만들어진 모든 관계 목록을 볼 수 있습니다.

![](../images/clients/postico/show-queries.png)

## SQL 문 만들기

새 SQL 쿼리를 만들려면 &quot;SQL 쿼리&quot;를 선택하고 엽니다.

![](../images/clients/postico/create-query.png)

상자가 나타나고 여기에서 실행하려는 쿼리를 입력할 수 있습니다. 완료되면 **[!DNL Execute Statement]**&#x200B;을 선택하여 쿼리를 실행합니다.

![](../images/clients/postico/run-statement.png)

완료된 쿼리 실행 결과를 보여주는 테이블이 나타납니다.

![](../images/clients/postico/query-results.png)

## 다음 단계

이제 [!DNL Query Service]에 연결되었으므로 [!DNL Postico]를 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md)를 참조하십시오.
