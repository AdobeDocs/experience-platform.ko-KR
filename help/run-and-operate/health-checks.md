---
title: 상태 검사
description: Adobe Experience Platform에서 상태 검사를 사용하여 스키마 및 ID 구성 문제가 데이터 작업에 영향을 미치기 전에 미리 감지하는 방법에 대해 알아봅니다.
solution: Experience Platform
type: Documentation
role: Admin, User
hide: true
source-git-commit: ab2420b898dc38d19187cee627b5c44e7fb44a6c
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 1%

---

# 상태 검사

상태 검사에서는 샌드박스에 사용된 스키마와 ID를 검사하고 [!UICONTROL AI Assistant]을(를) 탐색하고 문제를 해결하는 데 사용할 수 있는 문제 요약을 제공합니다. 앞으로는 보다 포괄적인 보고서를 위해 더 많은 객체를 스캔할 수 있습니다.

스키마 및 ID 구성이 잘못되면 잘못된 프로필 생성, 세그먼트 자격 실패 및 부정확한 활성화 등 중요한 다운스트림 문제가 발생합니다. 이러한 문제는 발견하기 어렵고 진단하기 위해 전문적인 전문성을 필요로 하는 경우가 많다. 상태 검사는 사후 문제 해결에서 사전 예방적 유지 관리로 접근 방식을 전환합니다.

상태 검사를 통해 다음을 수행할 수 있습니다.

* **구성 문제를 조기에 감지**: 누락된 모범 사례, 잘못된 구성 및 개인화, 활성화 등에서 비효율성을 초래하는 패턴을 식별합니다.
* **안내가 있는 업데이트 관리를 받습니다**: 각 문제의 의미와 해결 방법에 대한 명확한 지침을 받으십시오.
* **계속 모니터링**: 현재 상태 검사는 매일 자동 검사를 실행하므로 심각한 오류가 발생하기 전에 문제를 확인할 수 있습니다. 향후 릴리스에서 일정이 변경될 수 있습니다.

## 전제 조건 {#prerequisites}

상태 검사에 액세스하려면 **[!UICONTROL View Health Checks]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. 적절한 권한이 있는지 확인하려면 시스템 관리자에게 문의하십시오.

## 액세스 상태 확인 {#access-health-checks}

[!UICONTROL Experience Platform] UI에서 상태 검사에 액세스하려면:

1. 왼쪽 탐색에서 **[!UICONTROL Run and Operate]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL Health Checks]**&#x200B;를 선택합니다.

상태 검사 대시보드에는 가장 최근 검사 결과의 요약이 표시됩니다.

![평가된 개체, 검사 결과 및 확인된 문제를 표시하는 상태 검사 대시보드](assets/health-checks/dashboard.png)

## 대시보드 이해 {#understanding-dashboard}

상태 확인 대시보드는 구현 상태를 평가하는 데 도움이 되는 세 가지 정보 영역을 제공합니다.

### 평가된 오브젝트 {#objects-evaluated}

**[!UICONTROL Objects evaluated]** 섹션은 스캔한 총 스키마 및 ID 네임스페이스의 수와 함께 각 범주에 대해 발견된 문제의 수를 표시합니다. 이렇게 하면 샌드박스에서 구성 문제의 범위와 심각도를 빠르게 볼 수 있습니다.

### 검사 결과 {#scan-results}

**[!UICONTROL Scan results]** 섹션에는 실패한 검사 수가 표시됩니다. 실패한 검사는 하나 이상의 상태 검사에서 주의가 필요한 구성 문제를 감지했음을 나타냅니다. **마지막으로 수행한 일별 상태 검사 완료** 타임스탬프는 가장 최근 검사가 실행된 시점을 보여 줍니다.

### 식별된 문제 {#identified-issues}

**[!UICONTROL Identified issues]** 섹션에는 각 상태 검사에 대한 카드가 표시됩니다. 각 카드가 표시됩니다.

* 상태 검사 이름 및 문제에 대한 간략한 설명.
* 발견된 문제 수 또는 문제가 존재하지 않는지 확인
* 검사를 통과했는지 또는 주의가 필요한지 여부를 보여 주는 상태 표시기입니다.

해당 상태 검사의 세부 정보를 살펴보려면 카드를 선택하십시오.

## 사용 가능한 상태 확인 {#available-health-checks}

상태 검사는 현재 스키마 및 ID 구성의 다섯 가지 기본 영역을 평가합니다. 이러한 검사는 플랫폼 전반에서 가장 영향력 있는 데이터 모델링 문제를 타깃팅합니다.

### ID 필드 유효성 검사 {#identity-field-validation}

ID 필드에 최소 및 최대 길이 제약 조건과 데이터 무결성을 위한 정규 표현식 패턴 규칙이 있는지 검사합니다.

