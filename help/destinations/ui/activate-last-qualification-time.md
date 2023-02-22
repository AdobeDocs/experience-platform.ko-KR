---
title: 새로운 베타 클라우드 스토리지 대상에서 마지막 자격 시간 XDM 속성을 사용합니다
description: 새로운 베타 클라우드 스토리지 대상에서 마지막 검증 시간 XDM 속성을 사용하는 방법을 알아봅니다
hidefromtoc: y
hide: y
source-git-commit: 03031dcaad82932f92e76177adf3b55447c3c153
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# 새로운 베타 클라우드 스토리지 대상에서 마지막 자격 시간 XDM 속성을 사용합니다 {#last-qualification-time}

>[!IMPORTANT]
> 
>이 페이지에서는 베타에 있는 기능에 대해 설명합니다. 기능 및 설명서는 변경될 수 있습니다. 이 베타 프로그램에 액세스하려면 Adobe 담당자 또는 고객 지원 센터에 문의하십시오.

## 전제 조건 {#prerequisites}

마지막 자격 시간을 사용하려면`lastQualificationTime`) XDM 속성을 사용하려면 [베타 프로그램](/help/release-notes/2022/october-2022.md#destinations) 향상된 파일 내보내기 기능을 사용하고 데이터를 6개 중 하나로 내보내려면 다음을 수행하십시오 [베타 클라우드 스토리지 대상](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)). 아래에 표시된 대로 카탈로그에서 클라우드 스토리지 대상에 대한 새 베타 카드를 볼 수 있으면 등록됩니다 [!DNL Amazon S3].

![새로운 Amazon S3 베타 카드를 보여주는 이미지](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## 마지막 자격 시간 XDM 속성을 사용하는 방법 {#how-to-use}

6개의 새로운 클라우드 스토리지 베타 커넥터 중 하나를 사용하는 경우, 에서 마지막 자격 시간 XDM 속성을 사용할 수 있습니다 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 활성화 워크플로우 를 사용하십시오. 이를 통해 특정 측정 또는 분석 사용 사례를 사용할 수 있을 뿐만 아니라 특정 대상을 활성화할 시점을 더 잘 알 수 있습니다.

추가할 참고 사항 `lastQualificationTime` 파일 내보내기에 대해서는 현재 값을 수동으로 삽입해야 합니다 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 아래와 같이 소스 필드에 포함합니다. 대상 필드를 편집할 수도 있습니다 `lastQualificationTime` 또는 이 열의 이름을 지정할 다른 값입니다. 베타 기능이므로 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 값은 향후에 변경될 수 있습니다.

![마지막 자격 시간을 보여주는 화면 기록 XDM 속성을 매핑 단계에 붙여 넣습니다](/help/destinations/ui/last-qualification-time.gif)

## 추가 정보 {#more-information}

워크플로우의 모든 단계 및 필요한 권한을 포함하여 파일 기반 대상으로 데이터를 활성화하는 방법에 대한 광범위한 정보는 다음을 참조하십시오. [파일 기반 대상 활성화 자습서](/help/destinations/ui/activate-batch-profile-destinations.md).