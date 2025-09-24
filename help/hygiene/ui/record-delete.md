---
title: 삭제 요청 기록(UI 워크플로)
description: Adobe Experience Platform UI에서 레코드를 삭제하는 방법을 알아봅니다.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: a25187339a930f7feab4a1e0059bc9ac09f1a707
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 5%

---

# 삭제 요청 기록(UI 워크플로) {#record-delete}

[[!UICONTROL 데이터 주기] 작업 영역](./overview.md)을(를) 사용하여 기본 ID를 기반으로 Adobe Experience Platform에서 레코드를 삭제합니다. 이러한 레코드는 개별 소비자 또는 ID 그래프에 포함된 다른 엔티티에 연결할 수 있습니다.

>[!IMPORTANT]
>
>레코드 삭제는 데이터 정리, 익명 데이터 제거 또는 데이터 최소화에 사용됩니다. GDPR(일반 데이터 보호 규정)과 같은 개인 정보 보호 규정과 관련된 데이터 주체 권한 요청(준수)에 사용할 **not**&#x200B;입니다. 모든 규정 준수 사용 사례의 경우 대신 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md)을(를) 사용하십시오.

## 전제 조건 {#prerequisites}

레코드를 삭제하려면 Experience Platform에서 ID 필드가 작동하는 방식을 이해해야 합니다. 특히 삭제할 데이터 세트(또는 데이터 세트)에 따라 레코드를 삭제할 엔티티의 ID 네임스페이스 값을 알고 있어야 합니다.

Experience Platform의 ID에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Adobe Experience Platform ID 서비스](../../identity-service/home.md): 장치와 시스템 간에 ID를 브리징하여 준수하는 XDM 스키마에 의해 정의된 ID 필드를 기반으로 데이터 세트를 함께 연결합니다.
* [ID 네임스페이스](../../identity-service/features/namespaces.md): ID 네임스페이스는 한 사람과 관련된 다양한 유형의 ID 정보를 정의하며 각 ID 필드에 필요한 구성 요소입니다.
* [실시간 고객 프로필](../../profile/home.md): ID 그래프를 사용하여 실시간으로 업데이트되는 여러 소스의 집계 데이터를 기반으로 통합 소비자 프로필을 제공합니다.
* [XDM(경험 데이터 모델)](../../xdm/home.md): 스키마를 사용하여 Experience Platform 데이터에 대한 표준 정의 및 구조를 제공합니다. 모든 Experience Platform 데이터 세트는 특정 XDM 스키마를 준수하며, 스키마는 ID인 필드를 정의합니다.
* [ID 필드](../../xdm/ui/fields/identity.md): XDM 스키마에서 ID 필드를 정의하는 방법을 알아봅니다.

## 요청 만들기 {#create-request}

프로세스를 시작하려면 Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 데이터 수명 주기]**&#x200B;를 선택하십시오. [!UICONTROL 데이터 주기 요청] 작업 영역이 나타납니다. 그런 다음 작업 영역의 기본 페이지에서 **[!UICONTROL 요청 만들기]**&#x200B;를 선택합니다.

![[!UICONTROL 요청 만들기]가 선택된 [!UICONTROL 데이터 주기 요청] 작업 영역](../images/ui/record-delete/create-request-button.png)

요청 생성 워크플로가 나타납니다. 기본적으로 **[!UICONTROL 요청된 작업]** 섹션에서 **[!UICONTROL 레코드 삭제]** 옵션이 선택됩니다. 이 옵션을 선택된 상태로 두십시오.

