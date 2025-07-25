---
title: 쿼리 일정
description: Adobe Experience Platform UI를 통해 예약된 쿼리 실행을 자동화하고, 쿼리 일정을 삭제 또는 비활성화하고, 사용 가능한 예약 옵션을 활용하는 방법을 알아봅니다.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 04b804b81b605040c74db040bc5118e0392ddd32
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 0%

---

# 쿼리 일정

쿼리 일정을 생성하여 쿼리 실행을 자동화할 수 있습니다. 예약된 쿼리는 사용자 지정 케이던스에서 실행되어 빈도, 날짜 및 시간을 기준으로 데이터를 관리합니다. 필요한 경우 결과에 대한 출력 데이터 세트를 선택할 수도 있습니다. 템플릿으로 저장된 쿼리는 쿼리 편집기에서 예약할 수 있습니다.

>[!IMPORTANT]
>
>이미 생성되어 저장된 질의에만 스케줄을 추가할 수 있습니다.

## 예약된 쿼리에 대한 계정 요구 사항 {#technical-account-user-requirements}

예약된 쿼리가 안정적으로 실행될 수 있도록 Adobe에서는 관리자가 예약된 쿼리를 만들기 위해 기술 계정(OAuth 서버 간 자격 증명 사용)을 프로비저닝할 것을 권장합니다. 예약된 쿼리는 개인 사용자 계정으로 만들 수도 있지만, 이 방법으로 만든 쿼리는 해당 사용자의 액세스가 제거되거나 비활성화되면 실행이 중지됩니다.

