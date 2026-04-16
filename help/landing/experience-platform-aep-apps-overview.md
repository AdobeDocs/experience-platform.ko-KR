---
title: Adobe Experience Platform과 애플리케이션이 함께 작동하는 방식
description: Adobe Experience Platform과 각 애플리케이션은 단독으로 작동하며 함께 작동하여 고객 목표를 지원합니다.
solution: Experience Platform
feature: Getting Started
topic: Overview
role: Architect, Developer, Data Architect, Data Engineer, Business Practitioner
exl-id: c4f8e2a1-6b3d-4f92-9c7e-1a2b3c4d5e6f
source-git-commit: 60e7d803d72089348f11a34d6386aa9ccc51f487
workflow-type: tm+mt
source-wordcount: '3250'
ht-degree: 0%

---


# Adobe Experience Platform과 애플리케이션이 함께 작동하는 방식

이 주제에서는 세 가지 아이디어를 설명합니다.

1. [!DNL Adobe Experience Platform]이(가) 수행하는 작업
2. 각 애플리케이션이 수행하는 작업
3. 조직이 목표를 달성하고 고객에게 잘 제공할 수 있도록 플랫폼과 애플리케이션이 함께 작동하는 방식.

이 주제를 마케터, 제품 소유자 및 솔루션을 구축하거나 실행하는 사람과 공유합니다. 읽은 후에는 제품 작업이나 기술 세부 정보가 필요할 때 [!DNL Experience League]의 단계별 안내서를 사용하십시오.

