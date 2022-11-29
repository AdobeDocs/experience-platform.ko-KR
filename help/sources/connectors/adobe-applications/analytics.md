---
keywords: Experience Platform;홈;인기 항목;Analytics 소스 커넥터;분석;Analytics;AAID;
title: 보고서 세트 데이터용 Adobe Analytics 소스 커넥터
description: 이 문서에서는 Analytics에 대한 개요를 제공하며 Analytics 데이터의 사용 사례를 설명합니다.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: d94bbbd34b116f10098624d565c1ae285fc0461e
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 7%

---

# 보고서 세트 데이터용 Adobe Analytics 소스 커넥터

Adobe Experience Platform에서는 Analytics 소스 커넥터를 통해 Adobe Analytics 데이터를 수집할 수 있습니다. 다음 [!DNL Analytics] 소스 커넥터는 [!DNL Analytics] 를 실시간으로 플랫폼으로 변환하여 SCDS 포맷 변환 [!DNL Analytics] 데이터를에 [!DNL Experience Data Model] (XDM) 플랫폼별 소비 필드입니다.

이 문서에서는 [!DNL Analytics] 및에 대한 사용 사례에 대해 설명합니다. [!DNL Analytics] 데이터.

## Adobe Analytics 및 Analytics 데이터

[!DNL Analytics] 는 고객에 대해 자세히 알아보고 고객이 웹 자산과 상호 작용하는 방법, 디지털 마케팅 비용이 효과적인 위치를 확인하고 개선 영역을 식별하는 데 도움이 되는 강력한 엔진입니다. [!DNL Analytics] 매년 수 많은 웹 트랜잭션을 처리하고 [!DNL Analytics] 소스 커넥터를 사용하면 다양한 행동 데이터를 손쉽게 탭하고 [!DNL Real-time Customer Profile] 몇 분 안에

![](./images/analytics-data-experience-platform.png)

높은 수준에서 [!DNL Analytics] 전 세계의 다양한 디지털 채널 및 여러 데이터 센터에서 데이터를 수집합니다. 데이터가 수집되면 들어오는 데이터를 형성하기 위해 방문자 식별, 세그먼테이션 및 변환 아키텍처(VISTA) 규칙 및 처리 규칙이 적용됩니다. 원시 데이터가 이러한 경량 처리를 거친 후에는 다음을 소비할 준비가 된 것으로 간주됩니다 [!DNL Real-time Customer Profile]. 위에서 언급한 것과 동일한 프로세스에서 동일한 처리된 데이터는 마이크로 일괄 처리되어 다음을 소비하기 위해 플랫폼 데이터 세트에 수집됩니다 [!DNL Data Science Workspace], [!DNL Query Service], 및 기타 데이터 검색 애플리케이션

자세한 내용은 [처리 규칙 개요](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) 를 참조하십시오.

## XDM(경험 데이터 모델)

XDM은 Experience Platform 시 서비스와 통신하는 데 사용할 응용 프로그램에 대한 공통 구조 및 정의를 제공하는 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 균일하게 통합할 수 있으므로 데이터를 보다 쉽게 전달하고 정보를 수집할 수 있습니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../../xdm/home.md).

## Adobe Analytics에서 XDM으로 필드를 매핑하려면 어떻게 해야 합니까?

가져오도록 소스 연결이 설정된 경우 [!DNL Analytics] 플랫폼 사용자 인터페이스를 사용하여 데이터를 Experience Platform에 매핑하고 데이터 필드를 자동으로 [!DNL Real-time Customer Profile] 몇 분 안에 소스 연결을 만드는 방법에 대한 지침은 [!DNL Analytics] 플랫폼 UI를 사용하여 다음을 참조하십시오. [Analytics 소스 커넥터 자습서](../../tutorials/ui/create/adobe-applications/analytics.md).

사이에 발생하는 필드 매핑에 대한 자세한 정보 [!DNL Analytics] 및 Experience Platform은 [Adobe Analytics 필드 매핑](./mapping/analytics.md) 안내서.

## 플랫폼에서 Analytics 데이터의 예상 대기 시간은 어떻게 됩니까?

플랫폼의 분석 데이터에 대한 예상 대기 시간은 아래 표에 요약되어 있습니다. 지연은 고객 구성, 데이터 볼륨 및 소비자 애플리케이션에 따라 달라집니다. 예를 들어, Analytics 구현이 `A4T` 파이프라인에 대한 지연 시간은 5~10분으로 늘어납니다.

