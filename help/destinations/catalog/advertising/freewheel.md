---
title: FreeWheel 연결
description: 연결된 TV, 디스플레이 및 비디오 인벤토리에서 프로그래밍 방식 광고를 위해 Adobe Experience Platform에서 FreeWheel로 대상을 활성화하는 방법에 대해 알아봅니다.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
exl-id: 1f1d3e57-a8ef-4971-b3d1-43521bd158bb
source-git-commit: 705e94b13af6830916e7d4bf500c48ae1be88874
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 8%

---

# [!DNL FreeWheel] 연결 {#freewheel}

>[!AVAILABILITY]
>
>[!DNL FreeWheel] 대상은 현재 Beta에 있으며 일부 고객에게만 제공됩니다. 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오.

## 개요 {#overview}

[!DNL FreeWheel]은(는) 연결된 TV(CTV), 비디오 및 디스플레이 인벤토리에서 프로그래밍 방식의 구매 및 판매를 지원하는 글로벌 광고 기술 플랫폼입니다. [!DNL FreeWheel]은(는) 광고주와 전 세계 프리미엄 미디어 소유자를 연결하는 데이터 기반 마켓플레이스를 제공합니다.

이 대상을 사용하여 Adobe Experience Platform에서 [!DNL FreeWheel]&#x200B;(으)로 대상자를 보냅니다. 대상자는 일일 배치 파일로 제공되며 [!DNL FreeWheel]개의 거래 및 캠페인에서 타깃팅에 사용할 수 있습니다.

## 전제 조건 {#prerequisites}

대상자를 [!DNL FreeWheel]에 활성화하기 전에 다음 요구 사항을 검토하십시오.

* **FreeWheel 네트워크 ID**: 올바른 [!DNL FreeWheel] 네트워크 ID가 있어야 합니다. 계정을 설정할 때 [!DNL FreeWheel]에서 제공합니다.

## 지원되는 ID {#supported-identities}

[!DNL FreeWheel]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. 이러한 ID 외에도 [!DNL FreeWheel] 계정에서 사용할 수 있는 모든 ID를 사용할 수 있습니다. 아래 표에 없는 ID를 매핑하는 방법에 대한 지침은 [특성 및 ID 매핑](#map)을 참조하십시오. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 타겟 ID | 설명 | 고려 사항 |
|---|---|---|
| `idfa` | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| `aaid` | ANDROID ADVERTISING ID | 소스 ID가 GAID 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| `ctv` | 연결된 TV 장치 ID | CTV 디바이스를 타깃팅할 때 이 타겟 ID를 선택합니다. |
| `ip` | IPv4 주소 | IP 주소를 기준으로 사용자를 타겟팅하려면 이 타겟 ID를 선택하십시오. 유효한 IPv4 주소가 포함된 프로필 속성을 매핑하거나 계산된 필드를 사용하여 값을 파생합니다. |
| `ipv6` | IPv6 주소 | IPv6 주소를 기준으로 사용자를 타깃팅하려면 이 대상 ID를 선택하십시오. 유효한 IPv6 주소가 포함된 프로필 속성을 매핑하거나 계산된 필드를 사용하여 값을 파생합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 예 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | 예 | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li>CSV 파일에서 Experience Platform으로 사용자 지정 업로드 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience),</li><li>유사 대상,</li><li>페더레이션 대상,</li><li>Adobe Journey Optimizer과 같은 다른 Experience Platform 앱에서 생성된 대상자</li><li>등.</li></ul> |

{style="table-layout:auto"}

대상 데이터 유형별 지원되는 대상:

