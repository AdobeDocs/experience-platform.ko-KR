---
keywords: IP 주소, IP 범위, 허용 목록, 스트리밍 대상 허용 목록 허용 목록에 추가하다
title: 허용 목록에 추가하다 스트리밍 대상의 IP 주소
type: Documentation
description: 이 페이지에서는 Experience Platform에서 HTTP REST API 끝점, Amazon Kinesis 또는 Azure Event Hubs 인스턴스로 데이터를 안전하게 내보내도록 허용 목록에 추가할 수 있는 IP 범위를 제공합니다.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 5c67466f5321038e75d22e216a8be2e745adac49
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# 허용 목록에 추가하다 스트리밍 대상의 IP 주소 {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe은 이 페이지에 책갈피를 지정하고 3개월마다 다시 방문하여 최신 IP 주소를 확인하는 것을 권장합니다. Adobe은 새 IP 범위에 대한 알림을 제공하지 않습니다.
> * 여기에 문서화된 IP 목록 *은(는)*&#x200B;을(를) 사용하여 빌드하는 대상에 적용되지 않습니다[[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).

## 개요 {#overview}

여기에 설명된 IP 범위는 다음 대상에 적용됩니다.

* [HTTP API 대상](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Experience Platform에서 이러한 대상으로의 아웃바운드 트래픽은 항상 이 페이지에 나열된 IP를 통해 이동합니다.

이 페이지에서는 Experience Platform에서 HTTP 끝점, [!DNL Amazon Kinesis] 또는 [!DNL Azure Event Hubs] 인스턴스로 데이터를 안전하게 내보내기 위해 허용 목록에 추가하다에 추가할 수 있는 IP 범위를 제공합니다. 이 기능은 HTTP 끝점이 엔터프라이즈 방화벽 뒤에 있거나 회사 보안 및 규정 준수 표준에서 IP 범위 목록을 허용 목록에추가된으로 유지해야 하는 경우에 특히 유용합니다.

네트워크 방화벽을 통해 네트워크 액세스 제어를 정의할 수 있습니다. 적절한 IP 범위를 지정하여 데이터 전송 서비스에 트래픽을 허용할 수 있습니다.

Adobe은 이 페이지에서 위에 언급된 대상으로 작업하기 전에 다음 IP 범위를 허용 목록에 추가하다에 추가할 것을 권장합니다. 지역에 따른 IP 범위를 허용 목록에 추가하다에 추가하지 않으면 이러한 스트리밍 대상을 사용할 때 오류나 성능이 저하될 수 있습니다.

## VA7: 미국 및 아메리카 고객 {#us-americas}

* `4.152.211.251`
* `20.22.83.112`
* `20.186.185.181`
* `20.186.185.227`
* `20.186.185.239`
* `40.70.154.136/29`
* `52.254.105.192/28`
* `52.254.106.0/28`
* `52.254.106.144/28`
* `52.254.106.160/28`
* `52.254.106.176/28`
* `52.254.106.192/28`
* `52.254.106.208/28`
* `52.254.106.224/28`
* `52.254.106.240/28`
* `52.254.107.0/28`
* `52.254.107.16/28`
* `52.254.107.32/28`
* `52.254.107.64/28`
* `52.254.107.80/28`
* `52.254.107.128/28`
* `52.254.107.144/28`

## VA6: AWS에서 실행하는 미국 및 아메리카 고객 {#aws}

아래 IP 범위는 Amazon Web Services(AWS)에서 실행 중인 Experience Platform 고객에게 적용됩니다. 자세한 내용은 [Experience Platform Multi-Cloud 개요](../../../landing/multi-cloud.md)를 참조하십시오.

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

## NLD2: EMEA 고객 {#emea}

* `20.50.23.153`
* `20.101.246.9`
* `40.74.3.176/28`
* `40.74.4.144/28`
* `40.74.4.160/28`
* `40.74.4.176/28`
* `40.74.5.128/28`
* `40.74.6.80/28`
* `40.74.6.96/28`
* `40.74.6.112/28`
* `40.74.6.128/28`
* `40.74.6.144/28`
* `40.74.7.128/28`
* `40.74.7.144/28`
* `40.74.7.160/28`
* `40.74.7.176/28`
* `40.74.7.192/28`
* `40.74.7.208/28`
* `51.105.144.1`
* `51.105.144.81`
* `51.124.70.4`
* `51.144.184.248/29`
* `52.142.236.87`
* `108.141.12.47`

## AUS5: APAC 고객 {#apac}

* `20.40.188.166`
* `20.40.188.194`
* `20.40.188.227`
* `20.40.191.96/28`
* `20.40.191.224/28`
* `20.40.191.240/28`
* `20.43.104.0/28`
* `20.43.104.16/28`
* `20.43.104.32/28`
* `20.43.104.48/28`
* `20.43.104.64/28`
* `20.43.104.80/28`
* `20.43.104.96/28`
* `20.43.104.112/28`
* `20.43.104.128/28`
* `20.43.104.144/28`
* `20.43.104.160/28`
* `20.43.104.176/28`
* `20.43.104.192/28`
* `20.43.105.0/28`
* `20.43.105.16/28`
* `20.43.105.32/28`
* `20.43.105.48/28`
* `20.227.35.177`
* `20.53.206.128`

## CAN2: 캐나다 고객 {#can}

* `20.104.46.64/28`
* `20.104.46.80/28`
* `20.104.46.128/28`
* `20.104.46.160/28`
* `20.116.145.94`
* `20.116.147.168`
* `20.200.70.192/28`
* `20.200.70.208/28`
* `20.200.70.224/28`
* `20.200.70.240/28`
* `20.200.71.0/28`
* `20.200.71.16/28`
* `20.200.71.32/28`
* `20.200.71.48/28`
* `20.200.71.64/28`
* `20.200.71.80/28`
* `20.200.71.96/28`
* `20.200.71.112/28`
* `20.200.71.128/28`
* `20.200.71.144/28`
* `20.200.71.160/28`
* `20.200.71.176/28`
* `20.200.93.180`
* `20.200.94.83`
* `20.200.94.116`

## GBR9: 영국 고객 {#gbr}

* `20.26.64.112/28`
* `20.26.64.208/28`
* `20.26.64.240/28`
* `20.26.65.0/28`
* `20.26.128.247`
* `20.26.130.226`
* `20.26.131.71`
* `20.108.119.100`
* `20.108.202.84`
* `20.254.1.128/28`
* `20.254.2.32/28`
* `20.254.2.128/28`
* `20.254.2.208/28`
* `20.254.3.32/28`
* `20.254.3.48/28`
* `20.254.3.112/28`
* `20.254.3.144/28`
* `20.254.3.176/28`
* `20.254.3.192/28`
* `20.254.3.240/28`
* `20.254.4.0/28`
* `20.254.4.16/28`
* `20.254.4.32/28`
* `20.254.4.64/28`
* `20.254.4.96/28`

## IND2: 인도 고객 {#india}

* `4.188.4.11`
* `4.188.4.99`
* `4.188.4.138`
* `4.188.4.154`
* `4.188.4.167`
* `4.213.40.145`
* `4.224.74.0/28`
* `4.224.74.64/28`
* `4.224.74.80/28`
* `4.224.74.96/28`
* `20.244.74.112/28`
* `20.244.77.0/28`
* `20.244.77.16/28`
* `20.244.77.160/28`
* `20.244.77.208/28`
* `20.244.78.0/28`
* `20.244.78.208/28`
* `20.244.79.0/28`
* `20.244.79.16/28`
* `20.244.79.48/28`
* `20.244.79.80/28`
* `20.244.79.128/28`
* `20.244.79.144/28`
* `20.244.79.192/28`
* `20.244.79.208/28`
* `20.244.79.224/28`
