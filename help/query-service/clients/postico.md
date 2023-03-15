---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;위치;위치;Postico;쿼리 서비스에 연결;
solution: Experience Platform
title: Postico를 Query Service에 연결
description: 이 문서에는 Adobe Experience Platform 쿼리 서비스용 백업 클라이언트 Postico를 설치하기 위한 링크가 포함되어 있습니다.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# 연결 [!DNL Postico] 쿼리 서비스(Mac)로

이 문서에서는 다음 연결 단계를 다룹니다 [!DNL Postico] Adobe Experience Platform 사용 [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 이미 다음에 대한 액세스 권한이 있다고 가정합니다. [!DNL Postico] 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 다음에 대한 추가 정보: [!DNL Postico] 에서 찾을 수 있음 [공식 [!DNL Postico] 설명서](https://eggerapps.at/postico/docs).
> 
> 또한, [!DNL Postico] 은(는) **전용** macOS 디바이스에서 사용할 수 있습니다.

연결하려면 [!DNL Postico] Query Service를 열려면 를 엽니다. [!DNL Postico] 및 선택 **[!DNL New Favorite]**. 연결 설정 대화 상자가 나타납니다. 여기에서 Adobe Experience Platform에 연결할 매개 변수 값을 입력할 수 있습니다. 아래 나열된 연결 설정을 입력하십시오. 방법 지침 [posttico를 사용하여 PostgreSQL 서버에 연결](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) 공식 Postico 웹사이트에서도 구할 수 있다.

| 연결 매개 변수 | 설명 |
|---|---|
| **[!DNL Host]:** | PostgreSQL 서버의 호스트 이름입니다. |
| **[!DNL Port]:** | 의 포트 [!DNL Query Service]. 포트를 사용해야 합니다. **80** 또는 **5432** 연결 대상 [!DNL Query Service]. |
| **[!DNL User]** | 특정 연결의 이름을 만듭니다. Mac 로그인 이름을 사용하려면 필드를 비워 둡니다. |
| **[!DNL Password]** | 이 영숫자 문자열은 Experience Platform입니다. **[!UICONTROL 암호]** 자격 증명. 만료되지 않는 자격 증명을 사용하려는 경우 이 값은 `technicalAccountID` 및 `credential` 구성 JSON 파일에서 다운로드되었습니다. 암호 값은 {technicalAccountId}:{credential} 형식을 사용합니다. 만료되지 않는 자격 증명에 대한 구성 JSON 파일은 초기화 중에 Adobe이 복사본을 보관하지 않는 한 번 다운로드됩니다. |
| **[!DNL Database]** | Experience Platform 사용 **[!UICONTROL 데이터베이스]** 자격 증명 값: `prod:all`. |

데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md). 자격 증명을 찾으려면 다음 위치에 로그인합니다. [!DNL Platform]을 선택한 다음 을 선택합니다. **[!UICONTROL 쿼리]**, 그 다음 **[!UICONTROL 자격 증명]**.

자격 증명을 삽입한 후 을(를) 선택합니다 **[!DNL Connect]** 쿼리 서비스에 연결합니다.

Platform에 연결하면 이전에 Query Service와 맺은 모든 관계의 목록을 볼 수 있습니다.

## SQL 문 만들기

새 SQL 쿼리를 생성하려면 다음을 선택합니다. **[!DNL SQL Query]** 사이드바에서. 또는 키보드 단축키(⇧⌘T)를 사용하여 쿼리 보기로 이동하고 실행할 쿼리를 입력합니다. 완료되면 다음을 선택합니다. **[!DNL Execute Statement]** 쿼리를 실행합니다. 완료된 쿼리 실행 결과가 포함된 테이블이 나타납니다.

에 대한 자세한 내용은 공식 Postico 설명서 를 참조하십시오. [쿼리 보기 사용](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## 다음 단계

이제 을(를) 연결했습니다. [!DNL Query Service], 다음을 사용할 수 있습니다 [!DNL Postico] 쿼리를 작성합니다. 쿼리 작성 및 실행 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
