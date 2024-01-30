---
title: 쿼리 로그
description: 쿼리가 실행될 때마다 쿼리 로그가 자동으로 생성되며 UI를 통해 문제 해결에 도움을 줄 수 있습니다. 이 문서에서는 UI의 쿼리 서비스 로그 섹션을 사용하고 탐색하는 방법에 대해 간략하게 설명합니다.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: 445738f78f44ab8eb1632dbda82c4dd69dbebefd
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 0%

---

# 쿼리 로그

>[!IMPORTANT]
>
>특정 쿼리 로그 기능은 현재 제한된 릴리스에 있으며 일부 고객은 사용할 수 없습니다. 편집 아이콘이 없으면 UI가 약간 다르게 표시될 수 있습니다. 또한 쿼리 이름을 선택하는 프로세스는 쿼리 편집기 대신 로 이동할 수 있습니다. [!UICONTROL 쿼리 로그 세부 정보] 보기.

Adobe Experience Platform은 API 및 UI를 통해 발생하는 모든 쿼리 이벤트의 로그를 유지 관리합니다. 이 정보는 쿼리 서비스 UI의 [!UICONTROL 로그] 탭.

로그 파일은 모든 쿼리 이벤트에 의해 자동으로 생성되며 사용된 SQL, 쿼리 상태, 소요 시간 및 마지막 실행 시간 등의 정보를 포함합니다. 쿼리 로그 데이터를 비효율적이거나 문제가 있는 쿼리 문제를 해결하는 강력한 도구로 사용할 수 있습니다. 보다 포괄적인 로그 정보는 감사 로그 기능의 일부로 유지되며 [감사 로그 설명서](../../landing/governance-privacy-security/audit-logs/overview.md).

## 쿼리 로그 확인

쿼리 로그를 확인하려면 다음을 선택합니다 [!UICONTROL 쿼리] 쿼리 서비스 작업 영역으로 이동하여 [!UICONTROL 로그] 사용 가능한 옵션에서

![쿼리 및 로그가 강조 표시된 Platform UI.](../images/ui/query-log/logs.png)

## 사용자 지정 및 검색 {#customize-and-search}

쿼리 서비스 로그는 사용자 지정 가능한 테이블 형식으로 표시됩니다. 테이블 열을 사용자 정의하려면 설정 아이콘(![설정 아이콘](../images/ui/query-log/settings-icon.png))을 클릭하여 제품에서 사용할 수 있습니다. A [!UICONTROL 표 맞춤화] 각 열을 선택 취소할 수 있는 대화 상자가 나타납니다.

검색 필드에 템플릿 이름을 입력하여 특정 쿼리 템플릿과 관련된 로그를 검색할 수도 있습니다.

![검색 창 및 관리 열 테이블 드롭다운이 강조 표시된 쿼리 로그 작업 영역.](../images/ui/query-log/customize-logs.png)

