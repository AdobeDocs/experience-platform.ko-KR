---
title: Adobe Experience Platform 릴리스 노트 - 2020년 1월
description: Adobe Experience Platform에 대한 2020년 1월 릴리스 노트입니다.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 1월 15일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM) 시스템 {#xdm}

표준화와 상호 운용성은 이면의 주요 개념입니다 [!DNL Experience Platform]. [!DNL Experience Data Model] Adobe 기반의 XDM(Customer Experience Management)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하려는 노력입니다.

XDM은 디지털 경험의 힘을 향상시키기 위해 설계된 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신할 수 있도록 모든 애플리케이션에 대한 공통 구조 및 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 보다 빠르고 통합된 방식으로 통찰력을 제공하는 공통 표현에 통합할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 동일한 계층 구조의 필드에 대한 필드 유형 제한 | XDM 필드가 특정 유형으로 정의된 후에는 클래스 또는 스키마 필드 그룹에 관계없이 동일한 이름 및 계층 구조의 다른 모든 필드는 동일한 필드 유형을 사용해야 합니다. 예를 들어 XDM에 대한 필드 그룹이 있는 경우 [!DNL Profile] 클래스에 가 포함되어 있습니다. `profile.age` XDM의 유사한 필드 그룹인 &quot;정수&quot; 유형 필드 [!DNL ExperienceEvent] 에는 를 사용할 수 없습니다. `profile.age` &quot;string&quot; 유형의 필드. 다른 필드 유형을 활용하려면 필드가 이전에 정의한 필드와 다른 계층 구조여야 합니다(예: `profile.person.age`). 이 기능은 스키마를 조합에서 함께 가져올 때 충돌을 방지하기 위한 것입니다. 제약 조건은 기존 스키마에 소급하여 영향을 주지 않지만 필드 유형 충돌을 검토하고 필요에 따라 편집하는 것이 좋습니다. |
| 대/소문자 구분 필드 유효성 검사 | 동일한 수준의 사용자 지정 필드에는 대소문자와는 관계없이 이름이 달라야 합니다. 예를 들어 &quot;Email&quot;이라는 사용자 지정 필드를 추가하는 경우 동일한 수준에서 &quot;email&quot;이라는 다른 사용자 지정 필드를 추가할 수 없습니다. |

**알려진 문제**

* None

를 사용하여 XDM을 사용하는 방법에 대해 자세히 알아보려면 [!DNL Schema Registry] API 및 [!DNL Schema Editor] 사용자 인터페이스를 참조하십시오. [XDM 시스템 설명서](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service] 은 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. 사용 [!DNL Privacy Service]를 사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터에 대한 액세스 및 삭제 요청을 제출할 수 있으므로, 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| [!DNL Privacy Service] 리브랜딩 | 이전에 &quot;GDPR Service&quot;라고 이름이 변경된 사용자가 [!DNL Privacy Service] 서비스는 GDPR 외에도 다른 규정을 지원하도록 성장했습니다. |
| 새 API 엔드포인트 | 의 기본 경로 [!DNL Privacy Service] API가 `/data/privacy/gdpr` to `/data/core/privacy/jobs`. |
| 새로운 필수 `regulation` 속성 | 에서 새 작업을 만들 때 [!DNL Privacy Service] API, a `regulation` 작업을 추적할 규칙을 나타내려면 요청 페이로드에서 속성을 제공해야 합니다. 허용되는 값은 다음과 같습니다 `gdpr` 및 `ccpa`. |
| 지원 대상 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 이제 Adobe에서 액세스/삭제 요청을 허용합니다 [!DNL Primetime Authentication], 사용 `primetimeAuthentication` 를 제품 값으로 채우는 방법을 설명합니다. |
| Privacy Service UI 개선 사항 | GDPR 및 CCPA 규정에 대한 별도의 작업 추적 페이지. GDPR과 CCPA에 대한 추적 데이터 간을 전환할 새로운 **규정 유형 **드롭다운. |

**알려진 문제**

* 없음

에 대한 자세한 정보 [!DNL Privacy Service]먼저 읽어보세요 [Privacy Service 개요](../../privacy-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다 [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 고객 특성 데이터 지원 | 고객 특성 데이터를 수집하기 위한 스트리밍 커넥터를 만들기 위한 UI 및 API를 지원합니다. |
| 클라우드 스토리지를 위한 추가 파일 형식 지원 | 클라우드 저장소에서 파일 수집은 이제 XDM 호환 Parquet 및 JSON 파일 형식을 지원합니다. |
| 액세스 제어 권한 지원 | Adobe Experience Platform의 액세스 제어 프레임워크는 데이터 수집의 소스에 대한 액세스 권한을 부여하는 데 필요한 권한을 제공합니다. 사용자의 권한 수준에 따라 사용자는 소스를 보거나 소스를 관리하거나 완전히 액세스가 거부될 수 있습니다. |

**액세스 제어 권한**

| 카테고리 | 사용 권한 | 설명 |
|--- | --- | ---|
| 데이터 수집 | 소스 관리 | 소스를 읽고, 만들고, 편집하고, 비활성화할 수 있는 액세스 권한. |
| 데이터 수집 | 소스 보기 | 에서 사용 가능한 소스에 대한 읽기 전용 액세스 권한 **[!UICONTROL 카탈로그]** 의 탭 및 인증된 소스 **[!UICONTROL 찾아보기]** 탭. |

**알려진 문제**

* 없음

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)

## 대상 {#destinations}

in [Real-Time CDP](../../rtcdp/overview.md), 대상은 대상 플랫폼과의 사전 구축된 통합으로 이러한 파트너에게 데이터를 원활하게 제공할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 액세스 제어 권한 지원 | Real-Time CDP의 대상 기능은 Adobe Experience Platform 액세스 제어 권한과 함께 작동합니다. 사용자의 권한 수준에 따라 대상을 보고, 관리하고, 활성화할 수 있습니다. |

**액세스 제어 권한**

| 카테고리 | 사용 권한 | 설명 |
|--- | --- | ---|
| 대상 | 대상 관리 | 대상을 읽기, 만들기, 편집 및 비활성화하기 위한 액세스 권한. |
| 대상 | 대상 보기 | 에서 사용 가능한 대상에 대한 읽기 전용 액세스 **[!UICONTROL 카탈로그]** 의 탭 및 인증된 대상 **찾아보기** 탭. |
| 대상 | 대상 활성화 | 대상에 데이터를 활성화하는 기능. 이 권한을 사용하려면 제품 프로필에 &quot;대상 관리&quot; 또는 &quot;대상 보기&quot;를 추가해야 합니다. |

**알려진 문제**

* 없음

자세한 내용은 [대상 개요](../../destinations/home.md) 추가 정보.
