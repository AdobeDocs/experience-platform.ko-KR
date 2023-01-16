---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;조회;조회;쿼리 서비스에 연결
solution: Experience Platform
title: 조회 서비스에 연결
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스와 전환 확인을 연결하는 단계를 설명합니다.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Connect [!DNL Looker] 쿼리 서비스

이 문서에서는 연결 단계를 설명합니다 [!DNL Looker] Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Looker] 및 은 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 에 대한 추가 정보 [!DNL Looker] 은 [공식 [!DNL Looker] 설명서](https://docs.looker.com/).

## 새 데이터베이스 연결 만들기 {#create-connection}

로그인한 후 [!DNL Looker], 선택 **[!DNL Admin]**, 그 다음 **[!DNL Connections]**. 다음 [!DNL Connections] 페이지가 열립니다. 설정 [!DNL Connections] 페이지를 선택하고 **[!DNL Add Connection]**.

여기에서 아래 나열된 연결 설정에 대한 세부 정보를 입력합니다. 에 대한 공식 전환 확인 설명서를 참조하십시오. [새 데이터베이스 연결을 만드는 지침 및 사용 가능한 속성에 대한 설명](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** 연결의 이름입니다.
- **[!DNL Dialect]:** SQL 데이터베이스에 사용되는 언어입니다. [!DNL Query Service] 사용 **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** 호스트 끝점 및 해당 포트 [!DNL Query Service].
- **[!DNL Database]:** 사용할 데이터베이스입니다.
- **[!DNL Username and Password]:** 사용할 로그인 자격 증명입니다. 사용자 이름은 `ORG_ID@AdobeOrg`.
- **SSL**: SSL을 활성화하여 네트워크 간 보안 연결을 확인합니다.

조회 서비스와 쿼리 서비스를 연결하는 데 필요한 자격 증명을 찾으려면 플랫폼 UI에 로그인하고 를 선택합니다 **[!UICONTROL 쿼리]** 왼쪽 탐색에서 다음을 차례로 수행합니다 **[!UICONTROL 자격 증명]**. 검색 결과에 대한 자세한 정보 **호스트**, **포트**, **데이터베이스**, **사용자 이름**, 및 **암호** 자격 증명, [자격 증명 안내서](../ui/credentials.md).

![자격 증명과 만료 자격 증명이 강조 표시된 Experience Platform 쿼리 작업 영역의 자격 증명 페이지.](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 또한 타사 클라이언트로 1회 설정할 수 있도록 만료되는 자격 증명을 제공합니다. 다음 문서를 참조하십시오. [만료되지 않은 자격 증명을 생성하고 사용하는 방법에 대한 전체 지침](../ui/credentials.md#non-expiring-credentials). 1회 설정으로 조회를 연결하려면 이 프로세스를 완료해야 합니다. 다음 `credential` 및 `technicalAccountId` 획득된 값은 Looker의 값을 포함합니다 `password` 매개 변수.

Adobe Experience Platform의 타사 연결에 대한 SSL 지원에 대해 알려면 다음을 참조하십시오. [[!DNL Query Service] SSL 설명서](./ssl-modes.md). 이 문서에서는 `verify-full` SSL 모드.

연결 세부 정보를 입력한 후 **[!DNL Test These Settings]** 자격 증명이 제대로 작동하는지 확인합니다. 추가 정보 [연결 설정 테스트](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) 는 공식 전환 확인 문서에 제공됩니다. 연결에 성공하면 연결할 수 있다는 메시지가 화면에 나타납니다. 연결이 성공하면 를 선택합니다 **[!DNL Add Connection]** 연결 만들기

## 다음 단계

이제 [!DNL Query Service], 다음 사용 가능 [!DNL Looker] 쿼리를 작성하려면 다음을 수행하십시오. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
