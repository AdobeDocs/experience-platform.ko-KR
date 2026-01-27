---
title: Salesforce Marketing Cloud (V2) Source 개요
description: API 또는 사용자 인터페이스를 사용하여 Salesforce Marketing Cloud(V2)를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
source-git-commit: 3c200ff1a29c3462a5d4fef554f6a410cfcbdde8
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]&#x200B;(V2) 소스 개요

>[!IMPORTANT]
>
>원래 [[!DNL Salesforce Marketing Cloud] (V1)](salesforce-marketing-cloud.md) 원본은 2026년 1월부터 더 이상 사용되지 않습니다. 더 이상 사용되지 않는 이 원본에 대해 사용할 수 있는 마이그레이션이 없으므로 새 [!DNL Salesforce Marketing Cloud]&#x200B;(V2) 원본을 사용하여 데이터를 다시 구현해야 합니다.

Adobe [Real-Time CDP](../../../rtcdp/overview.md)과(와) [!DNL Salesforce Marketing Cloud] 간의 통합은 데이터 확장이 제공하는 유연성과 제어성으로 인해 데이터 확장을 활용하도록 설계되었습니다. 미리 정의된 필드로 제한되고 주로 시스템 수준 추적을 제공하는 표준 시스템 테이블(데이터 보기 및 기본 제공 개체)과 달리, 데이터 확장 기능을 사용하여 사용자 정의 필드를 정의하고, 다양한 비즈니스별 데이터를 구성하며, 고유한 요구 사항에 맞게 데이터 구조를 조정할 수 있습니다.

이러한 수준의 사용자 지정 및 확장성으로 인해 Real-Time CDP과 [!DNL Salesforce Marketing Cloud] 간의 통합은 표준 시스템 테이블이 아닌 데이터 확장을 사용합니다. 이 접근 방식은 보다 유연하고 확장 가능하며 통합된 데이터 관리 기반을 제공하여 비즈니스 목표에 부합하도록 합니다

[!DNL Salesforce Marketing Cloud] 원본을 사용하여 [!DNL Salesforce Marketing Cloud] 계정을 Real-Time CDP 및 Adobe Experience Platform에 연결할 수 있습니다. 시작하는 방법을 알려면 아래 설명서를 읽어 보십시오.

## 사용 사례 예 {#use-case-examples}

### 연락처 데이터를 사용하여 이메일 캠페인 개인화

소매 브랜드는 고객 라이프사이클 단계(예: 신규 고객, 반복 구매자, 단골 고객)를 기반으로 이메일 캠페인을 개인화하려고 합니다. 이를 위해 연락처 데이터 확장 을 만들어 이름, 이메일, 라이프사이클 단계 및 구매 행동을 포함한 주요 고객 정보를 저장합니다. 그런 다음 더 자세한 세분화 및 타겟팅을 위해 이 데이터를 Experience Platform에 수집합니다.

Contact Data Extension의 데이터를 Experience Platform에 수집함으로써, 브랜드는 라이프사이클 단계 및 구매 행동에 따라 고객을 세그먼트화할 수 있습니다. 예를 들어, 새 고객에게 환영 오퍼를 보내거나, 반복 구매자에게 충성도 보상을 보내거나, 타겟팅된 오퍼로 비활성 고객을 다시 참여시킬 수도 있습니다. 이 접근 방식은 개인화된 커뮤니케이션을 보장하며 보다 관련성 있고 효과적인 고객 참여를 가능하게 합니다.

### 개인화된 세분화를 위한 캠페인 데이터 수집

마케팅 팀은 이전 캠페인과의 관계를 기반으로 고객을 타겟팅하여 이메일 캠페인을 최적화하려고 합니다. 이를 위해 [!DNL Salesforce Marketing Cloud]에 Campaign 데이터 확장을 만들어 이메일 열기, 클릭 수, 캠페인 반응과 같은 고객 참여 데이터를 저장합니다. 그런 다음 추가적인 세그멘테이션 및 개인화를 위해 이 데이터가 Experience Platform에 수집됩니다.

마케팅 팀은 Campaign 데이터 확장에서 Experience Platform으로 이 데이터를 수집함으로써 제품 오퍼를 클릭하거나 긍정적인 반응을 보인 고객과 같은 과거 참여를 기반으로 고객을 세그먼트화할 수 있습니다. 참여한 고객은 향후 이메일에서 타겟팅된 프로모션을 받을 수 있으며, 부정적인 응답을 한 고객은 고객 서비스 후속 조치를 보낼 수 있습니다. Experience Platform과의 이러한 통합을 통해 마케팅 팀은 고객 행동을 기반으로 보다 개인화되고 관련성 있는 콘텐츠를 제공할 수 있습니다.

### 활동 데이터를 기반으로 고객 타겟팅

마케팅 팀은 웹 사이트 방문, 양식 제출 또는 이전 이메일 캠페인과의 상호 작용과 같은 활동을 기반으로 고객을 타깃팅하려고 합니다. 이를 위해 활동 데이터 확장 을 만들어 각 고객의 참여 활동에 대한 정보를 저장합니다. 그런 다음 추가적인 세그멘테이션 및 개인화된 캠페인 타깃팅을 위해 이 데이터가 Experience Platform에 수집됩니다.

마케팅 팀은 활동 데이터 확장의 데이터를 Experience Platform에 수집함으로써 고객의 참여 내역을 기반으로 고객을 세그먼트화할 수 있습니다. 예를 들어 최근에 웹 사이트를 방문했지만 구매를 완료하지 않은 고객은 특별 오퍼가 포함된 미리 알림 이메일을 보낼 수 있습니다. 마찬가지로 양식을 작성한 고객은 개인화된 후속 커뮤니케이션을 받을 수 있습니다. 이 접근 방식을 사용하면 각 고객이 최신 활동을 기반으로 관련 콘텐츠를 수령하여 참여도와 전환율을 향상시킬 수 있습니다.