| 세부 정보 | 설명 |
| --- | --- |
| **문제** | ID로 표시된 필드에 최소/최대 길이 또는 패턴 유효성 검사가 누락되었습니다. |
| **영향** | 유효성을 검사하지 않으면 가비지 값이 [!UICONTROL Identity Service]을(를) 입력할 수 있습니다. &quot;0&quot;, &quot;Guest&quot; 또는 일치하지 않는 케이스(예: &quot;xyz123&quot; 대 &quot;XYZ123&quot;)와 같은 값은 세분화 및 활성화 중에 어셈블되는 프로필의 무결성을 손상합니다. |
| **업데이트 관리** | ID로 표시된 사용자 지정 필드에 최소/최대 길이 및 패턴 제한을 설정합니다. 정규 표현식을 사용하여 숫자만, 대문자, 소문자 또는 특정 문자 조합과 같은 규칙을 적용합니다. |

**[!UICONTROL Identity Field Validation]** 카드를 선택하면 오른쪽에 세부 정보 패널이 열립니다. 패널에 다음이 표시됩니다.

* **[!UICONTROL Description]**: ID 필드에 최소/최대 길이 및 정규 표현식 패턴 규칙이 있는지 확인하기 위해 스캔합니다. 영향을 받는 스키마 및 필드를 나열합니다.
* **[!UICONTROL Impact]**: 스키마의 ID 필드에 최소/최대 길이와 패턴 유효성 검사가 설정되지 않은 경우 데이터가 일관되지 않아 데이터의 무결성과 품질을 손상시킬 수 있습니다.
* **[!UICONTROL General areas of impact]**: [!UICONTROL Identity Service]의 낮은 품질 식별자, 신뢰할 수 없는 연결.
* **[!UICONTROL Experience League Documentation]**: 데이터 모델링을 위한 모범 사례에 대한 링크입니다.
* **[!UICONTROL Affected Schemas]**: 영향을 받는 스키마 목록으로서, 각 목록에는 더 자세한 정보를 볼 수 있는 확장자와 스키마를 열 수 있는 링크가 있습니다.

설명, 영향 및 영향을 받는 스키마를 보여 주는 ![ID 필드 유효성 검사 세부 정보 패널](assets/health-checks/identity-field-validation-detail.png)

