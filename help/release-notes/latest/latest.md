---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 2023년 3월 릴리스 노트입니다.
source-git-commit: 2a7ff5d56ccc1a0b4c86018936d139f2e6d46cd6
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2023년 3월 29일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [데이터 준비](#data-prep)
- [세분화 서비스](#segmentation)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 메타 전환 API(베타)에 대한 빠른 시작 워크플로우 | 데이터 수집 홈 화면에서 &quot;시작하기&quot;에서 새로운 빠른 시작 워크플로우에 액세스합니다. 다음 [메타 전환 API에 대한 빠른 시작 워크플로우](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 에서는 몇 가지 간단한 단계로 이벤트 데이터를 서버 측에서 Meta로 수집하여 전송할 수 있습니다. |
| [!DNL Braze] 이벤트 전달 확장 | 다음 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 이벤트 전달 확장을 사용하면 Adobe Experience Platform Edge Network에서 캡처한 데이터를 활용하여 로 보낼 수 있습니다 [!DNL Braze] 를 사용하여 서버측 이벤트 형태로 [!DNL Braze] 사용자 추적 API. |
| [!DNL Mixpanel] 이벤트 전달 확장 | 다음 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 확장 을 사용하면 이벤트 전달을 활용하여 Adobe Experience Platform Edge Network에서 이벤트 정보를 캡처하고 이벤트 추적 API를 사용하여 Mixpanel에 전송할 수 있습니다. |

{style="table-layout:auto"}

## 데이터 준비 {#data-prep}

데이터 준비를 통해 데이터 엔지니어가 XDM(Experience Data Model) 간 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 URL 문자열 인코딩 및 디코딩 함수 | <ul><li>다음 `get_url_encoded` 함수는 URL을 입력으로 사용하고 특수 문자를 ASCII 문자로 바꾸거나 인코딩합니다.</li><li>다음 `get_url_decoded` 함수는 URL을 입력으로 사용하고 ASCII 문자를 특수 문자로 디코딩합니다.</li></ul> 자세한 내용은 [데이터 준비 함수 안내서](../../data-prep/functions.md). 예약된 문자와 해당 인코딩된 문자의 전체 목록을 보려면 다음 안내서를 읽어 보십시오 [특수 문자](../../data-prep/functions.md#special-characters). |

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## 세분화 서비스 {#segmentation}

[!DNL Segmentation Service] 고객 기반 내의 마케팅 가능한 사람 그룹을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 프로필 지표 | 프로필 지표를 더 정확하게 표현하기 위해 멤버십 분류 및 이탈 지표가 결합되고 이제 24시간 동안 계산됩니다. 에서 사용할 수 있는 추가 정보 [세그멘테이션 UI 안내서](../../segmentation/ui/overview.md) |

{style="table-layout:auto"}

자세한 내용은 [!DNL Segmentation Service]를 보려면 [세그먼테이션 개요](../../segmentation/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 베타 가용성 [!DNL Chatlio] | 다음 [!DNL Chatlio] 이제 베타 버전으로 소스를 사용할 수 있습니다. 를 사용하십시오 [!DNL Chatlio] 스트리밍할 소스 [!DNL Chatlio] 이벤트 데이터를 Experience Platform에 추가합니다. 자세한 내용은 [[!DNL Chatlio] 개요](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| 베타 가용성 [!DNL Customer.io] | 다음 [!DNL Customer.io] 이제 베타 버전으로 소스를 사용할 수 있습니다. 를 사용하십시오 [!DNL Customer.io] Experience Platform으로 고객 이벤트 데이터를 스트리밍할 소스입니다. 자세한 내용은 [[!DNL Customer.io] 개요](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| 베타 가용성 [!DNL Pendo] | 다음 [!DNL Pendo] 이제 베타 버전으로 소스를 사용할 수 있습니다. 를 사용하십시오 [!DNL Pendo] 제품 분석 데이터를 Experience Platform으로 스트리밍할 소스입니다. 자세한 내용은 [[!DNL Pendo] 개요](../../sources/connectors/analytics/pendo-webhook.md). |
| 초안 데이터 흐름 지원 | 이제 Flow Service API를 사용하여 데이터 흐름을 초안 상태로 설정할 수 있습니다. 초안 데이터 흐름은 나중에 새로운 정보를 사용하여 업데이트 및 게시할 수 있습니다. 자세한 내용은 다음 안내서를 참조하십시오. [소스 데이터 흐름을 초안으로 설정](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