| 대상 데이터 유형 | 지원됨 | 설명 | 사용 사례 |
|--------------------|-----------|-------------|-----------|
| [사람 대상](/help/segmentation/types/people-audiences.md) | 예 | 고객 프로필을 기반으로 마케팅 캠페인을 위해 특정 사용자 그룹을 타깃팅할 수 있습니다. | CTV 재타겟팅, 도달 억제 |
| [계정 대상자](/help/segmentation/types/account-audiences.md) | 아니요 | 계정 기반 마케팅 전략을 위해 특정 조직 내의 개인을 타깃팅합니다. | B2B 마케팅 |
| [잠재 고객](/help/segmentation/types/prospect-audiences.md) | 아니요 | 아직 고객이 아니지만 타겟 대상자와 특성을 공유하는 개인을 타겟팅합니다. | 타사 데이터를 이용한 잠재 고객 확보 |
| [데이터 집합 내보내기](/help/catalog/datasets/overview.md) | 아니요 | Adobe Experience Platform 데이터 레이크에 저장된 구조화된 데이터의 컬렉션입니다. | 보고, 데이터 과학 워크플로 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Profile-based]** | [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)의 매핑 단계에서 선택한 원하는 ID 필드와 함께 대상의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL Batch]** | 첫 번째 내보내기는 활성화된 대상에 적합한 모든 프로필의 전체 스냅샷입니다. 이후 내보내기는 새로운 대상 자격(추가) 및 대상 종료(제거)를 포함하는 일별 증분 업데이트입니다. 또한 구성 가능한 전체 대상 새로 고침 간격(4, 8 또는 12주)을 사용할 수 있으므로 일별 증분 외에 정기적인 전체 내보내기를 트리거할 수 있습니다. 전체 내보내기에는 현재 자격을 갖춘 프로필만 포함됩니다. 대상자 종료는 포함되지 않으며 일별 증분 업데이트를 통해서만 제공됩니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

[!DNL FreeWheel] 대상에 대한 인증은 Adobe에서 자동으로 처리됩니다. 인증 중에 자격 증명이나 API 키가 필요하지 않습니다. Adobe이 귀하를 대신하여 [!DNL FreeWheel]에 대한 보안 연결을 관리합니다.

![FreeWheel 대상에 대한 인증 단계의 스크린샷입니다.](../../assets/catalog/advertising/freewheel/connect-destination.png)

