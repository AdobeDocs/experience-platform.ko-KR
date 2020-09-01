---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Adobe Experience Platform 쿼리 서비스 UI 안내서
topic: guide
description: Adobe Experience Platform 쿼리 서비스는 쿼리를 작성 및 실행하고, 이전에 실행된 쿼리를 보고, IMS 조직 내에서 사용자가 저장한 쿼리에 액세스하는 데 사용할 수 있는 사용자 인터페이스를 제공합니다.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 2%

---


# [!DNL Query Service] 가이드

Adobe Experience Platform [!DNL Query Service] 는 IMS 조직 내에서 사용자가 저장하고 있는 쿼리를 작성 및 실행하고, 이전에 실행한 쿼리를 보고, 액세스하는 데 사용할 수 있는 사용자 인터페이스를 제공합니다. [Adobe Experience Platform][platform-ui]내의 UI에 액세스하려면 왼쪽 탐색 **[!UICONTROL 에서 [쿼리]** ]를 선택합니다.

## [!DNL Query Editor]

이 [!DNL Query Editor] 를 사용하면 외부 클라이언트를 사용하지 않고도 쿼리를 작성하고 실행할 수 있습니다. 쿼리 **[!UICONTROL 만들기를]** 클릭하여 [!DNL Query Editor] 쿼리를 열고 새 쿼리를 만듭니다. [로그] 또는 [찾아보기] 탭 [!DNL Query Editor] 에서 쿼리를 선택하여 **[!UICONTROL 에]** 액세스할 **[!UICONTROL 수도]** 있습니다. 이전에 실행되거나 저장된 쿼리를 선택하면 선택한 쿼리에 대한 SQL이 [!DNL Query Editor] 열리고 표시됩니다.

![이미지](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] 은 쿼리를 입력하기 시작할 수 있는 편집 공간을 제공합니다. 입력하면 편집기가 테이블 내의 SQL 예약어, 테이블 및 필드 이름을 자동으로 완료합니다. 쿼리 작성을 마치면 [ **재생** ] 단추를 클릭하여 쿼리를 실행합니다. 편집기 아래의 **[!UICONTROL 콘솔]** 탭에는 [!DNL Query Service] 현재 수행 중인 작업이 표시되어 쿼리가 반환된 시기를 나타냅니다. 콘솔 **[!UICONTROL 옆에 있는 결과]** 탭에 쿼리 결과가 표시됩니다. 사용 방법에 대한 자세한 내용은 [쿼리 편집기 안내서][query-editor] 를 참조하십시오 [!DNL Query Editor].

![이미지](../images/queries/ui-overview/query-editor.png)

## 찾아보기

[ **[!UICONTROL 검색]** ] 탭에는 조직의 사용자가 저장한 쿼리가 표시됩니다. 여기에 저장된 쿼리는 아직 건설 중이어서 쿼리 프로젝트로 생각하면 유용합니다. 검색 탭 **[!UICONTROL 에]** 표시된 쿼리는 이전에 **[!UICONTROL 에]** 의해 실행된 경우 로그 [!DNL Query Service]탭에 실행 쿼리로도 표시됩니다.

![이미지](../images/queries/ui-overview/browse.png)

| 열 | 설명 |
| --- | --- |
| 이름 | 사용자가 만든 쿼리 이름입니다. 이름을 클릭하여 [!DNL Query Editor] 검색 막대를 사용하여 쿼리 이름을 검색할 수도 있습니다. 검색은 대소문자를 구분합니다. |
| SQL | SQL 쿼리의 처음 몇 자입니다. 코드 위로 마우스를 가져가면 전체 쿼리가 표시됩니다. |
| 수정한 사람 | 쿼리를 수정한 마지막 사용자입니다. 조직의 모든 사용자가 쿼리를 수정할 수 [!DNL Query Service] 있습니다. |
| 마지막 수정일 | 브라우저의 표준 시간대에서 마지막으로 쿼리를 수정한 날짜 및 시간입니다. |

## 로그

[ **[!UICONTROL 로그]** ] 탭은 이전에 실행된 쿼리 목록을 제공합니다. 기본적으로 로그는 역 크로노로지어로 나열됩니다.

![이미지](../images/queries/ui-overview/log.png)

| 열 | 설명 |
| --- | --- |
| **[!UICONTROL 이름]** | SQL 쿼리의 처음 여러 문자로 구성된 쿼리 이름입니다. 이름을 클릭하면 쿼리를 편집할 수 [!DNL Query Editor]있는 창이 열립니다. 검색 막대를 사용하여 쿼리 이름을 검색할 수 있습니다. 검색은 대소문자를 구분합니다. |
| **[!UICONTROL 작성자]** | 쿼리를 만든 사람의 이름입니다. |
| **[!UICONTROL 고객]** | 쿼리에 사용된 클라이언트 |
| **[!UICONTROL 데이터 집합]** | 쿼리에 사용되는 입력 데이터 집합입니다. 데이터 세트를 클릭하여 입력 데이터 세트 세부 정보 화면으로 이동합니다. |
| **[!UICONTROL 상태]** | 쿼리의 현재 상태입니다. |
| **[!UICONTROL 마지막 실행]** | 쿼리가 마지막으로 실행되었을 때 이 열 위에 있는 화살표를 클릭하여 목록을 오름차순이나 내림차순으로 정렬할 수 있습니다. |
| **[!UICONTROL 실행 시간]** | 쿼리를 실행하는 데 걸린 시간입니다. |

## 자격 증명

자격 증명 **[!UICONTROL 탭에]** 자격 증명이 [!DNL Postgres] 표시됩니다. 필드 옆에 있는 **[!UICONTROL 복사]** 아이콘을 클릭하여 내용을 키보드 버퍼에 저장합니다. 이러한 자격 증명을 사용하여 외부 클라이언트와 연결하는 방법에 대한 자세한 내용은 클라이언트 [연결 안내서를 참조하십시오][connect-clients].

![이미지](../images/queries/ui-overview/credentials.png)

## 다음 단계

이제 사용자 인터페이스에 대해 잘 알고 [!DNL Query Service] 있으므로 직접 쿼리 프로젝트 [!DNL Platform][!DNL Query Editor] 를 만들어 조직의 다른 사용자와 공유할 수 있습니다. 쿼리 작성 및 실행에 대한 자세한 내용 [!DNL Query Editor]은 [쿼리 편집기 사용 안내서를 참조하십시오][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