자세한 내용은 스키마 모범 사례 설명서에서 [데이터 무결성 팁](/help/xdm/schema/best-practices.md#data-integrity-tips)을 참조하십시오.

### 아이덴티티 그래프 연결 규칙 {#identity-graph-linking-rules}

축소된 프로필을 방지하기 위해 샌드박스에 ID 그래프 연결 규칙이 구성되어 있는지 확인합니다.

| 세부 정보 | 설명 |
| --- | --- |
| **문제** | 이 샌드박스에 대해 ID 그래프 연결 규칙이 구성되지 않았습니다. |
| **영향** | 연결 규칙을 사용하지 않으면 여러 개별 프로필이 하나의 프로필로 병합될 수 있습니다(그래프 축소). 공유된 디바이스 또는 고유하지 않은 ID의 특정 데이터가 원하지 않는 병합을 트리거하여 개인화를 부정확하게 만들 수 있습니다. |
| **업데이트 관리** | **[!UICONTROL Identities]** 메뉴로 이동하여 **[!UICONTROL Settings]**&#x200B;을(를) 선택하고 그래프당 고유한 ID를 하나 이상 선택하십시오. 이를 통해 ID 그래프 연결 규칙을 사용할 수 있으며 프로필 축소를 방지할 수 있습니다. |

**[!UICONTROL Identity Graph Linking Rules]** 카드를 선택하면 오른쪽에 세부 정보 패널이 열립니다. 패널에 다음이 표시됩니다.

* **[!UICONTROL Description]**: 축소된 프로필을 방지하도록 적절한 연결 규칙이 구성되어 있는지 확인합니다. 현재 규칙 상태와 그래프당 고유한 ID를 표시합니다.
* **[!UICONTROL Impact]**: ID 그래프 연결 규칙이 설정되지 않은 경우 특정 데이터가 서로 다른 여러 프로필을 하나의 프로필로 병합하려고 시도할 수 있습니다. 원치 않는 병합을 방지하려면 ID 그래프 연결 규칙을 통해 제공된 구성을 사용해야 합니다.
* **[!UICONTROL General areas of impact]**: 축소되거나 병합된 프로필입니다.
* **[!UICONTROL Experience League Documentation]**: ID 그래프 연결 규칙 개요에 대한 링크입니다.
* **[!UICONTROL Configure linking rules]**: 검사에 실패하면 패널에서 직접 연결 규칙을 구성할 수 있는 단추가 나타납니다.

설명, 영향 및 연결 규칙 구성 단추를 보여 주는 ![ID 그래프 연결 규칙 세부 정보 패널](assets/health-checks/identity-graph-linking-detail.png)

자세한 내용은 [ID 그래프 연결 규칙 개요](/help/identity-service/identity-graph-linking-rules/overview.md) 및 [구현 안내서](/help/identity-service/identity-graph-linking-rules/implementation-guide.md)를 참조하십시오.

### 사용자 및 비사용자 ID 구성 {#people-non-people-identity}

스키마 클래스 간에 사람 및 사람이 아닌 ID 유형이 올바르게 사용되는지 확인합니다.

| 세부 정보 | 설명 |
| --- | --- |
| **문제** | 비사용자 식별자는 개별 프로필 또는 경험 이벤트 클래스 스키마에서 사용되거나, 사용자 식별자는 조회 스키마에서 사용됩니다. |
| **영향** | 프로필 스키마의 비사용자 식별자가 ID 그래프에 참여하지 않아 ID 확인이 불완전합니다. 조회 스키마의 사용자 식별자는 프로필 수를 부풀려서 데이터를 조회 사용 사례에 부적격 상태로 만듭니다. 두 경우 모두 향후 제품 개선 사항으로 인해 구현이 중단될 위험이 있습니다. |
| **업데이트 관리** | 플래그가 지정된 스키마를 검토하고 ID 유형 할당을 수정하십시오. 가능한 경우 개별 프로필 스키마에서 비개인 식별자를 제거합니다. 데이터 세트에서 이미 사용 중인 스키마의 경우 [스키마 진화 규칙](/help/xdm/schema/composition.md#evolution)을 참조하세요. |

**[!UICONTROL People & Non-People Identity Config]** 카드를 선택하면 오른쪽에 세부 정보 패널이 열립니다. 패널에 다음이 표시됩니다.

* **[!UICONTROL Description]**: 스키마 클래스에서 ID 형식이 올바르게 사용되었는지 확인합니다. 잘못 구성된 스키마를 나열하고 잘못된 할당을 강조 표시합니다.
* **[!UICONTROL Impact]**: 비개인 엔터티에 개인 ID가 지정되면 프로필 수가 부풀려지고 이 데이터가 조회로 적합하지 않게 됩니다. 개인 엔티티에 비개인 ID가 부여되는 경우 데이터를 스트리밍 또는 에지 세분화에 사용할 수 없습니다.
* **[!UICONTROL General areas of impact]**: 불완전한 ID 그래프, 부풀려진 프로필 수, 조회 오용.
* **[!UICONTROL Affected Schemas]**: 문제가 있는 스키마 목록입니다. 스키마 행을 확장하여 각 잘못된 구성에 대한 경로, ID 이름 및 스키마 유형을 확인합니다. 링크 아이콘을 사용하여 스키마를 엽니다.

![설명, 영향 및 확장 가능한 행이 있는 영향을 받는 스키마를 보여 주는 사용자 및 비사용자 ID 구성 세부 정보 패널](assets/health-checks/people-non-people-identity-detail.png)

자세한 내용은 [ID 유형 설명서](/help/identity-service/features/namespaces.md#identity-type) 및 [스키마 모범 사례](/help/xdm/schema/best-practices.md)를 참조하세요.

### 사용자 정의 ID 네임스페이스 설명 {#namespace-missing-description}

사용자 지정 ID 네임스페이스 메타데이터 및 설명이 완료되었는지 검색합니다.

| 세부 정보 | 설명 |
| --- | --- |
| **문제** | 사용자 정의 ID 네임스페이스에 설명 필드가 누락되었습니다. |
| **영향** | 설명이 누락되면 사용 및 디버깅 중에 혼동이 발생할 수 있습니다. |
| **업데이트 관리** | 설명 필드를 채워 각 사용자 지정 네임스페이스를 문서화합니다. 이러한 ID를 생성할 외부 소스 시스템을 식별하는 유효성 검사 기준(최소/최대 길이, 패턴) 및 라이프사이클 정보를 포함합니다. |

**[!UICONTROL Custom Identity Namespace Description]** 카드를 선택하면 오른쪽에 세부 정보 패널이 열립니다. 패널에 다음이 표시됩니다.

* **[!UICONTROL Description]**: 네임스페이스 메타데이터 및 설명이 완료되었는지 검색합니다. 설명 필드가 비어 있는 네임스페이스 및 소유자를 표시합니다.
* **[!UICONTROL Impact]**: 사용자 지정 ID 네임스페이스에 대한 설명을 설정하면 각 네임스페이스의 목적에 대한 컨텍스트를 제공하여 명확성이 향상됩니다. 이렇게 하면 팀 구성원과 이해 관계자가 각 네임스페이스의 기능을 혼동 없이 빠르게 이해할 수 있습니다.
* **[!UICONTROL General areas of impact]**: 디버그 또는 사용 혼동. 유효성 검사 의도가 명확하지 않습니다.
* **[!UICONTROL Experience League Documentation]**: 추가 정보를 위해 사용자 지정 네임스페이스를 만드는 링크입니다.
* **[!UICONTROL Affected namespaces]**: 설명이 없는 사용자 지정 ID 네임스페이스 목록입니다. 각 네임스페이스 옆에 있는 링크 아이콘을 사용하여 보거나 편집합니다.

![설명, 영향 및 영향을 받는 네임스페이스 목록을 표시하는 사용자 지정 ID 네임스페이스 설명 세부 정보 패널](assets/health-checks/custom-namespace-description-detail.png)

자세한 내용은 [사용자 지정 네임스페이스 만들기](/help/identity-service/features/namespaces.md#create-namespaces)에 대한 설명서를 참조하십시오.

### 더 이상 사용되지 않는 ID 네임스페이스 {#deprecated-namespace}

정리용으로 표시해야 하는 사용되지 않거나 오래된 ID 네임스페이스를 검색합니다.

| 세부 정보 | 설명 |
| --- | --- |
| **문제** | 오래된 ID 네임스페이스는 더 이상 사용되지 않는 것으로 표시되지 않습니다. |
| **영향** | 사용되지 않거나 오래된 네임스페이스는 현재 사용 중인 네임스페이스에 혼동을 일으키고 ID 필드에 잘못된 레이블을 지정할 수 있는 위험을 증가시킵니다. |
| **업데이트 관리** | 사용하지 않는 네임스페이스의 이름을 &quot;사용하지 않음&quot; 접두사를 포함하도록 바꾸십시오(예: &quot;사용하지 않음 - [원래 이름]&quot;). Adobe Experience Platform은 현재 네임스페이스 삭제를 지원하지 않으므로 이름을 바꾸는 것이 좋습니다. |

**[!UICONTROL Deprecated Identity Namespace]** 카드를 선택하면 오른쪽에 세부 정보 패널이 열립니다. 패널에 다음이 표시됩니다.

* **[!UICONTROL Description]**: 정리할 사용되지 않거나 오래된 ID 네임스페이스를 검색합니다. 사용되지 않은 네임스페이스를 마지막 사용 타임스탬프 또는 스키마 참조로 나열합니다.
* **[!UICONTROL Impact]**: 스키마에서 사용되지 않는 ID 네임스페이스는 해당 이름에 &quot;사용되지 않음&quot; 또는 &quot;DO NOT USE&quot; 태그를 추가하여 제거하도록 표시해야 합니다. ID 네임스페이스 삭제는 현재 지원되지 않습니다.
* **[!UICONTROL General areas of impact]**: 혼동 및 잘못된 레이블 지정 위험.
* **[!UICONTROL Experience League Documentation]**: 추가 설명서를 위한 오래된 ID 네임스페이스에 대한 링크입니다.
* **[!UICONTROL Affected namespaces]**: 사용되지 않거나 사용되지 않는 ID 네임스페이스 목록입니다. 각 네임스페이스 옆에 있는 링크 아이콘을 사용하여 해당 네임스페이스를 보거나 관리할 수 있습니다.

![설명, 영향 및 영향을 받는 네임스페이스 목록을 표시하는 사용되지 않는 ID 네임스페이스 세부 정보 패널](assets/health-checks/deprecated-namespace-detail.png)

자세한 내용은 [사용되지 않는 네임스페이스에 대한 Experience Cloud 기술 자료 문서](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-18155){target="_blank"}를 참조하십시오.

## 다음 단계 {#next-steps}

상태 확인 결과를 검토한 후 다음 리소스를 탐색하여 이해를 심화하십시오.

* 신뢰할 수 있는 데이터 모델을 디자인하기 위한 [스키마 모범 사례](/help/xdm/schema/best-practices.md)에 대해 알아봅니다.
* 프로필 축소를 방지하기 위해 [ID 그래프 연결 규칙](/help/identity-service/identity-graph-linking-rules/overview.md)을 이해합니다.
* 네임스페이스 관리 모범 사례를 보려면 [ID 네임스페이스 설명서](/help/identity-service/features/namespaces.md)를 검토하십시오.
* 일괄 처리 작업 가시성을 위해 [을(를) 포함한 다른 &#x200B;](/help/run-and-operate/overview.md)도구 실행 및 작업[[!UICONTROL Job Schedules]](/help/run-and-operate/job-schedules.md)을 살펴보십시오.