## 전제 조건 {#prerequisites}

소스를 Experience Platform에 연결하기 전에 완료해야 하는 필수 구성 요소 설정에 대해서는 아래 섹션을 참조하십시오.

### 인증을 위한 애플리케이션 설정 {#set-up-application-for-authentication}

[!DNL Salesforce Marketing Cloud]과(와) 통합을 빌드할 때 첫 번째 단계 중 하나는 **내에**&#x200B;설치된 패키지[!DNL Salesforce Marketing Cloud]를 만드는 것입니다. 설치된 패키지는 API 호출을 인증하는 데 필요한 클라이언트 자격 증명을 생성하고 통합 유형 및 관련 권한 범위를 정의합니다. 또한 설치된 패키지는 테넌트에 올바른 API 끝점을 제공합니다. 또한 액세스 관리, 모니터링 및 취소를 위한 관리 컨테이너 역할을 하므로 모든 통합이 안전하고 감사할 수 있으며 Salesforce의 권장 인증 모델과 일치하도록 합니다.

설치된 패키지를 만들려면 [!DNL Salesforce Marketing Cloud] UI를 사용하고 **[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]**(으)로 이동한 다음 **[!DNL New]**&#x200B;을(를) 선택합니다. [!DNL New Package Details] 인터페이스를 사용하여 패키지의 이름과 정보를 제공하십시오. 완료되면 **[!DNL Save]**&#x200B;을(를) 선택합니다.

![Salesforce Marketing Cloud UI의 새 패키지 인터페이스입니다.](../../images/tutorials/create/sfmc/new-package.png)

새 패키지가 만들어지면 **[!DNL Add Component]**&#x200B;을(를) 선택합니다.

![Salesforce Marketing Cloud UI의 구성 요소 추가 인터페이스](../../images/tutorials/create/sfmc/add-component.png)

구성 요소 유형으로 **[!DNL API Integration]**&#x200B;을(를) 선택하십시오.

![&quot;API 통합&quot;이 있는 구성 요소 선택 창이 선택되었습니다.](../../images/tutorials/create/sfmc/api-integration.png)

**[!DNL Server-to-Server]**&#x200B;을(를) 통합 유형으로 선택하십시오.

![통합 유형 선택 창](../../images/tutorials/create/sfmc/server-to-server.png)

마지막으로 **[!DNL Scope]** > **[!DNL Data]**(으)로 이동합니다. **[!DNL Data Extensions]**&#x200B;에서 **[!DNL Read]**&#x200B;을(를) 선택합니다.

![Salesforce 마케팅 범위의 데이터 확장 섹션](../../images/tutorials/create/sfmc/data-extensions.png)

**[!DNL Save]**&#x200B;을(를) 선택한 다음 **클라이언트 암호**&#x200B;를 복사하여 저장합니다. 완료되면 **[!DNL Finish]**&#x200B;을(를) 선택합니다.

![클라이언트 암호를 생성하기 위한 Salesforce Marketing Cloud 창입니다.](../../images/tutorials/create/sfmc/generate-secret.png)

[!DNL Salesforce Marketing Cloud] UI를 종료하기 전에 **클라이언트 ID** 및 **고유한 기본 URI 접두사**&#x200B;를 복사하십시오. 두 값을 모두 사용하여 Experience Platform에 대한 연결을 만들 수 있습니다. 인증 기본 URI의 경우 `.auth.marketingcloudapis.com/` 이후에 모든 항목을 제거했는지 확인하십시오.

![클라이언트 ID와 고유한 기본 URI를 검색할 수 있는 Salesforce Marketing Cloud 구성 요소 인터페이스입니다.](../../images/tutorials/create/sfmc/client-id-and-uri.png)

설치된 패키지를 만드는 자세한 단계는 [[!DNL Salesforce] 설명서](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment)를 참조하세요.

### 필요한 자격 증명 수집 {#gather-required-credentials}

[!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 클라이언트 ID | Experience Platform 인증 시 계정을 식별하기 위해 [!DNL Salesforce Marketing Cloud]에서 사용하는 공개적으로 노출된 식별자입니다. 클라이언트 ID는 [!DNL Salesforce Marketing Cloud] UI의 구성 요소 패널에서 검색할 수 있습니다. |
| 클라이언트 암호 | 클라이언트 응용 프로그램 및 인증 서버에만 알려진 비밀 키입니다. 위에 설명된 [응용 프로그램 설정 단계](#set-up-application-for-authentication)에 따라 클라이언트 암호를 생성할 수 있습니다. |
| 기본 엔드포인트 | [!DNL Salesforce Marketing Cloud]에 대한 인증 기본 URI의 접두사입니다. |

{style="table-layout:auto"}

## Experience Platform에 [!DNL Salesforce Marketing Cloud] 연결

Experience Platform 내에서 [!DNL Salesforce Marketing Cloud] 소스 연결을 구성하십시오. UI를 통해 연결을 설정하는 방법에 대한 단계별 안내서는 [튜토리얼 여기](../../tutorials/ui/create/marketing-automation/sfmc.md)를 참조하십시오. 이 튜토리얼을 참조하여 [!DNL Salesforce Marketing Cloud] 계정 연결, 데이터 선택, 필드 매핑, 수집 예약 및 데이터 흐름 모니터링에 대해 알아보십시오.
