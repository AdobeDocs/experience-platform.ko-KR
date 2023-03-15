---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;룩커;룩커;쿼리 서비스에 연결;
solution: Experience Platform
title: Query Service에 Loker 연결
description: 이 문서에서는 Looker를 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 안내합니다.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# 연결 [!DNL Looker] 쿼리 서비스

이 문서에서는 다음 연결 단계를 다룹니다 [!DNL Looker] Adobe Experience Platform 사용 [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 이미 다음에 대한 액세스 권한이 있다고 가정합니다. [!DNL Looker] 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 다음에 대한 추가 정보: [!DNL Looker] 에서 찾을 수 있음 [공식 [!DNL Looker] 설명서](https://docs.looker.com/).

## 새 데이터베이스 연결 만들기 {#create-connection}

에 로그인한 후 [!DNL Looker], 선택 **[!DNL Admin]**, 그 다음 **[!DNL Connections]**. 다음 [!DNL Connections] 페이지가 열립니다. 다음에서 [!DNL Connections] 페이지, 선택 **[!DNL Add Connection]**.

여기에서 아래에 나열된 연결 설정에 대한 세부 정보를 입력합니다. 다음에 대한 공식 Looker 설명서 참조: [새 데이터베이스 연결을 만드는 지침 및 사용 가능한 속성에 대한 설명](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** 연결의 이름입니다.
- **[!DNL Dialect]:** SQL 데이터베이스에 사용되는 변수입니다. [!DNL Query Service] 사용 **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** 에 대한 호스트 엔드포인트 및 해당 포트 [!DNL Query Service].
- **[!DNL Database]:** 사용할 데이터베이스입니다.
- **[!DNL Username and Password]:** 사용할 로그인 자격 증명입니다. 사용자 이름은 다음 형식으로 표시됩니다. `ORG_ID@AdobeOrg`.
- **SSL**: SSL을 활성화하여 네트워크 전반에서 보안 연결을 보장합니다.

Looker를 쿼리 서비스와 연결하는 데 필요한 자격 증명을 찾으려면 플랫폼 UI에 로그인하고 을 선택합니다 **[!UICONTROL 쿼리]** 왼쪽 탐색 후 **[!UICONTROL 자격 증명]**. 을(를) 찾는 방법에 대한 자세한 내용은 **호스트**, **포트**, **데이터베이스**, **사용자 이름**, 및 **암호** 자격 증명, 다음을 읽으십시오. [자격 증명 안내서](../ui/credentials.md).

![[인증서] 및 [만료 인증서]가 강조 표시된 Experience Platform 쿼리 작업 영역의 [인증서] 페이지](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 또한 타사 클라이언트와의 1회 설정을 허용하는 만료되지 않는 자격 증명을 제공합니다. 다음 설명서를 참조하십시오. [만료되지 않는 자격 증명을 생성하고 사용하는 방법에 대한 전체 지침](../ui/credentials.md#non-expiring-credentials). Looker를 1회 설정으로 연결하려면 이 프로세스를 완료해야 합니다. 다음 `credential` 및 `technicalAccountId` 획득한 값은 Looker의 값을 구성합니다. `password` 매개 변수.

Adobe Experience Platform의 타사 연결에 대한 SSL 지원에 대한 자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md). 이 문서에서는 을 사용하여 연결하는 방법에 대한 지침을 제공합니다. `verify-full` SSL 모드.

연결 세부 정보를 입력한 후 다음을 선택합니다. **[!DNL Test These Settings]** 자격 증명이 제대로 작동하는지 확인합니다. 다음에 대한 추가 정보: [연결 설정 테스트](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) 은 공식 Looker 설명서에 제공됩니다. 연결에 성공하면 연결할 수 있다는 메시지가 화면에 나타납니다. 연결이 성공하면 을(를) 선택합니다. **[!DNL Add Connection]** 연결을 만듭니다.

## 다음 단계

이제 을(를) 연결했습니다. [!DNL Query Service], 다음을 사용할 수 있습니다 [!DNL Looker] 쿼리를 작성합니다. 쿼리 작성 및 실행 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
