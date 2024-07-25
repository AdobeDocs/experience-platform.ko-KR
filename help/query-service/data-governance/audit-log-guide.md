---
title: 쿼리 서비스 감사 로그 통합
description: 쿼리 서비스 감사 로그는 다양한 사용자 작업에 대한 기록을 유지 관리하여 문제 해결 또는 기업 데이터 관리 정책 및 규정 요구 사항 준수에 대한 감사 추적을 구성합니다. 이 자습서에서는 쿼리 서비스와 관련된 감사 로그 기능에 대한 개요를 제공합니다.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 1%

---

# [!DNL Query Service] 감사 로그 통합

Adobe Experience Platform [!DNL Query Service] 감사 로그 통합은 쿼리 관련 사용자 작업의 레코드를 제공합니다. 감사 로그는 기업 데이터 관리 정책 및 규정 요구 사항을 준수하고 문제를 해결하는 데 필수적인 도구입니다. 이 기능을 사용하면 다양한 이벤트 유형에 대한 작업 로그를 반환하고 레코드를 필터링하고 내보낼 수 있습니다. Platform UI 또는 [감사 쿼리 API](https://www.adobe.io/experience-platform-apis/references/audit-query/)를 통해 로그에 액세스하고 CSV 또는 JSON 파일 형식으로 다운로드할 수 있습니다.

감사 로그 사용자 인터페이스에 대한 자세한 내용은 [감사 로그 개요 문서](../../landing/governance-privacy-security/audit-logs/overview.md)를 참조하세요. Platform API를 호출하는 방법에 대한 자세한 내용은 [감사 로그 API 안내서](../../landing/api-guide.md)를 참조하세요.

## 전제 조건

Platform UI에서 감사 로그 대시보드를 보려면 [!DNL Data Governance] [!UICONTROL 사용자 활동 로그 보기] 권한이 활성화되어야 합니다. Adobe [Admin Console](https://adminconsole.adobe.com/)을(를) 통해 사용 권한을 사용하도록 설정했습니다. 이 권한을 활성화하기 위한 관리자 권한이 없는 경우 조직의 관리자에게 문의하십시오. [Admin Console을 통해 권한을 추가하는 방법에 대한 전체 지침](../../access-control/home.md)은 액세스 제어 설명서를 참조하세요.

## [!DNL Query Service] 감사 로그 범주 {#audit-log-categories}

[!DNL Query Service]이(가) 제공한 감사 로그 범주는 다음과 같습니다.

| 카테고리 | 설명 |
|---|---|
| [!UICONTROL 쿼리] | 이 범주를 사용하면 쿼리 실행을 감사할 수 있습니다. |
| [!UICONTROL 쿼리 템플릿] | 이 범주를 사용하면 쿼리 템플릿에서 수행한 다양한 작업(만들기, 업데이트 및 삭제)을 감사할 수 있습니다. |
| [!UICONTROL 예약된 쿼리] | 이 범주를 사용하면 [!DNL Query Service] 내에서 생성, 업데이트 또는 삭제된 일정을 감사할 수 있습니다. |

## [!DNL Query Service] 감사 로그 수행 {#perform-an-audit-log}

[!DNL Query Service] 활동에 대한 감사를 수행하려면 왼쪽 탐색에서 **[!UICONTROL 감사]**&#x200B;를 선택한 다음 단계 아이콘(![필터 아이콘)을 선택하십시오.](/help/images/icons/filter.png)) 필터 컨트롤 목록을 표시하여 결과를 좁히는 데 도움이 됩니다.

![왼쪽 탐색 및 필터 컨트롤에 &quot;Audits&quot;가 강조 표시된 플랫폼 UI 감사 로그 대시보드입니다.](../images/audit-log/filter-controls.png)

[!UICONTROL 감사] 대시보드 [!UICONTROL 활동 로그] 탭에서 [!DNL Query Service] 범주 중 하나로 기록된 모든 Platform 작업을 필터링할 수 있습니다. 로그 결과는 실행된 기간, 수행한 작업/함수 또는 쿼리를 수행한 사용자를 기반으로 추가로 필터링될 수 있습니다. 범주, 작업, 사용자 및 상태에 따라 로그를 필터링하는 방법에 대한 [전체 지침은 감사 로그 설명서를 참조하세요](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

반환된 감사 로그 데이터에는 선택한 필터 기준을 충족하는 모든 쿼리에 대한 다음 정보가 포함됩니다.

| 열 이름 | 설명 |
|---|---|
| [!UICONTROL 타임스탬프] | `month/day/year hour:minute AM/PM` 형식으로 수행된 작업의 정확한 날짜 및 시간입니다. |
| [!UICONTROL 자산 이름] | [!UICONTROL 자산 이름] 필드의 값은 필터로 선택한 범주에 따라 다릅니다. [!UICONTROL 예약된 쿼리] 범주를 사용하는 경우 **일정 이름**&#x200B;입니다. [!UICONTROL 쿼리 템플릿] 범주를 사용하는 경우 **템플릿 이름**&#x200B;입니다. [!UICONTROL 쿼리] 범주를 사용하는 경우 **세션 ID**&#x200B;입니다. |
| [!UICONTROL 범주] | 이 필드는 필터 드롭다운에서 선택한 범주와 일치합니다. |
| [!UICONTROL 작업] | 작성, 삭제, 업데이트 또는 실행 중 하나일 수 있습니다. 사용 가능한 작업은 필터로 선택한 범주에 따라 다릅니다. |
| [!UICONTROL 사용자] | 이 필드는 쿼리를 실행한 사용자 ID를 제공합니다. |

![필터링된 작업 로그가 강조 표시된 감사 대시보드입니다.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>감사 로그 대시보드에 기본적으로 표시되는 것보다 더 많은 쿼리 세부 정보가 CSV 또는 JSON 파일 형식으로 로그 결과를 다운로드하여 제공됩니다.

## 세부 정보 패널

감사 로그 결과 행을 선택하여 화면 오른쪽에 세부 정보 패널을 엽니다.

![세부 정보 패널이 강조 표시된 대시보드 작업 로그 탭을 감사합니다.](../images/audit-log/details-panel.png)

세부 정보 패널을 사용하여 [!UICONTROL 자산 ID] 및 [!UICONTROL 이벤트 상태]를 찾을 수 있습니다.

[!UICONTROL 자산 ID]의 값이 감사에 사용된 범주에 따라 변경됩니다.

* [!UICONTROL 쿼리] 범주를 사용하는 경우 [!UICONTROL 자산 ID]은(는) **세션 ID**&#x200B;입니다.
* [!UICONTROL 쿼리 템플릿] 범주를 사용하는 경우 [!UICONTROL 자산 ID]은(는) **템플릿 ID**&#x200B;이며 앞에 `[!UICONTROL templateID:]`이(가) 붙습니다.
* [!UICONTROL 예약된 쿼리] 범주를 사용하는 경우 [!UICONTROL 자산 ID]은(는) **예약 ID**&#x200B;이며 접두사가 `[!UICONTROL scheduleID:]`입니다.

감사에 사용된 범주에 따라 [!UICONTROL 이벤트 상태]의 값이 변경됩니다.

* [!UICONTROL 쿼리] 범주를 사용하는 경우 [!UICONTROL 이벤트 상태] 필드에 해당 세션 내에서 사용자가 실행한 모든 **쿼리 ID**&#x200B;의 목록이 제공됩니다.
* [!UICONTROL 쿼리 템플릿] 범주를 사용하는 경우 [!UICONTROL 이벤트 상태] 필드는 이벤트 상태에 대한 접두사로 **템플릿 이름**&#x200B;을(를) 제공합니다.
* [!UICONTROL 쿼리 일정] 범주를 사용하는 경우 [!UICONTROL 이벤트 상태] 필드는 이벤트 상태에 대한 접두사로 **일정 이름**&#x200B;을(를) 제공합니다.

## [!DNL Query Service] 감사 로그 범주에 사용 가능한 필터 {#available-filters}

사용 가능한 필터는 드롭다운에서 선택한 카테고리에 따라 다릅니다. 다음 표에서는 [[!DNL Query Service] 감사 로그 범주](#audit-log-categories)에 사용할 수 있는 필터에 대해 자세히 설명합니다.

| 필터 | 설명 |
|---|---|
| 카테고리 | 사용 가능한 전체 범주 목록은 [[!DNL Query Service] 감사 로그 범주](#audit-log-categories) 섹션을 참조하십시오. |
| 작업 | 감사 범주 [!DNL Query Service]을(를) 참조할 때 업데이트는 **기존 양식에 대한 수정**&#x200B;이고, 삭제는 **일정 또는 템플릿 제거**&#x200B;이며, 만들기는 **새 일정 또는 템플릿 만들기**&#x200B;이고, 실행은 **쿼리를 실행**&#x200B;합니다. |
| 사용자 | 사용자별로 필터링할 전체 사용자 ID(예: johndoe@acme.com)를 입력합니다. |
| 상태 | [!UICONTROL Allow], [!UICONTROL Success] 및 [!UICONTROL Failure] 옵션은 &quot;상태&quot; 또는 &quot;이벤트 상태&quot;를 기준으로 로그를 필터링하지만 [!UICONTROL Deny] 옵션은 **모든** 로그를 필터링합니다. |
| 날짜 | 시작 날짜 및/또는 종료 날짜를 선택하여 결과를 필터링할 날짜 범위를 정의합니다. |

## 다음 단계

이 문서를 읽으면 [!DNL Query Service] 감사 로그 기능과 이 기능을 사용하여 [!DNL Query Service] 사용자 작업을 필터링하는 방법을 더 잘 이해할 수 있습니다.

문제 해결을 위해 [!DNL Query Service] 감사 로그 기능을 사용하는 경우 [문제 해결 가이드](../troubleshooting-guide.md)를 읽는 것이 좋습니다.
