---
keywords: IP 주소, IP 범위, 허용 목록 대상, 허용 목록에 추가하다 스트리밍 허용 목록에 추가하다 대상
title: 스트리밍 대상을 허용 목록에 추가하다 위한 IP 주소
type: Documentation
description: 이 페이지에서는 Experience Platform에서 HTTP REST API 엔드포인트, Amazon Kinesis 또는 Azure 이벤트 허브 인스턴스로 데이터를 안전하게 내보내기 위해 허용 목록에 추가할 수 있는 IP 범위를 제공합니다.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 8ea871d3ba66b9ee1a864a6319cde21f518f4534
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# 스트리밍 대상을 허용 목록에 추가하다 위한 IP 주소 {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe은 이 페이지를 책갈피로 지정하고 3개월마다 다시 방문하여 최신 IP 주소를 확인하는 것을 권장합니다. Adobe은 새 IP 범위에 대한 알림을 제공하지 않습니다.
> * 여기에 설명된 IP 목록 *포함하지 않음* 을 사용하여 빌드하는 모든 대상에 적용 [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).


## 개요 {#overview}

여기에 설명된 IP 범위는 다음 대상에 적용됩니다.

* [HTTP API 대상](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Experience Platform에서 이러한 대상으로의 아웃바운드 트래픽은 항상 이 페이지에 나열된 IP를 통해 수행됩니다.

이 페이지에서는 Experience Platform에서 HTTP 종단점으로 데이터를 안전하게 허용 목록에 추가하다 내보내기 위해에 추가할 수 있는 IP 범위를 제공합니다. [!DNL Amazon Kinesis], 또는 [!DNL Azure Event Hubs] 인스턴스. 이 기능은 HTTP 종단점이 엔터프라이즈 방화벽 뒤에 있거나 회사 보안 및 규정 준수 표준에 IP 범위 목록을 허용 목록에추가된으로 설정해야 하는 경우에 특히 유용합니다.

네트워크 방화벽을 통해 네트워크 액세스 제어를 정의할 수 있습니다. 적절한 IP 범위를 지정하여 데이터 전송 서비스에 대한 트래픽을 허용할 수 있습니다.

Adobe은 이 페이지에서 위에 허용 목록에 추가하다 언급된 대상으로 작업하기 전에 다음 IP 범위를에 추가할 것을 권장합니다. 이러한 스트리밍 대상을 사용할 때 지역별 IP 범위를에 추가하지 허용 목록에 추가하다 않으면 오류 또는 성능이 저하될 수 있습니다.

## VA7: 미국 및 미국 고객 {#us-americas}

`20.186.185.239`
`40.70.154.136/29`
`52.254.106.160/28`
`52.254.106.176/28`
`52.254.105.192/28`
`20.186.185.181`
`52.254.107.64/28`
`52.254.107.80/28`
`52.254.106.144/28`
`52.254.106.0/28`
`52.254.107.16/28`
`52.254.107.32/28`
`52.254.106.224/28`
`20.186.185.227`
`52.254.106.192/28`
`52.254.107.128/28`
`52.254.106.208/28`
`52.254.106.240/28`
`52.254.107.0/28`
`52.254.107.144/28`

## NLD2: EMEA 고객 {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`40.74.4.144/28`
`40.74.7.160/28`
`40.74.3.176/28`
`40.74.6.144/28`
`40.74.6.80/28`
`40.74.5.128/28`
`40.74.7.144/28`
`40.74.7.176/28`
`40.74.6.96/28`
`40.74.6.112/28`
`51.105.144.1`
`40.74.7.192/28`
`51.105.144.81`
`51.124.70.4`

## AUS5: APAC 고객 {#apac}

`20.43.104.80/28`
`20.43.104.16/28`
`20.43.104.128/28`
`20.40.188.166`
`20.40.191.224/28`
`20.43.104.176/28`
`20.43.104.0/28`
`20.43.105.0/28`
`20.43.105.48/28`
`20.40.191.240/28`
`20.43.104.192/28`
`20.40.188.227`
`20.40.188.194`
`20.43.104.144/28`
`20.43.104.160/28`
`20.43.104.96/28`
`20.43.105.32/28`
`20.43.104.112/28`
`20.43.105.16/28`
`20.43.104.48/28`
`20.40.191.96/28`
`20.43.104.32/28`
`20.43.104.64/28`
