---
keywords: Experience Platform;홈;인기 항목;Azure Event Hubs;Azure Event Hubs;이벤트 허브;이벤트 허브
solution: Experience Platform
title: Azure Event Hubs 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Azure Event Hubs를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform], 및 [!DNL Azure]. 이러한 시스템에서 데이터를 플랫폼으로 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 포맷 또는 업로드 없이도 고유한 데이터를 플랫폼으로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. 플랫폼에서 의 데이터를 가져올 수 있습니다. [!DNL Event Hubs] 실시간으로.

## 다음으로 크기 조절 [!DNL Event Hubs]

의 척도 요소 [!DNL Event Hubs] 대용량 데이터를 입력하거나, 병렬 처리를 늘리거나, 수집 플랫폼의 속도를 높여야 하는 경우 인스턴스를 늘려야 합니다.

### 더 높은 볼륨 데이터 수신

현재, 에서 가져올 수 있는 최대 데이터 볼륨입니다 [!DNL Event Hubs] Platform에 대한 계정은 초당 2000개의 레코드입니다. 더 많은 볼륨 데이터를 확장 및 수집하려면 Adobe 담당자에게 문의하십시오.

### 에서 병렬 처리 수 늘리기 [!DNL Event Hubs] 및 플랫폼

병렬화란 속도와 성능을 높이기 위해 여러 처리 장치에서 동일한 작업을 동시에 실행하는 것을 말합니다. 에서 병렬 처리를 늘릴 수 있습니다. [!DNL Event Hubs] 파티션을 늘리거나 [!DNL Event Hubs] 계정입니다. 이 항목 보기 [[!DNL Event Hubs] 크기 조정 문서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) 추가 정보.

플랫폼 측에서 수집 속도를 높이려면 플랫폼에서 소스 커넥터의 작업 수를 늘려야 합니다. [!DNL Event Hubs] 파티션. 에 대한 병렬 처리를 늘린 후 [!DNL Event Hubs] 또한 Adobe 담당자에게 연락하여 새 파티션을 기반으로 플랫폼 작업의 크기를 조정하십시오. 현재 이 프로세스는 자동화되지 않습니다.

## 가상 네트워크를 사용하여 연결 [!DNL Event Hubs] 대상 플랫폼

연결할 가상 네트워크를 설정할 수 있습니다. [!DNL Event Hubs] 방화벽 조치를 활성화한 상태에서 플랫폼으로 이동합니다. 가상 네트워크를 설정하려면 다음과 같이 하십시오. [[!DNL Event Hubs] 네트워크 규칙 세트 문서](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) 아래에 나열된 단계를 수행합니다.

* 선택 **사용해 보기** REST API 패널에서
* 인증 [!DNL Azure] 동일한 브라우저에서 자격 증명을 사용하는 계정
* 다음 항목 선택 [!DNL Event Hubs] 플랫폼으로 가져온 다음 선택할 네임스페이스, 리소스 그룹 및 구독 **실행**;
* 표시되는 JSON 본문에서 아래에 다음 플랫폼 서브넷을 추가합니다. `virtualNetworkRules` 내부 `properties`:


>[!IMPORTANT]
>
>업데이트하기 전에 받은 JSON 본문을 백업해야 합니다 `virtualNetworkRules` 기존 IP 필터링 규칙이 포함되어 있는 플랫폼 서브넷을 사용합니다. 그렇지 않으면 호출 후에 규칙이 삭제됩니다.


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

다음을 참조하십시오 [[!DNL Event Hubs] 문서](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) 네트워크 규칙 세트에 대한 자세한 내용을 참조하십시오.

## 연결 [!DNL Event Hubs] 대상 플랫폼

아래 설명서는 연결 방법에 대한 정보를 제공합니다 [!DNL Event Hubs] API 또는 사용자 인터페이스를 사용하여 Platform으로

### API 사용

* [흐름 서비스 API를 사용하여 이벤트 허브 소스 연결 만들기](../../tutorials/api/create/cloud-storage/eventhub.md)
* [흐름 서비스 API를 사용하여 스트리밍 데이터 수집](../../tutorials/api/collect/streaming.md)

### UI 사용

* [UI에서 이벤트 허브 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
