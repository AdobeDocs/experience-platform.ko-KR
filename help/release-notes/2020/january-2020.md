---
title: Adobe Experience Platform 릴리스 노트 2020년 1월
description: Adobe Experience Platform의 2020년 1월 릴리스 정보.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 25%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2020년 1월 15일 목요일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model]&#x200B;(XDM) 시스템 {#xdm}

표준화 및 상호 운용성은 [!DNL Experience Platform]의 핵심 개념입니다. Adobe을 기반으로 하는 [!DNL Experience Data Model]&#x200B;(XDM)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

XDM은 디지털 경험의 성능을 개선하기 위해 설계된 공개적으로 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신하는 모든 애플리케이션에 대한 일반적인 구조와 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 더 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 동일한 계층의 필드에 대한 필드 유형 제한 | XDM 필드가 특정 유형으로 정의된 후에는 클래스 또는 스키마 필드 그룹에 관계없이 동일한 이름 및 계층의 다른 필드에서 동일한 필드 유형을 사용해야 합니다. 예를 들어 XDM [!DNL Profile] 클래스에 대한 필드 그룹에 &quot;integer&quot; 유형의 `profile.age` 필드가 있는 경우 XDM [!DNL ExperienceEvent]에 대한 유사한 필드 그룹에는 &quot;string&quot; 유형의 `profile.age` 필드가 있을 수 없습니다. 다른 필드 형식을 사용하려면 필드가 이전에 정의한 필드(예: `profile.person.age`)와 다른 계층 구조여야 합니다. 이 기능은 스키마가 유니온에 함께 사용될 때 충돌을 방지하기 위한 것입니다. 제한 사항은 기존 스키마에 소급하여 영향을 주지 않지만, 필드 유형 충돌에 대해서는 스키마를 검토하고 필요에 따라 편집하는 것이 좋습니다. |
| 대/소문자 필드 유효성 검사 | 동일한 수준의 사용자 정의 필드는 대소문자와는 관계없이 이름이 달라야 합니다. 예를 들어 &quot;Email&quot;이라는 사용자 정의 필드를 추가하여 &quot;email&quot;이라는 동일한 수준에 다른 사용자 정의 필드를 추가할 수 없습니다. |

**알려진 문제**

* None

[!DNL Schema Registry] API 및 [!DNL Schema Editor] 사용자 인터페이스를 사용한 XDM 작업에 대한 자세한 내용은 [XDM 시스템 설명서](../../xdm/home.md)를 참조하십시오.

## [!DNL Privacy Service] {#privacy}

새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service]는 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service]를 사용하면 Adobe Experience Cloud 애플리케이션에서 비공개 또는 개인 고객 데이터에 액세스하고 삭제하도록 요청할 수 있으므로, 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| [!DNL Privacy Service] 리브랜딩 | 이전 명칭인 “GDPR 서비스”는 GDPR 외에도 다른 규정을 지원하도록 서비스가 확대됨에 따라 [!DNL Privacy Service]로 이름이 변경되었습니다. |
| 새로운 API 엔드포인트 | [!DNL Privacy Service] API의 기본 경로가 `/data/privacy/gdpr`에서 `/data/core/privacy/jobs`(으)로 업데이트되었습니다. |
| 새로운 필수 `regulation` 속성 | [!DNL Privacy Service] API에서 새로운 작업을 만들 때 요청 페이로드에 작업을 추적할 규정을 나타내는 `regulation` 속성을 제공해야 합니다. 허용되는 값은 `gdpr` 및 `ccpa`입니다. |
| [!DNL Adobe Primetime Authentication] 지원 | [!DNL Privacy Service]이(가) 이제 [!DNL Primetime Authentication]을(를) 제품 값으로 사용하여 Adobe `primetimeAuthentication`의 액세스/삭제 요청을 수락합니다. |
| Privacy Service UI 개선 사항 | GDPR 및 CCPA 규정에 대한 별도의 작업 추적 페이지입니다. GDPR과 CCPA에 대한 추적 데이터를 전환할 수 있는 새로운 **규정 유형** 드롭다운을 추가했습니다. |

**알려진 문제**

* None

[!DNL Privacy Service]에 대한 자세한 내용은 [Privacy Service 개요](../../privacy-service/home.md)를 읽는 것부터 시작해 보세요.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하는 동시에 [!DNL Experience Platform] 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform]에서는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 고객 속성 데이터 지원 | 고객 속성 데이터를 수집하기 위한 스트리밍 커넥터를 만들기 위한 UI 및 API 지원. |
| 클라우드 스토리지에 대한 추가 파일 형식 지원 | 이제 클라우드 스토리지에서의 파일 수집은 XDM 호환 Parquet 및 JSON 파일 형식을 지원합니다. |
| 액세스 제어 권한 지원 | Adobe Experience Platform의 액세스 제어 프레임워크는 데이터 수집에서 소스에 대한 액세스 권한을 부여하는 데 필요한 권한을 제공합니다. 사용자는 권한 수준에 따라 소스를 보거나, 소스를 관리하거나, 액세스가 거부될 수 있습니다. |

**액세스 제어 권한**

| 카테고리 | 사용 권한 | 설명 |
|--- | --- | ---|
| 데이터 수집 | 소스 관리 | 소스를 읽고, 만들고, 편집하고, 비활성화할 수 있는 액세스 권한. |
| 데이터 수집 | 소스 보기 | **[!UICONTROL Catalog]** 탭의 사용 가능한 소스와 **[!UICONTROL Browse]** 탭의 인증된 소스에 대한 읽기 전용 액세스 권한입니다. |

**알려진 문제**

* None

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하세요.

## 대상 {#destinations}

[Real-Time CDP](../../rtcdp/overview.md)에서 대상은 해당 파트너에게 데이터를 원활하게 활성화하는 대상 플랫폼과의 사전 빌드된 통합입니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 액세스 제어 권한 지원 | Real-Time CDP의 대상 기능은 Adobe Experience Platform 액세스 제어 권한과 함께 작동합니다. 사용자의 권한 수준에 따라 대상을 보고, 관리하고, 활성화할 수 있습니다. |

**액세스 제어 권한**

| 카테고리 | 사용 권한 | 설명 |
|--- | --- | ---|
| 대상 | 대상 관리 | 대상을 읽고, 만들고, 편집하고, 비활성화할 수 있는 액세스 권한. |
| 대상 | 대상 보기 | **[!UICONTROL Catalog]** 탭의 사용 가능한 대상 및 **찾아보기** 탭의 인증된 대상에 대한 읽기 전용 액세스 권한입니다. |
| 대상 | 대상 활성화 | 대상에 데이터를 활성화하는 기능. 이 권한을 사용하려면 제품 프로필에 &quot;대상 관리&quot; 또는 &quot;대상 보기&quot;를 추가해야 합니다. |

**알려진 문제**

* None

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하세요.
