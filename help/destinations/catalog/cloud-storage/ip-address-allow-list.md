---
title: 파일 기반 클라우드 스토리지 대상에 대한 IP 주소 허용 목록
type: Documentation
description: 이 페이지에서는 Experience Platform에서 클라우드 스토리지 대상으로 데이터를 안전하게 내보내기 위해 허용 목록에 추가할 수 있는 IP 범위를 제공합니다.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 118b0b5e6a1936b644da4153fe7bfeb872ae137e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# 허용 목록에 추가하다 파일 기반 클라우드용 IP 주소 스토리지 대상 {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe은 이 페이지에 책갈피를 지정하고 3개월마다 다시 방문하여 최신 IP 주소를 확인하는 것을 권장합니다. Adobe은 새 IP 범위에 대한 알림을 제공하지 않습니다.
> * Adobe은 SFTP 서버로 데이터 내보내기를 지원하지만 데이터를 내보내는 데 권장되는 클라우드 저장소 위치는 [!DNL Amazon S3] 및 [!DNL Azure Blob]입니다.

## 적용 가능성 {#applicability}

이 페이지의 IP 범위 정보는 대상 카탈로그의 다음 파일 기반 클라우드 스토리지 커넥터에 적용됩니다.

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Google 클라우드 저장소]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>이 페이지에 문서화된 IP 범위는 파일 기반 클라우드 저장소 대상 [!UICONTROL Azure Blob], [!UICONTROL Azure Data Lake Storage Gen2] 및 [!UICONTROL 데이터 랜딩 영역]에 대해 *지원되지 않음*&#x200B;입니다.

## 개요 {#overview}

이 페이지에서는 Experience Platform에서 여러 클라우드 스토리지 대상으로 데이터를 안전하게 내보내기 위해 허용 목록에 추가하다에 추가할 수 있는 IP 범위를 제공합니다.

네트워크 방화벽을 통해 네트워크 액세스 제어를 정의할 수 있습니다. 적절한 IP 범위를 지정하여 데이터 전송 서비스에 트래픽을 허용할 수 있습니다.

Adobe에서는 클라우드 스토리지 대상 연결을 사용하기 전에 다음 IP 범위를 허용 목록에 추가하다에 추가할 것을 권장합니다. 클라우드 스토리지 대상 연결을 사용할 때 지역별 IP 범위를 허용 목록에 추가하지 않으면 오류 또는 성능이 저하될 수 있습니다.

## 모든 고객에 필요 {#all-customers}

* `52.247.108.70`

## AWS에서 실행 중인 미국 고객 {#aws}

아래 IP 범위는 Amazon Web Services(AWS)에서 실행 중인 Experience Platform 고객에게 적용됩니다. 자세한 내용은 [Experience Platform Multi-Cloud 개요](../../../landing/multi-cloud.md)를 참조하십시오.

>[!NOTE]
>
>이 IP 범위는 AWS에서 실행 중인 고객 중 파일 기반 대상을 사용하여 데이터를 Amazon S3로 내보내는 고객에게는 지원되지 않습니다.

* `66.117.18.0/24`

## 미국 고객 {#us-customers}

* `52.252.71.64/29`

## 캐나다 고객 {#canada-customers}

* `20.220.135.16/29`

## EMEA 고객 {#emea-customers}

* `51.137.8.208/29`

## 영국 고객 {#uk-customers}

* `20.26.133.96/29`

## APAC 고객 {#apac-customers}

* `20.53.201.168/29`
