---
title: 케벨 연결
description: Kevel 스트리밍 대상을 사용하여 대상자를 Kevel의 UserDB 및 세그먼트 관리 API로 직접 활성화하고, 의사 결정 시 실시간 타깃팅을 지원합니다.
last-substantial-update: 2026-01-27T00:00:00Z
source-git-commit: 04d01b2deafb1b8f1b0c256f31475bb75989a2c4
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 3%

---


# [!DNL Kevel] 연결 {#kevel}

## 개요 {#overview}

[[!DNL Kevel]](https://www.kevel.com/)은(는) 혁신적인 상거래 리더가 소매 미디어를 출시하고, 확장하고, 성공할 수 있도록 지원하는 AI 지원 기술 및 전문가 지침을 제공합니다. [!DNL Kevel]의 Retail Media Cloud는 온사이트 및 오프사이트 광고를 위한 타깃팅되고, 귀속되며, 사용자 지정 가능한 광고 형식을 지원합니다.

Adobe Experience Platform용 [!DNL Kevel] 스트리밍 대상을 사용하면 고객이 [!DNL Kevel]의 UserDB 및 세그먼트 관리 API로 직접 Adobe 대상을 활성화하여 광고 결정 시 실시간 타깃팅을 지원할 수 있습니다.

>[!IMPORTANT]
> 
>질문이 있거나 [!DNL Kevel] 대상 또는 해당 설명서에 대한 업데이트를 요청하려면 [!DNL Kevel]support@kevel.com[에서 ](mailto:support@kevel.com) 팀에 전자 메일을 보내십시오.

## 사용 사례 {#use-cases}

소매 미디어 경험에서 풍부한 자사 행동 대상을 활성화하여 더 연관성 있는 광고와 더 강력한 성능을 제공할 수 있습니다. Experience Platform에서는 빈번한 카테고리 쇼핑객 또는 최근 제품에 관심이 있는 사용자와 같은 고부가가치 의도 기반 대상을 빌드하고 이러한 멤버십을 [!DNL Kevel]에 실시간으로 동기화합니다. [!DNL Kevel]은(는) 이러한 세그먼트를 즉시 광고 결정에 사용할 수 있도록 하므로 스폰서 제품 및 검색, 검색 및 앱 경험 전반에 걸쳐 다른 형식에 대한 정확한 타깃팅을 사용할 수 있습니다. 사용자가 자격을 부여하는 즉시 이러한 신호에 따라 더 적절한 노출, 더 나은 타기팅, 향상된 측정 및 ROAS를 구동할 수 있습니다.

## 전제 조건 {#prerequisites}

[!DNL Kevel] 대상 사용을 준비하려면 다음 전제 조건이 충족되는지 확인하십시오.

- 활성 **[!DNL Kevel]네트워크** 및 API 액세스 권한이 있어야 합니다.
- 세그먼트를 만들고 UserDB 레코드를 업데이트할 수 있는 권한이 있는 **[!DNL Kevel]API 키**&#x200B;이(가) 필요합니다.
- [!DNL Kevel] 광고 요청 동안 사이트 또는 앱에서 전송하는 ID(예: ECID, GAID, IDFA, 로열티 ID 등)에 매핑되는 Experience Platform의 ID 네임스페이스를 구성해야 합니다.
- 각 ID는 UserDB 레코드를 발생시키므로 Adobe 고객은 실시간 광고 요청 중에 사용되는 ID만 매핑해야 합니다.

## 지원되는 ID {#supported-identities}

[!DNL Kevel] 대상은 [!DNL Kevel]에 광고 요청을 보낼 때 응용 프로그램에서 사용할 수 있는 모든 ID에 대한 활성화를 지원합니다. 최대 3개의 ID 네임스페이스를 매핑하여 해당 UserDB 레코드를 생성할 수 있습니다.

[!DNL Kevel]은(는) 다음 Experience Platform id 네임스페이스를 지원합니다.

| ID 네임스페이스 | 설명 | 일반적인 사용 |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud ID | 온사이트 개인화 및 Adobe 간 식별에 사용됩니다. |
| **GAID** | GOOGLE ADVERTISING ID | Android 앱/장치 트래픽에 사용됩니다. |
| **IDFA** | APPLE ADVERTISING ID | iOS 앱/장치 트래픽에 사용됩니다(ATT 동의에 따름). |
| **외부 ID** | 외부 ID(사용자 지정 식별자) | 소유권 또는 백엔드 생성 ID를 전달합니다. |

{style="table-layout:auto"}

### 사용자 정의 ID 네임스페이스 지원

[!DNL Kevel] 대상 **에서도 Experience Platform 구현에 정의된 대로 사용자 지정 네임스페이스**&#x200B;를 허용합니다.

이것은 다음을 의미합니다.

- **고객별 ID 네임스페이스**&#x200B;를 매핑할 수 있습니다(예: `loyalty_id`, `gigya_id` 또는 ID 서비스에서 정의한 사용자 지정 ID).
- 이러한 네임스페이스는 전역 네임스페이스와 동일한 방식으로 `kevel_user_key1`, `kevel_user_key2` 또는 `kevel_user_key3`에 할당할 수 있습니다.
- [!DNL Kevel]은(는) 매핑된 각 ID의 인스턴스당 **하나의 UserDB 레코드를 생성합니다**. 따라서 시스템에서 전송하는 각 식별자에 대해 광고 결정 시간에 실시간으로 일치할 수 있습니다.

### ID 매핑 동작

- **최대 3개의** Experience Platform ID 네임스페이스를 [!DNL Kevel]의 3개의 ID 슬롯에 매핑할 수 있습니다.
- 활성화된 각 프로필에 대해 [!DNL Kevel]은(는) 매핑된 각 ID의 인스턴스당 **하나의 UserDB 레코드를 받습니다**.
- 고객은 불필요한 UserDB 저장소를 방지하기 위해 광고 요청에서 실제로 보내는 ID만 [!DNL Kevel]에 매핑해야 합니다.

![케벨 대상에 대한 매핑 예](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)

## 지원되는 대상자 {#supported-audiences}

| 대상자 원본 | 지원됨 | 설명 |
|-----------------------|-----------|---------------------------------------------------------- |
| Segmentation Service | 예 | 세그멘테이션 엔진에서 평가한 Adobe 프로필 대상입니다. |
| 사용자 정의 업로드 | 아니요 | 현재 지원되지 않습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

| 항목 | 유형 | 참고 |
|------|------|-------|
| 내보내기 유형 | **세그먼트 내보내기** | [!DNL Kevel]은(는) 프로필이 대상자 자격을 얻거나 대상을 종료할 때마다 업데이트를 받습니다. |
| 내보내기 빈도 | **스트리밍** | 업데이트는 Destination SDK 스트리밍 프레임워크를 사용하여 실시간으로 전송됩니다. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

표준 Experience Platform [대상 연결](../../ui/connect-destination.md) 워크플로를 따릅니다.

>[!IMPORTANT]
> 
>**대상 보기** 및 **대상 관리** 권한이 있어야 합니다.

### 대상으로 인증 {#authenticate}

[!DNL Kevel]에 연결할 때 다음 필드를 제공하십시오.

- **전달자 토큰** — [!DNL Kevel] API 키입니다.

![케벨 대상에 대한 인증 옵션](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### 대상 세부 정보 입력 {#destination-details}

인증 후 다음을 구성합니다.

- **이름** — 이 대상 인스턴스를 식별하는 레이블입니다.
- **설명** - 이 대상 인스턴스를 설명하는 선택적 텍스트입니다.
- **[!DNL Kevel]네트워크 ID** — [!DNL Kevel] 네트워크 식별자입니다.

![케벨 대상에 대한 대상 세부 정보](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## 이 대상에 대한 세그먼트 활성화 {#activate}

대상자를 [!DNL Kevel]&#x200B;(으)로 보내려면 다음 워크플로우를 따르십시오.\
[프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md).

### 대상자 비활성화 {#deactivate}

대상이 Experience Platform에서 [!DNL Kevel] 대상에서 비활성화되거나 제거되면 Experience Platform에서는 해당 대상에 대한 추가 프로필 자격 업데이트 전송을 중지합니다. [!DNL Kevel]에서 만들어진 기존 세그먼트는 계속 사용할 수 있으며 자동으로 삭제되지 않습니다.

[!DNL Kevel] 세그먼트가 현재 활성 캠페인에서 사용 중인 경우 [!DNL Kevel]은(는) 실시간 게재를 중단하지 않도록 삭제를 방지합니다. 이 경우 Experience Platform에서 비활성화되면 다음과 같은 결과가 발생합니다.

- Experience Platform 데이터 흐름이 중지됨
- [!DNL Kevel] 세그먼트는 계속 존재하며 수동으로 제거하거나 캠페인을 업데이트할 때까지 캠페인에 연결된 상태로 유지될 수 있습니다

[!DNL Kevel]에서 타깃팅을 완전히 중지하려면 [!DNL Kevel]의 캠페인 관리 시스템에 있는 모든 활성 캠페인에서 세그먼트가 제거되었는지 확인하십시오.

### 속성 및 ID 매핑 {#map}

[!DNL Kevel]에는 다음이 필요합니다.

- **ID 네임스페이스** — [!DNL Kevel] ID 슬롯에 매핑되는 최대 3개의 ID 네임스페이스입니다.
- **세그먼트 멤버십** — 수동 매핑이 필요하지 않습니다. Experience Platform은 세그먼트 멤버십 식별자 및 별칭을 자동으로 전달합니다.

활성화 중에 [!DNL Kevel]에 대해 구성한 ID 네임스페이스를 선택하십시오. 각 ID는 자체 UserDB 업데이트 호출을 생성합니다.

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

프로필이 대상 자격이 되거나 종료되면 Experience Platform에서 [!DNL Kevel]&#x200B;(으)로 스트리밍 업데이트를 보냅니다.

### [!DNL Kevel] UserDB에서 받은 샘플 페이로드

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| 매개변수 | 설명 |
|-----------|-------------|
| **userKey** | 매핑된 Adobe ID에서 파생됩니다. |
| **세그먼트** | 현재 프로필이 실현된 Adobe 대상에 해당하는 [!DNL Kevel] 세그먼트 ID 집합입니다. |

{style="table-layout:auto"}

### 내보내는 동안 사용되는 샘플 Experience Platform 프로필 {#sample-profile}

대상을 [!DNL Kevel] 대상으로 활성화하면 Experience Platform에서 **세그먼트 자격** 및 고객이 매핑한 **ID**&#x200B;가 모두 포함된 프로필 조각을 [!DNL Kevel]의 ID 슬롯으로 보냅니다.

다음은 를 보여주는 내보낸 프로필의 예입니다.

- `kevel_user_key1`, `kevel_user_key2` 및 `kevel_user_key3`에 매핑된 여러 ID 네임스페이스
- `ups` 네임스페이스에서 활성화된 단일 세그먼트

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### [!DNL Kevel]에서 이 프로필을 해석하는 방법

[!DNL Kevel] 대상 구성을 사용하여 매핑된 각 ID는 고유한 UserDB 레코드를 생성하는데, 이는 [!DNL Kevel]이(가) 다음을 수신함을 의미합니다.

- `ECID-fN1zo`에 대한 업데이트 1개
- `ECID-9Xr2p`에 대한 업데이트 1개
- `GAID-4oic4`에 대한 업데이트 1개
- `IDFA-nB5fU`에 대한 업데이트 1개

이를 통해 광고 결정 시 사용 가능한 ID를 사용하여 동일한 사용자를 인식할 수 있으며, 각 ID에는 동일한 세그먼트 멤버십 세트가 포함됩니다.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 추가 리소스 {#additional-resources}

- [[!DNL Kevel] UserDB 참조](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel] 사용자 세그먼트 타깃팅](https://dev.kevel.com/docs/segment-targeting)
