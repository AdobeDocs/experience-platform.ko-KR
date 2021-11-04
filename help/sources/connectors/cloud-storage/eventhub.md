---
keywords: Experience Platform;홈;인기 항목;Azure 이벤트 허브;azure 이벤트 허브;이벤트 허브;이벤트 허브
solution: Experience Platform
title: Azure 이벤트 허브 소스 커넥터 개요
topic-legacy: overview
description: API 또는 사용자 인터페이스를 사용하여 Azure Event Hub를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: cda9ca9c560b1af2147c00ea4e89dff09b7428ba
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform], 및 [!DNL Azure]. 이러한 시스템의 데이터를 플랫폼으로 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 고유한 데이터를 플랫폼으로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. Platform에서 데이터를 가져올 수 있습니다. [!DNL Event Hubs] 실시간으로

## 가상 네트워크를 사용하여 연결 [!DNL Event Hubs] 플랫폼

연결할 가상 네트워크를 설정할 수 있습니다 [!DNL Event Hubs] 방화벽 측정값을 사용하도록 설정하는 동안 플랫폼에 문의하십시오. 가상 네트워크를 설정하려면 다음 위치로 이동하십시오 [[!DNL Event Hubs] 네트워크 규칙 집합 문서](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) 그런 다음 **사용해 보기** 를 클릭합니다. 다음으로, [!DNL Azure] 자격 증명을 사용하여 계정을 만든 다음 [!DNL Event Hubs] Platform으로 가져올 네임스페이스, 리소스 그룹 및 구독입니다.

설정한 후에는 **요청 본문** 네트워크 영역에 해당하는 JSON과 함께 아래 목록에서 해당 JSON을 사용할 수 있습니다.

>[!TIP]
>
>이 호출 후에 삭제되므로 기존 방화벽 IP 필터링 규칙을 백업해야 합니다.

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
          "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
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

- [Flow Service API를 사용하여 이벤트 허브 소스 연결을 만듭니다](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Flow Service API를 사용하여 스트리밍 데이터를 수집합니다](../../tutorials/api/collect/streaming.md)

### UI 사용

- [UI에서 이벤트 허브 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [UI에서 클라우드 스토리지 연결에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
