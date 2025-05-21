---
keywords: Azure 이벤트 허브 대상;azure 이벤트 허브;azure eventhub
title: Azure 이벤트 허브 연결
description: ' [!DNL Azure Event Hubs] 저장소에 대한 실시간 아웃바운드 연결을 생성하여 Experience Platform에서 데이터를 스트리밍합니다.'
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 678f80445212edc1edd3f4799999990ddcc2a039
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 5%

---

# [!DNL Azure Event Hubs] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
> 이 대상은 [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html) 고객에게만 제공됩니다.

[!DNL Azure Event Hubs]은(는) 빅 데이터 스트리밍 플랫폼 및 이벤트 수집 서비스입니다. 초당 수백만 개의 이벤트를 수신하고 처리할 수 있습니다. 이벤트 허브로 전송된 데이터는 모든 실시간 분석 공급자나 일괄 처리/저장소 어댑터를 사용하여 변환하거나 저장할 수 있습니다.

[!DNL Azure Event Hubs] 저장소에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 데이터를 스트리밍할 수 있습니다.

* [!DNL Azure Event Hubs]에 대한 자세한 내용은 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)를 참조하세요.
* 프로그래밍 방식으로 [!DNL Azure Event Hubs]에 연결하려면 [스트리밍 대상 API 자습서](../../api/streaming-destinations.md)를 참조하십시오.
* Experience Platform 사용자 인터페이스를 사용하여 [!DNL Azure Event Hubs]에 연결하려면 아래 섹션을 참조하십시오.