>[!IMPORTANT]
> 
>효율성을 개선하고 데이터 세트 운영 비용을 절감하기 위해 델타 포맷으로 이동한 조직은 ID 서비스, 실시간 고객 프로필 및 데이터 레이크에서 데이터를 삭제할 수 있습니다. 이러한 유형의 사용자를 델타 마이그레이션이라고 합니다. 델타 마이그레이션된 조직의 사용자는 단일 데이터 세트 또는 모든 데이터 세트에서 레코드를 삭제할 수 있습니다. 델타 마이그레이션을 수행하지 않은 조직의 사용자는 아래 이미지에 표시된 대로 단일 데이터 세트 또는 모든 데이터 세트에서 레코드를 선택적으로 삭제할 수 없습니다. 이 경우 안내서의 [ID 제공](#provide-identities) 섹션을 계속하십시오.

![레코드 [!UICONTROL 삭제] 옵션을 선택하고 강조 표시한 요청 생성 워크플로우입니다.](../images/ui/record-delete/delete-record.png)

## 데이터 세트 선택 {#select-dataset}

다음 단계는 단일 데이터 세트에서 레코드를 삭제할지 또는 모든 데이터 세트에서 레코드를 삭제할지를 결정하는 것입니다. 조직의 구성에 따라 데이터 세트 선택 옵션을 사용하지 못할 수 있습니다. 이 옵션이 표시되지 않으면 안내서의 [ID 제공](#provide-identities) 섹션을 계속하십시오.

**[!UICONTROL 레코드 세부 정보]** 섹션에서 라디오 단추를 선택하여 특정 데이터 집합 또는 모든 데이터 집합을 선택합니다.

특정 데이터 집합에서 삭제하려면 **[!UICONTROL 데이터 집합 선택]**&#x200B;을 선택한 다음 데이터베이스 아이콘(![데이터베이스 아이콘](/help/images/icons/database.png))을 선택하십시오. 표시되는 대화 상자에서 데이터 세트를 선택하고 **[!UICONTROL 완료]**&#x200B;를 선택하여 확인합니다.

![데이터 세트를 선택하고 [!UICONTROL 완료]를 강조 표시한 상태로 [!UICONTROL 데이터 세트 선택] 대화 상자가 표시됩니다.](../images/ui/record-delete/select-dataset.png)

모든 데이터 세트에서 삭제하려면 **[!UICONTROL 모든 데이터 세트]**&#x200B;를 선택하십시오. 이 옵션은 작업 범위를 늘리며 모든 관련 ID 유형을 제공해야 합니다.

![[!UICONTROL 모든 데이터 세트] 옵션이 선택된 상태로 [!UICONTROL 데이터 세트 선택] 대화 상자가 나타납니다.](../images/ui/record-delete/all-datasets.png)

>[!WARNING]
>
>**[!UICONTROL 모든 데이터 세트]**&#x200B;를 선택하면 작업이 조직의 모든 데이터 세트로 확장됩니다. 각 데이터 세트는 다른 기본 ID 유형을 사용할 수 있습니다. 정확한 일치를 위해 **모든 필수 ID 유형**&#x200B;을 제공해야 합니다.
>
>ID 유형이 누락된 경우 삭제하는 동안 일부 레코드를 건너뛸 수 있습니다. 이로 인해 처리 속도가 느려지고 **일부 결과**&#x200B;이(가) 발생할 수 있습니다.

Experience Platform의 각 데이터 세트는 하나의 기본 ID 유형만 지원합니다.

* **단일 데이터 세트**&#x200B;에서 삭제할 때 요청의 모든 ID는 **동일한 형식**&#x200B;을 사용해야 합니다.
* **모든 데이터 세트**&#x200B;에서 삭제할 때 **여러 ID 유형**&#x200B;을 포함할 수 있습니다. 서로 다른 데이터 세트가 서로 다른 기본 ID를 사용할 수 있기 때문입니다.&quot;

## ID 입력 {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="ID 네임스페이스"
>abstract="ID 네임스페이스는 레코드를 Experience Platform의 소비자 프로필에 연결하는 속성입니다. 데이터 세트의 ID 네임스페이스 필드는 데이터 세트가 기반으로 하는 스키마에 의해 정의됩니다. 이 열에서는 이메일 주소의 경우 `email` 및 Experience Cloud ID의 경우 `ecid` 등 레코드의 ID 네임스페이스 유형(또는 네임스페이스)을 입력해야 합니다. 자세한 내용은 데이터 라이프사이클 UI 안내서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="기본 ID 값"
>abstract="이 열에서는 왼쪽 열에 입력한 ID 유형에 해당되는 레코드의 ID 네임스페이스 값을 입력해야 합니다. ID 네임스페이스 유형이 `email`인 경우 값은 레코드의 이메일 주소이어야 합니다. 자세한 내용은 데이터 라이프사이클 UI 안내서를 참조하십시오."

레코드를 삭제할 때 시스템에서 삭제할 레코드를 결정할 수 있도록 ID 정보를 제공해야 합니다. Experience Platform에 있는 모든 데이터 세트의 경우 데이터 세트의 스키마에 의해 정의된 **ID 네임스페이스** 필드를 기반으로 레코드가 삭제됩니다.

Experience Platform의 모든 ID 필드와 마찬가지로 ID 네임스페이스는 **type**(ID 네임스페이스라고도 함)과 **value**, 이렇게 두 가지로 구성됩니다. ID 유형은 필드가 레코드(예: 이메일 주소)를 식별하는 방법에 대한 컨텍스트를 제공합니다. 값은 해당 형식에 대한 레코드의 특정 ID를 나타냅니다(예: `jdoe@example.com` ID 형식의 경우 `email`). ID로 사용되는 일반적인 필드에는 계정 정보, 디바이스 ID 및 쿠키 ID가 포함됩니다.

>[!TIP]
>
>특정 데이터 세트에 대한 ID 네임스페이스를 모를 경우 Experience Platform UI에서 찾을 수 있습니다. **[!UICONTROL 데이터 세트]** 작업 영역의 목록에서 해당 데이터 세트를 선택합니다. 데이터 세트에 대한 세부 정보 페이지에서 오른쪽 레일의 데이터 세트 스키마 이름 위로 마우스를 가져갑니다. 스키마 이름 및 설명과 함께 ID 네임스페이스가 표시됩니다.
>
>![데이터 집합이 선택된 데이터 집합 대시보드이며 데이터 집합 세부 정보 패널에서 스키마 대화 상자가 열려 있습니다. 데이터 집합의 기본 ID가 강조 표시됩니다.](../images/ui/record-delete/dataset-primary-identity.png)

레코드를 삭제할 때 ID를 제공하는 두 가지 옵션이 있습니다.

* [JSON 파일 업로드](#upload-json)
* [수동으로 기본 ID 값 입력](#manual-identity)

### JSON 파일 업로드 {#upload-json}

JSON 파일을 업로드하려면 파일을 제공된 영역으로 끌어다 놓거나 **[!UICONTROL 파일 선택]**&#x200B;을 선택하여 로컬 디렉터리에서 찾아 선택할 수 있습니다.

![JSON 파일을 업로드하기 위한 파일 선택 및 드래그 앤 드롭 인터페이스가 강조 표시된 요청 생성 워크플로우입니다.](../images/ui/record-delete/upload-json.png)

JSON 파일의 형식은 개체 배열로 지정해야 하며 각 개체는 ID를 나타냅니다.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| 속성 | 설명 |
| --- | --- |
| `namespaceCode` | ID 유형. |
| `value` | 유형으로 표시되는 기본 ID 값입니다. |

파일이 업로드되면 [요청을 계속 제출](#submit)할 수 있습니다.

### ID 수동 입력 {#manual-identity}

ID를 수동으로 입력하려면 **[!UICONTROL ID 추가]**&#x200B;를 선택하십시오.

![ID 추가[!UICONTROL &#x200B; 옵션이 강조 표시된 요청 생성 워크플로우입니다.]](../images/ui/record-delete/add-identity.png)

ID를 한 번에 하나씩 입력할 수 있는 컨트롤이 나타납니다. **[!UICONTROL ID 네임스페이스]**&#x200B;에서 드롭다운 메뉴를 사용하여 ID 유형을 선택합니다. **[!UICONTROL 기본 ID 값]**&#x200B;에서 레코드에 대한 ID 네임스페이스 값을 제공합니다.

![ID 필드가 있는 요청 만들기 워크플로를 수동으로 추가했습니다.](../images/ui/record-delete/identity-added.png)

더 많은 ID를 추가하려면 더하기 아이콘(![더하기 아이콘)을 선택하십시오.](/help/images/icons/tree-expand-all.png)) 행 중 하나 옆에 있거나 **[!UICONTROL ID 추가]**&#x200B;를 선택합니다.

![더하기 아이콘과 ID 추가 아이콘이 강조 표시된 요청 생성 워크플로우입니다.](../images/ui/record-delete/more-identities.png)

## 할당량 및 처리 타임라인 {#quotas}

레코드 삭제 요청은 조직의 라이선스 자격에 따라 결정되는 일별 및 월별 식별자 제출 제한을 따릅니다. 이러한 제한은 UI 및 API 기반 삭제 요청 모두에 적용됩니다.

>[!NOTE]
>
>하루에 최대 **1,000,000개의 식별자를 제출할 수 있습니다**. 단, 남은 월별 할당량이 허용하는 경우에만 제출합니다. 월별 상한이 100만 개 미만인 경우 일일 제출액은 해당 상한을 초과할 수 없습니다.

### 제품별 월별 제출 권한 {#quota-limits}

아래 표에는 제품 및 자격 수준별 식별자 제출 제한이 나와 있습니다. 각 제품에 대해 월간 상한은 고정 식별자 천장이나 사용 허가된 데이터 볼륨에 연결된 백분율 기반 임계값의 두 값 중 적은 값입니다.

| 제품 | 권한 설명 | 월별 상한(둘 중 더 작은 값) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP 또는 Adobe Journey Optimizer | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 식별자 2,000,000개 또는 대응 가능 대상의 5% |
| Real-Time CDP 또는 Adobe Journey Optimizer | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 식별자 15,000,000개 또는 대응 가능 대상의 10% |
| Customer Journey Analytics | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 2,000,000개의 식별자 또는 100개의 식별자/백만 CJA 권한 행당 |
| Customer Journey Analytics | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 15,000,000개의 식별자 또는 100만 개의 CJA 권한 행당 200개의 식별자 |

>[!NOTE]
>
> 대부분의 조직에서는 실제 대응 가능 대상 또는 CJA 행 권한에 따라 월별 제한이 내려집니다.

할당량은 매월 1일에 재설정됩니다. 사용되지 않은 할당량은 **이월되지 않습니다**.

>[!NOTE]
>
>할당량은 **제출된 식별자**&#x200B;에 대한 조직의 라이선스가 부여된 월별 권한을 기반으로 합니다. 이러한 기능은 시스템 가드레일에 의해 적용되지 않지만 모니터링 및 검토 할 수 있습니다.
>
>레코드 삭제는 **공유 서비스**&#x200B;입니다. 월간 캡은 Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics 및 적용 가능한 모든 Shield 추가 기능에 걸쳐 가장 높은 권한을 반영합니다.

### 식별자 제출을 위한 처리 타임라인 {#sla-processing-timelines}

제출 후 레코드 삭제 요청은 자격 수준에 따라 큐에 추가되고 처리됩니다.

| 제품 및 자격 설명 | 대기열 기간 | 최대 처리 시간(SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 최대 15일 | 30일 |
| Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 일반적으로 24시간 | 15일 |

조직에서 더 높은 제한을 필요로 하는 경우 Adobe 담당자에게 권한 검토를 문의하십시오.

>[!TIP]
>
>현재 할당량 사용 또는 권한 계층을 확인하려면 [할당량 참조 안내서](../api/quota.md)를 참조하세요.

## 요청 제출 {#submit}

요청에 ID를 추가했으면 **[!UICONTROL 요청 설정]**&#x200B;에서 **[!UICONTROL 제출]**&#x200B;을 선택하기 전에 요청에 대한 이름과 선택적 설명을 제공하십시오.

>[!TIP]
>
>UI를 통해 요청당 최대 10,000개의 ID를 제출할 수 있습니다. 더 큰 볼륨(요청당 최대 100,000개의 ID)을 제출하려면 [API 메서드](../api/workorder.md#create)를 사용하십시오.

![요청 설정의 [!UICONTROL 이름] 및 [!UICONTROL 설명] 필드에 [!UICONTROL 제출]이 강조 표시되어 있습니다.](../images/ui/record-delete/submit.png)

[!UICONTROL 요청 확인] 대화 상자가 표시되어 삭제 후 ID를 복구할 수 없음을 나타냅니다. 데이터를 삭제할 ID 목록을 확인하려면 **[!UICONTROL 제출]**&#x200B;을 선택하십시오.

![[!UICONTROL 요청 확인] 대화 상자](../images/ui/record-delete/confirm-request.png)

요청이 제출되면 작업 순서가 만들어지고 [!UICONTROL 데이터 주기] 작업 영역의 [!UICONTROL 레코드] 탭에 나타납니다. 여기에서 요청을 처리할 때 작업 주문의 상태를 모니터링할 수 있습니다.

>[!NOTE]
>
>레코드 삭제가 실행되면 처리되는 방법에 대한 자세한 내용은 [타임라인 및 투명도](../home.md#record-delete-transparency)의 개요 섹션을 참조하십시오.

![새 요청이 강조 표시된 [!UICONTROL 데이터 주기] 작업 영역의 [!UICONTROL 레코드] 탭.](../images/ui/record-delete/request-log.png)

## 모델 기반 데이터 세트에서 레코드 삭제 {#model-based-record-delete}

삭제하려는 데이터 세트가 모델 기반 스키마인 경우 다음 고려 사항을 검토하여 Experience Platform과 소스 시스템 간의 불일치로 레코드가 올바르게 제거되고 다시 수집되지 않는지 확인하십시오.

### 레코드 삭제 동작

다음 표에서는 수집 방법 및 데이터 캡처 구성 변경에 따라 Experience Platform 및 소스 시스템 간에 레코드 삭제가 작동하는 방식을 간략하게 설명합니다.

| Aspect | 비헤이비어 |
|---------------------|--------------------------------------------------------------------------|
| 플랫폼 삭제 | 레코드는 Experience Platform 데이터 세트 및 데이터 레이크에서 제거됩니다. |
| Source 유지 | 레코드를 명시적으로 삭제하지 않는 한 소스 시스템에 남아 있습니다. |
| 전체 새로 고침 영향 | 전체 새로 고침을 사용하는 경우 삭제된 레코드는 소스에서 제거하거나 제외하지 않는 한 다시 수집할 수 있습니다. |
| 데이터 캡처 동작 변경 | `_change_request_type = 'd'`(으)로 플래그가 지정된 레코드가 수집 중에 삭제됩니다. 플래그가 지정되지 않은 레코드는 다시 수집할 수 있습니다. |

다시 수집하지 않도록 하려면 두 시스템에서 레코드를 제거하거나 삭제할 레코드에 대한 `_change_request_type = 'd'`을(를) 포함하여 소스 시스템과 Experience Platform 모두에서 동일한 삭제 방법을 적용하십시오.

### 데이터 캡처 및 컨트롤 열 변경

변경 데이터 캡처와 함께 소스를 사용하는 모델 기반 스키마는 업스트림에서 삭제를 구분할 때 `_change_request_type` 컨트롤 열을 사용할 수 있습니다. 수집 중에 `d`(으)로 플래그가 지정된 레코드는 데이터 집합에서 삭제되지만 `u`(으)로 또는 열 없이 플래그가 지정된 레코드는 업데이트로 처리됩니다. `_change_request_type` 열은 수집 시에만 읽으며 대상 스키마에 저장되거나 XDM 필드에 매핑되지 않습니다.

>[!NOTE]
>
>데이터 수명 주기 UI를 통해 레코드를 삭제해도 소스 시스템에는 영향을 주지 않습니다. 두 위치에서 데이터를 제거하려면 Experience Platform과 소스 모두에서 데이터를 삭제합니다.

### 모델 기반 스키마에 대한 추가 삭제 방법

표준 레코드 삭제 워크플로우 외에 모델 기반 스키마는 특정 사용 사례에 대한 추가 메서드를 지원합니다.

* **데이터 세트 안전 복사 접근 방식**: 프로덕션 데이터에 변경 사항을 적용하기 전에 제어된 테스트 또는 조정을 위해 프로덕션 데이터 세트를 복제하고 사본에 삭제를 적용합니다.
* **삭제 전용 일괄 업로드**: 다른 데이터에 영향을 주지 않고 특정 레코드를 제거해야 하는 경우 대상 위생에 대한 삭제 작업만 포함된 파일을 업로드합니다.

### 위생 작업에 대한 설명자 지원 {#descriptor-support}

모델 기반 스키마 설명자는 정확한 위생 작업을 위한 필수 메타데이터를 제공합니다.

* **기본 키 설명자**: 대상 업데이트 또는 삭제에 고유한 레코드를 식별하여 올바른 레코드가 영향을 받는지 확인합니다.
* **버전 설명자**: 삭제 및 업데이트가 올바른 시간 순서대로 적용되도록 하여 순서가 잘못된 작업을 방지합니다.
* **타임스탬프 설명자(시계열 스키마)**: 삭제 작업을 수집 시간이 아닌 이벤트 발생 시간에 맞춥니다.

>[!NOTE]
>
>위생 프로세스는 데이터 세트 수준에서 작동합니다. 프로필 지원 데이터 세트의 경우 실시간 고객 프로필 간에 일관성을 유지하기 위해 추가 프로필 워크플로우가 필요할 수 있습니다.

### 모델 기반 스키마에 대한 예약된 보존

특정 ID가 아닌 데이터 연령을 기반으로 한 자동화된 위생에 대해서는 데이터 레이크에서 예약된 행 수준 보존에 대한 [경험 이벤트 TTL(데이터 집합 보존) 관리](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md)를 참조하십시오.

>[!NOTE]
>
>행 수준 만료는 시계열 동작을 사용하는 데이터 세트에 대해서만 지원됩니다.

### 모델 기반 레코드 삭제 우수 사례

의도하지 않은 재수집을 방지하고 시스템 간 데이터 일관성을 유지하려면 다음 모범 사례를 따르십시오.

* **삭제 조정**: 레코드 삭제를 변경 데이터 캡처 구성 및 소스 데이터 관리 전략과 맞춥니다.
* **변경 데이터 캡처 흐름 모니터링**: 플랫폼에서 레코드를 삭제한 후 데이터 흐름을 모니터링하고 소스 시스템이 동일한 레코드를 제거하거나 `_change_request_type = 'd'`에 포함하는지 확인합니다.
* **소스 정리**: 전체 새로 고침 수집을 사용하는 소스 또는 변경 데이터 캡처를 통한 삭제를 지원하지 않는 소스의 경우 다시 수집하지 않도록 소스 시스템에서 직접 레코드를 삭제하십시오.

스키마 요구 사항에 대한 자세한 내용은 [모델 기반 스키마 설명자 요구 사항](../../xdm/schema/model-based.md#model-based-schemas)을 참조하십시오.\
변경 데이터 캡처가 소스에서 작동하는 방식에 대해 알아보려면 [소스에서 변경 데이터 캡처 사용](../../sources/tutorials/api/change-data-capture.md#using-change-data-capture-with-model-based-schemas)을 참조하세요.

## 다음 단계

이 문서에서는 Experience Platform UI에서 레코드를 삭제하는 방법을 다룹니다. UI에서 다른 데이터 수명 주기 관리 작업을 수행하는 방법에 대한 자세한 내용은 [데이터 수명 주기 UI 개요](./overview.md)를 참조하십시오.

데이터 위생 API를 사용하여 레코드를 삭제하는 방법에 대해 알아보려면 [작업 주문 끝점 안내서](../api/workorder.md)를 참조하세요.