대상 세부 사항 단계로 진행하려면 **[!UICONTROL Connect to destination]**&#x200B;을(를) 선택하십시오.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_freewheel_backfill"
>title="전체 대상 새로 고침 간격"
>abstract="일일 증분 업데이트 외에 전체 대상 내보내기를 [!DNL FreeWheel]&#x200B;(으)로 보낼 간격을 선택하십시오. 전체 대상 내보내기를 사용하면 대상 구성원이 [!DNL FreeWheel]에서 만료되지 않으므로 캠페인이 실행되는 동안 대상 구성원의 드롭다운이 발생하지 않습니다. 사용 가능한 옵션은 4주, 8주 및 12주입니다."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![FreeWheel 대상에 대한 세부 정보를 채우는 방법을 보여 주는 샘플 스크린샷입니다.](../../assets/catalog/advertising/freewheel/destination-details.png)

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Region]**: 계정이 호스팅되는 [!DNL FreeWheel] 지역입니다. 다음 옵션 중 하나를 선택합니다.
   * **[!UICONTROL US East]**
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Asia Pacific]**
* **[!UICONTROL FreeWheel network ID]**: [!DNL FreeWheel] 네트워크 ID입니다. 이 값은 [!DNL FreeWheel]에서 제공하며 [!DNL FreeWheel] 플랫폼에서 조직을 고유하게 식별합니다.
* **[!UICONTROL Full audience refresh interval]**: 일일 증분 업데이트 외에 전체 대상 내보내기가 [!DNL FreeWheel]&#x200B;(으)로 전송되는 빈도입니다. 전체 대상 내보내기를 사용하면 대상 구성원이 [!DNL FreeWheel]에서 만료되지 않으므로 캠페인이 실행되는 동안 대상 구성원의 드롭다운이 발생하지 않습니다. 드롭다운에서 간격을 선택합니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
>
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 대상자 내보내기 예약 {#schedule}

![FreeWheel 활성화 워크플로에서 예약 단계의 스크린샷입니다.](../../assets/catalog/advertising/freewheel/scheduling.png)

**[!UICONTROL Scheduling]** 단계에서 각 대상에 대한 내보내기 일정을 구성합니다. [!DNL FreeWheel]은(는) 하이브리드 내보내기 모델을 사용합니다. 활성화된 각 대상에 대한 첫 번째 내보내기는 전체 스냅숏 다음에 일별 증분 업데이트가 옵니다.

다음 필드를 구성합니다.

* **[!UICONTROL File export options]**: **[!UICONTROL Export incremental files]**&#x200B;이(가) 미리 선택되었으며 유일하게 지원되는 옵션입니다. 첫 번째 내보내기에는 모든 적격 프로필에 대한 전체 스냅샷이 자동으로 포함됩니다. 이후 내보내기는 마지막 내보내기 이후 새로운 대상 자격 요건 및 종료만 제공합니다.
* **[!UICONTROL Frequency]**: **[!UICONTROL Daily]** 선택. [!DNL FreeWheel]에 매일 증분 파일 배달이 필요합니다.
* **[!UICONTROL Scheduled start time]**: 일별 내보내기를 실행할 시간을 UTC로 입력하십시오.
* **[!UICONTROL Date]**: 활성화의 시작 및 종료 날짜를 설정합니다. 시작 날짜는 첫 번째 전체 스냅샷 내보내기가 전송되는 시기를 결정합니다.

>[!NOTE]
>
>전체 내보내기(초기 스냅샷 및 주기적 전체 새로 고침 모두)에는 현재 정규화된 프로필만 포함됩니다. 대상 종료는 전체 내보내기에 포함되지 않으며 일별 증분 업데이트를 통해서만 전달됩니다.

### 속성 및 ID 매핑 {#map}

매핑 단계에서 Experience Platform 프로필에서 소스 필드를 선택하고 [!DNL FreeWheel]에서 지원하는 ID 유형에 매핑합니다. 하나 이상의 매핑이 필요합니다.

>[!IMPORTANT]
>
>[!DNL FreeWheel] 지원 ID 유형은 ID 네임스페이스가 아닌 매핑 UI에서 **타겟 특성**(으)로 표시됩니다.

[!DNL FreeWheel] 계정이 [지원되는 ID](#supported-identities) 표에 나열되지 않은 ID 유형을 지원하는 경우 사전 정의된 목록에서 선택하는 대신 대상 필드에 ID 이름을 수동으로 입력하여 해당 ID에 매핑할 수 있습니다.

![매핑 단계에서 대상 필드에 직접 입력된 사용자 지정 ID 이름을 보여주는 스크린샷입니다.](../../assets/catalog/advertising/freewheel/custom-identity.png)

다음은 매핑 예입니다. 실제 매핑은 프로필 스키마와 [!DNL FreeWheel] 계정이 지원하는 ID 유형에 따라 달라집니다.

| 소스 필드 | 대상 필드 |
| --- | --- |
| `identityMap.IDFA` | `idfa` |
| `identityMap.GAID` | `aaid` |
| `homeAddress.ipAddress` | `ip` |

{style="table-layout:auto"}

>[!NOTE]
>
>필수 매핑은 강제 적용되지 않습니다. 그러나 유효한 ID 매핑이 하나 이상 없는 프로필은 내보낸 파일에 포함되지 않습니다.

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

[!DNL FreeWheel]은(는) 내보내기당 두 가지 유형의 파일을 받습니다. 두 파일 유형 모두 자동으로 생성되고 전달됩니다. 사용자 부분에는 필요한 작업이 없습니다.

**ID(데이터) 파일**&#x200B;에 대상 멤버십 데이터가 포함되어 있습니다. 각 행은 사용자 식별자를 하나 이상의 대상 ID에 매핑합니다. 파일은 열 헤더 없이 CSV 형식으로 [!DNL FreeWheel]에 전달됩니다. 내보내기에 있는 각 ID 유형에 대해 별도의 파일이 생성됩니다(예: `aaid`에 대한 하나의 파일과 `idfa`에 대한 별도의 파일).

데이터 파일 형식 예:

```csv
aebc1234-56f7-89ab-cdef-0123456789ab,segment_1,segment_2
f7c9a8b0-4d33-11ec-81d3-0242ac130003,segment_1,segment_3
123e4567-e89b-12d3-a456-426614174000,segment_2
```

**분류 파일**&#x200B;은(는) 내보내기에 포함된 대상을 설명합니다. 이러한 파일은 데이터 파일과 함께 제공되며 대상 ID, 이름 및 TTL(Time to Live)이 포함됩니다. [!DNL FreeWheel]이(가) 지원하는 최대 TTL은 90일입니다. 아래 예제의 값은 예시적인 것입니다.

분류 파일 형식 예:

```csv
Segment ID,Segment Name,TTL
segment_1,my_first_segment,30
segment_2,my_second_segment,30
segment_3,my_third_segment,30
```

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 추가 리소스 {#additional-resources}

[!DNL FreeWheel] 및 해당 광고 기술 플랫폼에 대한 자세한 내용은 [FreeWheel 웹 사이트](https://www.freewheel.com){target="_blank"}를 참조하십시오.