UI의 ![AWS Kinesis](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 사용 사례 {#use-cases}

[!DNL Azure Event Hubs]과(와) 같은 스트리밍 대상을 사용하면 고가치 세분화 이벤트 및 관련 프로필 속성을 선택한 시스템에 쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 백서를 다운로드하여 &quot;높은 전환 성향&quot; 세그먼트로 분류했습니다. 잠재 고객이 속한 대상을 [!DNL Azure Event Hubs] 대상에 매핑하면 [!DNL Azure Event Hubs]에서 이 이벤트를 받게 됩니다. 여기서는 엔터프라이즈 IT 시스템과 가장 잘 작동할 것으로 생각되므로 DIY(Do-It-Yourself) 방식을 채택하고 이벤트 상단에 비즈니스 논리를 설명할 수 있습니다.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 허용 목록에 추가하다 IP 주소 {#ip-address-allowlist}

고객 보안 및 규정 준수 요구 사항을 충족하기 위해 Experience Platform에서는 [!DNL Azure Event Hubs] 대상에 대해 허용 목록에 추가하다할 수 있는 정적 IP 목록을 제공합니다. IP에서 허용 목록에 추가하다에 대한 전체 목록은 [스트리밍 대상의 IP 주소 허용 목록](/help/destinations/catalog/streaming/ip-address-allow-list.md)을 참조하십시오.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 이 대상에 연결할 때 다음 정보를 제공해야 합니다.

### 인증 정보 {#authentication-information}

#### 표준 인증 {#standard-authentication}

![Azure Event Hubs 표준 인증 세부 정보에 대해 완료된 필드를 표시하는 UI 화면 이미지](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

HTTP 끝점에 연결할 **[!UICONTROL 표준 인증]** 유형을 선택한 경우 아래 필드를 입력하고 **[!UICONTROL 대상에 연결]**&#x200B;을 선택하십시오.

* **[!UICONTROL SAS 키 이름]**: SAS 키 이름이라고도 하는 인증 규칙의 이름입니다.
* **[!UICONTROL SAS 키]**: 이벤트 허브 네임스페이스의 기본 키입니다. 이벤트 허브 목록을 채우려면 `sasKey`에 해당하는 `sasPolicy`에 **관리** 권한이 구성되어 있어야 합니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)에서 SAS 키를 사용하여 [!DNL Azure Event Hubs]에 인증하는 방법에 대해 알아봅니다.
* **[!UICONTROL 네임스페이스]**: [!DNL Azure Event Hubs] 네임스페이스를 채웁니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)에서 [!DNL Azure Event Hubs] 네임스페이스에 대해 알아봅니다.

#### SAS(공유 액세스 서명) 인증 {#sas-authentication}

![Azure Event Hubs 표준 인증 세부 정보에 대해 완료된 필드를 표시하는 UI 화면 이미지](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

HTTP 끝점에 연결할 **[!UICONTROL 표준 인증]** 유형을 선택한 경우 아래 필드를 입력하고 **[!UICONTROL 대상에 연결]**&#x200B;을 선택하십시오.

* **[!UICONTROL SAS 키 이름]**: SAS 키 이름이라고도 하는 인증 규칙의 이름입니다.
* **[!UICONTROL SAS 키]**: 이벤트 허브 네임스페이스의 기본 키입니다. 이벤트 허브 목록을 채우려면 `sasKey`에 해당하는 `sasPolicy`에 **관리** 권한이 구성되어 있어야 합니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)에서 SAS 키를 사용하여 [!DNL Azure Event Hubs]에 인증하는 방법에 대해 알아봅니다.
* **[!UICONTROL 네임스페이스]**: [!DNL Azure Event Hubs] 네임스페이스를 채웁니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)에서 [!DNL Azure Event Hubs] 네임스페이스에 대해 알아봅니다.
* **[!UICONTROL 이벤트 허브 이름]**: [!DNL Azure Event Hub] 이름을 입력하십시오. [Microsoft 설명서](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)에서 [!DNL Azure Event Hubs] 이름에 대해 알아보세요.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="세그먼트 이름 포함"
>abstract="데이터 내보내기에 내보내는 대상자 이름이 포함되도록 하려면 전환하십시오. 이 옵션을 선택한 경우 데이터 내보내기 예는 설명서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="세그먼트 타임스탬프 포함"
>abstract="대상자를 생성 및 업데이트하거나 대상자를 대상에 매핑하여 활성화하는 경우 데이터 내보내기에 Unix 타임스탬프가 포함되도록 하려면 전환하십시오. 이 옵션을 선택한 경우 데이터 내보내기 예는 설명서를 참조하십시오."

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![Azure Event Hubs 대상 세부 사항에 대해 완료된 필드를 표시하는 UI 화면 이미지](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL 이름]**: [!DNL Azure Event Hubs]에 연결할 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 연결에 대한 설명을 입력하십시오.  예: &quot;프리미엄 계층 고객&quot;, &quot;카이트서핑에 관심이 있는 고객&quot;.
* **[!UICONTROL eventHubName]**: [!DNL Azure Event Hubs] 대상에 스트림의 이름을 제공하십시오.
* **[!UICONTROL 세그먼트 이름 포함]**: 내보내는 대상의 이름을 데이터 내보내기에 포함하려면 전환합니다. 이 옵션을 선택한 데이터 내보내기의 예는 아래의 [내보낸 데이터](#exported-data) 섹션을 참조하십시오.
* **[!UICONTROL 세그먼트 타임스탬프 포함]**: 대상을 만들고 업데이트할 때 데이터 내보내기에 UNIX 타임스탬프와 활성화를 위해 대상을 대상에 매핑할 때 UNIX 타임스탬프를 포함하도록 전환합니다. 이 옵션을 선택한 데이터 내보내기의 예는 아래의 [내보낸 데이터](#exported-data) 섹션을 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* [동의 정책 평가](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)는 현재 Azure Event Hubs 대상으로 내보내는 데 지원되지 않습니다. [자세히 보기](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-streaming-profile-destinations.md)를 참조하십시오.

## 프로필 내보내기 동작 {#profile-export-behavior}

Experience Platform은 대상 자격 조건 또는 기타 중요한 이벤트 후에 프로필에 대한 관련 업데이트가 발생한 경우에만 데이터를 대상으로 내보내도록 [!DNL Azure Event Hubs] 대상에 대한 프로필 내보내기 동작을 최적화합니다. 프로필은 다음과 같은 경우 대상으로 내보내집니다.

* 프로필 업데이트는 대상에 매핑된 대상자 중 하나 이상에 대한 대상자 멤버십 변경에 따라 결정되었습니다. 예를 들어 프로필이 대상에 매핑된 대상자 중 하나에 대해 자격이 있거나 대상에 매핑된 대상자 중 하나를 종료했습니다.
* 프로필 업데이트는 [ID 맵](/help/xdm/field-groups/profile/identitymap.md)의 변경 내용으로 결정됩니다. 예를 들어 대상에 매핑된 대상자 중 하나에 대해 이미 자격이 있는 프로필이 ID 맵 특성에 새 ID를 추가했습니다.
* 프로필 업데이트는 대상에 매핑된 속성 중 하나 이상에 대한 속성 변경에 의해 결정되었습니다. 예를 들어 매핑 단계에서 대상에 매핑된 속성 중 하나가 프로필에 추가됩니다.

위에서 설명한 모든 경우에 관련 업데이트가 발생한 프로필만 대상으로 내보냅니다. 예를 들어 대상 흐름에 매핑된 대상자에 100명의 멤버가 있고 5개의 새 프로필이 세그먼트에 해당하는 경우 대상으로 내보내는 것은 증분 것이며 5개의 새 프로필만 포함합니다.

변경 내용이 있는 위치에 관계없이 매핑된 모든 속성을 프로파일에 대해 내보냅니다. 따라서 위의 예에서는 속성 자체가 변경되지 않았더라도 이러한 5개의 새 프로필에 대해 매핑된 모든 속성을 내보냅니다.

### 데이터 내보내기를 결정하는 사항 및 내보내기에 포함되는 사항 {#what-determines-export-what-is-included}

지정된 프로필에 대해 내보내는 데이터와 관련하여 *데이터를 [!DNL Azure Event Hubs] 대상으로 내보내는 방법을 결정하는 요소* 및 *내보내기에 포함되는 데이터*&#x200B;의 두 가지 개념을 이해하는 것이 중요합니다.

| 대상 내보내기를 결정하는 사항 | 대상 내보내기에 포함된 사항 |
|---------|----------|
| <ul><li>매핑된 속성 및 세그먼트는 대상 내보내기에 대한 큐 역할을 합니다. 즉, 프로필의 `segmentMembership` 상태가 `realized` 또는 `exiting`(으)로 변경되거나 매핑된 특성이 업데이트되면 대상 내보내기가 시작됩니다.</li><li>현재 ID를 [!DNL Azure Event Hubs] 대상에 매핑할 수 없으므로 지정된 프로필의 ID를 변경하면 대상 내보내기도 결정됩니다.</li><li>속성에 대한 변경 사항은 동일한 값인지 여부에 관계없이 속성에 대한 모든 업데이트로 정의됩니다. 즉, 값 자체가 변경되지 않았더라도 속성에 대한 덮어쓰기를 변경 사항으로 간주합니다.</li></ul> | <ul><li>`segmentMembership` 개체에는 활성화 데이터 흐름에서 매핑된 세그먼트가 포함되어 있습니다. 이 경우 자격 또는 세그먼트 종료 이벤트 후 프로필의 상태가 변경되었습니다. 활성화 데이터 흐름에서 매핑된 세그먼트와 동일한 [병합 정책](/help/profile/merge-policies/overview.md)에 속하는 경우 프로필이 자격을 갖춘 매핑되지 않은 다른 세그먼트는 대상 내보내기의 일부가 될 수 있습니다. </li><li>`identityMap` 개체의 모든 ID도 포함됩니다. Experience Platform은 현재 [!DNL Azure Event Hubs] 대상에서 ID 매핑을 지원하지 않습니다.</li><li>매핑된 속성만 대상 내보내기에 포함됩니다.</li></ul> |

{style="table-layout:fixed"}

예를 들어, 데이터 흐름에서 대상이 세 개 선택되고 대상에 네 개의 특성이 매핑되는 [!DNL Azure Event Hubs] 대상에 대한 이 데이터 흐름을 고려해 보십시오.

![Amazon Kinesis 대상 데이터 흐름](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

대상으로의 프로필 내보내기는 *3개의 매핑된 세그먼트 중 하나를 사용하거나 종료하는 프로필에 의해 결정됩니다*. 그러나 데이터 내보내기에서 `segmentMembership` 개체(아래 [내보낸 데이터](#exported-data) 섹션 참조)에 매핑되지 않은 다른 대상이 나타날 수 있습니다. 해당 프로필이 해당 대상의 구성원이고 이러한 대상이 내보내기를 트리거한 대상과 동일한 병합 정책을 공유하는 경우. 프로필이 **Customer with DeLorean Cars** 대상자를 대상으로 하지만 **Watched &quot;Back to the Future&quot;** movie 및 **Science fans** segments의 회원이면 **DeLorean Cars를 사용하는 고객** 세그먼트와 동일한 병합 정책을 공유하는 경우 이 두 대상자가 데이터 흐름에서 매핑되지 않았더라도 데이터 내보내기의 `segmentMembership` 개체에도 표시됩니다.

프로필 속성 관점에서 위에 매핑된 네 개의 속성에 대한 변경 사항은 대상 내보내기를 결정하고 프로필에 있는 네 개의 매핑된 속성 중 하나는 데이터 내보내기에 표시됩니다.

## 내역 데이터 채우기 {#historical-data-backfill}

기존 대상에 새 대상을 추가하거나 새 대상을 만들고 대상에 대상을 매핑하면 Experience Platform에서 이전 대상 자격 데이터를 대상으로 내보냅니다. 대상에 대상을 추가하기 전에 대상 *이전*&#x200B;에 대해 자격이 있는 프로필은 약 1시간 내에 대상으로 내보냅니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 [!DNL Azure Event Hubs] 대상에 JSON 형식으로 도착합니다. 예를 들어, 아래 내보내기에는 특정 세그먼트에 대해 자격이 있고 다른 두 세그먼트의 구성원이며 다른 세그먼트를 종료한 프로필이 포함됩니다. 내보내기에는 프로필 속성 이름, 성, 생년월일 및 개인 이메일 주소도 포함됩니다. 이 프로필의 ID는 ECID와 이메일입니다.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

다음은 **[!UICONTROL 세그먼트 이름 포함]** 및 **[!UICONTROL 세그먼트 타임스탬프 포함]** 옵션에 대한 연결 대상 흐름에서 선택한 UI 설정에 따라 내보낸 데이터의 추가 예입니다.

+++ 아래 데이터 내보내기 샘플에는 `segmentMembership` 섹션의 대상 이름이 포함되어 있습니다

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ 아래 데이터 내보내기 샘플에는 `segmentMembership` 섹션의 대상 타임스탬프가 포함되어 있습니다

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## 제한 및 재시도 정책 {#limits-retry-policy}

그 중 95% 동안 Experience Platform은 HTTP 대상에 대한 각 데이터 흐름의 초당 요청 수가 10,000개 미만인 상태로 성공적으로 전송된 메시지에 대해 10분 미만의 처리량 지연 시간을 제공하려고 합니다.

HTTP API 대상에 대한 요청이 실패한 경우 Experience Platform은 실패한 요청을 저장하고 두 번 재시도하여 요청을 엔드포인트에 전송합니다.

>[!MORELIKETHIS]
>
>* [Azure Event Hubs에 연결하고 흐름 서비스 API를 사용하여 데이터를 활성화하세요](../../api/streaming-destinations.md)
>* [AWS Kinesis 대상](./amazon-kinesis.md)
>* [대상 유형 및 범주](../../destination-types.md)
