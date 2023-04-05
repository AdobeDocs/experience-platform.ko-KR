---
keywords: Azure 이벤트 허브 대상;azure 이벤트 허브;azure 이벤트 허브
title: Azure 이벤트 허브 연결
description: 에 대한 실시간 아웃바운드 연결을 만듭니다. [!DNL Azure Event Hubs] Experience Platform에서 데이터를 스트리밍할 스토리지.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 4d1f9fa19bd35095e3ccbd8d83bcc33dcd4c45a8
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 4%

---

# [!DNL Azure Event Hubs] 연결

## 개요 {#overview}

>[!IMPORTANT]
>
> 이 대상은 다음 작업에만 사용할 수 있습니다 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 고객.

[!DNL Azure Event Hubs] 는 빅데이터 스트리밍 플랫폼 및 이벤트 수집 서비스입니다. 초당 수백만 개의 이벤트를 받고 처리할 수 있습니다. 이벤트 허브로 전송된 데이터는 모든 실시간 분석 공급자나 일괄 처리/저장소 어댑터를 사용하여 변환하고 저장할 수 있습니다.

에 대한 실시간 아웃바운드 연결을 만들 수 있습니다 [!DNL Azure Event Hubs] Adobe Experience Platform에서 데이터를 스트리밍할 수 있는 스토리지.

* 에 대한 자세한 정보 [!DNL Azure Event Hubs]를 참조하고 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* 에 연결하려면 [!DNL Azure Event Hubs] 프로그래밍 방식으로 [스트리밍 대상 API 자습서](../../api/streaming-destinations.md).
* 에 연결하려면 [!DNL Azure Event Hubs] platform 사용자 인터페이스를 사용하여 아래 섹션을 참조하십시오.