>[!NOTE]
>
>이 항목은 개요입니다. 방법 단계, 사용자 인터페이스 작업 및 API 세부 정보는 [추가 리소스](#additional-resources)의 링크를 참조하십시오.

## 애플리케이션 정의 및 각 애플리케이션의 주요 목적 {#applications-at-a-glance}

이 설명서에서 응용 프로그램은 [!DNL Adobe Experience Platform]에서 실행되는 라이선스가 부여된 Adobe 제품입니다. 애플리케이션은 플랫폼과 동일한 고객 프로필, 데이터 구조, ID 링크 및 데이터 규칙을 사용합니다. 각 애플리케이션은 작업 유형(예: 채널에 대상자 보내기, 여정 실행 또는 결과 보고)에 대한 자체 화면 및 워크플로우를 추가합니다.

아래 표에는 각 응용 프로그램이 나와 있습니다. 그것은 짧은 설명과 주요 목적을 제공합니다. 모든 제품 에디션을 나열하지는 않습니다. 구입하실 수 있는 것은 면허증에 따라 다릅니다

| 애플리케이션 | 정의 | 주요 목적 |
|---------------|------------|----------------|
| [[!DNL Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/home) | 고객 데이터 및 대상용 애플리케이션 | 나만의 고객 데이터를 하나로 모읍니다. 자주 업데이트되는 대상을 작성합니다. 광고, 이메일, 모바일 앱 및 기타 도구로 대상과 속성을 보냅니다. 데이터 규칙이 적용됩니다. 동일한 제품군은 소비자 비즈니스, 비즈니스 고객 및 혼합 모델을 지원합니다. 버전에 대해서는 제품 도움말을 참조하십시오. |
| [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/en/docs/journey-optimizer) | 여정 및 메시지 애플리케이션 | 개인화된 여정(예: 시작 경로, 유지 또는 서비스 후 후속 조치)를 계획하고 실행합니다. 라이브 이벤트 및 프로필 데이터를 사용하여 채널 간에 메시지를 전송합니다. |
| [[!DNL Customer Journey Analytics]](https://experienceleague.adobe.com/ko/docs/customer-journey-analytics) | 채널 간 분석을 위한 애플리케이션 | 고객이 여정을 통해 이동하는 방법과 마케팅이 수행되는 방식을 측정하고 연구합니다. [!DNL Adobe Experience Platform]에 준비된 데이터를 사용합니다. |
| [[!DNL Adobe Mix Modeler]](https://experienceleague.adobe.com/ko/docs/mix-modeler) | 마케팅 측정 및 계획 애플리케이션 | 측정을 함께 가져옵니다(마케팅 믹스 모델링 포함). 마케팅을 위한 지출 시나리오를 계획합니다. [!DNL Adobe Experience Platform]을(를) 통해 연결된 데이터를 사용하므로 팀에서 결과를 도출하고 예산을 계획할 수 있습니다. |

>[!NOTE]
>
>다른 Adobe Experience Cloud 제품은 [!DNL Adobe Experience Platform]에 연결할 수 있습니다. 이 항목에서는 플랫폼을 고객 데이터의 주요 소스로 사용하는 애플리케이션에 중점을 둡니다. 제품 이름, 에디션 및 판매 품목은 라이센스와 국가 또는 지역에 따라 다를 수 있습니다.

## 읽고 이해할 내용 {#learning-outcomes}

이 주제를 읽고 나면 다음과 같은 작업을 수행할 수 있습니다.

1. 플랫폼 설명 — [!DNL Adobe Experience Platform]이(가) 데이터 및 데이터 규칙의 공유 기반으로 수행하는 작업을 설명합니다. 특정 응용 프로그램의 이름을 지정하지 않고 이를 설명할 수 있습니다.
2. 각 주요 애플리케이션에 대한 설명 — 각 애플리케이션이 지원하는 비즈니스 목표와 해당 애플리케이션이 어떤 작업을 위한 것인지 설명합니다.
3. 플랫폼과 애플리케이션이 서로 맞물리는 방식 설명 — 고객 프로필, ID, 데이터 셰이프(스키마) 및 데이터 규칙이 플랫폼에서 애플리케이션으로 이동하는 방식을 설명합니다. 팀이 각 도구에 대해 서로 상충하는 별도의 데이터 파이프라인을 빌드할 필요가 없는 이유를 설명합니다.
4. 목표를 솔루션의 오른쪽 부분에 연결 — 샘플 목표(예: &quot;이메일 및 모바일에서 온보딩 실행&quot;)에 대해 플랫폼의 어떤 부분과 해당 목표를 일반적으로 지원하는 애플리케이션의 이름을 지정합니다.

이 항목에서 &quot;목표&quot;는 조직이 원하는 것(예: 성장, 효율성 또는 고객 신뢰)을 의미합니다. &quot;고객&quot;은 브랜드와 상호 작용하는 사람을 의미합니다. 플랫폼과 애플리케이션은 팀이 이러한 고객에게 서비스를 제공하는 데 도움을 주기 위해 존재합니다.

## 이 주제를 읽어야 하는 사람 {#who-should-read}

| 내 역할 | 이 주제의 장점 |
|-----------|------------------------|
| 비즈니스 및 마케팅 리더 | 고객 및 브랜드 목표를 플랫폼 기능 및 애플리케이션에 연결합니다. 기술 팀과 동일한 단어를 사용합니다. |
| 마케팅 운영, 분석 또는 고객 경험 담당자 | 데이터의 결합 위치, 선택 위치 및 어느 단계에 맞는 애플리케이션을 확인하십시오. |
| 설계자, 엔지니어 및 개발자 | 디자인하거나 빌드할 때 나머지 [!DNL Experience League]과(와) 동일한 간단한 모델과 용어를 사용하십시오. |

## [!DNL Adobe Experience Platform]이(가) 단독으로 작동하는 방식 {#platform-alone}

[!DNL Adobe Experience Platform]은(는) 고객 경험 데이터의 기본 계층입니다. 단일 마케팅 화면이 아닙니다. 백그라운드에서 실행되는 서비스를 기반으로 구축됩니다. 애플리케이션을 열기 전에 플랫폼은 다음을 수행할 수 있습니다.

| 플랫폼의 기능 | 이것이 유용한 이유 |
|--------------------------|---------------------|
| 웹 사이트, 앱 및 비즈니스 시스템에서 데이터를 가져옵니다(파일 또는 라이브 스트림으로). | 하나의 채널 또는 하나의 데이터베이스로 고정되어 있지 않습니다. 시간이 지남에 따라 더 완전한 보기를 작성할 수 있습니다. |
| 이벤트와 필드가 하나의 의미를 공유하도록 XDM(Experience Data Model) 기반의 스키마로 데이터를 구조화합니다 | 데이터를 분석하고 대상을 보내고 규정 준수를 확인하는 팀은 모두 동일한 정의를 사용합니다. 그것은 실수를 줄이고 일을 반복한다. |
| 규칙 내에서 동일한 사용자 또는 계정을 장치 및 시스템 간에 인식할 수 있도록 ID를 연결합니다 | 팀은 정책이 허용하는 고객의 단일 보기에서 작업할 수 있습니다. |
| 결정 및 데이터 전송을 위해 [!DNL Real-Time Customer Profile]을(를) 실시간 보기로 최신 상태로 유지합니다. | 선택 항목은 어제의 이전 파일뿐만 아니라 현재 데이터를 사용할 수 있습니다. |
| 프로필 데이터, 비헤이비어 및 동의에서 대상자(세그먼테이션) 구축 | 한 곳에 누가 포함되는지 정의합니다. 다른 단계는 해당 논리를 재사용합니다. |
| 데이터를 대상(내보내기 및 연결된 시스템)으로 보내고 레이블, 정책 및 [!DNL Privacy Service]을 통해 데이터 규칙을 적용합니다. | 팀은 여전히 동의와 법률을 준수하면서 더 빠르게 이동할 수 있습니다. |

한마디로 이 플랫폼은 고객 데이터를 하나로 묶어 규칙을 적용하고 사용할 데이터를 준비한다. 애플리케이션이 여정 디자인, 미디어 워크플로우 또는 크로스 채널 보고서에 제공하는 전체 화면을 대체하지는 않습니다. 애플리케이션은 이러한 경험을 제공합니다.

### 플랫폼 서비스 개요 {#core-platform-services}

| 영역 | 기본 계층에서 수행하는 작업 |
|------|--------------------------------|
| 데이터 수집([!DNL Tags], [!DNL Experience Platform Web SDK], [!DNL Experience Platform Mobile SDK], 데이터스트림) | 표준 방식으로 디지털 경험에서 데이터를 수집합니다. |
| 소스 및 데이터 가져오기 | 회사 시스템 및 클라우드 소스의 데이터를 플랫폼에 연결합니다. |
| XDM 및 스키마 | 경험 데이터의 구조 및 의미를 설정합니다. |
| [!DNL Identity Service] | 식별자를 정책 내의 단일 보기에 연결합니다. |
| [!DNL Real-Time Customer Profile] | 의사 결정 및 데이터 전송에 사용되는 라이브 프로필을 유지합니다. |
| 세분화 | 프로필 데이터 및 이벤트에서 대상자를 정의합니다. |
| 대상 | 마케팅 또는 서비스를 실행하는 다른 시스템에 대상과 속성을 보냅니다. |
| 데이터 거버넌스, [!DNL Privacy Service], 동의 | 데이터 사용 방법을 제어합니다. |
| [!DNL Data Science Workspace] | 플랫폼 데이터에 대한 머신 러닝 모델을 구축, 교육 및 실행합니다. 이는 애플리케이션이 아닌 플랫폼 기능입니다. |
| [!DNL Query Service] | 분석 및 보고를 위해 Experience Platform 데이터에 대해 SQL을 실행합니다. 애플리케이션이 아닌 플랫폼 서비스입니다. |

이러한 영역은 간단한 흐름을 지원합니다. 수집 → 통합 → 측정→ 활성화→ 결정합니다. 데이터 규칙은 각 단계에서 적용됩니다.

## 응용 프로그램이 스스로 작동하는 방식 {#applications-alone}

각 응용 프로그램 및 주요 용도의 간단한 목록은 [응용 프로그램 및 각 응용 프로그램의 주요 용도에 있습니다](#applications-at-a-glance). 아래 표에는 세부 사항이 추가됩니다. 각 애플리케이션이 스스로 수행하는 작업과 지원하는 목표를 보여 줍니다.

애플리케이션은 플랫폼의 사용자 경험 및 워크플로우입니다. 각각은 팀이 주요 유형의 작업을 수행하는 데 도움이 됩니다. 이러한 모든 규칙은 동일한 프로필 및 데이터 규칙에서 파생됩니다. 팀에서는 각 도구의 전체 데이터 스택을 복사할 필요가 없습니다.

| 애플리케이션 | 자체 작업(주요 작업) | 목표에 도달하는 데 도움이 되는 목표 |
|-------------|-------------------------------------|------------------------------|
| [[!DNL Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/home) | 대상자 및 활성화 관리: 세그먼트를 작성하고, 멤버십을 자주 업데이트하고, 대상과 속성을 대상으로 보냅니다. 라이선스에 따라 소비자, 비즈니스 및 혼합 사용 사례를 지원합니다. | 통합 고객 데이터를 사용하여 적합한 사람에게 연락하고 유료, 소유 및 파트너 채널에서 잘못된 사람을 제외합니다. |
| [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/en/docs/journey-optimizer) | 여정 디자인 및 메시지 보내기: 하나의 여정 작업 공간에서 이벤트, 분기 경로에 반응하고 채널 간에 전송합니다. | 고객이 수행한 작업에 응답하는 개인화된 시퀀스(예: 온보딩, 유지 또는 서비스 후속 작업)를 실행합니다. |
| [[!DNL Customer Journey Analytics]](https://experienceleague.adobe.com/ko/docs/customer-journey-analytics) | 하나의 데이터 기반을 사용하여 여정 및 캠페인 결과를 보고하고 분석합니다. | 채널 전반에서 발생한 상황과 그 이유를 확인하여 지출과 경험을 개선할 수 있습니다. |
| [[!DNL Adobe Mix Modeler]](https://experienceleague.adobe.com/ko/docs/mix-modeler) | 플랫폼에 연결된 데이터를 모델과 결합하여 채널을 측정하고 계획 시나리오를 실행할 수 있습니다. | 채널 및 기타 요인이 결과에 미치는 영향을 꾸준히 확인하여 마케팅 지출을 계획하고 조정할 수 있습니다. |

간단히 말해, 애플리케이션은 팀이 매일 작업을 수행하는 방식입니다(활성화, 여정, 분석, 마케팅 측정). 플랫폼은 이러한 모든 팀이 신뢰하는 고객 데이터와 규칙을 보유하는 것입니다. 또한 플랫폼은 위의 서비스를 통해 쿼리 및 고급 모델링을 제공합니다.

>[!IMPORTANT]
>
>사용할 수 있는 애플리케이션은 Adobe 라이선스에 따라 다릅니다. 기능, 제한 및 가용성은 변경될 수 있습니다. 계약서와 최신 [!DNL Experience League] 설명서를 확인하십시오.

## 플랫폼과 애플리케이션이 함께 작동하는 방식 {#platform-and-apps-together}

플랫폼과 애플리케이션이 함께 작동한다고 하면 세 가지를 의미합니다.

1. 하나의 고객 프로필, 많은 제품([!DNL Real-Time Customer Profile], [!DNL Identity Service] 및 데이터 규칙)이 공유됩니다. [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics] 및 [!DNL Adobe Mix Modeler]이(가) 같은 기준(및 관련 데이터)에서 읽었습니다. 프로세스에 필요하지 않는 한 분석에 대한 고객 목록과 마케팅에 대한 다른 목록을 유지 관리하지 않습니다.
2. 발생한 일에 대한 한 가지 의미 — 데이터는 XDM 스키마로 형성됩니다. 동일한 이벤트에서 보고, 여정 및 대상 규칙을 제공할 수 있습니다. 팀은 정의에 대해 논쟁하는 시간이 줄어듭니다.
3. 데이터 규칙 한 곳 — 응용 프로그램이 사용하는 데이터에 레이블과 정책이 적용됩니다. 데이터 규칙은 나중에 각 도구 내부에 추가되지 않습니다.


### 엔드 투 엔드 흐름(플랫폼과 앱에서 작업이 실행되는 방식) {#end-to-end-flows}

| 단계 | 플랫폼의 기능 | 일반적으로 어떤 애플리케이션을 추가합니까 |
|-------|----------------------------|-------------------------------------|
| 아름 | 데이터 가져오기, 구성, ID 연결 및 프로필 업데이트 | 애플리케이션은 프로필 및 이벤트를 읽습니다. 이 두 함수는 데이터를 가져오는 단계를 대체하지 않습니다. |
| 결정 | 통합된 데이터를 사용하여 세그먼트 작성 및 자격 확인 | 대상을 빌드할 [!DNL Real-Time CDP]입니다. 여정 경로 및 컨텍스트의 다음 최적 작업용 [!DNL Adobe Journey Optimizer]. |
| 활성화 | 대상 및 대상자 및 속성의 제어된 내보내기 | [!DNL Real-Time CDP]은(는) 다양한 활성화 패턴을 지원합니다. 여정은 사용자가 설정한 채널을 통해 메시지를 보냅니다. |
| 측정 | 데이터 레이어에서 하나의 모델을 따르는 이벤트 및 ID | 여정 및 캠페인 보고용 [!DNL Customer Journey Analytics]. 플랫폼에 연결된 데이터를 사용하는 통합 마케팅 측정 및 계획에 대한 [!DNL Adobe Mix Modeler]. |

## 예: 플랫폼과 4개의 애플리케이션을 모두 사용하는 워크플로우 1개 {#example-full-stack-workflow}

아래의 이야기는 하나의 일반적인 패턴입니다. 팀이 순서를 변경하거나 단계를 건너뛸 수 있습니다. 목표는 [!DNL Adobe Experience Platform]과(와) [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics] 및 [!DNL Adobe Mix Modeler]이(가) 모두 동일한 프로그램에 나타날 수 있는 방법을 보여 주는 것입니다.

### 시나리오 {#example-scenario}

소매 브랜드는 계절별로 구매 및 온보딩 프로그램을 실행합니다. 리더쉽은 지출 계획, 유료 미디어로 새로운 구매자에게 연결, 메시지로 새로운 고객 환영, 결과 보고 등을 원합니다. 브랜드는 [!DNL Adobe Experience Platform]에서 통합 고객 데이터를 사용합니다.

### 워크플로우에서 수행되는 작업 {#example-steps}

1. [!DNL Adobe Experience Platform]&#x200B;(플랫폼)\
   팀은 가능한 경우 광고에서 웹 및 앱 이벤트, 주문, 동의, 비용 또는 성능 데이터를 가져옵니다. 데이터는 공유 XDM 스키마를 사용합니다. 알려진 고객 링크 [!DNL Identity Service]개. 사람들이 쇼핑하고 등록할 때 [!DNL Real-Time Customer Profile]개의 업데이트가 있습니다. 데이터 규칙 및 동의는 플랫폼에 저장됩니다.\
   *이 단계를 수행하지 않으면 아래의 응용 프로그램을 읽을 수 없습니다.*

2. [!DNL Adobe Mix Modeler]\
   마케팅 및 재무 부서에서는 채널이 매출에 기여하는 방식 및 해당 시즌 동안 미디어 간에 예산을 분할하는 방식을 검토합니다. 이들은 플랫폼에 연결된 조화로운 마케팅 및 결과 데이터를 도출하는 모델 및 계획 뷰를 사용합니다.\
   *계획 수준에서 &quot;어떻게 투자해야 합니까&quot;에 대한 답을 제공합니다. 전자 메일을 보내거나 일일 대상을 직접 만들지 않습니다.*

3. [!DNL Real-Time CDP]\
   획득 팀은 대상을 구성합니다(예: 구매자나 장바구니에 항목을 남긴 사람일 수 있음). 이러한 대상을 광고 및 기타 대상으로 활성화합니다. 또한 현재 고객이 잠재 고객으로 타겟팅되지 않도록 제외 대상을 구축할 수도 있습니다.\
   *이 단계에서는 &quot;유료 채널과 소유 채널에서 연결하거나 제외해야 하는 사람&quot;에 대한 답을 제공합니다.*

4. [!DNL Adobe Journey Optimizer]\
   라이프사이클 팀은 구매 또는 등록 후 시작 여정을 실행합니다. 여정은 프로필 또는 이벤트 조건, 분기(예: 첫 구매와 반복)를 수신하고 이메일 또는 모바일 메시지를 보냅니다.\
   *이 단계에서는 &quot;이 사용자가 다음에 어떤 메시지 또는 경로를 받게 됨&quot;에 대한 답을 제공합니다.*

5. [!DNL Customer Journey Analytics]\
   Analytics 팀은 광고 터치에서 구매 및 온보딩에 이르기까지 전체 경로에서 보고서와 대시보드를 작성합니다. 다른 곳에서 비즈니스가 사용하는 것과 동일한 이벤트 및 프로필 기반 정의를 사용하여 단계, 채널 및 세그먼트를 측정합니다.\
   *이 단계에서는 &quot;여정에서 무슨 일이 발생했으며 어떤 부분이 작동했는지&quot;*&#x200B;에 답합니다.

팀은 한 분기에 걸쳐 2~5단계를 동시에 실행하는 경우가 많습니다. Mix Modeler 업데이트는 라이브 대상이나 여정에 비해 느리게 순환될 수 있습니다. 그건 정상이야

### 애플리케이션 작동 방식 {#example-together}

- 프로필 하나와 이벤트 모델 하나. 동일한 사람과 동일한 이벤트가 플랫폼에서 [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer] 및 [!DNL Customer Journey Analytics]&#x200B;(으)로 이동합니다. Mix Modeler은 플랫폼의 연결 및 통합 데이터를 사용합니다. 설정에 따라 요약(예: 주간 지출)과 이벤트 수준 데이터를 사용할 수 있습니다.
- 다른 직업과 같은 진실. [!DNL Real-Time CDP]이(가) 연결할 사용자를 푸시합니다. [!DNL Adobe Journey Optimizer]은(는) 작업 후 다음에 수행되는 작업을 실행합니다. [!DNL Customer Journey Analytics]은(는) 여러 단계에서 발생한 내용을 표시합니다. [!DNL Adobe Mix Modeler]은(는) 예산을 더 높은 수준으로 이동해야 하는 이유를 지원합니다.
- 데이터 규칙은 데이터와 함께 이동합니다. 플랫폼의 레이블 및 동의는 세그먼트, 여정 및 보고에서 사용할 수 있는 프로필에 영향을 줍니다.

### 구성 시 주의 사항 {#example-gotchas}

>[!IMPORTANT]
>
>이러한 이슈들은 실제 프로젝트에서 혼란을 야기한다. 설계자 및 관리자를 위한 체크포인트로 처리합니다.

| 영역 | 시청 항목 |
|------|----------------|
| ID | 웹, 앱 및 CRM에서 서로 다른 식별자 또는 네임스페이스 설정을 전송하는 경우 프로필은 한 사람을 두 사람으로 분할할 수 있습니다. 세그먼트, 여정 및 보고서가 일치하지 않습니다. 활성화 규모를 조정하기 전에 ID 규칙과 기본 ID를 맞춥니다. |
| 동의 및 데이터 규칙 | [!DNL Real-Time CDP] 또는 [!DNL Adobe Journey Optimizer]에서 사용되는 데이터 세트에 레이블이 지정되지 않았거나 올바르게 동의되지 않으면 활성화하거나 다른 사용자에게 보내지 말아야 할 메시지를 보낼 수 있습니다. 대상자 및 여정에 사용하는 동일한 데이터 세트의 레이블, 정책 및 동의 필드를 검토하십시오. |
| 동시에 [!DNL Real-Time CDP] 및 [!DNL Adobe Journey Optimizer] | 동일한 사람이 활성화된 대상과 여정에 있을 수 있습니다. 여정을 입력하는 사용자에 대해 제외 목록, 여정 항목 필터 또는 규칙 지우기를 사용하지 않는 경우 메시지를 이중으로 표시하거나 오퍼와 충돌할 수 있습니다. 먼저 팀을 조정하고 샌드박스에서 테스트합니다. |
| [!DNL Customer Journey Analytics]개 정의 | 보고서에서 [!UICONTROL Data views] 및 지표 규칙을 사용합니다. 해당 정의가 [!DNL Real-Time CDP] 또는 [!DNL Adobe Journey Optimizer]에서 마케터가 사용하는 이벤트 또는 특성과 일치하지 않으면 대시보드가 캠페인 보고서와 일치하지 않습니다. 차원 및 지표 정의를 관련자와 맞춥니다. |
| [!DNL Adobe Mix Modeler] 시간 및 데이터 셰이프 | 믹스 모델링은 종종 조화되거나 롤업된 입력 및 예약된 새로 고침을 사용합니다. [!DNL Real-Time Customer Profile]과(와) 동일한 실시간 답변을 기대하지 마십시오. 지출과 결과 데이터는 조화롭게 매핑되고 정리되어야 한다. 잘못된 매핑은 채널 크레딧과 예산 조언을 왜곡합니다. |
| Mix Modeler과 여정 분석 비교 | Mix Modeler은 채널 수준의 기여도와 계획에 중점을 둡니다. [!DNL Customer Journey Analytics]은(는) 여정 경로 및 세그먼트에 중점을 둡니다. 관련 질문에 대한 답변은 서로 다릅니다. 문서화된 브리지 없이 하나의 KPI를 다른 KPI와 일치시키지 마십시오. |
| 샌드박스 | 샌드박스의 구성이 자동으로 프로덕션으로 이동하지 않습니다. 스키마, 세그먼트, 여정 및 연결에 대한 프로모션 프로세스를 계획합니다. |
| 시간대 | 여정, 보고 창 및 광고 플랫폼은 서로 다른 시간대를 사용할 수 있습니다. 창 맞춤이 잘못되면 &quot;잘못된&quot; 카운트가 발생하고 여정 항목이 손상됩니다. |

### 가드레일 및 제한 사항 {#example-guardrails}

Adobe에서는 [!DNL Adobe Experience Platform] 및 각 애플리케이션에 대한 보호 기능을 게시합니다. 보호 기능에는 구성에 대한 제한, 예상 성능 및 안전 범위가 설명되어 있습니다. 오류, 속도 저하 또는 불안정한 행동을 방지하는 데 도움이 됩니다. 보호 기능은 SLA(서비스 수준 계약)가 아닙니다. 법적 의미에서 속도나 가동 시간을 보장하지는 않습니다.

계약, 제품 설명 및 판매 주문은 계약 한도 또는 권한을 설정할 수 있습니다. 이러한 규칙은 일반적인 설명서와 다를 수 있습니다. 확실하지 않은 경우 [!DNL Experience League]과(와) 함께 계약 및 Adobe 계정 팀을 사용하십시오.

| 주제 | 계획 대상 |
|-------|------------------|
| 소프트 제한 및 하드 제한 | 몇 가지 제한은 지침입니다. 이를 훨씬 능가하는 경우 성능이 저하되거나 지연 시간이 늘어날 수 있습니다. 기타 제한은 시스템 또는 계약에 의해 결정됩니다. 설정 또는 구매를 변경하지 않으면 이를 초과할 수 없습니다. |
| 제한이 적용되는 위치 | 샌드박스가 아닌 조직 수준에서 많은 제한이 적용됩니다. 샌드박스 환경에서는 프로덕션 환경보다 최대 용량이 더 작은 경우가 많습니다. 샌드박스의 테스트 결과는 전체 성능을 나타내지 않을 수 있습니다. |
| 수집 및 프로필 | 많은 이벤트 볼륨, ID 볼륨 또는 프로필 수는 비용, 속도 및 안정성에 영향을 줍니다. 파이프라인을 디자인할 때 데이터 수집 및 프로필 보호를 따르십시오. 대상이 매우 많거나 업데이트가 자주 있으면 활성화 경로에 문제가 발생할 수 있습니다. |
| 세분화 및 활성화 | [!DNL Real-Time CDP]에 세그먼트, 활성화 및 대상에 대한 보호 기능이 있습니다. 또한 파트너 대상에는 고유한 대문자, 파일 크기 또는 필수 필드가 있습니다. 양쪽을 모두 무시해도 UI에서 작동하는 세그먼트는 여전히 대상에서 실패하거나 잘릴 수 있습니다. |
| [!DNL Adobe Journey Optimizer] | 여정, 채널 및 메시지 전송 속도에는 제품 제한이 있습니다. 복잡한 여정 또는 많은 양의 메시지는 [!DNL Adobe Journey Optimizer] 가드레일에 대해 검토해야 메시지를 신뢰할 수 있습니다. |
| [!DNL Customer Journey Analytics] | 보고에 연결, [!UICONTROL Data views], 행 및 카디널리티에 대한 제한이 있습니다. 크기가 크거나 이벤트가 많은 경우 보고서를 계속 사용할 수 있도록 설계를 검토해야 합니다. |
| [!DNL Adobe Mix Modeler] | 모델링과 계획은 충분한 역사와 깔끔한 조화 데이터에 의존합니다. 데이터 세트, 모델 및 새로 고침 동작에 대한 제품 제한이 있습니다. 얇거나 시끄러운 데이터는 취약하거나 불안정한 모델을 생성합니다. |
| API 및 자동화 | 프로그래밍 방식 호출은 비율 제한과 할당량을 사용합니다. 이러한 제한을 무시하는 일괄 처리 작업은 실패하거나 제한될 수 있습니다. |
| 지역 및 가용성 | 일부 기능, 대상 또는 애플리케이션은 모든 지역에서 사용할 수 없습니다. 전체 워크플로우를 설계하기 전에 데이터 상주 및 제품 가용성에 대한 지역을 확인합니다. |

>[!NOTE]
>
>숫자 제한 및 기본값은 시간에 따라 변경됩니다. 이 개요의 제한을 디자인 문서에 복사하지 마십시오. [!DNL Experience League]의 현재 보호 페이지, 조직에서 사용 중인 라이선스 사용 보기 및 계약을 사용하십시오.

### 자세한 내용 {#where-to-read-guardrails}

&#x200B;* [Experience Platform 및 응용 프로그램 보호](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-diagrams/architecture-overview/guardrails) - 플랫폼과 응용 프로그램에서 보호 기능이 작동하는 방식에 대한 개요입니다.
&#x200B;* [데이터 수집을 위한 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/ingestion/guardrails) — 수집 처리량 및 관련 제한.
&#x200B;* [Real-Time CDP 보호](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview) — 세그먼트, 활성화 및 Real-Time CDP 사용.
&#x200B;* [라이선스 사용](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/data-management-best-practices) - Experience Platform의 데이터 관리 및 라이선스 사용 사례(조직에 해당하는 경우).

워크플로우가 [!DNL Customer Journey Analytics], [!DNL Adobe Journey Optimizer], [!DNL Adobe Mix Modeler] 또는 [!DNL Query Service]에 많이 의존하는 경우 제품 도움말에서 해당 제품에 대한 보호 항목도 읽어 보십시오.

## 플랫폼 및 애플리케이션에 목표 매핑 {#goals-map}

이 표를 사용하여 원하는 항목, 플랫폼이 제공하는 항목 및 도움이 되는 애플리케이션을 확인합니다.

| 목표 | 플랫폼에서 사용 방법 | 응용 프로그램에서 사용할 사항 |
|-----------|-------------------------------------|--------------------------------------|
| 채널에서 한 사람 또는 계정 보기 | [!DNL Identity Service], [!DNL Real-Time Customer Profile], XDM | 나열된 모든 응용 프로그램이 혜택을 받습니다. [!DNL Real-Time CDP] 및 [!DNL Adobe Journey Optimizer]은(는) 대상자와 여정을 보낼 때 프로필을 사용합니다. |
| 최신 멤버십으로 캠페인 및 목록 실행 | 프로필, 세그먼테이션, 대상, 데이터 규칙 | 대상자를 보내는 방법에 대한 [!DNL Real-Time CDP]. 대상은 정책 컨텍스트를 전달합니다. |
| 동작에 반응하는 여러 단계 경험 실행 | 프로필, 라이브 이벤트, 데이터 규칙 | 여정 논리 및 메시지의 경우 [!DNL Adobe Journey Optimizer]입니다. |
| 숫자가 일치하는 여정 및 채널에 대한 보고서 | 공유 XDM 이벤트 및 ID | 같은 데이터에 대한 분석을 위해 [!DNL Customer Journey Analytics]을(를) 사용합니다. |
| 채널이 마케팅 예산을 기여하고 계획하는 방법 보기 | 통합 데이터 세트, 데이터 규칙, 모델에 맞는 데이터 준비 완료 | 혼합 모델링 및 지출 계획에 대한 [!DNL Adobe Mix Modeler]. |
| 고객 사실에 맞게 마케팅 및 서비스 유지 | 프로필, 데이터 규칙, 다른 시스템에 대한 선택적 연결 | 다른 시스템을 연결하는 방법은 다를 수 있습니다. 플랫폼은 고객 데이터의 기반이 됩니다. |

## 역할 및 핸드오프 {#roles-and-handoffs}

| 단계 | 자주 관련된 사용자 | 주로 사용하는 항목 |
|-------|------------------------|----------------------|
| 데이터에 대한 의미 및 규칙 정의 | 데이터 거버넌스, 법률, 마케팅 리더십 | 플랫폼의 스키마, 레이블, 정책 |
| 컬렉션 및 데이터 파이프라인 설정 | 데이터 엔지니어, 마케팅 기술 | 플랫폼에서 [!DNL Tags], SDK, 소스, 데이터 준비 |
| 대상자 및 여정 작성 | 마케팅, CRM, 여정 팀 | 동일한 프로필의 응용 프로그램([!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer]) |
| 매일 활성화 및 실행 | 마케팅 운영, 미디어, 라이프사이클 팀 | 대상, 여정 보고, 경고 |
| 감사 및 개선 | Analytics, 규정 준수, 운영 | 감사 로그, 모니터링, 대시보드 |

## 용어 {#terminology}

&#x200B;* [!DNL Adobe Experience Platform] — 공유 서비스 및 기능: 데이터 가져오기, 데이터 모델링, [!DNL Identity Service], [!DNL Real-Time Customer Profile], 세그먼테이션, 대상, 데이터 거버넌스, 개인 정보 및 [!DNL Data Science Workspace] 및 [!DNL Query Service]과(와) 같은 기능.
&#x200B;* 응용 프로그램 — 특정 작업의 워크플로를 패키지하는 플랫폼의 사용 허가된 제품(예: [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics], [!DNL Adobe Mix Modeler]). [!DNL Query Service] 및 [!DNL Data Science Workspace]과(와) 같은 플랫폼 서비스와 다릅니다.

이는 [Experience Platform 설명서 개요](https://experienceleague.adobe.com/en/docs/experience-platform/landing/documentation/overview)가 콘텐츠를 그룹화하는 방식과 일치합니다.

## 추가 리소스 {#additional-resources}

&#x200B;* [Adobe Experience Platform 개요](https://experienceleague.adobe.com/en/docs/experience-platform/landing/home) - 도움말의 기본 진입점입니다.
&#x200B;* [Experience Platform 설명서 개요](https://experienceleague.adobe.com/en/docs/experience-platform/landing/documentation/overview) - 도움말 항목을 구성하는 방법.
&#x200B;* [Digital Experience 블루프린트](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/overview/experience-cloud) - 사용 사례 및 산업별 디자인 예

실습형 학습은 [!DNL Experience League]의 [!DNL Experience Platform Web SDK]에 있는 튜토리얼과 과정, XDM과 스키마, ID, 세그멘테이션 및 대상을 참조하십시오.

>[!NOTE]
>
>이 항목을 Adobe 문서 저장소에 추가할 때 저장소 규칙에 대해 `exl-id`, `feature` 및 `topic`을(를) 확인하십시오. 워크플로우에서 새 ID를 할당하는 경우 YAML 헤더의 자리 표시자 `exl-id`을(를) 바꾸십시오.