기술 계정 설정 및 필수 권한 할당에 대한 자세한 내용은 [자격 증명 가이드 사전 요구 사항](./credentials.md#prerequisites) 및 [API 인증](../../landing/api-authentication.md)을 참조하십시오.

기술 계정 만들기 및 구성에 대한 추가 지침은 다음을 참조하십시오.

- [Developer Console 설정](https://experienceleague.adobe.com/ko/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman): Adobe Developer Console을 구성하고 OAuth 자격 증명을 얻는 방법에 대한 단계별 지침입니다.
- [전체 기술 계정 설정](https://experienceleague.adobe.com/ko/docs/platform-learn/tutorial-comprehensive-technical/setup): Adobe Experience Platform에서 기술 계정을 만들고 구성하기 위한 포괄적인 연습입니다.

쿼리 서비스 UI만 사용하는 경우 필요한 권한이 있는지 확인하거나 기술 계정을 관리하는 관리자와 협력하십시오. 예약된 쿼리가 [!UICONTROL 예약된 쿼리] 탭의 목록에 추가되어 모든 예약된 쿼리 작업의 상태, 일정 세부 정보 및 오류 메시지를 모니터링하고 경고를 구독할 수 있습니다. 쿼리 모니터링 및 관리에 대한 자세한 내용은 [예약된 쿼리 모니터링 문서](./monitor-queries.md)를 참조하십시오.

이 워크플로우는 쿼리 서비스 UI의 예약 프로세스를 다룹니다. API를 사용하여 일정을 추가하는 방법에 대해 알아보려면 [예약된 쿼리 끝점 안내서](../api/scheduled-queries.md)를 참조하세요.

>[!NOTE]
>
>기술 계정을 사용하여 사용자가 조직을 떠나거나 역할이 변경된 경우에도 예약된 쿼리가 계속 실행되도록 합니다. 중단 없는 쿼리 자동화를 위해 가능한 한 기술 계정을 선택하십시오.

## 쿼리 일정 만들기 {#create-schedule}

쿼리를 예약하려면 [!UICONTROL 템플릿] 탭 또는 [!UICONTROL 예약된 쿼리] 탭의 [!UICONTROL 템플릿] 열에서 쿼리 템플릿을 선택하십시오. 템플릿 이름을 선택하면 쿼리 편집기로 이동합니다.

쿼리 편집기에서 저장된 쿼리에 액세스하는 경우 쿼리에 대한 일정을 만들거나 세부 정보 패널에서 쿼리의 일정을 볼 수 있습니다.

>[!TIP]
>
>**[!UICONTROL 일정 보기]**&#x200B;를 선택하여 일정 작업 영역으로 이동하여 예약된 쿼리가 실행되는 것을 한 눈에 확인합니다.

![쿼리 편집기 [!UICONTROL 일정 보기] 및 [!UICONTROL 일정 추가]가 강조 표시되어 있습니다.](../images/ui/query-schedules/view-add-schedule.png)

**[!UICONTROL 일정 추가]**&#x200B;를 선택하여 [일정 세부 정보 페이지](#schedule-details)(으)로 이동합니다.

또는 쿼리 이름 아래의 **[!UICONTROL 일정]** 탭을 선택합니다.

![일정 탭이 강조 표시된 쿼리 편집기입니다.](../images/ui/query-schedules/schedules-tab.png)

스케줄 작업 공간이 나타납니다. UI에 템플릿과 연결된 모든 예약된 실행 목록이 표시됩니다. **[!UICONTROL 일정 추가]**&#x200B;를 선택하여 일정을 만듭니다.

![일정 추가가 강조 표시된 쿼리 편집기 일정 작업 영역입니다.](../images/ui/query-schedules/add-schedule.png)

### 일정 세부 정보 추가 {#schedule-details}

[일정 세부 정보] 페이지가 나타납니다. 이 페이지에서 예약된 쿼리에 대한 다양한 세부 정보를 편집할 수 있습니다. 세부 정보에는 예약된 쿼리의 [실행 빈도 및 평일](#scheduled-query-frequency), 시작 및 종료 날짜, 결과를 내보낼 데이터 세트, [쿼리 상태 경고](#alerts-for-query-status)가 포함됩니다.

>[!IMPORTANT]
>
>쿼리 스케줄러 UI는 무기한 또는 영구적인 예약을 지원하지 않습니다. 종료 날짜를 지정해야 합니다. 종료 날짜에는 상한이 없습니다.

![일정 세부 정보 패널이 강조 표시되었습니다.](../images/ui/query-schedules/schedule-details.png)

#### 예약된 쿼리 빈도 {#scheduled-query-frequency}

**[!UICONTROL 빈도]**&#x200B;에 대해 다음 옵션을 선택할 수 있습니다.

- **[!UICONTROL 시간별]**: 예약된 쿼리는 선택한 날짜 기간 동안 매 시간마다 실행됩니다.
- **[!UICONTROL 일별]**: 예약된 쿼리는 선택한 시간 및 날짜 기간에 X일마다 실행됩니다. 선택한 시간은 **UTC**&#x200B;이며 현지 표준 시간대가 아닙니다.
- **[!UICONTROL 주별]**: 선택한 쿼리가 선택한 요일, 시간 및 기간에 실행됩니다. 선택한 시간은 **UTC**&#x200B;이며 현지 표준 시간대가 아닙니다.
- **[!UICONTROL 월별]**: 선택한 쿼리는 매월 선택한 날짜, 시간 및 날짜 기간에 실행됩니다. 선택한 시간은 **UTC**&#x200B;이며 현지 표준 시간대가 아닙니다.
- **[!UICONTROL 연간]**: 선택한 쿼리는 매년 선택한 일, 월, 시간 및 날짜 기간에 실행됩니다. 선택한 시간은 **UTC**&#x200B;이며 현지 표준 시간대가 아닙니다.

### 데이터 세트 세부 정보 제공 {#dataset-details}

기존 데이터 세트에 데이터를 추가하거나 새 데이터 세트를 생성하고 여기에 데이터를 추가하여 쿼리 결과를 관리합니다.

쿼리를 처음 실행할 때 데이터 집합을 만들려면 **[!UICONTROL 새 데이터 집합에 만들기 및 추가]**&#x200B;를 선택하십시오. 후속 실행은 해당 데이터 세트에 데이터를 계속 삽입합니다. 마지막으로 데이터 세트의 이름과 설명을 입력합니다.

>[!IMPORTANT]
>
> 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들고 있으므로 데이터 세트가 이미 설정되어 있으므로 **not**&#x200B;은(는) `INSERT INTO` 또는 `CREATE TABLE AS SELECT`을(를) 쿼리의 일부로 포함할 필요가 없습니다. `INSERT INTO` 또는 `CREATE TABLE AS SELECT`을(를) 예약된 쿼리의 일부로 포함하면 오류가 발생합니다.

![데이터 세트 세부 정보와 [!UICONTROL 새 데이터 세트에 만들기 및 추가] 옵션이 강조 표시된 일정 세부 정보 패널.](../images/ui/query-schedules/dataset-details-create-and-append.png)

또는 **[!UICONTROL 기존 데이터 집합에 추가]**&#x200B;를 선택한 다음 데이터 집합 아이콘(![데이터 집합 아이콘.](/help/images/icons/database.png))을 선택하십시오.

![데이터 세트 세부 정보 및 기존 데이터 세트에 추가 기능이 강조 표시된 예약 세부 정보 패널.](../images/ui/query-schedules/dataset-details-existing.png)

**[!UICONTROL 출력 데이터 세트 선택]** 대화 상자가 나타납니다.

그런 다음 기존 데이터 세트를 찾아보거나 검색 필드를 사용하여 옵션을 필터링합니다. 사용하려는 데이터 세트 행을 선택합니다. 데이터 세트 세부 사항이 오른쪽 패널에 표시됩니다. **[!UICONTROL 완료]**&#x200B;를 선택하여 선택을 확인합니다.

![검색 필드, 데이터 세트 행, 완료 강조 표시된 출력 데이터 세트 선택 대화 상자입니다.](../images/ui/query-schedules/select-output-dataset-dialog.png)

### 계속 실패할 경우 쿼리 격리 {#quarantine}

일정을 만들 때 시스템 리소스를 보호하고 잠재적인 중단을 방지하기 위해 격리 기능에 쿼리를 등록할 수 있습니다. 격리 기능은 [!UICONTROL 격리됨] 상태에 배치하여 반복적으로 실패한 쿼리를 자동으로 식별하고 격리합니다. 10회 연속 실패 후 쿼리를 격리하면 문제를 개입, 검토 및 수정한 후 추가 실행을 허용할 수 있습니다. 이를 통해 운영 효율성과 데이터 무결성을 유지할 수 있습니다.

![쿼리 일정 작업 영역에 [!UICONTROL 쿼리 격리]가 강조 표시되고 [예]가 선택되었습니다.](../images/ui/query-schedules/quarantine-enroll.png)

쿼리가 격리 기능에 등록되면 이 쿼리 상태 변경에 대한 경고를 구독할 수 있습니다. 예약된 쿼리가 격리에 등록되지 않은 경우 [경고 대화 상자](./monitor-queries.md#alert-subscription)에 옵션으로 표시되지 않습니다.

[!UICONTROL 예약된 쿼리] 탭의 인라인 작업에서 예약된 쿼리를 격리 기능에 등록할 수도 있습니다. 자세한 내용은 [쿼리 모니터링 설명서](./monitor-queries.md#alert-subscription)를 참조하세요.

### 예약된 쿼리 상태에 대한 경고 설정 {#alerts-for-query-status}

예약된 쿼리 설정의 일부로 쿼리 경고에 가입할 수도 있습니다. 다양한 상황에 대한 알림을 받도록 설정을 구성할 수 있습니다. 격리된 상태, 쿼리 처리 지연 또는 쿼리 상태 변경에 대해 경고를 설정할 수 있습니다. 사용 가능한 쿼리 상태 경고 옵션에는 시작, 성공 및 실패가 포함됩니다. 경고는 팝업 알림 또는 이메일로 받을 수 있습니다. 예약된 쿼리의 해당 상태에 대한 경고를 구독하려면 확인란을 선택합니다.

![경고 옵션이 강조 표시된 예약 세부 정보 패널입니다.](../images/ui/query-editor/alerts.png)

아래 표에서는 지원되는 쿼리 경고 유형에 대해 설명합니다.

| 경고 유형 | 설명 |
|---|---|
| `start` | 이 경고는 예약된 쿼리 실행이 시작되거나 처리를 시작할 때 알려줍니다. |
| `success` | 이 경고는 예약된 쿼리 실행이 성공적으로 완료되면 사용자에게 알려 주며 이는 쿼리가 오류 없이 실행되었음을 나타냅니다. |
| `failed` | 이 경고는 예약된 쿼리 실행에 오류가 발생하거나 성공적으로 실행되지 않을 때 트리거됩니다. 문제를 신속하게 식별하고 해결하는 데 도움이 됩니다. |
| `quarantine` | 이 경고는 예약된 쿼리 실행이 격리된 상태로 전환되면 활성화됩니다. 쿼리가 [격리 기능에 등록](#quarantine)되면 10번의 연속 실행에 실패한 예약된 쿼리는 자동으로 [!UICONTROL 격리됨] 상태가 됩니다. 그러면 격리된 쿼리에서 더 이상의 실행이 수행되기 전에 사용자의 개입이 필요합니다. 참고: 격리 경고를 구독하려면 격리 기능에 쿼리를 등록해야 합니다. |
| `delay` | 이 경고는 예약된 쿼리 실행의 결과에 [지연이 지정된 임계값을 초과하는 경우](./monitor-queries.md#query-run-delay)을(를) 알려줍니다. 완료하거나 실패하지 않고 해당 기간 동안 쿼리가 실행될 때 경고를 트리거하는 사용자 지정 시간을 설정할 수 있습니다. 기본 동작은 쿼리 처리가 시작된 후 150분 동안 경고를 설정합니다. |

>[!NOTE]
>
>[!UICONTROL 쿼리 실행 지연] 경고를 설정하도록 선택한 경우 Experience Platform UI에서 원하는 지연 시간을 분 단위로 설정해야 합니다. 기간을 분 단위로 입력하십시오. 최대 지연은 24시간(1440분)입니다.

경고 규칙이 정의되는 구조를 포함하여 Adobe Experience Platform의 경고에 대한 개요는 [경고 개요](../../observability/alerts/overview.md)를 참조하십시오. Adobe Experience Platform UI에서 경고 및 경고 규칙을 관리하는 방법에 대한 지침은 [경고 UI 안내서](../../observability/alerts/ui.md)를 참조하십시오.

### 예약된 매개 변수가 있는 쿼리에 대해 매개 변수 설정 {#set-parameters}

매개 변수가 있는 쿼리에 대해 예약된 쿼리를 만드는 경우 이제 이러한 쿼리 실행에 대한 매개 변수 값을 설정해야 합니다.

![쿼리 매개 변수 섹션이 강조 표시된 일정 만들기 워크플로의 일정 세부 정보 섹션입니다.](../images/ui/query-schedules/scheduled-query-parameter.png)

일정 세부 정보를 확인한 후 **[!UICONTROL 저장]**&#x200B;을 선택하여 일정을 만듭니다. 템플릿의 일정 탭으로 돌아갑니다. 이 작업 공간에는 일정 ID, 일정 자체 및 일정의 출력 데이터 세트를 포함하여 새로 만든 일정의 세부 사항이 표시됩니다.

## 예약된 쿼리 실행 보기 {#scheduled-query-runs}

템플릿의 [!UICONTROL 일정] 탭에서 예약 ID를 선택하여 새로 예약된 쿼리에 대한 쿼리 실행 목록으로 이동합니다.

![새로 만든 일정이 강조 표시된 일정 작업 영역입니다.](../images/ui/query-schedules/schedules-workspace.png)

또는 쿼리 템플릿의 예약된 실행 목록을 보려면 **[!UICONTROL 예약된 쿼리]** 탭으로 이동하여 사용 가능한 목록에서 템플릿 이름을 선택하십시오.

![이름이 지정된 서식 파일이 강조 표시된 예약된 쿼리 탭입니다.](../images/ui/query-schedules/view-scheduled-runs.png)

예약된 해당 쿼리에 대한 쿼리 실행 목록이 나타납니다.

### 작업 수준에서 시간 계산 {#compute-hours}

CTAS/ITAS 일괄 처리 쿼리에 대해 쿼리 실행 수준에서 소비된 계산 시간을 추적합니다. 이 기능은 컴퓨팅 사용에 대한 통찰력을 제공하여 리소스 할당을 최적화하고 쿼리 성능을 개선하는 데 도움이 됩니다.

>[!AVAILABILITY]
>
>시간 계산 기능은 [Data Distiller SKU](../data-distiller/overview.md)를 구매한 사용자에게만 제공됩니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

![예약된 쿼리에 대해 쿼리 실행 목록이 강조 표시된 예약된 쿼리 작업 영역의 세부 정보 섹션입니다.](../images/ui/query-schedules/list-of-scheduled-runs.png)

다음 표에서는 예약된 쿼리 실행을 나열하는 세부 정보 섹션에서 사용할 수 있는 각 열에 대한 설명을 제공합니다.

| 열 제목 | 설명 |
|---------------------|----------------------------------|
| [!UICONTROL 쿼리 실행 ID] | 예약된 쿼리의 개별 실행을 추적하고 참조할 수 있도록 각 쿼리 실행에 대한 고유 식별자를 표시합니다. |
| [!UICONTROL 쿼리 실행 시작] | 각 실행이 시작된 시기를 모니터링하는 데 도움이 되도록 쿼리 실행의 시작 날짜 및 시간을 나타냅니다. |
| [!UICONTROL 쿼리 실행 완료] | insight에 실행 지속 시간 및 상태를 제공하기 위해 쿼리 실행의 완료 날짜 및 시간을 표시합니다. |
| [!UICONTROL 상태] | 결과를 빠르게 평가하기 위해 쿼리 실행의 현재 상태(예: `Completed,` `Running,` 또는 `Failed,`)를 표시합니다. |
| [!UICONTROL 데이터 세트] | 쿼리 실행에 사용된 데이터 세트를 나열하여 실행에 관련된 데이터 소스를 표시합니다. |
| [!UICONTROL 시간 계산] | 각 쿼리 실행에 사용된 계산 시간을 시간 단위로 표시합니다. 리소스 사용을 추적하고 쿼리 성능을 최적화하는 데 도움이 됩니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>시간 계산 데이터는 2024/08/15부터 사용할 수 있습니다. 이 날짜 이전의 데이터는 &#39;사용할 수 없음&#39;으로 표시됩니다.

UI를 통해 모든 쿼리 작업의 상태를 모니터링하는 방법에 대한 자세한 내용은 [예약된 쿼리 모니터링 안내서](./monitor-queries.md#inline-actions)를 참조하십시오.

목록에서 **[!UICONTROL 쿼리 실행 ID]**&#x200B;를 선택하여 쿼리 실행 개요로 이동합니다. [쿼리 실행 개요](./monitor-queries.md#query-run-overview)에서 사용할 수 있는 정보의 전체 분류는 예약된 쿼리 모니터링 설명서를 참조하십시오.

쿼리 서비스 API를 사용하여 예약된 쿼리를 모니터링하려면 [예약된 쿼리 실행 끝점 안내서](../api/runs-scheduled-queries.md)를 참조하십시오.

## 일정 활성화, 비활성화 또는 삭제 {#delete-schedule}

특정 쿼리의 일정 작업 영역 또는 예약된 모든 쿼리를 나열하는 [!UICONTROL 예약된 쿼리] 작업 영역에서 일정을 활성화, 비활성화 또는 삭제할 수 있습니다.

선택한 쿼리의 [!UICONTROL 일정] 탭에 액세스하려면 [!UICONTROL 템플릿] 탭 또는 [!UICONTROL 예약된 쿼리] 탭에서 쿼리 템플릿의 이름을 선택해야 합니다. 해당 쿼리에 대한 쿼리 편집기로 이동합니다. 쿼리 편집기에서 **[!UICONTROL 일정]**&#x200B;을(를) 선택하여 일정 작업 영역에 액세스합니다.

사용 가능한 일정 행에서 일정을 선택하여 세부 정보 패널을 채웁니다. 예약된 쿼리를 비활성화(또는 활성화)하려면 토글을 사용합니다.

### 비활성화된 쿼리 삭제

>[!IMPORTANT]
>
>쿼리에 대한 일정을 삭제하려면 먼저 일정을 비활성화해야 합니다.

![세부 정보 패널이 강조 표시된 템플릿 일정 목록입니다.](../images/ui/query-schedules/schedule-details-panel.png)

확인 대화 상자가 나타납니다. **[!UICONTROL 사용 안 함]**&#x200B;을 선택하여 작업을 확인합니다.

![일정 확인 대화 상자 사용 안 함](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

비활성화된 일정을 삭제하려면 **[!UICONTROL 일정 삭제]**&#x200B;를 선택하십시오.

![삭제 일정이 강조 표시된 일정 작업 영역입니다.](../images/ui/query-schedules/delete-schedule.png)

또는 [!UICONTROL 예약된 쿼리] 탭에서는 각 예약된 쿼리에 대한 인라인 작업 컬렉션을 제공합니다. 사용할 수 있는 인라인 작업에는 예약된 쿼리에 대한 알림을 받으려면 [!UICONTROL 일정 비활성화] 또는 [!UICONTROL 일정 활성화], [!UICONTROL 일정 삭제] 및 [!UICONTROL 구독]이 포함됩니다. 예약된 쿼리 탭을 통해 예약된 쿼리를 삭제하거나 비활성화하는 방법에 대한 자세한 지침은 [예약된 쿼리 모니터링 안내서](./monitor-queries.md#inline-actions)를 참조하십시오.
