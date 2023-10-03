---
title: 파트너가 제공한 속성으로 자사 프로필 보완
description: 신뢰할 수 있는 데이터 파트너의 속성으로 자사 프로필을 보완하여 데이터 기반을 개선하고 고객층에 대한 새로운 인사이트를 얻고 대상자 최적화를 개선하는 방법에 대해 알아봅니다.
exl-id: ee21b988-88f9-4c8e-bd82-7fc55c37ec24
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 90%

---

# 파트너가 제공한 속성으로 자사 프로필 보완

>[!AVAILABILITY]
>
>* 이 기능은 Real-Time CDP(앱 서비스), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate에 라이선스를 부여한 고객이 사용할 수 있습니다. 이 패키지에 대한 자세한 내용은 [제품 설명](https://helpx.adobe.com/legal/product-descriptions.html)을 참조하고 Adobe 담당자에게 문의하십시오.

신뢰할 수 있는 데이터 파트너의 속성으로 자사 프로필을 보완하여 데이터 기반을 개선하고 고객층에 대한 새로운 인사이트를 얻고 대상자 최적화를 개선합니다.

![파트너가 제공한 속성 사용 사례를 사용하여 프로필을 보강하는 높은 수준의 시각적 개요입니다.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## 전제 조건 및 계획 {#prerequisites-and-planning}

데이터 파트너의 속성으로 자사 프로필의 보완을 고려할 때 데이터 파트너와 데이터 보강 루프에 대한 다음 세부 정보를 논의하고 해결해야 합니다.

* 대상자 목록을 데이터 공급업체와 공유하기 위해 Real-Time CDP에서 내보낼 위치를 생각해 보십시오. 이 위치는 파일 내보내기를 지원해야 합니다.
* 추가 속성에 계층화할 수 있도록 데이터 공급업체가 기대하는 식별자는 무엇입니까?
* 파트너가 제공한 속성이 포함된 파일은 어떻게 Real-Time CDP에 다시 수집됩니까? 예를 들어 [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) 또는 [SFTP](/help/sources/connectors/cloud-storage/sftp.md)와 같은 클라우드 스토리지 소스 커넥터를 통해 파일을 수집할 수 있습니다.
* 파트너가 제공한 속성을 Real-Time CDP로 다시 가져와서 새로 고치는 예상 주기는 어떻게 됩니까?

>[!WARNING]
>
>Real-Time CDP에 수집된 파트너가 제공한 추가 속성은 *평균 프로필 풍부도*&#x200B;에 영향을 미칩니다. 프로필 풍부도에 대한 자세한 내용은 [Real-Time Customer Data Platform 제품 설명](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)을 참조하십시오.

## 비디오 워크스루 {#video-walkthrough}

파트너가 제공한 속성을 사용하여 자사 대상을 보완하는 방법에 대한 연습은 아래 비디오 튜토리얼을 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3423075/?learn=on)

## 사용 사례를 달성하는 방법: 높은 수준의 개요 {#achieve-the-use-case-high-level}

![파트너가 제공한 속성 사용 사례를 사용하여 프로필을 보강하는 높은 수준의 시각적 개요입니다.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. **고객**&#x200B;은 **데이터 파트너**&#x200B;의 속성에 라이선스를 부여합니다.
2. **고객**&#x200B;은 **파트너**&#x200B;가 제공한 속성을 수용할 수 있도록 프로필 데이터 및 거버넌스 모델을 확장합니다.
3. **고객**&#x200B;은 데이터 파트너와 함께 보강하고 싶은 대상자를 참여시킬 수 있습니다. 일반적으로 이러한 대상자는 이메일, 이름, 주소 등과 같은 개인 식별 정보(PII) 요소와 같은 입력 식별자를 제거합니다.
4. **파트너**&#x200B;는 일치시킬 수 있는 프로필에 대해 라이선스가 부여된 속성을 추가합니다. 필요한 경우 [파트너 ID](/help/identity-service/namespaces.md)를 포함하여 파트너 범위의 ID 네임스페이스에 가져올 수 있습니다.
5. **고객**&#x200B;은 Real-Time CDP에서 데이터 파트너의 속성을 고객 프로필로 로드합니다.

## 사용 사례 달성 방법: 단계별 지침 {#step-by-step-instructions}

위의 높은 수준의 개요에 있는 각 단계를 완료하려면 추가 설명서에 대한 링크가 포함된 아래 섹션을 읽어보십시오.

### 파트너의 속성에 라이선스 부여 {#license-attributes-from-partner}

이 단계는 [사전 요구 사항](#prerequisites-and-planning)에서 다루며, Adobe는 신뢰할 수 있는 데이터 공급업체와 계약을 체결하여 서드파티 프로필을 보강할 수 있다고 가정합니다.

### 파트너가 제공한 속성을 수용할 수 있도록 프로필 데이터 및 거버넌스 모델을 확장합니다. {#extend-governance-model}

이 시점에서 Real-Time CDP의 데이터 관리 프레임워크를 확장하여 파트너가 제공한 속성을 수용합니다.

**[!UICONTROL XDM 개별 프로필]** 클래스의 새 스키마를 만들거나 파트너가 제공한 속성을 포함하도록 동일한 유형의 기존 스키마를 확장할 수 있습니다. Adobe는 데이터 공급업체의 추가 속성을 가장 잘 나타내는 새로운 필드 그룹 세트로 새 스키마를 생성할 것을 강력히 권장합니다. 이를 통해 데이터 스키마가 정리되고 서로 독립적으로 발전할 수 있습니다.

파트너가 제공한 속성을 스키마에 포함하려면 원하는 속성으로 새 필드 그룹을 만들거나 Adobe에서 제공하는 미리 구성된 필드 그룹 중 하나를 사용할 수 있습니다.

자세한 내용은 아래의 설명서 페이지를 참조하십시오.

* [스키마 구성의 기본 사항](/help/xdm/schema/composition.md)
* [[!UICONTROL XDM 개별 프로필] 클래스의 개요](/help/xdm/classes/individual-profile.md)
* [UI에서 스키마 생성 및 편집](/help/xdm/ui/resources/schemas.md)
* [UI에서 스키마 필드 그룹 생성 및 편집](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

또한 이 단계에서는 파트너가 제공한 서드파티 데이터를 포함하도록 데이터 관리 전략을 확장할 때 데이터 거버넌스 모델의 변경 방식에 대해 살펴봅니다. 아래 설명서 링크에서 고려 사항을 살펴보십시오.

* (**준비 중**) 서드파티 데이터를 삭제하고 통합 실행을 취소하기 쉽도록 별도의 데이터 세트에 보관합니다.
* (**준비 중**) 데이터 위생 추가 기능을 구입한 클라이언트의 데이터 세트에서 [데이터 세트 만료](/help/hygiene/ui/dataset-expiration.md) 기능을 사용합니다.
* (**준비 중**) 서드파티 데이터를 혼합한 후에는 전체 파생 데이터 세트를 삭제하는 것만이 서드파티 데이터를 제거하는 유일한 방법이기 때문에 서드파티 데이터를 가져오는 파생 데이터 세트를 만들 때는 주의해야 합니다.

>[!TIP]
>
>데이터 공급업체의 사용자 기반 식별자로 고객 프로필을 보완하도록 선택한 경우 **[[!UICONTROL 파트너 ID]](/help/identity-service/namespaces.md)** 유형의 새 ID 유형을 생성할 수 있습니다.
>
>[ID 유형 섹션](/help/identity-service/namespaces.md)의 파트너 ID에 대해 자세히 알아보십시오.
>Experience Platform 사용자 인터페이스에서 [ID 필드를 정의하는 방법](/help/xdm/ui/fields/identity.md)에 대해 알아보십시오.

### 개인 식별 정보(PII) 또는 해시된 PII를 제거할 때 보강하려는 대상자를 내보냅니다. {#export-audiences}

파트너가 보강할 대상자를 내보냅니다. Amazon S3 또는 SFTP와 같이 Real-Time CDP에서 제공하는 클라우드 스토리지 대상을 사용합니다. 이 단계를 완료하려면 다음 설명서 페이지를 읽으십시오.

* [Amazon S3 대상](/help/destinations/catalog/cloud-storage/amazon-s3.md) 설명서 페이지
* [SFTP 대상](/help/destinations/catalog/cloud-storage/sftp.md) 설명서 페이지
* [대상에 연결](/help/destinations/ui/connect-destination.md)하는 방법
* [클라우드 스토리지 대상에 데이터를 내보내는](/help/destinations/ui/activate-batch-profile-destinations.md) 방법

### 데이터 파트너는 일치시킬 수 있는 프로필에 대해 라이선스가 부여된 속성을 추가합니다. {#partner-appends-attributes}

이 단계에서 데이터 파트너는 내보낸 대상자에 대해 라이선스가 부여된 속성을 추가합니다. 출력은 일반적으로 Real-Time CDP로 다시 수집할 수 있는 플랫 파일로 제공됩니다. [Real-Time CDP로 파일 수집](/help/ingestion/tutorials/ingest-batch-data.md#upload-file)에 대해 알아보십시오.

### Real-Time CDP는 보강된 속성을 고객 프로필에 추가합니다. {#ingest-data}

이제 소스 커넥터를 통해 파트너로부터 데이터를 수집하여 보강된 데이터를 Real-Time CDP로 가져와서 파트너가 제공한 데이터로 프로필을 보완해야 합니다.

이 용도로 권장되는 일부 소스 커넥터는 다음과 같습니다.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## 제한 사항 및 문제 해결 {#limitations-and-troubleshooting}

이 페이지에 설명된 사용 사례를 탐색할 때 다음 제한 사항에 유의하십시오.

* 파트너 ID를 사용하기로 선택한 경우 [ID 그래프](/help/identity-service/ui/identity-graph-viewer.md)를 구축할 때 이 ID는 사용하지 않습니다.

## 파트너 데이터 지원을 통해 달성한 기타 사용 사례 {#other-use-cases}

Real-Time CDP에서 파트너 데이터 지원을 통해 활성화된 추가 사용 사례를 살펴보십시오.

* Real-Time CDP에서 서드파티 데이터 지원을 사용하여 [데이터 파트너의 잠재 고객 프로필로 프로필 기반을 확장하고 데이터 파트너와 협력하여 신규 고객에게 도달하거나 확보할 수 있습니다](/help/rtcdp/partner-data/prospecting.md).
* [온사이트 경험을 개인화하기 위해 파트너 지원 인식 활용](/help/rtcdp/partner-data/onsite-personalization.md) 방문에서 사용자 인증이 없거나 브랜드와 이전 기록이 있는 경우.
* [잠재 고객 프로필 및 잠재 고객 활성화 확장](/help/destinations/ui/activate-prospect-audiences.md) 대상을 선택합니다.
