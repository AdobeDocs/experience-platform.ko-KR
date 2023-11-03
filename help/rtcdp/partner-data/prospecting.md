---
title: 서드파티 쿠키에 의존하지 않고 새로운 고객 참여 및 확보
description: 서드파티 쿠키에 의존하지 않고 전망 사용 사례를 통해 새로운 고객을 참여하고 획득하는 방법을 알아봅니다.
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: 645295958ea6f94a9f9da13517b0fa1d02010b52
workflow-type: tm+mt
source-wordcount: '2077'
ht-degree: 85%

---

# 서드파티 쿠키에 의존하지 않고 새로운 고객 참여 및 확보

>[!AVAILABILITY]
>
>* 이 기능은 Real-Time CDP(앱 서비스), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate에 라이선스를 부여한 고객이 사용할 수 있습니다. 이 패키지에 대한 자세한 내용은 [제품 설명](https://helpx.adobe.com/legal/product-descriptions.html)을 참조하고 Adobe 담당자에게 문의하십시오.

Real-Time CDP에서 서드파티 데이터 지원을 사용하여 데이터 파트너의 잠재 고객 프로필로 프로필 기반을 확장하고 데이터 파트너와 협력하여 신규 고객에게 도달하거나 확보할 수 있습니다.

![고객 발굴 사용 사례에 대한 높은 수준의 시각적 개요.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## 이 사용 사례를 고려하는 이유 {#why-this-use-case}

브랜드는 서드파티 쿠키에 의존하지 않고, 제한된 예산, 투명성 및 광고 지출 수익률에 대한 높은 요구 없이 단계별로 최고의 고객 확보 사용 사례를 책임감 있게 실행하는 어려운 문제에 동시에 직면하고 있습니다.

Adobe Real-time Customer Data Platform은 브랜드가 DMP(데이터 관리 플랫폼)에서 지원하는 사용 사례를 쿠키 없는 대안으로 안전하게 전환하고 셀프서비스 세분화, 대상자 큐레이션 및 활성화를 완전히 정교화하고 강력하게 단일 시스템으로 구현하는 방식으로 수행할 수 있도록 지원할 수 있습니다. 특허 받은 데이터 거버넌스 및 동의 프레임워크를 통해 책임감 있는 데이터 사용에 대한 Adobe의 확고한 초점은 그대로 유지합니다.

예를 들어 잠재 고객을 사용자 또는 알려진 고객으로 끌어들이기 위해 캠페인을 실행해야 하는 경우 이 사용 사례에 설명된 단계를 따릅니다.

## 전제 조건 및 계획 {#prerequisites-and-planning}

신규 고객을 유치하고 공략할 때 계획 프로세스에서 다음 전제 조건을 고려하십시오.

* 파트너가 제공한 프로필을 Real-Time CDP로 수집해서 새로 고치는 예상 주기
* 다운스트림 대상에 필요한 ID
* 수집된 식별자가 실행 가능한 다운스트림인지 여부
* 수집 중인 파트너 데이터가 PII(개인 식별 정보), 해시된 PII 또는 파트너 식별자와 같이 널리 허용되는 지속 가능한 식별자에 연결되어 있는지 여부
* 파트너 관점과 자체 법률, 프라이버시 또는 규정 준수 팀에서 알아야 할 데이터 사용 정책

## 사용 사례를 달성하는 방법: 높은 수준의 개요 {#achieve-the-use-case-high-level}

신규 고객 참여 유도 및 확보를 위해 Real-Time CDP를 확장하기 전에 Real-Time CDP를 사용하여 첫 번째 부분 데이터를 위한 강력한 기반을 구축해야 합니다. 이 사용 사례를 달성하기 위한 워크플로는 알려진 고객과 소통하기 위한 워크플로와 유사합니다.

![고객 발굴 사용 사례에 대한 높은 수준의 시각적 개요.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. **고객**&#x200B;은 하나 이상의 **데이터 파트너**&#x200B;의 잠재 고객 프로필에 라이선스를 부여하여 단계 고객 확보를 촉진할 수 있습니다.
2. **고객**&#x200B;은 프로필 데이터 및 거버넌스 모델을 확장하여 **파트너**&#x200B;가 제공한 잠재 고객 프로필 목록을 수집합니다.
3. **고객**&#x200B;은 잠재 고객 프로필을 Real-Time CDP에 로드하고 책임 있는 사용을 보장하기 위한 거버넌스 정책을 구축합니다.
4. **고객**&#x200B;은 잠재 고객 프로필 목록에서 집중 대상자를 빌드합니다.
5. **고객**&#x200B;은 잠재 고객 목록에서 사용할 수 있는 ID를 허용하는 대상으로 잠재 고객 대상자를 활성화합니다.
6. 필요한 경우 **데이터 파트너**&#x200B;와 협력하여 원하는 유료 미디어 대상에 대한 대상자를 최종적으로 활성화할 수 있습니다.

## 비디오 워크스루 {#video-walkthrough}

잠재 고객에게 도달하고 참여시키는 방법에 대한 연습은 아래 비디오 튜토리얼을 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## 사용 사례 달성 방법: 단계별 지침 {#step-by-step-instructions}

위의 높은 수준의 개요에 있는 각 단계를 완료하려면 추가 설명서에 대한 링크가 포함된 아래 섹션을 읽어보십시오.

### 사용할 UI 기능 및 요소 {#ui-functionality-and-elements}

사용 사례를 구현하는 단계를 완료하면 다음 Real-Time CDP 기능 및 UI 요소(사용할 순서대로 나열됨)를 사용하게 됩니다. 이러한 모든 영역에 대해 필요한 속성 기반 액세스 제어 권한이 있는지 확인하거나 시스템 관리자에게 필요한 권한 부여를 요청하십시오.

* [ID](/help/identity-service/namespaces.md)
* [스키마](/help/xdm/home.md)
* [데이터 사용 레이블](/help/data-governance/labels/overview.md)
* [데이터 세트](/help/catalog/datasets/overview.md)
* [소스](/help/sources/home.md)
* [잠재 고객 프로필](/help/profile/ui/prospect-profile.md)
* [잠재 고객](/help/segmentation/ui/prospect-audience.md)
* [대상](/help/destinations/home.md)

### 파트너의 라이선스 서드파티 프로필 세부 정보 {#license-profiles-from-partner}

이 단계는 [사전 요구 사항](#prerequisites-and-planning)에서 다루며, Adobe는 신뢰할 수 있는 데이터 공급업체와 계약을 체결하여 데이터 파트너가 제공한 잠재 고객 프로필을 수집할 수 있다고 가정합니다.

### 파트너가 제공한 잠재 고객 프로필을 수용할 수 있도록 프로필 데이터 및 거버넌스 모델을 확장합니다. {#extend-governance-model}

데이터 파트너로부터 잠재 고객 프로필을 받을 때 이 새로운 프로필 유형을 수용할 수 있도록 Real-Time CDP에서 데이터 관리 프레임워크를 확장해야 합니다.

사용할 ID, 데이터 관리 및 거버넌스 구성 요소는 다음과 같습니다.

* 파트너가 제공하는 프로필의 새 **[!UICONTROL 파트너 ID]** ID 유형
* 새 **[!UICONTROL XDM 개별 잠재 고객 프로필]** XDM 클래스
* **(설명서 준비 중)** 파트너 데이터 지원에 맞게 조정된 필드 그룹
* **(설명서 준비 중)** 파트너로부터 수신되는 속성에 추가할 서드파티 레이블

#### 파트너 ID 네임스페이스 만들기 {#create-partner-id-namespace}

파트너로부터 받을 프로필에 대한 새 ID 유형을 생성하여 시작합니다. 이렇게 하려면 ID 섹션에서 **[!UICONTROL 파트너 ID]** 유형의 새 ID 네임스페이스를 만들어야 합니다.

![새 파트너 ID 네임스페이스를 만듭니다.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* [ID 유형 섹션](/help/identity-service/namespaces.md)에서 파트너 ID 네임스페이스에 대해 자세히 알아보십시오.
* Experience Platform 사용자 인터페이스에서 [ID 필드를 정의하는 방법](/help/xdm/ui/fields/identity.md)에 대해 알아보십시오.

#### **[!UICONTROL XDM 개별 잠재 고객 프로필]** 클래스로 새 스키마를 만듭니다.

다음으로 **[!UICONTROL 데이터 관리]** > **[!UICONTROL 스키마]**&#x200B;에서 새 스키마를 만들고 **[!UICONTROL XDM 개별 잠재 고객 프로필]** 클래스에 할당합니다.

![XDM 스키마 빌더에서 XDM 개별 잠재 고객 프로필 클래스를 검색합니다.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

[UI에서 스키마를 생성 및 편집](/help/xdm/ui/resources/schemas.md)하는 방법에 대해 알아보고 XDM 개별 잠재 고객 프로필 클래스(링크 제공 예정)에 대해 자세한 내용을 확인하십시오.

**[!UICONTROL XDM 개별 잠재 고객 프로필]** 클래스는 아래 표시된 필드로 사전 구성되어 제공됩니다. 잠재 고객 프로필에 대해 파트너가 제공한 속성으로 스키마를 보강하려면 원하는 속성으로 새 필드 그룹을 만들어 스키마에 추가하거나 Adobe에서 제공하는 사전 구성된 필드 그룹 중 하나를 사용하면 됩니다.

![XDM 개별 잠재 고객 프로필 클래스에 대해 사전 구성된 필드.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

그런 다음 이전에 스키마의 기본 ID로 만든 partnerID ID를 선택해야 합니다. 프로필 레코드에는 기본 식별자가 포함되어야 합니다. 이 단계는 잠재 고객 데이터를 프로필 스토어에 로드하고 세분화 및 활성화에 사용할 수 있는지 확인하는 데 필요합니다.

>[!AVAILABILITY]
>
>잠재 고객 프로필은 파트너 ID 유형의 ID 네임스페이스만 사용하도록 자동으로 제한됩니다. 이것은 의도적으로 설계된 것이며 이를 통해 자사 프로필과 잠재 고객 프로필이 명확하게 구분됩니다.

![이전에 구성된 파트너 ID를 스키마의 기본 ID로 선택합니다.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

프로필에 대해 스키마가 아직 활성화되지 않았습니다. 이 스키마를 프로필 서비스에 포함하려면 프로필 버튼을 전환합니다. 실시간 고객 프로필에서 사용할 스키마를 활성화하는 방법에 대한 자세한 내용은 [스키마 튜토리얼 만들기](/help/xdm/tutorials/create-schema-ui.md#profile)를 참조하십시오.

![프로필용으로 스키마를 활성화합니다.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### 스키마의 모든 필드에 서드파티 데이터 거버넌스 레이블 추가

스키마를 구성하는 모든 필드에 서드파티 데이터 거버넌스 레이블을 추가하는 것이 좋습니다. 이는 서드파티 데이터의 책임 있는 사용을 보장하고 데이터 유출 위험을 최소화하기 위해 중요합니다. 에 대한 추가 정보 찾기 [타사 데이터 거버넌스 레이블](../../data-governance/labels/reference.md#partner-ecosystem-labels).

이렇게 하려면 아래 단계를 수행합니다.

1. 생성한 스키마로 이동하고 **[!UICONTROL 레이블]** 탭을 선택합니다.
2. 맨 위에 있는 확인란 버튼을 사용하여 이 스키마의 모든 필드를 선택한 다음 오른쪽에 있는 연필 모양 아이콘을 클릭하여 이 스키마에 데이터 거버넌스 레이블을 적용합니다.
3. 왼쪽에 있는 범주 중 **[!UICONTROL 파트너 생태계]** 레이블을 선택합니다.
4. **[!UICONTROL 서드파티]** 레이블을 선택한 다음 **[!UICONTROL 저장]**&#x200B;을 선택합니다.
5. 이렇게 하면 스키마의 모든 필드에 이전 단계에서 선택한 레이블이 지정됩니다.

>[!SUCCESS]
>
>이제 스키마를 사용할 준비가 되었습니다. 다음 단계로 진행하여 데이터 파트너로부터 잠재 고객 데이터를 수집할 수 있습니다.

또한 이 단계에서는 파트너가 제공한 서드파티 데이터를 포함하도록 데이터 관리 전략을 확장할 때 데이터 거버넌스 모델의 변경 방식에 대해 살펴봅니다. 아래 설명서 링크에서 고려 사항을 살펴보십시오.

* (**준비 중**) 서드파티 데이터를 삭제하고 통합 실행을 취소하기 쉽도록 별도의 데이터 세트에 보관합니다.
* (**준비 중**) 데이터 위생 추가 기능을 구입한 클라이언트의 데이터 세트에서 [데이터 세트 만료](/help/hygiene/ui/dataset-expiration.md) 기능을 사용합니다.
* (**준비 중**) 서드파티 데이터를 혼합한 후에는 전체 파생 데이터 세트를 삭제하는 것만이 서드파티 데이터를 제거하는 유일한 방법이기 때문에 서드파티 데이터를 가져오는 파생 데이터 세트를 만들 때는 주의해야 합니다.

### 잠재 고객 프로필 목록 로드 및 잠재 고객 프로필 보기 검사

잠재 고객 프로필을 관리하기 위해 데이터 모델을 준비했다면 이제 데이터를 수집할 차례입니다.

#### 데이터 세트 생성 및 샘플 잠재 고객 데이터 로드

일부 샘플 데이터를 로드하고 잠재 고객 프로필을 채우려면 데이터 세트를 만들고 데이터 파트너로부터 받은 파일을 업로드합니다. 아래의 단계를 완료하십시오.

1. **[!UICONTROL 데이터 관리]** > **[!UICONTROL 데이터 세트]**&#x200B;로 이동한 다음 **[!UICONTROL 데이터 세트 만들기]**&#x200B;를 선택합니다.
2. 스키마에서 데이터 세트 만들기를 선택합니다.
3. 이전 단계에서 생성한 스키마를 선택합니다.
4. 데이터 세트의 이름을 지정하고 필요한 경우 설명을 제공합니다.
5. **[!UICONTROL 마침]**&#x200B;을 선택합니다.

![잠재 고객 프로필에 대한 데이터 세트를 만드는 단계에 대한 녹화본.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

스키마를 생성하는 단계와 유사하게 실시간 고객 프로필에 포함할 데이터 세트를 활성화해야 합니다. 실시간 고객 프로필에서 사용할 데이터 세트를 활성화하는 방법에 대한 자세한 내용은 [스키마 튜토리얼 만들기](/help/xdm/tutorials/create-schema-ui.md#profile)를 참조하십시오.

![프로필용으로 데이터 세트를 활성화합니다.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

파트너로부터 받은 파일을 데이터 세트로 로드하려면 데이터 세트를 선택하고 오른쪽 레일에서 아래로 스크롤한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다. 파일을 드래그 앤 드롭하거나 **[!UICONTROL 파일 선택]**&#x200B;을 선택하여 파일 위치로 이동한 다음 선택할 수 있습니다.

![데이터 세트에 파일을 추가합니다.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

데이터 파트너의 프로필 목록을 Real-Time CDP로 로드한 다음에는 [로드한 잠재 고객 프로필 검사 섹션](#inspect-profiles)으로 진행하여 UI에서 잠재 고객 프로필이 채워지고 있는지 확인합니다.

#### 소스 커넥터를 통해 잠재 고객 데이터 수집

소스 커넥터를 통해 파트너의 데이터를 수집하고 잠재 고객 프로필 목록을 Real-Time CDP로 가져오도록 반복 파일 가져오기를 설정할 수 있습니다.

이 용도로 권장되는 일부 소스 커넥터는 아래에 따로 나열되어 있지만 Real-Time CDP에 대한 모든 파일 기반 수집 방법을 목적에 부합하게 사용할 수 있습니다.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

데이터 파트너의 프로필 목록을 Real-Time CDP로 로드한 다음에는 다음 섹션으로 진행하여 UI에서 잠재 고객 프로필이 채워지고 있는지 확인합니다.

#### 로드된 잠재 고객 프로필 검사 {#inspect-profiles}

잠재 고객 프로필 목록을 보려면 왼쪽 레일에서 **[!UICONTROL 잠재 고객]** > **[!UICONTROL 프로필]**&#x200B;로 이동합니다.

Real-Time CDP에 방금 로드한 잠재 고객 프로필이 잠재 고객 프로필 화면의 **[!UICONTROL 탐색]** 보기에 표시되는 데 2시간 정도 소요될 수 있습니다. 페이지에 “지금 검색할 수 있는 잠재 고객 프로필이 없습니다”라는 메시지가 표시되면 잠시 후 다시 시도하십시오. 잠시 기다리면 **[!UICONTROL 탐색]** 보기에 잠재 고객 프로필이 표시됩니다.

>[!TIP]
>
>**[!UICONTROL ID 네임스페이스]**&#x200B;라는 열도 있습니다. 여러 데이터 공급업체와 작업하는 경우 이 열을 사용하여 잠재 고객 프로필의 출처를 유추할 수 있습니다.

![Real-Time CDP에 로드된 잠재 고객 프로필의 보기.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

아래와 같이 추가적인 검사를 위해 잠재 고객 프로필을 선택할 수도 있습니다.

![잠재 고객 프로필 검사 방법의 보기.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

자세한 내용 [잠재 고객 프로필](/help/profile/ui/prospect-profile.md).

### 잠재 고객 대상자 만들기 {#create-prospect-audiences}

Real-Time CDP의 세분화 기능을 사용하여 잠재 고객 프로필에서 대상자를 생성할 수 있습니다. 원하는 세분화 규칙을 사용하여 맞춤형 대상자를 생성할 수 있습니다.

시작하고 잠재 고객 프로필로 구성된 잠재 고객을 구축하려면 **[!UICONTROL 잠재 고객]** > **[!UICONTROL 대상자]**&#x200B;로 이동하십시오.

![잠재 고객 대상자 보기.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

잠재 고객 프로필에 대한 대상자 구축 경험은 알려진 자사 고객으로부터 대상자를 빌드하는 경험과 다릅니다. 이 보기는 다음으로 제한됩니다.

* 이전에 생성한 잠재 고객 클래스의 속성
* 배치 프로필 평가 전용
* 시계열 이벤트를 기반으로 하는 대상자 구축 지원 안 함

자세한 내용 [잠재 고객](/help/segmentation/ui/prospect-audience.md).

### 잠재 고객 프로필을 대상으로 활성화 {#activate-to-destinations}

잠재 고객 대상자를 대상으로 내보내 활용할 수 있습니다. 현재 특정 클라우드 스토리지 대상만 잠재 고객 프로필 활성화를 지원합니다.

![잠재 고객을 지원하는 대상.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[자세히 보기](/help/destinations/ui/activate-prospect-audiences.md) 클라우드 스토리지 대상에 대한 잠재 고객 활성화 정보.

## 파트너 데이터 지원을 통해 달성한 기타 사용 사례 {#other-use-cases}

Real-Time CDP에서 파트너 데이터 지원을 통해 활성화된 추가 사용 사례를 살펴보십시오.

* [신뢰할 수 있는 데이터 파트너의 속성으로 자사 프로필을 보완](/help/rtcdp/partner-data/supplement-first-party-profiles.md)하여 데이터 기반을 개선하고 고객층에 대한 새로운 인사이트를 얻고 대상자 최적화를 개선합니다.
* [파트너 지원 방문자 인식을 사용하여 알 수 없는 방문자에 대한 온사이트 경험 개인화](/help/rtcdp/partner-data/onsite-personalization.md) 방문에서 사용자 인증이 없거나 브랜드와 이전 기록이 있는 경우.
* [잠재 고객 프로필 및 잠재 고객 활성화 확장](/help/destinations/ui/activate-prospect-audiences.md) 대상을 선택합니다.
