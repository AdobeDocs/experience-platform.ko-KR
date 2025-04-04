---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;룩커;룩커;쿼리 서비스에 연결;
solution: Experience Platform
title: Query Service에 Loker 연결
description: 이 문서에서는 Looker를 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 안내합니다.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL Looker] 연결

이 문서에서는 [!DNL Looker]을(를) Adobe Experience Platform [!DNL Query Service]과(와) 연결하는 단계를 다룹니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Looker]에 액세스할 수 있고 해당 인터페이스를 탐색하는 방법을 잘 알고 있다고 가정합니다. [!DNL Looker]에 대한 자세한 내용은 [공식 [!DNL Looker] 설명서](https://docs.looker.com/)에서 확인할 수 있습니다.

## 새 데이터베이스 연결 만들기 {#create-connection}

[!DNL Looker]에 로그인한 후 **[!DNL Admin]**&#x200B;을(를) 선택한 후 **[!DNL Connections]**&#x200B;을(를) 선택합니다. [!DNL Connections] 페이지가 열립니다. [!DNL Connections] 페이지에서 **[!DNL Add Connection]**&#x200B;을(를) 선택합니다.

여기에서 아래에 나열된 연결 설정에 대한 세부 정보를 입력합니다. 새 데이터베이스 연결을 만드는 지침 [사용 가능한 속성에 대한 설명](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection)은 공식 Looker 설명서를 참조하십시오.

- **[!DNL Name]:** 연결 이름입니다.
- **[!DNL Dialect]:** SQL 데이터베이스에 사용되는 언어. [!DNL Query Service]이(가) **[!DNL PostgreSQL]**&#x200B;을(를) 사용합니다.
- **[!DNL Host and Port]:** [!DNL Query Service]에 대한 호스트 끝점 및 해당 포트입니다.
- **[!DNL Database]:** 사용할 데이터베이스입니다.
- **[!DNL Username and Password]:** 사용할 로그인 자격 증명입니다. 사용자 이름은 `ORG_ID@AdobeOrg` 형식입니다.
- **SSL**: SSL을 사용하도록 설정하여 네트워크에서 보안 연결을 보장합니다.

쿼리 서비스와 Looker에 연결하는 데 필요한 자격 증명을 찾으려면 Experience Platform UI에 로그인하고 왼쪽 탐색에서 **[!UICONTROL 쿼리]**&#x200B;를 선택한 다음 **[!UICONTROL 자격 증명]**&#x200B;을 선택합니다. **호스트**, **포트**, **데이터베이스**, **사용자 이름** 및 **암호** 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오.

![자격 증명과 만료 자격 증명이 강조 표시된 Experience Platform 쿼리 작업 영역의 자격 증명 페이지입니다.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service]은(는) 타사 클라이언트와의 일회성 설정을 허용하기 위해 만료되지 않는 자격 증명도 제공합니다. 만료되지 않는 자격 증명을 생성하고 사용하는 방법에 대한 [전체 지침](../ui/credentials.md#non-expiring-credentials)에 대해서는 설명서를 참조하십시오. Looker를 1회 설정으로 연결하려면 이 프로세스를 완료해야 합니다. 획득한 `credential` 및 `technicalAccountId` 값은 Looker `password` 매개 변수의 값을 구성합니다.

Adobe Experience Platform의 타사 연결에 대한 SSL 지원에 대한 자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md)를 참조하세요. 이 문서에서는 `verify-full` SSL 모드를 사용하여 연결하는 방법에 대한 지침을 제공합니다.

연결 세부 정보를 입력한 후 **[!DNL Test These Settings]**&#x200B;을(를) 선택하여 자격 증명이 제대로 작동하는지 확인하십시오. [연결 설정 테스트](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings)에 대한 자세한 내용은 공식 Looker 설명서를 참조하십시오. 연결에 성공하면 연결할 수 있다는 메시지가 화면에 나타납니다. 연결이 성공하면 **[!DNL Add Connection]**&#x200B;을(를) 선택하여 연결을 만듭니다.

## 다음 단계

[!DNL Query Service]에 연결되었으므로 [!DNL Looker]을(를) 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 가이드](../best-practices/writing-queries.md)를 참조하십시오.