| 분석 데이터 | 예상 지연 |
| -------------- | ---------------- |
| 새 데이터를에 [!DNL Real-time Customer Profile] (A4T **not** enabled) | &lt; 2분 |
| 새 데이터를에 [!DNL Real-time Customer Profile] (A4T **is** enabled) | &lt; 15분 |
| Data Lake의 새로운 데이터 | &lt; 90분 |
| 100억 개 미만의 이벤트 채우기 | &lt; 4주 |

Analytics 채우기 작업은 기본적으로 13개월로 채워집니다. 위의 표에 언급된 100억 개의 이벤트 제한은 예상 지연에 대해 엄격히 적용됩니다.

>[!NOTE]
>
>Analytics 채우기 데이터는 수집되지 않습니다. [!DNL Profile] 따라서 라이센스 프로필에서는 를 고려하지 않습니다.

## 의 기본 식별자 [!DNL Analytics] 데이터

의 모든 히트 [!DNL Analytics] 소스 커넥터에는 ECID 또는 AAID가 있는지 여부에 따라 달라지는 기본 식별자가 포함되어 있습니다. ECID가 있는 경우 ECID가 기본 식별자로 지정됩니다. AAID가 있는 경우, AAID가 기본 AID로 지정됩니다.

다음 표는 페이지의 ID 필드에 대한 자세한 정보를 제공합니다. [!DNL Analytics] 데이터.

| ID 필드 | 설명 |
| --- | --- |
| AAID | AAID는 Adobe Analytics의 기본 장치 식별자이며, 를 통해 전달되는 모든 이벤트에 계속 존재할 수 있습니다 [!DNL Analytics] 소스. AAID는 때로 *기존 Analytics ID* 또는 `s_vi` 쿠키 ID. 그럼에도 불구하고, `s_vi` 쿠키가 없습니다. AAID는 `post_visid_high` 및 `post_visid_low` 열 [[!DNL Analytics] 데이터 피드](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 제공된 이벤트에서 AAID 필드에는 단일 ID가 포함되어 있습니다. ID는 [작업 순서 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **참고**: 전체 보고서 세트 내에서 AAID에는 여러 이벤트 간에 유형이 혼합되어 있을 수 있습니다. |
| ECID | ECID(Experience Cloud ID)는 Adobe Analytics에서 채워지는 별도의 장치 식별자 필드입니다 [!DNL Analytics] 는 Experience Cloud ID 서비스를 사용하여 구현됩니다. ECID를 MCID(Marketing Cloud ID)라고도 합니다. 이벤트에 ECID가 존재하는 경우 AAID는 Analytics가 있는지에 따라 ECID를 기반으로 할 수 있습니다 [유예 기간](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) 가 구성되어 있습니다. ECID는 `mcvisid` Analytics 데이터 피드에서 참조할 수 있습니다. ECID에 대한 자세한 내용은 [ECID 개요](../../../identity-service/ecid.md). ECID가 작동하는 방식에 대한 자세한 정보 [!DNL Analytics]에서 문서를 참조하십시오. [Analytics 및 Experience Cloud ID 요청](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=ko-kr). |
| AACUSTOMID | AACUCUSTOMER ID는 페이지의 `s.VisitorID` 변수를으로 지정합니다. [!DNL Analytics] 구현 을 참조하십시오. AACUCUSTOMERid는 `cust_visid` 열 [[!DNL Analytics] 데이터 피드](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). AACUCUSTOMER id가 있는 경우 AAID는 AACUCUSTOMER id가 [작업 순서 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### 방법 [!DNL Analytics] 소스 ID 처리

다음 [!DNL Analytics] 소스는 이러한 ID를 다음과 같이 XDM 양식의 Experience Platform에 전달합니다.

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

이들 필드는 ID로 표시되지 않습니다. 대신 동일한 ID가 XDM의 `identityMap` 키 값 쌍으로:

* `{ “key”: “AAID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “ECID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “AACUSTOMID”, “value”: [ { “id”: “<identity>”, “primary”: false } ] }`

ID 맵에서 ECID가 있으면 이벤트의 기본 ID로 표시됩니다. 이 경우 AAID는 [ID 서비스 유예 기간](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). 그렇지 않으면 AAID가 이벤트의 기본 ID로 표시됩니다. AACUSTOMID는 이벤트의 기본 ID로 표시되지 않습니다. 그러나 AACUSTOMID가 있는 경우 작업의 Experience Cloud 순서 때문에 AAID는 AACUSTOMID를 기반으로 합니다.