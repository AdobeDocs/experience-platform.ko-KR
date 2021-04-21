---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리;쿼리 편집기;쿼리 편집기;쿼리 편집기;;home;popular topics service;query Editor;Query Editor;
solution: Experience Platform
title: 쿼리 서비스 UI 안내서
topic-legacy: guide
description: Adobe Experience Platform 쿼리 서비스는 IMS 조직 내에서 사용자가 저장한 쿼리를 작성 및 실행하고 이전에 실행한 쿼리를 보고 액세스하는 데 사용할 수 있는 사용자 인터페이스를 제공합니다.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 2%

---

# [!DNL Query Service] 가이드

Adobe Experience Platform [!DNL Query Service]은 IMS 조직 내에서 사용자가 저장한 쿼리를 작성 및 실행하고 이전에 실행한 쿼리를 보고 액세스하는 데 사용할 수 있는 사용자 인터페이스를 제공합니다. [Adobe Experience Platform][platform-ui] 내의 UI에 액세스하려면 왼쪽 탐색 영역에서 **[!UICONTROL Queries]**&#x200B;를 선택합니다.

## [!DNL Query Editor]

[!DNL Query Editor]을 사용하면 외부 클라이언트를 사용하지 않고도 쿼리를 작성하고 실행할 수 있습니다. **[!UICONTROL Create Query]**&#x200B;을 클릭하여 [!DNL Query Editor]을 열고 새 쿼리를 만듭니다. **[!UICONTROL Log]** 또는 **[!UICONTROL Browse]** 탭에서 쿼리를 선택하여 [!DNL Query Editor]에 액세스할 수도 있습니다. 이전에 실행되거나 저장된 쿼리를 선택하면 [!DNL Query Editor]이 열리고 선택한 쿼리에 대한 SQL이 표시됩니다.

![이미지](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] 은 쿼리를 입력하기 시작할 수 있는 편집 공간을 제공합니다. 입력할 때 편집기는 테이블 내의 SQL 예약어, 테이블 및 필드 이름을 자동으로 완성합니다. 쿼리 작성을 마쳤으면 **재생** 단추를 클릭하여 쿼리를 실행합니다. 편집기 아래의 **[!UICONTROL Console]** 탭에는 쿼리가 반환되었을 때를 나타내는 [!DNL Query Service]이(가) 현재 수행 중인 내용이 표시됩니다. 콘솔 옆에 있는 **[!UICONTROL Result]** 탭에는 쿼리 결과가 표시됩니다. [!DNL Query Editor] 사용에 대한 자세한 내용은 [쿼리 편집기 안내서][query-editor]를 참조하십시오.

![이미지](../images/queries/ui-overview/query-editor.png)

## 찾아보기

**[!UICONTROL Browse]** 탭에는 조직의 사용자가 저장한 쿼리가 표시됩니다. 여기에 저장된 쿼리는 아직 건설 중일 수 있으므로 이러한 쿼리를 쿼리 프로젝트로 생각하면 유용합니다. **[!UICONTROL Browse]** 탭에 표시된 쿼리는 이전에 [!DNL Query Service]에 의해 실행된 경우 **[!UICONTROL Log]** 탭에 실행 쿼리로도 표시됩니다.

![이미지](../images/queries/ui-overview/browse.png)

| 열 | 설명 |
| --- | --- |
| 이름 | 사용자가 만든 쿼리 이름입니다. 이름을 클릭하여 [!DNL Query Editor]에서 쿼리를 열 수 있습니다. 검색 막대를 사용하여 쿼리 이름에서 검색할 수도 있습니다. 검색은 대소문자를 구분합니다. |
| SQL | SQL 쿼리의 처음 몇 자. 코드 위로 마우스를 가져가면 전체 쿼리가 표시됩니다. |
| 수정한 사람 | 쿼리를 수정한 마지막 사용자입니다. [!DNL Query Service]에 대한 액세스 권한이 있는 조직의 모든 사용자는 쿼리를 수정할 수 있습니다. |
| 마지막 수정 날짜 | 브라우저의 표준 시간대에서 마지막으로 쿼리를 수정한 날짜 및 시간입니다. |

## 로그

**[!UICONTROL Log]** 탭은 이전에 실행된 쿼리 목록을 제공합니다. 기본적으로 로그는 역연순으로 나열됩니다.

![이미지](../images/queries/ui-overview/log.png)

| 열 | 설명 |
| --- | --- |
| **[!UICONTROL Name]** | SQL 쿼리의 처음 여러 문자로 구성된 쿼리 이름입니다. 이름을 클릭하면 [!DNL Query Editor]이 열리고 쿼리를 편집할 수 있습니다. 검색 막대를 사용하여 쿼리 이름을 검색할 수 있습니다. 검색은 대소문자를 구분합니다. |
| **[!UICONTROL Created By]** | 쿼리를 만든 사람의 이름입니다. |
| **[!UICONTROL Client]** | 쿼리에 사용되는 클라이언트입니다. |
| **[!UICONTROL Dataset]** | 쿼리에서 사용하는 입력 데이터 집합입니다. 데이터 세트를 클릭하여 데이터 세트 정보 입력 화면으로 이동합니다. |
| **[!UICONTROL Status]** | 쿼리의 현재 상태입니다. |
| **[!UICONTROL Last Run]** | 쿼리가 마지막으로 실행되었을 때 이 열 위의 화살표를 클릭하여 목록을 오름차순이나 내림차순으로 정렬할 수 있습니다. |
| **[!UICONTROL Run Time]** | 쿼리를 실행하는 데 걸린 시간입니다. |

## 자격 증명

**[!UICONTROL Credentials]** 탭에는 [!DNL Postgres] 자격 증명이 표시됩니다. 키보드 버퍼에 내용을 저장하려면 필드 옆에 있는 **[!UICONTROL Copy]** 아이콘을 클릭합니다. 이러한 자격 증명을 사용하여 외부 클라이언트와 연결하는 방법에 대한 자세한 내용은 [클라이언트 안내서][connect-clients]를 참조하십시오.

![이미지](../images/queries/ui-overview/credentials.png)

## 다음 단계

이제 [!DNL Platform]의 [!DNL Query Service] 사용자 인터페이스에 익숙하다면 [!DNL Query Editor]에 액세스하여 자신의 쿼리 프로젝트를 만들어 조직의 다른 사용자와 공유할 수 있습니다. [!DNL Query Editor]에서 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 편집기 사용자 안내서][query-editor]를 참조하십시오.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
