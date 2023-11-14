---
title: IP 주소 허용 목록 SFTP 대상
type: Documentation
description: 이 페이지에서는 데이터를 Experience Platform에서 SFTP 서버로 안전하게 내보내기 위해 허용 목록에 추가할 수 있는 IP 범위를 제공합니다.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 3d870975593313062d796601f0e19a0a3aec7854
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 허용 목록에 추가하다 SFTP 대상의 IP 주소 {#ip-address-allow-list-sftp}

>[!IMPORTANT]
>
> * Adobe은 이 페이지에 책갈피를 지정하고 3개월마다 다시 방문하여 최신 IP 주소를 확인하는 것을 권장합니다. Adobe은 새 IP 범위에 대한 알림을 제공하지 않습니다.
> * Adobe은 SFTP 서버로 데이터 내보내기를 지원하지만 데이터를 내보내는 데 권장되는 클라우드 스토리지 위치는 다음과 같습니다 [!DNL Amazon S3] 및 [!DNL Azure Blob].

## 개요 {#overview}

이 페이지는 Experience Platform에서 로 데이터를 안전하게 내보내기 위해 허용 목록에 추가하다에 추가할 수 있는 IP 범위를 제공합니다. [SFTP 서버](./sftp.md).

네트워크 방화벽을 통해 네트워크 액세스 제어를 정의할 수 있습니다. 적절한 IP 범위를 지정하여 데이터 전송 서비스에 트래픽을 허용할 수 있습니다.

Adobe은 클라우드 스토리지 연결을 사용하기 전에 다음 IP 범위를 허용 목록에 추가하다에 추가할 것을 권장합니다. 클라우드 스토리지 대상 연결을 사용할 때 지역별 IP 범위를 허용 목록에 추가하지 않으면 오류 또는 성능이 저하될 수 있습니다.

## 모든 고객에 필요

* `52.247.108.70`

## 미국 고객

* `52.252.71.64/29`

## EMEA 고객

* `51.137.8.208/29`

## APAC 고객

* `20.53.201.168/29`
