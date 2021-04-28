---
keywords: IP 주소, IP 범위, 허용 목록 대상, 허용 목록에 추가하다
title: '클라우드 스토리지 대상에 대한 IP 주소 허용 목록 '
type: Documentation
description: 이 페이지는 Experience Platform에서 SFTP 서버, Amazon S3 또는 Azure Blob 저장소로 데이터를 안전하게 내보낼 수 있도록 허용 목록에 추가할 수 있는 IP 범위를 제공합니다.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
translation-type: tm+mt
source-git-commit: 4cc7fb2714f6df8065a0531f7e507983940d662c
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# 클라우드 스토리지 대상 {#ip-address-allow-list}에 대한 IP 주소 허용 목록

>[!IMPORTANT]
>
> * Adobe은 최신 IP 주소를 확인하기 위해 이 페이지를 책갈피에 추가하고 3개월마다 다시 방문하는 것이 좋습니다. Adobe은 새 IP 범위에 대한 알림을 제공하지 않습니다.
> * Adobe은 SFTP 서버로 데이터 내보내기를 지원하지만 데이터를 내보낼 권장되는 클라우드 저장소 위치는 [!DNL Amazon S3] 및 [!DNL Azure Blob]입니다.


## 개요 {#overview}

이 페이지에서는 Experience Platform에서 [SFTP 서버](./sftp.md)로 데이터를 안전하게 내보낼 수 있도록 허용 목록에 추가할 수 있는 IP 범위를 제공합니다.

네트워크 방화벽을 통해 네트워크 액세스 제어를 정의할 수 있습니다. 적절한 IP 범위를 지정하여 데이터 전송 서비스에 대한 트래픽을 허용할 수 있습니다.

Adobe에서는 클라우드 저장소 대상 연결을 사용하기 전에 다음 IP 범위를 허용 목록에 추가하는 것이 좋습니다. 클라우드 스토리지 대상 연결을 사용할 때 영역별 IP 범위를 허용 목록에 추가하지 않으면 오류나 비성능이 발생할 수 있습니다.

## 모든 고객에게 필요

* `52.247.108.70`

## 미국 고객

* `52.252.71.64/29`

## EMEA 고객

* `51.137.8.208/29`

## APAC 고객

* `20.53.201.168/29`
