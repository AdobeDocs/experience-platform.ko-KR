---
title: 쿼리 서비스의 데이터 거버넌스
description: 이 개요에서는 Experience Platform 쿼리 서비스 데이터 거버넌스의 주요 요소를 다룹니다.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: 54a6f508818016df1a4ab2a217bc0765b91df9e9
workflow-type: tm+mt
source-wordcount: '2843'
ht-degree: 2%

---

# 쿼리 서비스의 데이터 거버넌스

Adobe Experience Platform은 여러 엔터프라이즈 시스템의 데이터를 함께 가져오며 필요에 따라 쿼리 서비스를 통해 데이터를 정리하고, 구체화하고, 조작하고, 보강할 수 있습니다. 이를 통해 마케터는 고객을 더 나은 방식으로 식별하고, 이해하고, 참여시킬 수 있습니다. 특정 데이터는 조직 정책 및 법적 규정에 따라 사용 제한이 발생할 수 있으므로 적절한 데이터 거버넌스 보장은 개인 정보 처리에 있어 중요한 측면입니다. 수집된 데이터 및 관련 작업이 정의된 데이터 사용 정책을 준수하는지 확인하는 것이 중요합니다.

Query Service 내의 데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수할 수 있습니다. 이는 비즈니스 정의에 정의된 규정에 따라 사용 정책이 적용되었는지 확인할 때 중요한 역할을 합니다.

데이터 처리를 일상적으로 수행하는 조직에서는 모든 사용자를 위한 개인 정보 보호 환경을 만들기 위해 이러한 지침을 개요, 실습 및 적용하는 것이 좋습니다.

다음 카테고리는 쿼리 서비스를 사용할 때 데이터 준수 규정을 준수하는 데 유용합니다.

1. 보안
1. 감사
1. 데이터 사용
1. 개인정보 보호
<!-- 1. Data hygiene -->

이 문서에서는 다양한 거버넌스 영역을 살펴보고 쿼리 서비스를 사용할 때 데이터 규정 준수를 용이하게 하는 방법을 보여 줍니다. 다음을 참조하십시오. [거버넌스, 개인 정보 보호 및 보안 개요](../../landing/governance-privacy-security/overview.md) Experience Platform을 통해 고객 데이터를 관리하고 규정 준수를 보장하는 방법에 대한 자세한 정보.

## 보안

데이터 보안은 데이터의 무단 액세스로부터 데이터를 보호하고 전체 수명주기 동안 안전한 액세스를 보장하는 프로세스입니다. 보안 액세스는 역할 기반 액세스 제어 및 속성 기반 액세스 제어와 같은 기능별 역할 및 권한 적용을 통해 Experience Platform 시 유지됩니다. 또한 자격 증명, SSL 및 데이터 암호화를 사용하여 플랫폼 전반에서 데이터를 보호합니다.

쿼리 서비스와 관련된 보안은 다음 카테고리로 나뉩니다.