A [각 로그 테이블 열에 대한 설명](./overview.md#log) 쿼리 서비스 개요의 로그 섹션에서 찾을 수 있습니다.

## 로그 데이터 검색

각 행은 쿼리 템플릿과 연관된 쿼리 실행에 대한 로그 데이터를 나타냅니다. 테이블에서 임의 행을 선택하여 해당 실행에 대한 로그 데이터로 오른쪽 사이드바를 채웁니다.

![행이 선택되어 있고 오른쪽 사이드바의 로그 데이터가 강조 표시된 쿼리 로그 작업 영역입니다.](../images/ui/query-log/log-details.png)

로그 세부 정보 패널에서 다양한 작업을 수행할 수 있습니다. 쿼리를 CTAS로 실행하여 새 출력 데이터 세트를 만들거나 실행에 사용된 전체 SQL 쿼리를 보거나 복사하거나 쿼리를 삭제할 수 있습니다.

>[!NOTE]
>
>다음에 대한 옵션: [!UICONTROL CTAS로 실행] 는 SELECT 쿼리에만 사용할 수 있습니다.

![행이 선택된 쿼리 로그 작업 영역, CTAS로 실행, 쿼리 삭제 및 SQL 복사 아이콘이 강조 표시됩니다.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>특정 쿼리 로그 기능은 현재 제한된 릴리스에 있으며 일부 고객은 사용할 수 없습니다.

다음에서 쿼리 템플릿 이름을 선택할 수도 있습니다. [!UICONTROL 이름] 열을 사용하여 [!UICONTROL 쿼리 로그 세부 정보] 보기.

>[!NOTE]
>
>API를 사용하여 쿼리를 만들었는데 초기화 중에 템플릿 이름이 제공되지 않은 경우, SQL 쿼리의 처음 수십 문자가 대신 표시됩니다.

![쿼리 로그 세부 사항 보기.](../images/ui/query-log/query-log-details.png)

## 로그 편집 {#edit-logs}

각 행의 템플릿 이름 또는 SQL 코드 조각 옆에 연필 아이콘(![연필 아이콘.](../images/ui/query-log/edit-icon.png))를 사용하여 쿼리 편집기로 이동할 수 있습니다. 그런 다음 편집기에서 편집을 위해 쿼리를 미리 채웁니다.

![연필 아이콘이 강조 표시된 쿼리 로그 작업 영역](../images/ui/query-log/edit-query.png)

## 로그 필터링 {#filter-logs}

다양한 설정을 기반으로 쿼리 로그 목록을 필터링할 수 있습니다. 필터 아이콘(![필터 아이콘](../images/ui/query-log/filter-icon.png))를 클릭하여 필터 옵션 세트를 왼쪽 레일에서 열 수 있습니다.

![필터 아이콘이 강조 표시된 쿼리 로그 작업 영역](../images/ui/query-log/log-filter.png)

사용 가능한 필터 목록이 표시됩니다.

![필터 옵션이 표시되고 강조 표시된 쿼리 로그 작업 영역](../images/ui/query-log/log-filter-settings.png)

다음 표는 각 필터에 대한 설명을 증명했습니다.

| 필터 | 설명 |
| ------ | ----------- |
| [!UICONTROL 대시보드 쿼리 제외] | 이 확인란은 기본적으로 활성화되어 있으며 인사이트 생성에 사용된 쿼리에서 생성된 로그를 제외합니다. 이러한 쿼리는 시스템에서 생성되며 모니터링, 관리 및 문제 해결에 필요한 사용자 생성 로그의 레코드를 숨깁니다. 시스템에서 생성한 로그를 보려면 확인란을 선택 취소합니다. |
| [!UICONTROL 시작일] | 특정 기간 동안 생성된 쿼리에 대한 로그를 필터링하려면 [!UICONTROL 시작] 및 [!UICONTROL 종료] 날짜: [!UICONTROL 시작일] 섹션. |
| [!UICONTROL 완료 날짜] | 특정 기간 동안 완료된 쿼리에 대한 로그를 필터링하려면 다음을 설정하십시오. [!UICONTROL 시작] 및 [!UICONTROL 종료] 날짜: [!UICONTROL 완료 날짜] 섹션. |
| [!UICONTROL 상태] | 다음을 기준으로 로그를 필터링하려면 [!UICONTROL 상태] 쿼리에서 적절한 라디오 단추를 선택합니다. 사용 가능한 옵션은 다음과 같습니다 [!UICONTROL 제출됨], [!UICONTROL 진행 중], [!UICONTROL 성공], 및 [!UICONTROL 실패]. 한 번에 하나의 상태 조건을 기준으로 로그만 필터링할 수 있습니다. |
| [!UICONTROL 클라이언트] | 사용된 쿼리 클라이언트를 기반으로 로그를 필터링하려면 자유 텍스트 필드에 다음 허용 값 중 하나를 입력합니다. `API`, `Adobe Query Service UI`, 또는 `QsAccel`. |
| [!UICONTROL 내 쿼리] | 사용 [!UICONTROL 내 쿼리] 자신이 실행한 쿼리에 대한 로그를 필터링하려면 전환합니다. |
| [!UICONTROL 쿼리 로그 ID] | 쿼리의 고유 로그 ID를 기준으로 필터링하려면 사용 가능한 텍스트 필드에 로그 ID를 입력합니다. 이 정보는 [!UICONTROL 로그 세부 정보]. |

적용된 모든 필터는 필터링된 로그 결과 위에 표시됩니다.

![적용된 필터 목록이 강조 표시된 쿼리 작업 영역의 로그 탭](../images/ui/query-log/applied-log-filters.png)

## 다음 단계

이제 이 문서를 읽고 쿼리 서비스 UI에서 쿼리 로그에 액세스하고 사용하는 방법을 더 잘 이해할 수 있습니다.

다음을 참조하십시오. [UI 개요](./overview.md)또는 [쿼리 서비스 API 안내서](../api/getting-started.md) 쿼리 서비스 기능에 대해 자세히 알아보십시오.

다음을 참조하십시오. [쿼리 문서 모니터링](./monitor-queries.md) 쿼리 서비스를 통해 예약된 쿼리 실행의 가시성을 높이는 방법을 알아봅니다.
