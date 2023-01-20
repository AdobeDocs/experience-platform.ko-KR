---
title: 쿼리 서비스 감사 로그 통합
description: Query Service 감사 로그는 다양한 사용자 작업에 대한 기록을 유지 관리하여 문제를 해결하거나 기업 데이터 관리 정책 및 규정 요구 사항을 준수할 수 있는 감사 추적을 형성합니다. 이 자습서에서는 Query Service와 관련된 감사 로그 기능에 대한 개요를 제공합니다.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] 감사 로그 통합

Adobe Experience Platform [!DNL Query Service] 감사 로그 통합에서는 쿼리 관련 사용자 작업 레코드를 제공합니다. 감사 로그는 기업의 데이터 관리 정책과 규정 요구 사항을 해결하고 준수하기 위한 필수 도구입니다. 기능을 사용하면 많은 이벤트 유형에 대한 작업 로그를 반환하고 레코드를 필터링하고 내보낼 수 있습니다. Platform UI 또는 [감사 쿼리 API](https://www.adobe.io/experience-platform-apis/references/audit-query/) CSV 또는 JSON 파일 형식으로 다운로드했습니다.

감사 로그 사용자 인터페이스에 대한 자세한 내용은 [감사 로그 개요 문서](../../landing/governance-privacy-security/audit-logs/overview.md). 플랫폼 API 호출에 대한 자세한 내용은 [감사 로그 API 안내서](../../landing/api-guide.md).

## 전제 조건

다음 항목이 있어야 합니다. [!DNL Data Governance] [!UICONTROL 사용자 활동 로그 보기] 플랫폼 UI 내에서 감사 로그 대시보드를 볼 수 있는 권한이 활성화되었습니다. Adobe을 통해 권한이 활성화됩니다 [Admin Console](https://adminconsole.adobe.com/). 이 권한을 활성화할 관리자 권한이 없는 경우 조직의 관리자에게 문의하십시오. 다음에 대한 액세스 제어 설명서를 참조하십시오. [Admin Console을 통한 권한 추가에 대한 전체 지침](../../access-control/home.md).

## [!DNL Query Service] 감사 로그 범주 {#audit-log-categories}

에서 제공하는 감사 로그 카테고리입니다. [!DNL Query Service] 는 다음과 같습니다.

| 카테고리 | 설명 |
|---|---|
| [!UICONTROL 쿼리] | 이 카테고리를 사용하면 쿼리 실행을 감사할 수 있습니다. |
| [!UICONTROL 쿼리 템플릿] | 이 카테고리를 사용하면 쿼리 템플릿에서 수행한 다양한 작업(만들기, 업데이트 및 삭제)을 감사할 수 있습니다. |
| [!UICONTROL 예약된 쿼리] | 이 카테고리를 사용하면 내에서 생성, 업데이트 또는 삭제된 예약을 감사할 수 있습니다 [!DNL Query Service]. |

## 다음 작업을 수행합니다. [!DNL Query Service] 감사 로그 {#perform-an-audit-log}

감사를 수행하려면 [!DNL Query Service] 활동, 선택 **[!UICONTROL 감사]** 왼쪽 탐색에서 단계 아이콘(![필터 아이콘.](../images/audit-log/filter.png))을 클릭하여 필터 컨트롤 목록을 표시하여 결과를 좁힐 수 있습니다.

![왼쪽 탐색 및 필터 컨트롤이 강조 표시된 Platform UI 감사 로그 대시보드입니다.](../images/audit-log/filter-controls.png)

에서 [!UICONTROL 감사] 대시보드 [!UICONTROL 활동 로그] 탭에서 기록된 모든 플랫폼 작업을 [!DNL Query Service] 카테고리. 로그 결과는 실행된 시간, 수행한 작업/함수 또는 쿼리를 만든 사용자에 따라 추가로 필터링할 수 있습니다. 다음 항목에 대한 감사 로그 설명서를 참조하십시오. [카테고리, 작업, 사용자 및 상태에 따라 로그를 필터링하는 방법에 대한 전체 지침](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

반환된 감사 로그 데이터에는 선택한 필터 기준을 충족하는 모든 쿼리에 대한 다음 정보가 포함됩니다.

| 열 이름 | 설명 |
|---|---|
| [!UICONTROL 타임스탬프] | 에서 수행한 작업의 정확한 날짜 및 시간입니다 `month/day/year hour:minute AM/PM` 형식 지정 |
| [!UICONTROL 자산 이름] | 에 대한 값 [!UICONTROL 자산 이름] 필드는 필터로 선택한 카테고리에 따라 다릅니다. 를 사용할 때 [!UICONTROL 예약된 쿼리] 카테고리 이것은 **예약 이름**. 를 사용할 때 [!UICONTROL 쿼리 템플릿] 카테고리, 다음 **템플릿 이름**. 를 사용할 때 [!UICONTROL 쿼리] 카테고리, 다음 **session ID** |
| [!UICONTROL 카테고리] | 이 필드는 필터 드롭다운에서 사용자가 선택한 카테고리와 일치합니다. |
| [!UICONTROL 작업] | 생성, 삭제, 업데이트 또는 실행할 수 있습니다. 사용 가능한 작업은 필터로 선택한 카테고리에 따라 다릅니다. |
| [!UICONTROL 사용자] | 이 필드는 쿼리를 실행한 사용자 ID를 제공합니다. |

![필터링된 활동 로그가 강조 표시된 감사 대시보드.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>로그 결과를 CSV 또는 JSON 파일 형식으로 다운로드하면 감사 로그 대시보드에 기본적으로 표시되는 것보다 더 많은 쿼리 세부 사항이 제공됩니다.

## 세부 사항 패널

감사 로그 결과 행을 선택하여 화면 오른쪽에 있는 세부 사항 패널을 엽니다.

![세부 사항 패널이 강조 표시된 대시보드 활동 로그 탭을 감사합니다.](../images/audit-log/details-panel.png)

세부 사항 패널을 사용하여 [!UICONTROL 자산 ID] 그리고 [!UICONTROL 이벤트 상태].

의 값 [!UICONTROL 자산 ID] 감사에서 사용되는 카테고리에 따라 변경됩니다.

* 를 사용할 때 [!UICONTROL 쿼리] 카테고리, [!UICONTROL 자산 ID] 은  **session ID**.
* 를 사용할 때 [!UICONTROL 쿼리 템플릿] 카테고리, [!UICONTROL 자산 ID] 은 **템플릿 ID** 접두사로 `[!UICONTROL templateID:]`.
* 를 사용할 때 [!UICONTROL 예약된 쿼리] 카테고리, [!UICONTROL 자산 ID] 은  **예약 ID** 접두사로 `[!UICONTROL scheduleID:]`.

의 값 [!UICONTROL 이벤트 상태] 감사에서 사용되는 카테고리에 따라 변경됩니다.

* 를 사용할 때 [!UICONTROL 쿼리] 카테고리, [!UICONTROL 이벤트 상태] 필드는 모두 목록을 제공합니다 **쿼리 ID** 가 해당 세션 내에 사용자가 실행합니다.
* 를 사용할 때 [!UICONTROL 쿼리 템플릿] 카테고리, [!UICONTROL 이벤트 상태] 필드에서는 **템플릿 이름** 이벤트 상태의 접두사로 사용됩니다.
* 를 사용할 때 [!UICONTROL 쿼리 일정] 카테고리, [!UICONTROL 이벤트 상태] 필드에서는 **예약 이름** 이벤트 상태의 접두사로 사용됩니다.

## 사용 가능한 필터 [!DNL Query Service] 감사 로그 범주 {#available-filters}

사용 가능한 필터는 드롭다운에서 선택한 카테고리에 따라 다릅니다. 다음 표에서는 [[!DNL Query Service] 감사 로그 범주](#audit-log-categories).

| 필터 | 설명 |
|---|---|
| 카테고리 | 자세한 내용은 [[!DNL Query Service] 감사 로그 범주](#audit-log-categories) 섹션을 참조하십시오. |
| 작업 | 참조 시 [!DNL Query Service] 감사 카테고리, 업데이트는 **기존 양식 수정**, delete 는 입니다. **일정 또는 템플릿 제거**, 만들기 입니다. **새 일정 또는 템플릿 만들기**, 및 execute **쿼리 실행**. |
| 사용자 | 사용자별로 필터링할 전체 사용자 ID(예: johndoe@acme.com)을 입력합니다. |
| 상태 | 다음 [!UICONTROL 허용], [!UICONTROL 성공], 및 [!UICONTROL 실패] 옵션은 &quot;상태&quot; 또는 &quot;이벤트 상태&quot;를 기준으로 로그를 필터링하지만 [!UICONTROL 거부] 옵션이 필터링됩니다. **모두** 로그. |
| 날짜 | 결과를 필터링할 날짜 범위를 정의하려면 시작 날짜 및/또는 종료 날짜를 선택합니다. |

## 다음 단계

이 문서를 읽으면 [!DNL Query Service] 감사 로그 기능 및 감사 로그 기능을 사용하여 [!DNL Query Service] 사용자 작업.

를 사용하는 경우 [!DNL Query Service] 문제 해결을 위한 감사 로그 기능은 [문제 해결 안내서](../troubleshooting-guide.md).
