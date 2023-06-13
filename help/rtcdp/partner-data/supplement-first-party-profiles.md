---
title: (베타) 파트너가 제공한 속성으로 자사 프로필 보완
description: 신뢰할 수 있는 데이터 파트너의 속성으로 자사 프로필을 보완하여 데이터 기반을 개선하고, 고객 기반에 대한 새로운 통찰력을 얻고, 대상 최적화를 향상시키는 방법을 알아봅니다
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: c4f34afb7a05707ed9f62f09685ff50a1de2ef93
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 0%

---

# 파트너가 제공한 속성으로 자사 프로필 보완

>[!AVAILABILITY]
>
>* 이 Beta 기능은 Real-Time CDP(앱 서비스), Adobe Experience Platform Activation, Real-time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate 라이선스가 있는 고객이 사용할 수 있습니다. 다음에서 이 패키지에 대해 자세히 알아보십시오. [제품 설명](https://helpx.adobe.com/legal/product-descriptions.html) 자세한 내용은 Adobe 담당자에게 문의하십시오.

신뢰할 수 있는 데이터 파트너의 속성으로 자사 프로필을 보완하여 데이터 기반을 개선하고 고객 기반에 대한 새로운 통찰력을 확보하며 더 나은 고객 최적화를 얻을 수 있습니다.

![파트너가 제공한 속성을 사용하여 프로필을 보강합니다. 사용 사례 높은 수준의 시각적 개요.](/help/rtcdp/assets/partner-data/enrichment-use-case-overview.png)

## 사전 요구 사항 및 계획 {#prerequisites-and-planning}

데이터 파트너의 속성으로 자사 프로필을 보완하는 것을 고려할 때 데이터 파트너와 데이터 보강 루프에 대해 다음 세부 사항을 논의하고 해결해야 합니다.

* 대상 목록을 Real-Time CDP에서 내보내 데이터 공급업체와 공유할 위치에 대해 생각해 보십시오. 이 위치는 파일 내보내기를 지원해야 합니다.
* 데이터 공급업체가 추가 속성에 대해 계층화할 수 있도록 기대하는 식별자는 무엇입니까?
* 파트너가 제공한 속성이 포함된 파일은 어떻게 실시간 CDP로 다시 수집됩니까? 예를 들어 다음과 같은 클라우드 스토리지 소스 커넥터를 통해 파일을 수집할 수 있습니다. [Amazon](/help/sources/connectors/cloud-storage/s3.md) 또는 [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* 파트너가 제공한 속성을 Real-Time CDP으로 다시 가져와 새로 고치는 케이던스는 무엇입니까?

>[!WARNING]
>
>Real-Time CDP에 수집된 추가 파트너 제공 속성은 다음 사항에 영향을 줍니다. *평균 프로필 풍부도*. 읽기 [Real-time Customer Data Platform 제품 설명](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 프로필 풍부성에 대한 자세한 정보입니다.

## 사용 사례 달성 방법: 높은 수준 개요 {#achieve-the-use-case-high-level}

![파트너가 제공한 속성을 사용하여 프로필을 보강합니다. 사용 사례 높은 수준의 시각적 개요.](/help/rtcdp/assets/partner-data/enrichment-use-case-steps.png)

1. 로서의 **고객**, 다음에서 속성을 라이선스를 부여합니다. **데이터 파트너**.
2. 로서의 **고객**, 를 포함하도록 프로필 데이터 및 거버넌스 모델을 확장합니다. **파트너**-제공된 특성입니다.
3. 로서의 **고객**, 데이터 파트너에 보강할 대상을 온보딩합니다. 일반적으로 이러한 대상은 이메일, 이름, 주소 또는 기타 요소와 같은 PII(개인 식별 정보) 요소와 같은 입력 식별자에서 제외됩니다.
4. 다음 **파트너** 일치하는 수 있는 프로필에 대해 라이선스가 부여된 속성을 추가합니다. 필요한 경우 [파트너 ID](/help/identity-service/namespaces.md) 파트너 범위 ID 네임스페이스에 포함되고 수집될 수 있습니다.
5. 로서의 **고객**, 데이터 파트너의 속성을 Real-Time CDP의 고객 프로필로 로드합니다.

## 사용 사례 달성 방법: 단계별 지침 {#step-by-step-instructions}

추가 설명서에 대한 링크가 포함된 아래 섹션을 읽어 위의 높은 수준 개요에서 각 단계를 완료합니다.

### 파트너의 라이선스 속성 {#license-attributes-from-partner}

이 단계는 전제 조건에서 다루며, Adobe은 사용자가 신뢰할 수 있는 데이터 공급업체와 적절한 계약 계약을 체결하여 자사 프로필을 보강했다고 가정합니다.

### 파트너가 제공한 속성을 수용하도록 프로필 데이터 및 거버넌스 모델을 확장합니다. {#extend-governance-model}

이제 파트너가 제공한 특성을 수용하도록 Real-Time CDP에서 데이터 관리 프레임워크를 확장합니다.

의 새 스키마를 생성할 수 있는 옵션이 있습니다 **[!UICONTROL XDM 개별 프로필]** 파트너가 제공한 속성을 포함하도록 동일한 유형의 기존 스키마를 클래스화하거나 확장합니다. Adobe은 데이터 공급업체의 추가 속성을 가장 잘 나타내는 새 필드 그룹 세트로 새 스키마를 만들 것을 강력히 권장합니다. 이렇게 하면 데이터 스키마가 깔끔하고 서로 독립적으로 발전할 수 있습니다.

Adobe에 파트너가 제공한 속성을 포함하기 위해 기대하는 속성으로 새 필드 그룹을 만들거나 파트너가 제공한 기본 필드 그룹 중 하나를 사용할 수 있습니다.

자세한 내용은 아래 설명서 페이지를 참조하십시오.

* [스키마 컴포지션의 기본 사항](/help/xdm/schema/composition.md)
* [개요 [!UICONTROL XDM 개별 프로필] 클래스](/help/xdm/classes/individual-profile.md)
* [UI에서 스키마 만들기 및 편집](/help/xdm/ui/resources/schemas.md)
* [UI에서 스키마 필드 그룹 만들기 및 편집](/help/xdm/ui/resources/field-groups.md)
* [API를 사용하여 스키마 만들기 및 편집](/help/xdm/api/schemas.md#create)
* [API를 사용하여 필드 그룹을 추가하도록 기존 스키마 업데이트](/help/xdm/api/schemas.md#patch)
* 새 필드 그룹 설명서 페이지(존재하는 경우)에 연결

또한 이 단계에서는 파트너가 제공한 타사 데이터를 포함하도록 데이터 관리 전략을 확장할 때 데이터 거버넌스 모델이 어떻게 변경되는지 생각해 보십시오. 아래 설명서 링크에서 고려 사항을 살펴보십시오.

* (**곧 출시 예정**) 타사 데이터를 별도의 데이터 세트에 보관하여 쉽게 삭제하고 통합을 취소할 수 있습니다
* (**곧 출시 예정**) 데이터 위생 추가 기능이 있는 클라이언트의 경우 데이터 세트에 대한 TTL을 사용합니다
* (**곧 출시 예정**) 타사 데이터를 가져오는 파생 데이터 세트를 만들 때 주의해야 합니다. 한 번 혼합된 타사 데이터는 파생된 데이터 세트 전체를 삭제하는 것밖에 없기 때문입니다

>[!TIP]
>
>데이터 공급업체의 개인 기반 식별자로 고객 프로필을 보완하도록 선택하는 경우 유형의 새 ID 유형을 만들 수 있습니다 **[[!UICONTROL 파트너 ID]](/help/identity-service/namespaces.md)**.
>
>에서 파트너 ID에 대해 자세히 알아보십시오. [id 유형 섹션](/help/identity-service/namespaces.md).
> 읽어보기 [id 필드를 정의하는 방법](/help/xdm/ui/fields/identity.md) Experience Platform 사용자 인터페이스에서 다음을 수행합니다.


### PII(개인 식별 정보) 또는 해시된 PII에서 보강할 대상을 내보냅니다. {#export-audiences}

파트너가 보강할 대상을 내보냅니다. Amazon S3 또는 SFTP와 같이 Real-Time CDP에서 제공하는 클라우드 스토리지 대상을 사용합니다. 다음 설명서 페이지를 읽고 이 단계를 완료하십시오.

* [Amazon 대상](/help/destinations/catalog/cloud-storage/amazon-s3.md) 설명서 페이지
* [SFTP 대상](/help/destinations/catalog/cloud-storage/sftp.md) 설명서 페이지
* 방법 [대상에 연결](/help/destinations/ui/connect-destination.md)
* 방법 [클라우드 스토리지 대상으로 데이터 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md)


### 파트너는 일치하는 프로필에 대해 라이선스가 부여된 속성을 추가합니다. {#partner-appends-attributes}

이 단계에서 파트너는 내보낸 대상에 대해 라이선스 속성을 추가합니다. 출력은 일반적으로 Real-Time CDP으로 다시 수집할 수 있는 플랫 파일로 사용할 수 있습니다.

### Real-Time CDP은 보강된 속성을 고객 프로필에 추가합니다 {#ingest-data}

이제 소스 커넥터를 통해 파트너로부터 데이터를 수집하여 풍부한 데이터를 Real-Time CDP으로 다시 가져오고 파트너가 제공한 데이터로 프로필을 보완해야 합니다.

이 용도로 권장되는 일부 소스 커넥터는 다음과 같습니다.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## 제한 사항 및 문제 해결 {#limitations-and-troubleshooting}

이 페이지에 설명된 사용 사례를 살펴볼 때 다음 제한 사항에 유의하십시오.

파트너 ID를 사용하도록 선택하는 경우, 이 ID는에서 를 빌드하는 데 사용되지 않습니다. [id 그래프](/help/identity-service/ui/identity-graph-viewer.md).

## 파트너 데이터 지원을 통해 달성한 기타 사용 사례 {#other-use-cases}

Real-Time CDP의 파트너 데이터 지원을 통해 활성화된 추가 사용 사례를 살펴보십시오.

* (**곧 출시 예정**) [!BADGE 베타]{type=Informative}**파트너 지원 인식 활용** 방문자가 인증을 받거나 브랜드에 대한 이전 기록이 없는 경우, 방문 중 온사이트 경험을 개인화하고 오프사이트 리타기팅 후 방문을 수행할 수 있습니다.
* (**곧 출시 예정**) [!BADGE 베타]{type=Informative}**확장된 활성화** pii 또는 해시된 PII를 허용하지 않는 게시 에코시스템에 파트너 ID 사용.