* [액세스 제어](#access-control): 액세스는 데이터 세트 및 열 수준 권한을 포함한 역할 및 권한을 통해 제어됩니다.
* 를 통한 데이터 보호 [연결](#connectivity): 만료되는 자격 증명 또는 만료되지 않는 자격 증명으로 제한된 연결을 만들어 플랫폼 및 외부 클라이언트를 통해 데이터를 보호합니다.
* 를 통한 데이터 보호 [암호화 및 시스템 수준 키](#encryption): 데이터 보안은 데이터가 유휴 상태일 때 암호화를 통해 보장됩니다.

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### 액세스 제어 {#access-control}

Adobe Experience Platform의 액세스 제어를 사용하면 다음을 사용할 수 있습니다. [Adobe Admin Console](https://adminconsole.adobe.com/) 역할 기반 권한을 사용하여 쿼리 서비스 기능에 대한 액세스를 관리합니다. 마찬가지로 스키마와 데이터 필드에 대한 레이블 관리를 통해 특정 데이터 속성에 대한 액세스를 제어할 수 있습니다.

이 섹션에서는 쿼리 서비스 기능을 완전히 활용하기 위해 사용자가 보유해야 하는 필수 액세스 제어 권한에 대해 간략히 설명합니다. 의 문서 보기 [권한 관리](../../access-control/ui/permissions.md) 및 [사용자 관리](../../access-control/ui/users.md) 제품 프로필에 대한 액세스 권한을 할당하는 방법에 대한 자세한 지침을 확인하십시오.

#### 관련 권한

관련 액세스 제어 권한은 범위 수준에 따라 아래 표에 정의되어 있습니다.

**쿼리 실행 권한**

쿼리 서비스 내에서 쿼리를 실행하려면 사용자에게 다음 권한이 있는 역할을 할당해야 합니다.

| 사용 권한 | 설명 |
|---|---|
| [!UICONTROL 쿼리 관리] | 이 권한을 사용하면 데이터 탐색 및 일괄 처리 쿼리를 실행하여 기존 데이터 세트를 읽거나 데이터 세트에 데이터를 쓸 수 있습니다. 여기에는 두 가지가 모두 포함됩니다 `CREATE TABLE AS SELECT` (`CTAS`) 및 `INSERT INTO AS SELECT` (`ITAS`) 쿼리. |

**데이터 세트 권한**

이 섹션은 쿼리 서비스를 통해 데이터를 쿼리하는 동안 데이터 세트에 액세스하는 데 필요한 리소스 기반 액세스 가이드 역할을 합니다.

권한 인터페이스를 통해 다음 권한을 사용하여 데이터 세트 및 스키마에 대한 리소스 기반 액세스 제어를 정의할 수 있습니다.

| 사용 권한 | 설명 |
|---|---|
| [!UICONTROL 데이터 세트 관리] | 이 권한은 스키마에 대한 읽기 전용 액세스를 제공하며 쿼리 서비스와 함께 사용할 데이터 세트를 읽기, 만들기, 편집 및 삭제할 수 있는 액세스를 허용합니다. |
| [!UICONTROL 데이터 세트 보기] | 이 권한은 쿼리 서비스와 함께 사용할 데이터 세트 및 스키마에 대한 읽기 전용 액세스를 허용합니다. |

#### 열/필드에 대한 액세스 제어

속성 기반 액세스 제어 기능을 사용하면 쿼리 서비스 사용자가 중요한 사용자 데이터에 대한 액세스를 제한할 수 있습니다. 액세스 권한은 역할에 할당된 권한에 따라 부여되거나 제한될 수 있습니다. 개별 열에 대한 사용자 액세스는 관련 데이터 사용 레이블 및 사용자에게 할당된 역할에 적용되는 권한 집합에 의해 제어됩니다.

데이터 사용 레이블이 있는 스키마 필드 그룹 및 클래스에 태그를 지정하면 필드 그룹 및 클래스가 동일한 모든 스키마에 데이터 사용 제한이 적용됩니다. 의 개요 보기 [속성 기반 액세스 제어](../../access-control/abac/overview.md) 를 참조하십시오.

이 기능을 사용하면 선택한 사용자 그룹에 기밀 열에 대한 액세스 권한을 부여할 수 있습니다. 열에 대한 액세스 제어를 사용하면 특정 유형의 사용자에 대해 읽기 및 쓰기 기능을 모두 제한할 수 있습니다.

열에 대한 액세스 제어는 표준 및 임시 스키마 모두에 대해 스키마 수준에서 적용할 수 있습니다. XDM 스키마에 데이터 사용 레이블을 적용하여 하나 이상의 열에 대한 액세스를 제한합니다. 데이터 레이블 지정은 CTAS 작업의 일부로 생성된 사전 정의된 스키마 또는 애드혹 스키마를 사용하여 쿼리 서비스를 통해 생성된 데이터 세트에 대해서도 일관되게 적용됩니다.

레이블과 역할을 사용하여 적절한 액세스 수준이 적용되면 사용자가 액세스할 수 없는 데이터에 액세스하려고 하면 다음과 같은 시스템 동작이 발생합니다.

1. 사용자에게 스키마 내의 열 중 하나에 대한 액세스가 거부된 경우 제한된 열에 대한 읽기 또는 쓰기 권한도 거부됩니다. 이는 다음과 같은 일반적인 시나리오에 적용됩니다.

   * **사례 1**: 사용자가 제한된 열에만 영향을 주는 쿼리를 실행하려고 하면 열이 존재하지 않는다는 오류가 발생합니다.
   * **사례 2**: 사용자가 제한된 열을 포함하는 여러 열로 쿼리를 실행하려고 하면 시스템이 제한되지 않은 모든 열에 대한 출력만 반환합니다.

1. 사용자가 계산된 필드에 액세스하려고 하면 사용자는 컴포지션에 사용되는 모든 필드에 액세스해야 하거나 시스템에서 계산된 필드에 대한 액세스를 거부합니다.

#### 보기에 대한 액세스 제어

쿼리 서비스는에 표준 ANSI SQL을 사용하는 기능을 제공합니다. [`CREATE VIEW`](../sql/syntax.md#create-view) 명령문입니다. 중요한 데이터 워크플로우의 경우 보기를 만들 때 적절한 제어를 적용해야 합니다.

다음 `CREATE VIEW` 키워드는 질의 뷰를 정의하지만 뷰가 물리적으로 구체화되지 않습니다. 대신 쿼리에서 보기를 참조할 때마다 쿼리가 실행됩니다. 사용자가 데이터 세트에서 보기를 만들 때 상위 데이터 세트에 대한 역할 및 속성 기반 액세스 제어 규칙은 다음과 같습니다 **아님** 계층적으로 적용되었습니다. 따라서 보기를 만들 때 각 열에 대한 권한을 명시적으로 설정해야 합니다.

#### 가속화된 데이터 세트에 대한 필드 기반 액세스 제한 사항 만들기 {#create-field-based-access-restrictions-on-accelerated-datasets}

포함 [속성 기반 액세스 제어 기능](../../access-control/abac/overview.md) 에서 팩트 및 차원 데이터 세트에 대한 조직 또는 데이터 사용 범위를 정의할 수 있습니다. [가속 저장소](../data-distiller/query-accelerated-store/send-accelerated-queries.md). 이를 통해 관리자는 특정 세그먼트에 대한 액세스를 관리하고 사용자 또는 사용자 그룹에 부여된 액세스를 더 잘 관리할 수 있습니다.

가속화된 데이터 세트에 대한 필드 기반 액세스 제한을 만들려면 쿼리 서비스 CTAS 쿼리를 사용하여 가속화된 데이터 세트를 만들고 기존 XDM 스키마 또는 애드혹 스키마를 기반으로 이러한 데이터 세트를 구조화할 수 있습니다. 그러면 관리자는 [스키마에 대한 데이터 사용 레이블 추가 및 편집](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) 또는 [애드혹 스키마](./ad-hoc-schema-labels.md#edit-governance-labels). 다음에서 스키마에 레이블을 적용, 생성 및 편집할 수 있습니다. [!UICONTROL 레이블] 의 작업 공간 [!UICONTROL 스키마] UI.

데이터 사용 레이블은 [데이터 세트에 바로 적용되거나 편집됨](../../data-governance/labels/user-guide.md#add-labels) 데이터 세트 UI를 통하거나 액세스 제어에서 생성합니다. [!UICONTROL 레이블] 작업 영역. 방법은 안내서 참조 [새 레이블 만들기](../../access-control/abac/ui/labels.md) 추가 정보.

개별 열에 대한 사용자 액세스는 첨부된 데이터 사용 레이블 및 사용자에게 할당된 역할에 적용되는 권한 세트에 의해 제어될 수 있습니다.

### 연결 {#connectivity}

쿼리 서비스는 Platform UI를 통해 또는 외부 호환 클라이언트와 연결을 형성하여 액세스할 수 있습니다. 사용 가능한 모든 프론트에 대한 액세스는 자격 증명 집합에 의해 제어됩니다.

#### 외부 클라이언트를 통한 연결

서드파티 클라이언트를 사용하여 쿼리 서비스에 액세스하려면 인증을 위한 자격 증명이 필요합니다. 이러한 자격 증명은 호환되는 외부 클라이언트에서 Query Service에 액세스하는 데 필요합니다. 다음 중 하나를 사용하여 외부 클라이언트에 연결할 수 있습니다 [자격 증명 만료](#expiring-credentials) 또는 [만료되지 않는 자격 증명](#non-expiring-credentials).

#### 만료 자격 증명을 통한 제한된 연결 시간 {#expiring-credentials}

[자격 증명 만료](../ui/credentials.md) 사용자가 외부 클라이언트와 임시 연결을 구성할 수 있도록 허용합니다. 이 자격 증명 집합은 24시간 동안만 유효합니다. 이러한 유형의 자격 증명 만료는 쿼리 서비스 대시보드의 자격 증명 탭과 함께 볼 수 있습니다.

![만료 자격 증명이 강조 표시된 쿼리 서비스 작업 영역의 자격 증명 탭입니다.](../images/data-governance/overview/expiring-credentials.png)

#### 만료되지 않는 자격 증명 {#non-expiring-credentials}

[만료되지 않는 자격 증명](../ui/credentials.md#non-expiring-credentials) 외부 클라이언트와의 영구 연결을 구성할 수 있으므로 수동 암호 없이도 Query Service에 쉽게 연결할 수 있습니다.

만료되지 않는 자격 증명을 생성하는 옵션을 활성화하려면 설명된 대로 해야 합니다 [전제 조건 워크플로](../ui/credentials.md#prerequisites). 이 프로세스의 일부로, 조직 관리자가 제품 프로필에 대한 권한을 구성해야 하며, 관리자가 만료되지 않는 자격 증명을 사용할 수 있는 액세스 권한을 보유할 수 있습니다.

만료되지 않는 자격 증명으로 허용된 기술 사용자 계정에는 역할로 할당하여 책임 및 요구 사항에 따라 읽기 및 쓰기 액세스 범위를 정의하여 적절한 데이터 거버넌스를 보장할 수 있습니다. 의 이전 섹션 참조 [액세스 제어를 통해 역할 기반 권한 사용](#access-control) 쿼리 서비스에 대한 액세스를 관리합니다.

필수 구성 요소 워크플로가 완료되면 이제 권한이 있는 사용자가 작업을 수행할 수 있습니다 [필요한 연결 자격 증명 생성](../ui/credentials.md#generate-credentials).

#### SSL 데이터 암호화

보안 강화를 위해 Query Service는 클라이언트/서버 통신을 암호화하기 위한 SSL 연결을 기본적으로 지원합니다. 플랫폼은 사용자의 데이터 보안 요구 사항에 맞게 다양한 SSL 옵션을 지원하며 암호화 및 키 교환의 처리 오버헤드를 조정합니다.

사용 가능한 설명서 참조 [쿼리 서비스에 대한 타사 클라이언트 연결을 위한 SSL 옵션](../clients/ssl-modes.md) 를 사용하여 연결하는 방법 등 자세한 내용은 `verify-full` SSL 매개 변수 값입니다.

### 암호화 {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

암호화는 데이터를 암호화하고 읽을 수 없는 텍스트로 변환하는 알고리즘 프로세스를 사용하여 암호 해독 키 없이 정보를 보호하고 액세스할 수 없도록 합니다.

Query Service 데이터 규정 준수는 데이터가 항상 암호화되도록 합니다. 전송 중인 데이터는 항상 HTTPS를 준수하며 사용하지 않는 데이터는 시스템 수준 키를 사용하여 Azure Data Lake 저장소에서 암호화됩니다. 다음에서 설명서를 참조하십시오. [Adobe Experience Platform에서 데이터를 암호화하는 방법](../../landing/governance-privacy-security/encryption.md) 추가 정보. 사용하지 않는 데이터를 Azure Data Lake Storage에서 암호화하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [공식 Azure 설명서](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## 감사 {#audit}

쿼리 서비스는 사용자 활동을 기록하고 해당 활동을 다른 로그 유형으로 분류합니다. 다음에 대한 공급 정보를 기록합니다. **사용자** 수행됨 **내용** 작업 및 **조건**. 로그에 기록된 각 작업에는 작업 유형, 날짜 및 시간, 작업을 수행한 사용자의 이메일 ID 및 작업 유형과 관련된 추가 속성을 나타내는 메타데이터가 포함됩니다.

Platform 사용자가 원하는 대로 모든 로그 범주를 요청할 수 있습니다. 이 섹션에서는 Query Service에 대해 캡처된 정보 유형 및 이 정보에 액세스할 수 있는 위치에 대한 세부 정보를 제공합니다.

### 쿼리 로그 {#query-logs}

쿼리 로그 UI를 사용하면 쿼리 편집기 또는 쿼리 서비스 API를 통해 실행된 모든 쿼리에 대한 실행 세부 정보를 모니터링하고 검토할 수 있습니다. 이렇게 하면 다음에 대한 메타데이터를 확인할 수 있도록 쿼리 서비스 활동이 투명해집니다. **모두** 쿼리 서비스 간에 실행된 쿼리입니다. 탐색적 쿼리, 일괄 처리 쿼리 또는 예약된 쿼리인지에 관계없이 모든 유형의 쿼리가 포함됩니다.

쿼리 로그는 Platform UI의 [!UICONTROL 로그] 의 탭 [!UICONTROL 쿼리] 작업 영역.

![세부 정보 패널이 강조 표시된 쿼리 로그 탭](../images/data-governance/overview/queries-log.png)

### 감사 로그 {#audit-logs}

감사 로그에는 쿼리 로그보다 자세한 정보가 포함되어 있으며 이를 통해 사용자, 날짜, 쿼리 유형 등의 속성을 기준으로 로그를 필터링할 수 있습니다. 감사 로그는 쿼리 로그 UI에서 사용할 수 있는 세부 사항 외에 개별 사용자에 대한 세부 사항을 세션 데이터 또는 서드파티 클라이언트와의 연결과 함께 저장합니다.

감사 추적을 통해 사용자 작업에 대한 정확한 기록을 제공함으로써 문제 해결에 도움을 주고 기업 데이터 관리 정책 및 규정 요구 사항을 효과적으로 준수할 수 있습니다. 감사 로그는 모든 플랫폼 활동에 대한 기록을 제공합니다. 감사 로그를 사용하여 쿼리 실행, 템플릿 및 예약된 쿼리와 관련된 사용자 작업을 감사하여 쿼리 서비스에서 사용자가 수행한 작업의 투명성과 가시성을 높일 수 있습니다.

다음 표는 감사 로그로 캡처된 쿼리 범주와 이들이 기록하는 작업 유형을 나타냅니다.

| 카테고리 | 작업 유형 |
|---|---|
| 쿼리 | 실행 |
| 쿼리 템플릿 | 만들기, 삭제, 업데이트 |
| 예약된 쿼리 | 만들기, 삭제, 업데이트 |

다음은 쿼리 로그에 있는 것보다 더 많은 세부 정보를 포함하는 세 개의 확장 서버 로그 목록입니다. 확장 로그는 감사 로그 쿼리 범주 내에서 찾을 수 있습니다.

1. **메타 쿼리 로그**: 쿼리가 실행되면 다양한 관련 백엔드 하위 쿼리(예: 구문 분석)가 실행됩니다. 이러한 유형의 쿼리를 &quot;메타데이터&quot; 쿼리라고 합니다. 감사 로그에서 관련 세부 정보를 확인할 수 있습니다.
1. **세션 로그**: 시스템은 사용자가 쿼리를 실행하는지 여부에 관계없이 쿼리 서비스에 로그인할 때 사용자에 대한 세션 항목 로그를 생성합니다.
1. **타사 클라이언트 연결 로그**: 사용자가 쿼리 서비스를 타사 클라이언트에 연결하면 연결 감사 로그가 생성됩니다.

다음을 참조하십시오. [감사 로그 개요](../../landing/governance-privacy-security/audit-logs/overview.md) 감사 로그가 데이터 규정 준수에 접근하는 데 어떻게 도움이 되는지에 대한 자세한 정보.

## 데이터 사용 {#data-usage}

플랫폼의 데이터 거버넌스 프레임워크는 모든 Adobe 솔루션, 서비스 및 플랫폼에서 데이터를 책임감 있게 사용할 수 있는 동일한 방법을 제공합니다. Adobe Experience Cloud 전체에서 메타데이터를 캡처, 통신 및 사용하는 시스템 접근 방식을 조정합니다. 이렇게 하면 데이터 제어자가 필요한 마케팅 작업과 이러한 의도된 마케팅 작업에서 해당 데이터에 지정된 제한 사항에 따라 데이터에 레이블을 지정하는 데 도움이 됩니다. 의 개요 보기 [데이터 사용 레이블](../../data-governance/labels/overview.md) 데이터 거버넌스에서 데이터 세트 및 필드에 데이터 사용 레이블을 적용하는 방법에 대한 자세한 내용을 보려면 를 참조하십시오.

데이터 여정의 모든 단계에서 데이터 규정 준수를 위해 작업하는 것이 가장 좋습니다. 이를 위해 임시 스키마를 사용하는 파생된 데이터 세트는 데이터 거버넌스 프레임워크의 일부로 적절하게 레이블이 지정되어야 합니다. Query Service에서 형성되는 파생 데이터 세트에는 표준 스키마를 사용하는 데이터 세트와 애드혹 스키마를 사용하는 데이터 세트, 이렇게 두 가지 유형이 있습니다.

>[!NOTE]
>
>쿼리 서비스를 사용하여 만든 데이터 세트를 &quot;파생 데이터 세트&quot;라고 합니다.

애드혹 스키마는 특정 목적을 위해 개별 사용자에 의해 생성되므로 XDM 스키마 필드는 해당 특정 데이터 세트에 대해 네임스페이스가 지정되며 다른 데이터 세트에서 사용하기 위한 것이 아닙니다. 따라서 임시 스키마는 기본적으로 Experience Platform UI에 표시되지 않습니다. 표준 스키마와 애드혹 스키마 간에 데이터 사용 레이블 적용에 차이가 없지만 레이블 지정을 위해 쿼리 서비스에서 생성한 애드혹 스키마는 먼저 Platform UI에 표시해야 합니다. 다음 안내서를 참조하십시오 [Platform UI에서 애드혹 스키마 검색](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) 을 참조하십시오.

스키마에 액세스한 후에는 다음 작업을 수행할 수 있습니다 [개별 필드에 레이블 적용](../../xdm/tutorials/labels.md). 스키마에 레이블이 지정되면 해당 스키마에서 파생된 모든 데이터 세트는 해당 레이블을 상속합니다. 여기에서 특정 레이블이 있는 데이터의 활성화를 특정 대상으로 제한할 수 있는 데이터 사용 정책을 설정할 수 있습니다. 자세한 내용은 의 개요를 참조하십시오. [데이터 사용 정책](../../data-governance/policies/overview.md).

## 개인정보 보호 {#privacy}

[Privacy Service](../../privacy-service/home.md) 는 법적 개인 정보 보호 규정에 따라 고객의 데이터 액세스 및 삭제 요청을 관리하는 데 도움이 됩니다. 이렇게 하려면 데이터에 기존 식별자를 검색하고 요청된 개인 정보 작업에 따라 해당 데이터에 액세스하거나 삭제합니다. 서비스에서 개인 정보 보호 작업 중에 액세스하거나 삭제할 필드를 결정하려면 데이터에 올바른 레이블을 지정해야 합니다. 개인 정보 보호 요청의 대상이 되는 데이터는 다양한 데이터를 개인 정보 보호 요청이 적용되는 개별 사용자와 연결하기 위해 고객 ID 정보를 포함해야 합니다. Query Service는 개인 정보 보호 작업을 충족하기 위해 고유 식별자로 사용하는 데이터를 보강할 수 있습니다.

개인 정보 보호 요청은 데이터 레이크 또는 프로필 데이터 저장소로 전송될 수 있습니다. 데이터 레이크에서 삭제된 레코드는 해당 레코드에서 만든 프로필을 삭제하지 않습니다. 또한 데이터 레이크에서 개인 정보를 삭제하는 개인 정보 작업은 프로필을 삭제하지 않으므로 개인 정보 작업 완료 후 수집된 정보(해당 프로필 ID가 포함)는 해당 프로필을 정상적으로 업데이트합니다. 이렇게 하면 임시 스키마에 사용되는 데이터를 제대로 식별해야 하는 필요성이 재확인됩니다.

자세한 내용은 Privacy Service 설명서 를 참조하십시오. [개인 정보 보호 요청에 대한 id 데이터](../../privacy-service/identity-data.md) 및 데이터 작업을 구성하고 Adobe 기술을 활용하여 고객 개인 정보 보호 요청에 적절한 id 정보를 효과적으로 검색하는 방법.

데이터 거버넌스를 위한 쿼리 서비스 기능은 데이터 분류 프로세스 및 데이터 사용 규정 준수를 간소화하고 간소화합니다. 데이터가 식별되면 쿼리 서비스를 사용하여 모든 출력 데이터 세트에 기본 ID를 할당할 수 있습니다. 본인 **필수** 데이터 개인 정보 보호 요청을 용이하게 하고 데이터 규정 준수를 위해 데이터 세트에 id를 추가합니다.

스키마 데이터 필드는 Platform UI를 통해 ID 필드로 설정할 수 있으며, 쿼리 서비스를 통해 다음을 수행할 수도 있습니다. [sql 명령 &#39;ALTER TABLE&#39;을 사용하여 기본 ID 표시](../sql/syntax.md#alter-table). 를 사용하여 ID 설정 `ALTER TABLE` 명령은 Platform UI를 통해 스키마에서 직접 만드는 것이 아니라 SQL을 사용하여 데이터 세트를 만들 때 특히 유용합니다. 방법에 대한 지침은 설명서 를 참조하십시오 [ui에서 id 필드 정의](../../xdm/ui/fields/identity.md) 표준 스키마를 사용하는 경우입니다.

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
