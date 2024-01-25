---
title: 새 Beta 클라우드 스토리지 대상에서 마지막 자격 시간 XDM 속성 사용
description: 새 Beta 클라우드 스토리지 대상에서 마지막 자격 시간 XDM 속성을 사용하는 방법을 알아봅니다
badgeBeta: label="Beta" type="Informative"
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 7130ac46a7768ea6e71bf73eb970bf2890323d0f
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# 새 Beta 클라우드 스토리지 대상에서 마지막 자격 시간 XDM 속성 사용 {#last-qualification-time}

>[!IMPORTANT]
> 
>이 페이지에서는 Beta 기능에 대해 설명합니다. 기능 및 설명서는 변경될 수 있습니다. 이 Beta 프로그램에 액세스하려면 Adobe 담당자 또는 고객 지원 센터에 문의하십시오.

## 전제 조건 {#prerequisites}

최종 선별 시간 사용(`lastQualificationTime`) XDM 속성에서 아래 나열된 6개의 클라우드 스토리지 대상 중 하나로 데이터를 내보내야 합니다.

* [[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md)
* [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)
* [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)

## 마지막 선별 시간 XDM 속성을 사용하는 방법 {#how-to-use}

위에 나열된 6개의 클라우드 스토리지 커넥터 중 하나를 사용하는 경우,에서 마지막 검증 시간 XDM 속성을 사용할 수 있습니다. [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 프로필이 세그먼트에 적합한 경우 최신 타임스탬프로 내보낸 파일에 열을 만드는 활성화 워크플로. 이렇게 하면 특정 측정 또는 분석 사용 사례에 도움이 될 뿐만 아니라 특정 대상을 활성화할 시기를 더 잘 파악할 수 있습니다.

추가하려면 다음을 참고하십시오. `lastQualificationTime` 파일 내보내기에 대해 현재 값을 수동으로 삽입해야 합니다 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 아래 표시된 대로 소스 필드로 이동합니다. 대상 필드를 편집할 수도 있습니다. `lastQualificationTime` 또는 이 열의 이름을 지정할 다른 모든 값. 베타 기능이므로 구문 `xdm: segmentMembership.ups.seg_id.lastQualificationTime` 값은 향후에 변경될 수 있습니다.

![매핑 단계로 붙여넣은 마지막 선별 시간 XDM 속성을 보여 주는 화면 레코딩](/help/destinations/ui/last-qualification-time.gif)

## 추가 정보 {#more-information}

워크플로우의 모든 단계 및 필요한 권한을 포함하여 파일 기반 대상으로 데이터를 활성화하는 방법에 대한 자세한 내용은 [파일 기반 대상 활성화 자습서](/help/destinations/ui/activate-batch-profile-destinations.md).
