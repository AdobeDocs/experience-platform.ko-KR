---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;리포티코;포스티코;쿼리 서비스에 연결
solution: Experience Platform
title: 쿼리 서비스에 Postico 연결
description: 이 문서에는 Adobe Experience Platform Query Service용 백업 클라이언트 Postico를 설치하기 위한 링크가 포함되어 있습니다.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Connect [!DNL Postico] to 쿼리 서비스(Mac)

이 문서에서는 연결 단계를 설명합니다 [!DNL Postico] Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Postico] 및 은 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 에 대한 추가 정보 [!DNL Postico] 은 [공식 [!DNL Postico] 설명서](https://eggerapps.at/postico/docs).
> 
> 또한, [!DNL Postico] is **전용** macOS 장치에서 사용할 수 있습니다.

연결하려면 [!DNL Postico] Query Service를 실행하려면 [!DNL Postico] 을(를) 선택합니다. **[!DNL New Favorite]**. 연결 설정에 대한 대화 상자가 나타납니다. 여기에서 Adobe Experience Platform과 연결할 매개 변수 값을 입력할 수 있습니다. 아래에 나열된 연결 설정을 입력합니다. 방법에 대한 지침 [Postchico를 사용하여 PostgreSQL 서버에 연결](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) 공식 포스티코 웹 사이트에서도 이용 가능합니다.

| 연결 매개 변수 | 설명 |
|---|---|
| **[!DNL Host]:** | PostgreSQL 서버의 호스트 이름입니다. |
| **[!DNL Port]:** | 포트 [!DNL Query Service]. 포트를 사용해야 합니다. **80** 또는 **5432년** 연결 [!DNL Query Service]. |
| **[!DNL User]** | 특정 연결의 이름을 만듭니다. Mac 로그인 이름을 사용하려면 필드를 비워 둡니다. |
| **[!DNL Password]** | 이 영숫자 문자열은 Experience Platform입니다 **[!UICONTROL 암호]** 자격 증명. 만료되지 않은 자격 증명을 사용하려면 이 값이 `technicalAccountID` 그리고 `credential` 구성 JSON 파일에서 다운로드되었습니다. 암호 값은 다음 형식을 사용합니다. {technicalAccountId}:{credential}. 만료되지 않은 자격 증명을 위한 구성 JSON 파일은 Adobe이 복사본을 보존하지 않는 초기화 중에 일회성 다운로드입니다. |
| **[!DNL Database]** | Experience Platform 사용 **[!UICONTROL 데이터베이스]** 자격 증명 값: `prod:all`. |

데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md). 자격 증명을 찾으려면 [!DNL Platform]를 선택하고 을 선택합니다. **[!UICONTROL 쿼리]**, 그 다음 **[!UICONTROL 자격 증명]**.

자격 증명을 삽입한 후 **[!DNL Connect]** 쿼리 서비스와 연결하기 위해

Platform에 연결하면 Query Service에서 이전에 수행한 모든 관계 목록을 볼 수 있습니다.

## SQL 문 만들기

새 SQL 쿼리를 만들려면 **[!DNL SQL Query]** 사이드바에서 또는 키보드 단축키 (⇧ ⌘ T)를 사용하여 쿼리 보기로 이동하고 실행할 쿼리를 입력합니다. 완료되면 을 선택합니다 **[!DNL Execute Statement]** 쿼리를 실행하려면 완료된 쿼리 실행 결과가 포함된 테이블이 나타납니다.

자세한 내용은 공식 포스티코 문서 를 참조하십시오 [쿼리 보기 사용](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## 다음 단계

이제 [!DNL Query Service], 다음 사용 가능 [!DNL Postico] 쿼리를 작성하려면 다음을 수행하십시오. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md).
