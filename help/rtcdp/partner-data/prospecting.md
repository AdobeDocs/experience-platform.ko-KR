---
title: (Beta) 잠재 고객 활용 사례를 통해 새로운 고객 참여 및 확보
description: Real-Time CDP의 파트너 데이터 지원 팀에서 활성화된 잠재 고객 사용 사례를 통해 새로운 고객을 확보하고 확보하는 방법에 대해 알아봅니다.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 486e1390dfa0602bef15d196d4a1a5befdc9ff23
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 15%

---

# 잠재 고객 활용 사례를 통해 신규 고객 유치

>[!AVAILABILITY]
>
>* 이 베타 기능은 라이선스가 부여된 Real-Time CDP(앱 서비스), Adobe Experience Platform 액티베이션, Real-time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate를 보유하고 있는 고객이 사용할 수 있습니다. 이 패키지에 대한 자세한 내용은 [제품 설명](https://helpx.adobe.com/legal/product-descriptions.html)을 참조하고 Adobe 담당자에게 문의하십시오.

Real-Time CDP의 타사 데이터 지원을 사용하여 데이터 파트너의 잠재 고객으로 프로필 기반을 확장하고 이들과 협력하여 새로운 고객을 확보하거나 연락하십시오.

![고객 전망 활용 사례 개요](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## 전제 조건 및 계획 {#prerequisites-and-planning}

Real-Time CDP에서 파트너 데이터 지원을 사용하여 새 고객에게 연락하고 고객을 확보하는 것을 고려하면서 계획 프로세스에서 다음 전제 조건을 고려하십시오.

* 파트너가 제공한 프로필이 Real-Time CDP에 수집되어 새로 고쳐질 것으로 기대하는 케이던스는 무엇입니까?
* 다운스트림 대상에는 어떤 ID가 필요합니까?
* 수집된 식별자가 실행 가능한 다운스트림인지 확인합니다.
* 수집하는 파트너 데이터가 PII(개인 식별 정보), 해시된 PII 또는 파트너 식별자와 같이 널리 받아들여지는 지속적인 식별자에 연결되어 있습니까?
* 파트너 관점과 법률, 개인 정보 보호 또는 규정 준수 팀에서 알아야 할 데이터 사용 정책은 무엇입니까?

## 사용 사례를 달성하는 방법: 높은 수준의 개요 {#achieve-the-use-case-high-level}

Real-Time CDP을 확장하여 새로운 고객을 확보하고 참여하기 전에 Real-Time CDP을 사용하여 첫 번째 부분 데이터에 대한 강력한 기반을 구축해야 합니다. 이 사용 사례를 달성하기 위한 워크플로우는 알려진 고객과 교류하기 위한 워크플로와 유사합니다.

![고객 전망 활용 사례 개요](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. 로서의 **고객**, 하나 이상의 잠재 고객 프로필에 라이선스를 부여합니다. **데이터 파트너** 단계 고객 확보의 최우선 과제 달성에 도움이 되도록
2. 로서의 **고객**, 프로필 데이터 및 거버넌스 모델을 확장하여 **파트너**-제공된 잠재 고객 프로필 목록입니다.
3. 로서의 **고객**&#x200B;에서는 잠재 고객 프로필을 Real-Time CDP에 로드하고, 책임 있는 사용을 보장하기 위해 거버넌스 정책을 빌드합니다.
4. 로서의 **고객**&#x200B;에서는 Prospect 프로필 목록에서 중점 대상을 작성합니다.
5. 로서의 **고객**&#x200B;를 활성화하면 Prospect 목록에서 사용 가능한 id를 수락하는 대상에 Prospect Audiences를 활성화합니다.
6. 필요한 경우 **데이터 파트너** 원하는 유료 미디어 대상에 대한 대상의 마지막 마일 활성화.

## 사용 사례 달성 방법: 단계별 지침 {#step-by-step-instructions}

위의 높은 수준의 개요에 있는 각 단계를 완료하려면 추가 설명서에 대한 링크가 포함된 아래 섹션을 읽어보십시오.

### 사용할 UI 기능 및 요소 {#ui-functionality-and-elements}

사용 사례를 구현하는 단계를 완료하면 다음 Real-Time CDP 기능 및 UI 요소(사용할 순서로 나열됨)를 사용하게 됩니다. 이러한 모든 영역에 대해 필요한 속성 기반 액세스 제어 권한이 있는지 확인하거나 시스템 관리자에게 필요한 권한을 부여하도록 요청하십시오.

* [ID](/help/identity-service/namespaces.md)
* [스키마](/help/xdm/home.md)
* [데이터 사용 레이블](/help/data-governance/labels/overview.md)
* [데이터 세트](/help/catalog/datasets/overview.md)
* [소스](/help/sources/home.md)
* 프로필(잠재 고객 프로필 링크)
* 대상자 (잠재 대상자에 대한 링크)
* [대상](/help/destinations/home.md)

### 파트너의 라이선스 타사 프로필 세부 정보 {#license-profiles-from-partner}

이 단계는에서 다룹니다 [전제 조건](#prerequisites-and-planning) 또한 Adobe은 신뢰할 수 있는 데이터 공급업체와 데이터 파트너가 제공한 잠재 고객 프로필을 수집할 수 있는 적절한 계약 계약을 체결했다고 가정합니다.

### 파트너가 제공한 잠재 고객을 수용하도록 프로필 데이터 및 거버넌스 모델 확장 {#extend-governance-model}

데이터 파트너로부터 잠재 고객 프로필을 받을 준비를 하려면 이 새 프로필 유형을 수용하도록 Real-Time CDP에서 데이터 관리 프레임워크를 확장해야 합니다.

사용할 ID, 데이터 관리 및 거버넌스 구성 요소는 다음과 같습니다.

* 새 항목 **[!UICONTROL 파트너 ID]** 파트너가 제공한 프로필에 대한 id 유형
* 새 항목 **[!UICONTROL XDM 개별 잠재 고객 프로필]** XDM 클래스
* **(설명서가 곧 제공됩니다.)** 파트너 데이터 지원에 맞춘 필드 그룹
* **(설명서가 곧 제공됩니다.)** 파트너로부터 들어오는 속성에 추가할 타사 레이블

#### 파트너 ID ID 네임스페이스 만들기

파트너로부터 받게 될 프로필에 대한 새 ID 유형을 만드는 것부터 시작합니다. 이렇게 하려면 ID 섹션에서 유형의 새 ID 네임스페이스를 만들어야 합니다 **[!UICONTROL 파트너 ID]**.

![새 파트너 ID ID 네임스페이스 만들기](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* 에서 파트너 ID 네임스페이스에 대해 자세히 알아보십시오. [id 유형 섹션](/help/identity-service/namespaces.md).
* Experience Platform 사용자 인터페이스의 [ID 필드를 정의하는 방법](/help/xdm/ui/fields/identity.md)에 대해 알아보십시오.

#### 을(를) 사용하여 새 스키마 만들기 **[!UICONTROL XDM 개별 잠재 고객 프로필]** 클래스

다음, 위치 **[!UICONTROL 데이터 관리]** > **[!UICONTROL 스키마]**, 새 스키마를 만들고 할당 **[!UICONTROL XDM 개별 잠재 고객 프로필]** 클래스.

![XDM 스키마 빌더에서 XDM 개별 잠재 고객 프로필 클래스를 검색합니다.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

방법 읽기 [ui에서 스키마 만들기 및 편집](/help/xdm/ui/resources/schemas.md) XDM 개별 잠재 고객 프로필 클래스(링크 예정)에 대한 전체 정보를 얻으십시오.

다음 **[!UICONTROL XDM 개별 잠재 고객 프로필]** 클래스는 아래 표시된 필드를 사용하여 사전 구성됩니다. 잠재 고객 프로필에 대해 파트너가 제공한 속성으로 스키마를 보강하려면 기대하는 속성으로 새 필드 그룹을 만들어 스키마에 추가하거나 Adobe에서 제공하는 사전 구성된 필드 그룹 중 하나를 사용할 수 있습니다.

![XDM 개별 잠재 고객 프로필 클래스에 대해 미리 구성된 필드.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

그런 다음 이전에 스키마의 기본 ID로 만든 partnerID ID를 선택해야 합니다. 프로필 레코드에는 기본 식별자가 있어야 합니다. 이 단계는 Prospect 데이터를 프로필 스토어에 로드하고 세그멘테이션 및 활성화에 사용할 수 있도록 하는 데 필요합니다.

>[!AVAILABILITY]
>
>잠재 고객 프로필은 파트너 ID 유형의 ID 네임스페이스만 사용하도록 자동으로 제한됩니다. 이는 설계에 의한 것이며 퍼스트 파티 프로필과 잠재 고객 프로필 간에 깔끔한 분리를 보장합니다.

![이전에 구성한 파트너 ID를 스키마의 기본 ID로 선택합니다.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

스키마가 아직 프로필에 대해 활성화되지 않았습니다. 프로필 버튼을 토글하여 프로필 서비스에 포함할 이 스키마를 활성화합니다. 실시간 고객 프로필에서 사용할 스키마를 활성화하는 방법에 대한 자세한 내용은 [스키마 튜토리얼 만들기.](/help/xdm/tutorials/create-schema-ui.md#profile)

![프로필용으로 스키마 활성화.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### 스키마의 모든 필드에 서드파티 데이터 거버넌스 레이블 추가

스키마를 구성하는 모든 필드에 타사 데이터 거버넌스 레이블을 추가하는 것이 좋습니다. 이는 서드파티 데이터의 책임 있는 사용을 보장하고 데이터 유출 위험을 최소화하기 위해 중요합니다. 서드파티 데이터 거버넌스 레이블에 대한 자세한 내용 찾기(Jordan의 문서에 대한 링크 추가)

이렇게 하려면 아래 단계를 수행합니다:

1. 생성한 스키마로 이동하여 **[!UICONTROL 레이블]** 탭.
2. 맨 위에 있는 확인란 버튼을 사용하여 이 스키마의 모든 필드를 선택한 다음 오른쪽의 연필 아이콘을 클릭하여 데이터 거버넌스 레이블을 이 스키마에 적용합니다.
3. 다음 항목 선택 **[!UICONTROL 파트너 에코시스템]** 왼쪽에 있는 범주에서 레이블을 지정합니다.
4. (이)라는 레이블 선택 **[!UICONTROL 서드파티]** 및 선택 **[!UICONTROL 저장]**.
5. 이제 스키마의 모든 필드에 이전 단계에서 선택한 레이블이 전달됩니다.

>[!SUCCESS]
>
>이제 스키마를 사용할 준비가 되었으며 다음 단계로 진행하여 데이터 파트너로부터 잠재 고객 데이터를 수집할 수 있습니다.

또한 이 단계에서는 파트너가 제공한 서드파티 데이터를 포함하도록 데이터 관리 전략을 확장할 때 데이터 거버넌스 모델의 변경 방식에 대해 살펴봅니다. 아래 설명서 링크에서 고려 사항을 살펴보십시오.

* (**준비 중**) 서드파티 데이터를 삭제하고 통합 실행을 취소하기 쉽도록 별도의 데이터 세트에 보관합니다.
* (**준비 중**) 데이터 위생 추가 기능을 구입한 클라이언트의 데이터 세트에서 [데이터 세트 만료](/help/hygiene/ui/dataset-expiration.md) 기능을 사용합니다.
* (**준비 중**) 서드파티 데이터를 혼합한 후에는 전체 파생 데이터 세트를 삭제하는 것만이 서드파티 데이터를 제거하는 유일한 방법이기 때문에 서드파티 데이터를 가져오는 파생 데이터 세트를 만들 때는 주의해야 합니다.

### 잠재 고객 프로필 목록 로드 및 잠재 고객 프로필 보기 검사

잠재 고객 프로필 관리를 위해 데이터 모델을 준비한 후에는 데이터를 수집할 차례입니다.

#### 데이터 세트 만들기 및 샘플 잠재 고객 데이터 로드

일부 샘플 데이터를 로드하고 잠재 고객 프로필을 채우려면 데이터 세트를 만들고 데이터 파트너로부터 받은 파일을 업로드합니다. 아래 단계를 완료합니다.

1. 다음으로 이동 **[!UICONTROL 데이터 관리]** > **[!UICONTROL 데이터 세트]** 및 선택 **[!UICONTROL 데이터 세트 만들기]**.
2. 스키마에서 데이터 세트 만들기를 선택합니다
3. 이전 단계에서 생성한 스키마 선택
4. 데이터 세트의 이름과 필요한 경우 설명을 제공합니다.
5. **[!UICONTROL 마침]**&#x200B;을 선택합니다.

![잠재 고객 프로필에 대한 데이터 세트를 만드는 단계를 기록하는 것입니다.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

스키마를 만드는 단계와 유사하게, 실시간 고객 프로필에 데이터 세트를 포함할 수 있도록 해야 합니다. 실시간 고객 프로필에서 사용할 데이터 세트를 활성화하는 방법에 대한 자세한 내용은 [스키마 튜토리얼 만들기.](/help/xdm/tutorials/create-schema-ui.md#profile)

![프로필에 대한 데이터 세트를 활성화합니다.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

파트너로부터 받은 파일을 데이터 세트로 로드하려면 데이터 세트를 선택하고 오른쪽 레일에서 아래로 스크롤한 다음 를 선택합니다 **[!UICONTROL 데이터 추가]**. 파일을 드래그하여 놓거나 선택할 수 있습니다. **[!UICONTROL 파일 선택]** 을 클릭하여 파일 위치로 이동한 다음 선택합니다.

![데이터 세트에 파일을 추가합니다.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

데이터 파트너의 프로필 목록을 Real-Time CDP에 로드한 후 로 진행합니다. [Inspect 로드된 잠재 고객 프로필 섹션](#inspect-profiles) 잠재 고객 프로필이 UI에서 채워지고 있는지 확인합니다.

#### 소스 커넥터를 통해 잠재 고객 데이터 수집

반복적으로 파일 가져오기를 설정하여 소스 커넥터를 통해 파트너의 데이터를 수집하고 잠재 프로필 목록을 Real-Time CDP으로 가져올 수 있습니다.

이러한 목적에 대한 몇 가지 권장 소스 커넥터가 아래에 나열되어 있지만, Real-Time CDP으로의 파일 기반 수집 방법은 사용자에게 적합합니다.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

데이터 파트너의 프로필 목록을 Real-Time CDP으로 로드한 후 다음 섹션으로 진행하여 잠재 고객 프로필이 UI에서 채워지고 있는지 확인하십시오.

#### Inspect 로드된 잠재 고객 프로필 {#inspect-profiles}

잠재 고객 프로필 목록을 보려면 **[!UICONTROL 잠재 고객]** > **[!UICONTROL 프로필]** 왼쪽 레일에서.

Real-Time CDP에 방금 로드한 잠재 고객 프로필이에서 표시되는 데 최대 2시간이 소요될 수 있습니다. **[!UICONTROL 찾아보기]** Prospect Profile 화면 보기 페이지에 &quot;지금 찾아볼 잠재 고객 프로필이 없습니다&quot;라는 메시지가 표시되면 잠시 후 다시 시도하십시오. 잠시 기다린 후 잠재 고객 프로필이에 표시되어야 합니다. **[!UICONTROL 찾아보기]** 보기.

>[!TIP]
>
>이(가) 있는지 확인합니다 **[!UICONTROL ID 네임스페이스]** 열. 여러 데이터 공급업체와 작업하는 경우 이 열을 사용하여 잠재 고객 프로필의 출처를 추론하십시오.

![Real-Time CDP에 로드된 잠재 고객 프로필 보기](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

아래 표시된 대로 추가 검사를 위해 모든 잠재 고객 프로필을 선택할 수도 있습니다.

![잠재 고객 프로필 검사 방법 보기](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

(**곧 출시 예정**) 잠재 고객 프로필에 대해 자세히 알아보십시오.

### 잠재 고객 만들기 {#create-prospect-audiences}

Real-Time CDP의 세분화 기능을 사용하여 잠재 고객 프로필에서 대상을 만들 수 있습니다. 원하는 세분화 규칙을 사용하여 맞춤화된 대상을 만들 수 있습니다.

잠재 고객 프로필로 구성된 대상을 시작하고 구축하려면 다음 위치로 이동하십시오. **[!UICONTROL 잠재 고객]** > **[!UICONTROL 대상]**.

![잠재 고객 보기.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

잠재 고객 프로필에 대한 대상 구축 경험은 알려진 자사 고객과 대상을 구축하는 경험과 다릅니다. 이 보기는 다음으로 제한됩니다.

* 이전에 생성한 Prospect 클래스의 속성입니다.
* 배치 프로필 평가만.
* 은 시계열 이벤트를 기반으로 대상 빌드를 지원하지 않습니다.

(**곧 출시 예정**) 잠재 고객에 대해 자세히 알아보십시오.

### 대상에 대한 잠재 고객 프로필 활성화 {#activate-to-destinations}

Prospect 대상을 대상으로 내보내 활용합니다. 현재 특정 대상: [Amazon](/help/destinations/catalog/cloud-storage/amazon-s3.md) 또는 [!BADGE 알파]{type=Informative}[LiveRamp](/help/destinations/catalog/advertising/liveramp.md) 대상은 잠재 고객 프로필의 활성화를 지원합니다.

## 파트너 데이터 지원을 통해 달성한 기타 사용 사례 {#other-use-cases}

Real-Time CDP에서 파트너 데이터 지원을 통해 활성화된 추가 사용 사례를 살펴보십시오.

* [!BADGE Beta]{type=Informative}[신뢰할 수 있는 데이터 파트너의 속성으로 자사 프로필을 보완하여 데이터 기반을 개선하고 고객층에 대한 새로운 인사이트를 얻고 대상자 최적화를 개선합니다.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* (**준비 중**) [!BADGE Beta]{type=Informative}사용자가 브랜드를 인증하거나 이전 기록을 가지고 있지 않아도 방문 중에 사이트 경험을 개인 설정하고 방문 후에 오프사이트 리타겟팅할 수 있도록 **파트너가 지원하는 인식을 활용합니다**.