---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;위치;위치;Postico;쿼리 서비스에 연결;
solution: Experience Platform
title: Postico를 Query Service에 연결
description: 이 문서에는 Adobe Experience Platform 쿼리 서비스용 백업 클라이언트 Postico를 설치하기 위한 링크가 포함되어 있습니다.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL Postico] 연결(Mac)

이 문서에서는 [!DNL Postico]을(를) Adobe Experience Platform [!DNL Query Service]과(와) 연결하는 단계를 다룹니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Postico]에 액세스할 수 있고 해당 인터페이스를 탐색하는 방법을 잘 알고 있다고 가정합니다. [!DNL Postico]에 대한 자세한 내용은 [공식 [!DNL Postico] 설명서](https://eggerapps.at/postico/docs)에서 확인할 수 있습니다.
> 
> 또한 [!DNL Postico]은(는) macOS 장치에서 **만**&#x200B;할 수 있습니다.

쿼리 서비스에 [!DNL Postico]을(를) 연결하려면 [!DNL Postico]을(를) 열고 **[!DNL New Favorite]**&#x200B;을(를) 선택하십시오. 연결 설정 대화 상자가 나타납니다. 여기에서 Adobe Experience Platform에 연결할 매개 변수 값을 입력할 수 있습니다. 아래 나열된 연결 설정을 입력하십시오. [PostgreSQL 서버에 Posttico로 연결](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html)하는 방법에 대한 지침은 공식 Posttico 웹 사이트에서도 제공됩니다.

| 연결 매개 변수 | 설명 |
|---|---|
| **[!DNL Host]:** | PostgreSQL 서버의 호스트 이름입니다. |
| **[!DNL Port]:** | [!DNL Query Service]에 대한 포트입니다. [!DNL Query Service]에 연결하려면 **80** 또는 **5432** 포트를 사용해야 합니다. |
| **[!DNL User]** | 특정 연결의 이름을 만듭니다. Mac 로그인 이름을 사용하려면 필드를 비워 둡니다. |
| **[!DNL Password]** | 이 영숫자 문자열은 Experience Platform **[!UICONTROL 암호]** 자격 증명입니다. 만료되지 않는 자격 증명을 사용하려면 이 값은 구성 JSON 파일에서 다운로드한 `technicalAccountID` 및 `credential`에서 연결된 인수입니다. 암호 값은 {technicalAccountId}:{credential} 형식을 사용합니다. 만료되지 않는 자격 증명에 대한 구성 JSON 파일은 초기화 중에 Adobe이 복사본을 보관하지 않는 한 번 다운로드됩니다. |
| **[!DNL Database]** | Experience Platform **[!UICONTROL 데이터베이스]** 자격 증명 값 사용: `prod:all`. |

데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오. 자격 증명을 찾으려면 [!DNL Experience Platform]에 로그인한 다음 **[!UICONTROL 쿼리]**, **[!UICONTROL 자격 증명]**&#x200B;을 선택하십시오.

자격 증명을 삽입한 후 **[!DNL Connect]**&#x200B;을(를) 선택하여 쿼리 서비스에 연결합니다.

Experience Platform에 연결하면 이전에 쿼리 서비스와 만든 모든 관계의 목록을 볼 수 있습니다.

## SQL 문 만들기

새 SQL 쿼리를 만들려면 사이드바에서 **[!DNL SQL Query]**&#x200B;을(를) 선택하십시오. 또는 키보드 단축키(⇧⌘T)를 사용하여 쿼리 보기로 이동하고 실행할 쿼리를 입력합니다. 완료되면 **[!DNL Execute Statement]**&#x200B;을(를) 선택하여 쿼리를 실행합니다. 완료된 쿼리 실행 결과가 포함된 테이블이 나타납니다.

[쿼리 보기 사용](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html)에 대한 자세한 내용은 공식 Postico 설명서를 참조하십시오.

## 다음 단계

[!DNL Query Service]에 연결되었으므로 [!DNL Postico]을(를) 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 가이드](../best-practices/writing-queries.md)를 참조하십시오.
