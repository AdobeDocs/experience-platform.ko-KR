---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리;쿼리 편집기;쿼리 편집기;쿼리 편집기;쿼리 편집기;
solution: Experience Platform
title: Query Service UI 안내서
topic-legacy: guide
description: Adobe Experience Platform 쿼리 서비스는 쿼리를 작성 및 실행하고, 이전에 실행된 쿼리를 보고, IMS 조직 내의 사용자가 저장한 쿼리에 액세스하는 데 사용할 수 있는 사용자 인터페이스를 제공합니다.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: a887c502213e96d6af90af0859da78c2984f89a7
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 2%

---

# [!DNL Query Service] UI 안내서

Adobe Experience Platform [!DNL Query Service] 은 IMS 조직 내에서 사용자가 저장한 쿼리를 작성 및 실행하고, 이전에 실행된 쿼리를 보고, 액세스하는 데 사용할 수 있는 사용자 인터페이스를 제공합니다. 내에서 UI에 액세스하려면 [Adobe Experience Platform](https://platform.adobe.com), 선택 **[!UICONTROL 쿼리]** 을 클릭합니다.

## [!DNL Query Editor]

다음 [!DNL Query Editor] 외부 클라이언트를 사용하지 않고 쿼리를 작성하고 실행할 수 있습니다. 선택 **[!UICONTROL 쿼리 만들기]** 열다 [!DNL Query Editor] 새 쿼리를 만듭니다. 또한 [!DNL Query Editor] 에서 쿼리를 선택하여 **[!UICONTROL 로그]** 또는 **[!UICONTROL 찾아보기]** 탭. 이전에 실행하거나 저장한 쿼리를 선택하면 [!DNL Query Editor] 선택한 쿼리의 SQL을 표시합니다.

![쿼리 만들기 가 강조 표시된 쿼리 대시보드](../images/ui/overview/overview.png)

[!DNL Query Editor] 은 쿼리 입력을 시작할 수 있는 편집 공간을 제공합니다. 입력할 때 편집기는 테이블 내의 SQL 예약 단어, 테이블 및 필드 이름을 자동으로 완료합니다. 쿼리 작성을 마쳤으면 **재생** 단추를 클릭하여 쿼리를 실행합니다. 다음 **[!UICONTROL 콘솔]** 편집기 아래 탭에 표시되는 내용은 [!DNL Query Service] 쿼리 반환 시기를 나타내는 현재 실행 중입니다. 다음 **[!UICONTROL 결과]** 콘솔 옆의 탭에 쿼리 결과가 표시됩니다. 자세한 내용은 [쿼리 편집기 안내서](./user-guide.md) 자세한 내용은 [!DNL Query Editor].

![갑자기 그 광경이 펼쳐졌다 [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## 찾아보기 {#browse}

다음 **[!UICONTROL 찾아보기]** 탭에는 조직의 사용자가 저장한 쿼리가 표시됩니다. 여기에 저장된 쿼리는 여전히 구성 중일 수 있으므로 이러한 쿼리를 쿼리 프로젝트로 생각하는 것이 유용합니다. 에 표시되는 쿼리 **[!UICONTROL 찾아보기]** 탭도 실행 쿼리로 표시됩니다 **[!UICONTROL 로그]** 탭에서 이전에 [!DNL Query Service].

![여러 개의 저장된 쿼리를 표시하는 쿼리 대시보드 찾아보기 탭의 보기가 축소되었습니다.](../images/ui/overview/browse.png)

| 열 | 설명 |
| --- | --- |
| **[!UICONTROL 이름]** | 사용자가 만든 쿼리 이름입니다. 이름에 을(를) 선택하여 [!DNL Query Editor]. 검색 막대를 사용하여 쿼리의 이름을 검색할 수도 있습니다. 검색은 대소문자를 구분합니다. |
| **[!UICONTROL SQL]** | SQL 쿼리의 처음 몇 문자입니다. 코드 위로 마우스를 가져가면 전체 쿼리가 표시됩니다. |
| **[!UICONTROL 수정한 사람]** | 쿼리를 수정한 마지막 사용자입니다. 조직의 모든 사용자가 [!DNL Query Service] 쿼리를 수정할 수 있습니다. |
| **[!UICONTROL 마지막 수정일]** | 브라우저의 시간대에서 쿼리를 마지막으로 수정한 날짜 및 시간입니다. |

## 로그

다음 **[!UICONTROL 로그]** 탭에는 이전에 실행된 쿼리 목록이 제공됩니다. 기본적으로 로그에는 쿼리를 역동기식으로 나열합니다.

![쿼리 대시보드 로그 탭의 보기에서 확대된 항목 - 역시간 순서로 쿼리 목록을 표시합니다.](../images/ui/overview/log.png)

| 열 | 설명 |
| --- | --- |
| **[!UICONTROL 이름]** | SQL 쿼리의 처음 여러 문자로 구성된 쿼리 이름입니다. 이름을 선택하면 [!DNL Query Editor]: 쿼리를 편집할 수 있습니다. 검색 막대를 사용하여 쿼리의 이름을 검색할 수 있습니다. 검색은 대소문자를 구분합니다. |
| **[!UICONTROL 작성자]** | 쿼리를 만든 사람의 이름입니다. |
| **[!UICONTROL 고객]** | 쿼리에 사용되는 클라이언트입니다. |
| **[!UICONTROL 데이터 세트]** | 쿼리에서 사용하는 입력 데이터 집합입니다. 데이터 세트를 선택하여 입력 데이터 세트 세부 사항 화면으로 이동합니다. |
| **[!UICONTROL 상태]** | 쿼리의 현재 상태입니다. |
| **[!UICONTROL 마지막 실행]** | 쿼리가 마지막으로 실행된 때입니다. 이 열 위에 있는 화살표를 선택하여 목록을 오름차순이나 내림차순으로 정렬할 수 있습니다. |
| **[!UICONTROL 런타임]** | 쿼리를 실행하는 데 걸린 시간입니다. |

## 자격 증명

다음 **[!UICONTROL 자격 증명]** 탭에는 만료 자격 증명과 비만료 자격 증명이 모두 표시됩니다. 이러한 자격 증명을 사용하여 외부 클라이언트와 연결하는 방법에 대한 자세한 내용은 [자격 증명 안내서](../clients/overview.md).

![자격 증명 탭이 강조 표시된 질의 대시보드입니다.](../images/ui/overview/credentials.png)

## 다음 단계

이제 잘 아시네요 [!DNL Query Service] 사용자 인터페이스 [!DNL Platform], 액세스 권한 [!DNL Query Editor] 조직의 다른 사용자와 공유할 고유한 쿼리 프로젝트 만들기를 시작하려면 다음을 수행하십시오. 의 쿼리 작성 및 실행에 대한 자세한 내용은 [!DNL Query Editor]를 참조하고 [[!DNL Query Editor] 사용 안내서](./user-guide.md).