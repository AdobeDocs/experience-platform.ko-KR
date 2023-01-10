---
keywords: Experience Platform;홈;인기 항목;Azure 이벤트 허브;azure 이벤트 허브;이벤트 허브;이벤트 허브
solution: Experience Platform
title: Azure 이벤트 허브 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Azure Event Hub를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform], 및 [!DNL Azure]. 이러한 시스템의 데이터를 플랫폼으로 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 고유한 데이터를 플랫폼으로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. Platform에서 데이터를 가져올 수 있습니다. [!DNL Event Hubs] 실시간으로

## 크기 조절 [!DNL Event Hubs]

스케일 팩터 [!DNL Event Hubs] 대용량 데이터를 처리하거나 병렬 처리를 증가하거나 수집 플랫폼의 속도를 높여야 하는 경우 인스턴스를 늘려야 합니다.

### 더 높은 볼륨 데이터 처리

현재 사용자에서 가져올 수 있는 최대 데이터 볼륨입니다 [!DNL Event Hubs] Platform에 대한 계정은 초당 2,000개의 레코드입니다. 더 높은 볼륨 데이터를 확장 및 수집하려면 Adobe 담당자에게 문의하십시오.

### 병렬 처리 수 증가 [!DNL Event Hubs] 및 플랫폼

병렬화는 속도와 성능을 향상시키기 위해 여러 처리 단위에 대해 동일한 작업을 동시에 실행하는 것을 의미합니다. 의 병렬 처리 수를 늘릴 수 있습니다 [!DNL Event Hubs] 파티션 증가 또는 추가 처리 단위 가져오기 [!DNL Event Hubs] 계정이 필요합니다. 다음 보기 [[!DNL Event Hubs] 크기 조절 문서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) 추가 정보.

플랫폼 쪽에서 수집 속도를 높이려면 플랫폼에서 소스 커넥터의 작업 수를 늘려 [!DNL Event Hubs] 분할 영역. 다음에 대한 병렬 처리 수가 증가하면 [!DNL Event Hubs] 새 파티션을 기반으로 플랫폼 작업을 확장하려면 Adobe 담당자에게 문의하십시오. 현재 이 프로세스는 자동화되지 않습니다.

## 가상 네트워크를 사용하여 연결 [!DNL Event Hubs] 플랫폼

연결할 가상 네트워크를 설정할 수 있습니다 [!DNL Event Hubs] 방화벽 측정값을 사용하도록 설정하는 동안 플랫폼에 문의하십시오. 가상 네트워크를 설정하려면 다음 위치로 이동하십시오 [[!DNL Event Hubs] 네트워크 규칙 집합 문서](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) 및 아래 나열된 단계를 수행합니다.

* 선택 **사용해 보기** REST API 패널에서
* 인증 [!DNL Azure] 동일한 브라우저에서 자격 증명을 사용한 계정
* 을(를) 선택합니다 [!DNL Event Hubs] Platform으로 가져올 네임스페이스, 리소스 그룹 및 구독을 선택한 다음 **실행**;
* 표시되는 JSON 본문에서 다음 플랫폼 서브넷을 추가합니다 `virtualNetworkRules` 내부 `properties`:


>[!IMPORTANT]
>
>업데이트하기 전에 받은 JSON 본문을 백업해야 합니다 `virtualNetworkRules` 기존 IP 필터링 규칙을 포함하고 있는 플랫폼 서브넷과 함께 제공됩니다. 그렇지 않으면 호출 후에 규칙이 삭제됩니다.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

플랫폼 서브넷의 다른 영역에 대해서는 아래 목록을 참조하십시오.

### VA7: 북미

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2: 유럽

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5: 오스트레일리아

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5_network_10_21_116_0_22/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

다음을 참조하십시오 [[!DNL Event Hubs] 문서](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) 네트워크 규칙 세트에 대한 자세한 정보.

## Connect [!DNL Event Hubs] 플랫폼

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Event Hubs] API 또는 사용자 인터페이스를 사용하여 플랫폼:

### API 사용

* [Flow Service API를 사용하여 이벤트 허브 소스 연결을 만듭니다](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Flow Service API를 사용하여 스트리밍 데이터를 수집합니다](../../tutorials/api/collect/streaming.md)

### UI 사용

* [UI에서 이벤트 허브 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [UI에서 클라우드 스토리지 연결에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