![UI의 AWS Kinesis](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 사용 사례 {#use-cases}

다음과 같은 스트리밍 대상 사용 [!DNL Azure Event Hubs]를 사용하면 고부가가치 세그먼테이션 이벤트 및 관련 프로필 속성을 선택한 시스템에 쉽게 제공할 수 있습니다.

예를 들어 잠재 고객이 백서를 다운로드하여 &quot;전환율이 높은&quot; 세그먼트로 분류하는 경우 잠재 고객이 속한 세그먼트를 [!DNL Azure Event Hubs] 대상, 이 이벤트를 [!DNL Azure Event Hubs]. 이 환경에서는 엔터프라이즈 IT 시스템에 가장 적합한 방식으로 IT 방식을 사용하고 이벤트 이외에도 비즈니스 논리를 설명할 수 있습니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## IP 주소 허용 목록에 추가하다 {#ip-address-allowlist}

Experience Platform은 고객의 보안 및 규정 준수 요구 사항을 충족하기 위해 [!DNL Azure Event Hubs] 대상. 을(를) 참조하십시오. [스트리밍 대상을 위한 IP 주소 허용 목록](/help/destinations/catalog/streaming/ip-address-allow-list.md) 을 클릭하여 검색할 IP의 전체 목록을 허용 목록에 추가하다 확인합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 이 대상에 연결할 때 다음 정보를 제공해야 합니다.

### 인증 정보 {#authentication-information}

#### 표준 인증 {#standard-authentication}

![Azure 이벤트 허브 표준 인증 세부 사항에 대해 완료된 필드를 표시하는 UI 화면의 이미지](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

을(를) 선택하는 경우 **[!UICONTROL 표준 인증]** HTTP 종단점에 연결하려면 아래 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**:

* **[!UICONTROL SAS 키 이름]**: SAS 키 이름이라고도 하는 인증 규칙의 이름입니다.
* **[!UICONTROL SAS 키]**: 이벤트 허브 네임스페이스의 기본 키입니다. 다음 `sasPolicy` 저것은 `sasKey` 에 해당해야 함 **관리** 이벤트 허브 목록을 채울 수 있도록 구성된 권한. 인증 방법에 대해 알아보기 [!DNL Azure Event Hubs] SAS 키를 사용하여 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 네임스페이스]**: 을 입력합니다. [!DNL Azure Event Hubs] 네임스페이스. 알아보기 [!DNL Azure Event Hubs] 네임스페이스 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### 공유 액세스 서명(SAS) 인증 {#sas-authentication}

![Azure 이벤트 허브 표준 인증 세부 사항에 대해 완료된 필드를 표시하는 UI 화면의 이미지](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

을(를) 선택하는 경우 **[!UICONTROL 표준 인증]** HTTP 종단점에 연결하려면 아래 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**:

* **[!UICONTROL SAS 키 이름]**: SAS 키 이름이라고도 하는 인증 규칙의 이름입니다.
* **[!UICONTROL SAS 키]**: 이벤트 허브 네임스페이스의 기본 키입니다. 다음 `sasPolicy` 저것은 `sasKey` 에 해당해야 함 **관리** 이벤트 허브 목록을 채울 수 있도록 구성된 권한. 인증 방법에 대해 알아보기 [!DNL Azure Event Hubs] SAS 키를 사용하여 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 네임스페이스]**: 을 입력합니다. [!DNL Azure Event Hubs] 네임스페이스. 알아보기 [!DNL Azure Event Hubs] 네임스페이스 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL 이벤트 허브 이름]**: 을 입력합니다. [!DNL Azure Event Hub] name 형식이어야 합니다. 알아보기 [!DNL Azure Event Hubs] 의 이름 [Microsoft 설명서](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub).

### 대상 세부 사항 채우기 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="세그먼트 이름 포함"
>abstract="데이터 내보내기에 내보내는 세그먼트 이름이 포함되도록 하려면 전환하십시오. 이 옵션을 선택한 경우 데이터 내보내기 예는 설명서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="세그먼트 타임스탬프 포함"
>abstract="세그먼트를 생성 및 업데이트하거나 세그먼트를 대상에 매핑하여 활성화하는 경우 데이터 내보내기에 Unix 타임스탬프가 포함되도록 하려면 전환하십시오. 이 옵션을 선택한 경우 데이터 내보내기 예는 설명서를 참조하십시오."

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![Azure 이벤트 허브 대상 세부 정보에 대해 완료된 필드를 표시하는 UI 화면의 이미지](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL 이름]**: 연결할 이름을 입력합니다 [!DNL Azure Event Hubs].
* **[!UICONTROL 설명]**: 연결에 대한 설명을 제공합니다.  예: &quot;Premium Tier 고객&quot;, &quot;고객 고객 키트서빙에 관심&quot;
* **[!UICONTROL eventHubName]**: 스트림의 이름을 로 입력합니다 [!DNL Azure Event Hubs] 대상.
* **[!UICONTROL 세그먼트 이름 포함]**: 데이터 내보내기에 내보낼 세그먼트의 이름이 포함되도록 하려면 전환합니다. 이 옵션을 선택한 데이터 내보내기의 예는 를 참조하십시오. [내보낸 데이터](#exported-data) 섹션을 참조하십시오.
* **[!UICONTROL 세그먼트 타임스탬프 포함]**: 세그먼트가 생성 및 업데이트될 때 데이터 내보내기에 UNIX 타임스탬프와 세그먼트가 활성화 대상에 매핑될 때 UNIX 타임스탬프를 포함하려면 을 전환합니다. 이 옵션을 선택한 데이터 내보내기의 예는 를 참조하십시오. [내보낸 데이터](#exported-data) 섹션을 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-streaming-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 프로필 내보내기 동작 {#profile-export-behavior}

Experience Platform은 프로필 내보내기 동작을 로 최적화합니다 [!DNL Azure Event Hubs] 대상: 세그먼트 자격 또는 기타 중요한 이벤트에 따라 프로필에 대한 관련 업데이트가 발생한 경우에만 데이터를 대상에 내보냅니다. 프로필은 다음과 같은 상황에서 대상에 내보내집니다.

* 프로필 업데이트는 대상에 매핑된 세그먼트 중 하나 이상에 대한 세그먼트 멤버십 변경에 의해 결정됩니다. 예를 들어 프로필이 대상에 매핑된 세그먼트 중 하나에 적격이거나 대상에 매핑된 세그먼트 중 하나를 끝냈습니다.
* 프로필 업데이트는 [id 맵](/help/xdm/field-groups/profile/identitymap.md). 예를 들어 대상에 매핑된 세그먼트 중 하나에 대해 이미 자격이 있는 프로필이 ID 맵 속성에 새 ID를 추가했습니다.
* 프로필 업데이트는 대상에 매핑된 특성 중 하나 이상에 대한 특성 변경에 의해 결정됩니다. 예를 들어 매핑 단계에서 대상에 매핑된 속성 중 하나가 프로필에 추가됩니다.

위에 설명된 모든 경우 관련 업데이트가 발생한 프로필만 대상으로 내보내집니다. 예를 들어 대상 플로우에 매핑된 세그먼트에 100개의 멤버가 있고 5개의 새 프로필이 세그먼트에 대한 자격이 있는 경우 대상에 내보내기는 증분 결과이며 5개의 새 프로필만 포함합니다.

변경 사항이 있는 위치에 상관없이 모든 매핑된 속성이 프로필에 대해 내보내집니다. 따라서 위의 예에서 이러한 5개의 새 프로필에 대해 매핑된 속성은 속성 자체가 변경되지 않았더라도 내보내집니다.

### 데이터 내보내기와 내보내기에 포함된 내용을 결정하는 것은 무엇입니까? {#what-determines-export-what-is-included}

주어진 프로필에 대해 내보낸 데이터에 대해서는 의 두 가지 개념을 이해하는 것이 중요합니다 *는 로 데이터 내보내기를 결정합니다 [!DNL Azure Event Hubs] 대상* 및 *내보내기에 포함된 데이터*.

| 대상 내보내기를 결정하는 것은 무엇입니까? | 대상 내보내기에 포함된 항목 |
|---------|----------|
| <ul><li>매핑된 속성 및 세그먼트는 대상 내보내기의 단서로 사용됩니다. 즉, 매핑된 세그먼트가 상태( `null` to `realized` 또는 `realized` to `exiting`) 또는 매핑된 속성이 업데이트되면 대상 내보내기가 해제됩니다.</li><li>현재 ID를 매핑할 수 없으므로 [!DNL Azure Event Hubs] 대상, 지정된 프로필의 모든 id의 변경 사항으로 대상 내보내기도 결정합니다.</li><li>속성 변경은 속성이 동일한 값이든 간에 속성에 대한 업데이트로 정의됩니다. 즉, 값 자체가 변경되지 않았더라도 속성에 대한 덮어쓰기는 변경 사항으로 간주됩니다.</li></ul> | <ul><li>다음 `segmentMembership` 개체에는 활성화 데이터 플로우에 매핑된 세그먼트가 포함되어 있습니다. 이 세그먼트는 자격 또는 세그먼트 종료 이벤트 후 프로필 상태가 변경되었습니다. 자격이 있는 프로파일이 동일한 세그먼트에 속하는 경우 매핑되지 않은 다른 세그먼트는 대상 내보내기의 일부일 수 있습니다 [병합 정책](/help/profile/merge-policies/overview.md) 를 활성화 데이터 플로우에 매핑된 세그먼트로 사용합니다. </li><li>의 모든 ID `identityMap` 개체도 포함됩니다(Experience Platform은 현재 [!DNL Azure Event Hubs] 대상).</li><li>매핑된 속성만 대상 내보내기에 포함됩니다.</li></ul> |

{style="table-layout:fixed"}

예를 들어 이 데이터 흐름을 [!DNL Azure Event Hubs] 대상: 데이터 흐름에서 세 개의 세그먼트를 선택하고 네 개의 속성이 대상에 매핑됩니다.

![Amazon Kinesis 대상 데이터 흐름](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

대상에 대한 프로필 내보내기는 하나 또는 둘 중 하나에 대해 자격이 있는 프로필로 결정할 수 있습니다 *3개의 매핑된 세그먼트*. 그러나 데이터 내보내기에서 `segmentMembership` 개체(참조 [내보낸 데이터](#exported-data) 아래 섹션)에서 매핑되지 않은 다른 세그먼트가 표시될 수 있습니다. 해당 특정 프로필이 해당 세그먼트의 구성원이고, 해당 세그먼트가 내보내기를 트리거한 세그먼트와 동일한 병합 정책을 공유하는 경우 말입니다. 프로필이 **데로리안 차종 고객** 세그먼트이지만 **&quot;미래로 돌아가기&quot;를 시청했습니다** 영화 및 **SF 팬** 세그먼트를 만들면 이러한 다른 두 세그먼트가 `segmentMembership` 동일한 병합 정책을 공유하면 데이터 내보내기의 개체가 데이터 흐름에서 매핑되지 않더라도 데이터 내보내기의 개체입니다 **데로리안 차종 고객** 세그먼트.

프로필 속성 POV에서 위에 매핑된 4개의 속성에 대한 변경 사항이 대상 내보내기를 결정하며 프로필에 있는 4개의 매핑된 속성이 데이터 내보내기에 표시됩니다.

## 내역 데이터 채우기 {#historical-data-backfill}

기존 대상에 새 세그먼트를 추가하거나 새 대상을 만들고 세그먼트를 대상에 매핑하면 Experience Platform이 내역 세그먼트 자격 데이터를 대상으로 내보냅니다. 세그먼트에 적합한 프로필 *이전* 대상에 추가된 세그먼트는 약 1시간 이내에 대상에 내보내집니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 [!DNL Azure Event Hubs] JSON 형식으로 대상을 타깃팅합니다. 예를 들어 아래 내보내기에는 특정 세그먼트에 대해 자격이 있고 다른 두 세그먼트의 구성원이며 다른 세그먼트를 종료한 프로필이 포함되어 있습니다. 내보내기에는 프로필 속성 이름, 성, 생년월일 및 개인 이메일 주소도 포함됩니다. 이 프로필의 ID는 ECID 및 이메일입니다.

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

아래는 의 연결 대상 플로우에서 선택한 UI 설정에 따라 내보낸 데이터의 추가 예입니다 **[!UICONTROL 세그먼트 이름 포함]** 및 **[!UICONTROL 세그먼트 타임스탬프 포함]** 옵션:

+++ 아래 데이터 내보내기 샘플에는 `segmentMembership` 섹션

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

+++ 아래 데이터 내보내기 샘플에는 `segmentMembership` 섹션

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

## 제한 및 다시 시도 정책 {#limits-retry-policy}

시간의 95% 동안 Experience Platform은 각 데이터 플로우에 대해 초당 10,000개 미만의 요청과 함께 성공적으로 전송된 메시지에 대해 10분 미만의 처리량 지연을 제공하기 위해 시도합니다.

HTTP API 대상에 대한 요청이 실패한 경우 Experience Platform은 실패한 요청을 저장하고 엔드포인트로 요청을 다시 두 번 전송합니다.

>[!MORELIKETHIS]
>
>* [Azure 이벤트 허브에 연결하고 플로우 서비스 API를 사용하여 데이터를 활성화합니다](../../api/streaming-destinations.md)
>* [AWS Kinesis 대상](./amazon-kinesis.md)
>* [대상 유형 및 카테고리](../../destination-types.md)

