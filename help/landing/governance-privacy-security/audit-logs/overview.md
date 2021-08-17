---
title: 감사 로그 개요
description: 감사 로그를 사용하여 Adobe Experience Platform에서 작업을 수행한 사용자를 확인하는 방법을 알아봅니다.
source-git-commit: eb8144ace087c68a159aab89195832860df431e2
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 4%

---

# 감사 로그(베타)

>[!IMPORTANT]
>
>Adobe Experience Platform의 감사 로그 기능은 현재 베타 버전입니다. 이 설명서에 설명된 기능은 변경될 수 있습니다.

시스템에서 수행되는 활동의 투명성과 가시성을 높이기 위해 Adobe Experience Platform을 사용하면 &quot;감사 로그&quot; 형태로 다양한 서비스 및 기능에 대한 사용자 활동을 감사할 수 있습니다. 이러한 로그는 플랫폼의 문제 해결에 도움이 될 수 있는 감사 추적을 형성하며 기업의 데이터 관리 정책 및 규정 요구 사항을 효과적으로 준수할 수 있도록 도와줍니다.

기본적으로 감사 로그는 **누가**&#x200B;어떤&#x200B;**작업을 수행했는지 및**&#x200B;언제&#x200B;**작업을 수행했는지 알려줍니다.** 로그에 기록된 각 작업에는 작업 유형, 날짜 및 시간, 작업을 수행한 사용자의 이메일 ID 및 작업 유형과 관련된 추가 속성을 나타내는 메타데이터가 포함됩니다.

이 문서에서는 UI 또는 API에서 감사 로그를 보고 관리하는 방법을 비롯하여 Platform의 감사 로그를 다룹니다.

## 감사 로그로 캡처된 이벤트 유형

다음 표에서는 감사 로그에서 리소스가 기록되는 작업을 설명합니다.

| 리소스 | 작업 |
| --- | --- |
| [샌드박스](../../../sandboxes/home.md) | <ul><li>선택 사항에서</li><li>업데이트</li><li>재설정</li><li>삭제</li></ul> |
| [데이터 세트](../../../catalog/datasets/overview.md) | <ul><li>선택 사항에서</li><li>업데이트</li><li>삭제</li><li>[실시간 고객 프로필 사용](../../../profile/home.md)</li></ul> |
| [스키마](../../../xdm/schema/composition.md) | <ul><li>선택 사항에서</li><li>업데이트</li><li>삭제</li></ul> |
| [필드 그룹](../../../xdm/schema/composition.md#field-group) | <ul><li>선택 사항에서</li><li>업데이트</li><li>삭제</li></ul> |
| [대상](../../../destinations/home.md) | <ul><li>활성화</li></ul> |

## 감사 로그에 대한 액세스

조직에 대해 이 기능이 활성화되면 활동이 발생하면 감사 로그가 자동으로 수집됩니다. 수동으로 로그 수집을 활성화할 필요는 없습니다.

감사 로그를 보고 내보내려면 &quot;감사 로그 보기&quot; 액세스 제어 권한이 부여되어야 합니다. 플랫폼 기능에 대한 개별 권한을 관리하는 방법에 대한 자세한 내용은 [액세스 제어 설명서](../../../access-control/home.md)를 참조하십시오.

## UI에서 감사 로그 관리

플랫폼 UI의 **[!UICONTROL 감사]** 작업 공간 내에서 다른 Experience Platform 기능에 대한 감사 로그를 볼 수 있습니다. 작업 공간에는 기본적으로 가장 최근 항목에서 가장 최근 항목으로 정렬된 기록된 로그 목록이 표시됩니다.

![감사 로그 대시보드](../../images/audit-logs/audits.png)

시스템은 작년의 감사 로그만 표시합니다. 이 제한을 초과하는 모든 로그는 시스템에서 자동으로 제거됩니다.

목록에서 이벤트를 선택하여 오른쪽 레일에서 해당 세부 사항을 확인합니다.

![이벤트 세부 사항](../../images/audit-logs/select-event.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## API에서 감사 로그 관리

UI에서 수행할 수 있는 모든 작업은 API 호출을 사용하여 수행할 수도 있습니다. 자세한 내용은 [API 참조 문서](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/audit-query.yaml)를 참조하십시오.

## Adobe Admin Console에 대한 감사 로그 관리

Adobe Admin Console에서 활동에 대한 감사 로그를 관리하는 방법에 대해 알아보려면 다음 [document](https://helpx.adobe.com/enterprise/using/audit-logs.html)을 참조하십시오.

## 다음 단계

이 안내서에서는 Experience Platform에서 감사 로그를 관리하는 방법을 다룹니다. 플랫폼 활동을 모니터링하는 방법에 대한 자세한 내용은 [Observability Insights](../../../observability/home.md) 및 [데이터 수집](../../../ingestion/quality/monitor-data-ingestion.md)에 대한 설명서를 참조하십시오.