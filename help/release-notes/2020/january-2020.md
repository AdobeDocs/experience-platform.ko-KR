---
title: Adobe Experience Platform 릴리스 정보
description: 'Experience Platform 릴리스 노트: 2020년 1월 15일'
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 7%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2020년 1월 15일**

Adobe Experience Platform의 기존 기능 업데이트:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM) 시스템  {#xdm}

표준화 및 상호 운용성은 [!DNL Experience Platform]의 주요 개념입니다. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

XDM은 디지털 경험의 강력함을 향상시키도록 고안된 문서화된 사양입니다. Adobe Experience Platform의 서비스와 통신할 수 있도록 모든 응용 프로그램에 대한 공통 구조와 정의를 제공합니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 보다 빠르고 통합된 방식으로 통찰력을 제공하는 일반적인 표현 방식으로 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고, 세그먼트를 통해 고객 고객을 정의하고, 고객 속성을 개인화를 위해 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 동일한 계층 필드의 필드 유형 제한 | XDM 필드가 특정 유형으로 정의된 후, 동일한 이름 및 계층의 다른 필드는 사용되는 클래스 또는 스키마 필드 그룹에 관계없이 동일한 필드 유형을 사용해야 합니다. 예를 들어 XDM [!DNL Profile] 클래스에 대한 필드 그룹에 &quot;integer&quot; 유형의 `profile.age` 필드가 포함되어 있으면 XDM [!DNL ExperienceEvent]에 대한 유사한 필드 그룹에는 &quot;string&quot; 유형의 `profile.age` 필드가 포함될 수 없습니다. 다른 필드 유형을 활용하려면 필드가 이전에 정의한 필드(예: `profile.person.age`)와 다른 계층 구조를 가져야 합니다. 이 기능은 스키마를 조합하여 가져올 때 충돌을 방지하기 위한 것입니다. 제약 조건은 기존 스키마에 소급되지 않지만 필드 유형 충돌에 대한 스키마를 검토하고 필요에 따라 편집하는 것이 좋습니다. |
| 대/소문자를 구분하는 필드 유효성 검사 | 동일한 수준의 사용자 지정 필드에는 대문자화에 관계없이 이름이 달라야 합니다. 예를 들어 &quot;이메일&quot;이라는 사용자 정의 필드를 추가하는 경우 &quot;email&quot;이라는 동일한 수준에서 다른 사용자 정의 필드를 추가할 수 없습니다. |

**알려진 문제**

* None

[!DNL Schema Registry] API 및 [!DNL Schema Editor] 사용자 인터페이스를 사용하여 XDM을 사용하는 방법에 대한 자세한 내용은 [XDM 시스템 설명서](../../xdm/home.md)를 참조하십시오.

## [!DNL Privacy Service] {#privacy}

새로운 법률 및 조직 규정은 사용자가 요청 시 데이터 저장소에서 개인 데이터를 액세스하거나 삭제할 수 있는 권한을 제공합니다. Adobe Experience Platform [!DNL Privacy Service]은(는) 고객의 이러한 데이터 요청을 관리하는 데 도움이 되는 RESTful API 및 사용자 인터페이스를 제공합니다. [!DNL Privacy Service]을 사용하면 Adobe Experience Cloud 애플리케이션에서 개인 또는 개인 고객 데이터를 액세스하고 삭제하기 위한 요청을 제출할 수 있으므로 법적 및 조직의 개인 정보 보호 규정을 자동으로 준수할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| [!DNL Privacy Service] 재브랜딩 | 이전에 &quot;GDPR 서비스&quot;라고 이름 붙여진 이 서비스는 GDPR 외에도 다른 규정을 지원하도록 성장하여 [!DNL Privacy Service](으)로 다시 브랜딩되었습니다. |
| 새 API 끝점 | [!DNL Privacy Service] API의 기본 경로가 `/data/privacy/gdpr`에서 `/data/core/privacy/jobs`(으)로 업데이트되었습니다. |
| 새로 필요한 `regulation` 속성 | [!DNL Privacy Service] API에서 새 작업을 만들 때 작업을 추적할 규칙을 나타내려면 요청 페이로드에 `regulation` 속성을 제공해야 합니다. 허용된 값은 `gdpr` 및 `ccpa`입니다. |
| 지원 대상 [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] 이제 Adobe의 액세스/삭제 요청 [!DNL Primetime Authentication]을 제품 값 `primetimeAuthentication` 으로 사용할 수 있습니다. |
| Privacy Service UI 개선 사항 | GDPR 및 CPA 규정에 대한 작업 추적 페이지를 따로 분류합니다. 새로운 **규정 유형 **드롭다운을 사용하여 GDPR과 CCPA에 대한 추적 데이터 간을 전환할 수 있습니다. |

**알려진 문제**

* 없음

[!DNL Privacy Service]에 대한 자세한 내용은 [Privacy Service 개요](../../privacy-service/home.md)를 읽어 보십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있는 동시에 [!DNL Platform] 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행에 대한 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 고객 속성 데이터 지원 | 고객 속성 데이터를 인제스트하는 스트리밍 커넥터를 만들기 위한 UI 및 API 지원. |
| 클라우드 스토리지를 위한 추가 파일 포맷 지원 | 클라우드 스토리지에서 파일 수집은 이제 XDM 호환 Portable 및 JSON 파일 포맷을 지원합니다. |
| 액세스 제어 권한 지원 | Adobe Experience Platform의 액세스 제어 프레임워크는 데이터 수집에서 소스에 대한 액세스 권한을 부여하는 데 필요한 권한을 제공합니다. 사용자는 사용 권한 수준에 따라 소스를 보거나 소스를 관리하거나 액세스 권한을 모두 거부할 수 있습니다. |

**액세스 제어 권한**

| 카테고리 | 사용 권한 | 설명 |
|--- | --- | ---|
| 데이터 수집 | 소스 관리 | 소스를 읽기, 만들기, 편집 및 비활성화할 수 있습니다. |
| 데이터 수집 | 소스 보기 | **[!UICONTROL Catalog]** 탭의 사용 가능한 소스와 **[!UICONTROL Browse]** 탭의 인증된 소스에 대한 읽기 전용 액세스. |

**알려진 문제**

* 없음

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

## 대상 {#destinations}

[실시간 CDP](../../rtcdp/overview.md)에서 대상은 대상 플랫폼과 사전 구축된 통합으로, 해당 파트너에게 데이터를 원활하게 활성화할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
|--- | ---|
| 액세스 제어 권한 지원 | 실시간 CDP의 대상 기능은 Adobe Experience Platform 액세스 제어 권한과 함께 작동합니다. 사용자의 권한 수준에 따라 대상을 보고, 관리하고, 활성화할 수 있습니다. |

**액세스 제어 권한**

| 카테고리 | 사용 권한 | 설명 |
|--- | --- | ---|
| 대상 | 대상 관리 | 대상을 읽고, 만들고, 편집하고, 비활성화하는 액세스. |
| 대상 | 대상 보기 | **찾아보기** 탭의 **[!UICONTROL Catalog]** 탭 및 인증된 대상에 있는 사용 가능한 대상에 대한 읽기 전용 액세스. |
| 대상 | 대상 활성화 | 대상에 대한 데이터 활성화 기능 이 권한을 사용하려면 제품 프로필에 &quot;대상 관리&quot; 또는 &quot;대상 보기&quot;를 추가해야 합니다. |

**알려진 문제**

* 없음

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.
