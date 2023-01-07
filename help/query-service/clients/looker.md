---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;조회;조회;쿼리 서비스에 연결
solution: Experience Platform
title: 조회 서비스에 연결
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스와 전환 확인을 연결하는 단계를 설명합니다.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Connect [!DNL Looker] 쿼리 서비스

이 문서에서는 연결 단계를 설명합니다 [!DNL Looker] Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Looker] 및 은 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 에 대한 추가 정보 [!DNL Looker] 은 [공식 [!DNL Looker] 설명서](https://docs.looker.com/).

로그인한 후 [!DNL Looker], 선택 **[!DNL Admin]**, 그 다음 **[!DNL Connections]**.

![다음 [!DNL Looker] 관리 드롭다운 메뉴에서 연결 이 강조 표시된 대시보드.](../images/clients/looker/click-admin-connections.png)

이 페이지에서 **[!DNL New Connection]**.

![새 연결이 강조 표시된 연결 작업 영역입니다.](../images/clients/looker/click-new-connection.png)

여기에서 연결 설정에 대한 세부 정보를 입력할 수 있습니다.

![새 연결에 대한 연결 설정 페이지입니다.](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** 연결의 이름입니다.
- **[!DNL Dialect]:** SQL 데이터베이스에 사용되는 언어입니다. [!DNL Query Service] 사용 **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** 호스트 끝점 및 해당 포트 [!DNL Query Service].
- **[!DNL Database]:** 사용할 데이터베이스입니다.
- **[!DNL Username and Password]:** 사용할 로그인 자격 증명입니다. 사용자 이름은 `ORG_ID@AdobeOrg`.
- **SSL**: SSL을 활성화하여 네트워크 간 보안 연결을 확인합니다.

>[!IMPORTANT]
>
>자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md) Adobe Experience Platform Query Service에 대한 타사 연결에 대한 SSL 지원 및 `verify-full` SSL 모드.

호스트 및 포트, 데이터베이스 이름 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md). 자격 증명을 찾으려면 [!DNL Platform]를 선택하고 을 선택합니다. **[!UICONTROL 쿼리]**, 그 다음 **[!UICONTROL 자격 증명]**.

연결 세부 정보를 입력한 후 을 선택합니다 **[!DNL Test These Settings]** 자격 증명이 제대로 작동하는지 확인합니다. 연결된 경우 아래에 연결할 수 있다는 메시지가 표시됩니다. 연결이 실제로 성공하면 **[!DNL Add Connection]** 연결 만들기

![이 설정을 테스트하여 새 연결에 대한 연결 설정 페이지가 강조 표시되어 있습니다.](../images/clients/looker/click-test-connection.png)

## 다음 단계

이제 [!DNL Query Service], 다음 사용 가능 [!DNL Looker] 쿼리를 작성하려면 다음을 수행하십시오. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
