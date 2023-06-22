---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform의 2023년 6월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a03d0eeab5ca42225705fdeab692020b1641395d
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 5%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2023년 6월 21일**

Adobe Experience Platform의 기존 기능 업데이트:

- [Experience Platform API 인증](#authentication-platform-apis)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [쿼리 서비스](#query-service)
- [소스](#sources)

## Experience Platform API 인증 {#authentication-platform-apis}

Experience Platform API 사용자의 경우, 이제 API 끝점을 인증하고 호출하는 데 필요한 액세스 토큰을 얻는 방법이 간소화되었습니다. 액세스 토큰을 얻는 JWT 방법은 더 이상 사용되지 않으며 더 간단한 OAuth 서버 간 인증 방법으로 대체됩니다.<p>![액세스 토큰을 강조 표시하는 새로운 OAuth 인증 방법입니다.](/help/landing/images/api-authentication/oauth-authentication-method.png "액세스 토큰을 강조 표시하는 새로운 OAuth 인증 방법입니다."){width="100" zoomable="yes"}</p>

JWT 인증 방법을 사용하는 기존 API 통합은 2025년 1월 1일까지 계속 작동하지만, Adobe은 해당 날짜 이전에 기존 통합을 새 OAuth 서버 간 수단으로 마이그레이션할 것을 강력히 권장합니다. 의 안내서 읽기 [서비스 계정(JWT) 자격 증명에서 OAuth 서버 간 자격 증명으로 마이그레이션](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

업데이트된 내용 읽기 [Experience Platform 인증 자습서](/help/landing/api-authentication.md) 추가 정보.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 제품군을 제공합니다.

**새 기능 또는 업데이트된 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| 확장 | [!DNL Google Cloud Platform] 이벤트 전달 확장 | 다음 [[!DNL Google Cloud Platform]](../../tags/extensions/server/google-cloud-platform/overview.md) 이벤트 전달 확장을 사용하면 를 통해 활성화를 위해 이벤트 데이터를 Google에 전달할 수 있습니다. [!DNL Google Pub/Sub]. |
| 확장 | [!DNL Cloud connector for Google Analytics 4 (ga4)] 확장 | 다음 [[!DNL Cloud connector for Google Analytics 4 (ga4)]](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.109820.html) 이벤트 전달 확장을 사용하면 를 통해 analytics를 추적할 수 있습니다 [!DNL Google Analytics 4 (ga4)] 표준. |
| 암호 | OAuth 2 JWT 암호 | 다음 [OAuth 2 JWT 암호](../../tags/ui/event-forwarding/secrets.md) 을(를) 통해 Adobe 및 [!DNL Google] 이벤트 전달에서 서버 간 상호 작용을 지원하는 서비스 토큰입니다. |
| 태그 및 이벤트 전달 | 사용자 속성 | 사용자 속성은 다음을 통해 주요 활동 데이터를 제공합니다 [태그](../../tags/home.md) 및 [이벤트 전달](../../tags/ui/event-forwarding/overview.md) UI.<br><br>데이터에는 누가 언제 어떤 변화를 주었는지 포함됩니다. 이 데이터는 다음 화면의 태그 및 이벤트 전달 UI에 표시됩니다.<br><ul><li> 속성 개요</li><li> 설치된 확장</li><li>규칙 비교 및 검토</li><li>데이터 요소 비교 검토</li><li>확장 비교 검토</li><li>라이브러리 리소스 변경 사항</li><li>라이브러리 마지막 빌드 및 게시됨</li></ul> |

{style="table-layout:auto"}

데이터 수집에 대해 자세히 알아보려면 [데이터 수집 개요](../../tags/home.md).

## 대상 {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상 또는 업데이트된 대상** {#new-updated-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [[!BADGE Beta]{type=Informative} [!DNL Amazon Ads] 연결](../../destinations/catalog/advertising/amazon-ads.md) | 다음 [!DNL Amazon Ads] Adobe Experience Platform과의 통합은 이제 다양한 항목에 대한 지역 라우팅을 지원합니다 [!DNL Amazon Ads] 마켓플레이스요 자세한 내용 [대상 변경 로그](../../destinations/catalog/advertising/amazon-ads.md#changelog). |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 에 대한 작업 공간 지원 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 대상. | 이제 새 Adobe Target 대상 연결을 구성할 때 대상을 공유할 Adobe Target 작업 영역을 선택할 수 있습니다. 다음을 참조하십시오. [연결 매개 변수](../../destinations/catalog/personalization/adobe-target-connection.md#parameters) 섹션에 자세히 설명되어 있습니다. 또한 다음에 대한 자습서를 참조하십시오. [작업 영역 구성](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=en) 작업 공간에 대한 자세한 내용은 Adobe Target을 참조하십시오. |

{style="table-layout:auto"}

<!--

**Fixes and enhancements** {#destinations-fixes-and-enhancements}

- Placeholder for fixes and enhancements

-->

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md).

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform 데이터 레이크의 데이터를 쿼리할 수 있습니다. 데이터 레이크에서 모든 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다. &#x200B;
**업데이트된 기능**
&#x200B; | 기능 | 설명 | | — | — | | &#x200B; 인라인 템플릿 | 이제 쿼리 서비스에서 SQL 내의 다른 템플릿을 참조하는 템플릿 사용을 지원합니다. 쿼리에서 인라인 템플릿을 활용하여 워크로드를 줄이고 오류를 방지합니다. 명령문이나 조건을 재사용하고 중첩된 템플릿을 참조하여 SQL의 유연성을 높일 수 있습니다. 템플릿으로 저장할 수 있는 쿼리 크기나 원래 쿼리에서 참조할 수 있는 템플릿 수에는 제한이 없습니다. 자세한 내용은 [인라인 템플릿 안내서](../../query-service/essential-concepts/inline-templates.md). | | 예약된 쿼리 UI 업데이트 | UI의 한 위치에서 모든 예약된 쿼리를 [[!UICONTROL 예약된 쿼리 탭]](../../query-service/ui/monitor-queries.md#inline-actions). 다음 [!UICONTROL 예약된 쿼리] 인라인 쿼리 작업과 새 쿼리 상태 열의 추가로 UI가 개선되었습니다. 최근 추가 기능에는 일정을 활성화, 비활성화 및 삭제하거나, 다음에서 바로 예정된 쿼리 실행에 대한 경고를 구독할 수 있는 기능이 포함됩니다. [!UICONTROL 예약된 쿼리] 보기. <p>![인라인 작업이에서 강조 표시됨 [!UICONTROL 예약된 쿼리] 보기.](../../query-service/images/ui/monitor-queries/disable-inline.png "인라인 작업이에서 강조 표시됨 [!UICONTROL 예약된 쿼리] 보기."){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}
쿼리 서비스에 대한 &#x200B; 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics 분류 소스 데이터 흐름 삭제 지원 | 이제 Adobe Analytics 분류를 소스로 사용하는 소스 데이터 흐름을 삭제할 수 있습니다. 아래 **[!UICONTROL 소스]** > **[!UICONTROL 데이터 흐름]**&#x200B;를 클릭하고 원하는 데이터 흐름을 선택한 다음 삭제를 선택합니다. 자세한 내용은 의 안내서를 참조하십시오. [Adobe Analytics 분류 데이터에 대한 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/classifications.md). |
| 필터링 지원 [!DNL Microsoft Dynamics] api 사용 | 논리 및 비교 연산자를 사용하여 [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) 소스. 자세한 내용은 의 안내서를 참조하십시오. [api를 사용하여 소스에 대한 데이터 필터링](../../sources/tutorials/api/filter.md). |
| [!BADGE 베타]{type=Informative}[!DNL RainFocus] | 이제 다음을 사용할 수 있습니다. [!DNL RainFocus] 소스 통합을 통해 다음에서 이벤트 관리 및 analytics 데이터 가져오기 [!DNL RainFocus] Experience Platform 계정. 자세한 내용은 [[!DNL RainFocus] 소스 개요](../../sources/connectors/analytics/rainfocus.md). |
| Adobe Commerce 지원 | 이제 Adobe Commerce 소스 통합을 사용하여 Adobe Commerce 계정의 데이터를 Experience Platform으로 가져올 수 있습니다. 자세한 내용은 [Adobe Commerce 소스 개요](../../sources/connectors/adobe-applications/commerce.md). |
| 지원 대상 [!DNL Mixpanel] | 이제 다음을 사용할 수 있습니다. [!DNL Mixpanel] 소스 통합을 통해 다음에서 analytics 데이터 가져오기 [!DNL Mixpanel] API 또는 Experience Platform 인터페이스를 사용하여 로그인할 계정입니다. 자세한 내용은 [[!DNL Mixpanel] 소스 개요](../../sources/connectors/analytics/mixpanel.md). |
| 지원 대상 [!DNL Zendesk] | 이제 다음을 사용할 수 있습니다. [!DNL Zendesk] 소스 통합을 통한 고객 성공 데이터 가져오기 [!DNL Zendesk] API 또는 Experience Platform 인터페이스를 사용하여 로그인할 계정입니다. 자세한 내용은 [[!DNL Zendesk] 소스 개요](../../sources/connectors/customer-success/zendesk.md). |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
