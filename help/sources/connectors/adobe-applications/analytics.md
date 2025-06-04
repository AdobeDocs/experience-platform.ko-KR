---
title: 보고서 세트 데이터용 Adobe Analytics Source 커넥터
description: 이 문서에서는 Analytics에 대한 개요를 제공하고 Analytics 데이터의 사용 사례를 설명합니다.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 816c41613844e0d2b53003bc865f1996a86297c6
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 0%

---

# 보고서 세트 데이터용 Adobe Analytics 소스 커넥터

Adobe Experience Platform을 사용하면 Analytics 소스 커넥터를 통해 Adobe Analytics 데이터를 수집할 수 있습니다. [!DNL Analytics] 원본 커넥터는 [!DNL Analytics]에서 수집한 데이터를 실시간으로 Experience Platform으로 스트리밍하여 SCDS 형식의 [!DNL Analytics] 데이터를 Experience Platform에서 사용할 수 있도록 [!DNL Experience Data Model]&#x200B;(XDM) 필드로 변환합니다.

이 문서에서는 [!DNL Analytics]에 대한 개요를 제공하고 [!DNL Analytics] 데이터의 사용 사례를 설명합니다.

## Adobe Analytics 및 Analytics 데이터

[!DNL Analytics]은(는) 고객에 대해 자세히 알아보고, 고객이 웹 속성과 상호 작용하는 방법을 알아보고, 디지털 마케팅 지출이 효과적인 위치를 확인하고, 개선 가능한 영역을 식별하는 데 도움이 되는 강력한 엔진입니다. [!DNL Analytics]이(가) 연간 수조 개의 웹 트랜잭션을 처리하며 [!DNL Analytics] 소스 커넥터를 사용하면 이러한 풍부한 동작 데이터를 손쉽게 활용하여 몇 분 안에 [!DNL Real-Time Customer Profile]을(를) 보강할 수 있습니다.

![Adobe Analytics을 포함한 다양한 Adobe 응용 프로그램의 데이터 여정을 보여 주는 그래픽입니다.](./images/analytics-data-experience-platform.png)

[!DNL Analytics]은(는) 높은 수준에서 전 세계 다양한 디지털 채널과 여러 데이터 센터에서 데이터를 수집합니다. 데이터가 수집되면 방문자 식별, VISTA(세그먼테이션 및 변형 아키텍처) 규칙 및 처리 규칙이 적용되어 들어오는 데이터를 형성합니다. 원시 데이터가 이 간단한 처리를 거친 후 [!DNL Real-Time Customer Profile]에서 사용할 준비가 된 것으로 간주됩니다. 앞에서 설명한 것과 병행되는 프로세스에서, 동일한 처리된 데이터는 마이크로 일괄 처리되어 [!DNL Query Service] 및 기타 데이터 검색 응용 프로그램에서 사용할 수 있도록 Experience Platform 데이터 세트로 수집됩니다.

처리 규칙에 대한 자세한 내용은 [처리 규칙 개요](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html)를 참조하십시오.

## 경험 데이터 모델 (XDM)

XDM은 Experience Platform의 서비스와 통신하는 데 사용할 애플리케이션에 대한 일반적인 구조와 정의를 제공하는 공개적으로 문서화된 사양입니다.

XDM 표준을 준수하면 데이터를 균일하게 통합할 수 있으므로 데이터를 더 쉽게 전달하고 정보를 수집할 수 있습니다.

XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../../xdm/home.md)를 참조하십시오.

## 필드는 Adobe Analytics에서 XDM으로 어떻게 매핑됩니까?

>[!IMPORTANT]
>
>데이터 준비 변환은 전체 데이터 흐름에 지연을 추가할 수 있습니다. 추가되는 지연은 변환 로직의 복잡성에 따라 달라집니다.

Experience Platform 사용자 인터페이스를 사용하여 [!DNL Analytics] 데이터를 Experience Platform으로 가져오기 위해 소스 연결이 설정되면 데이터 필드가 자동으로 매핑되고 분 내에 [!DNL Real-Time Customer Profile]에 수집됩니다. Experience Platform UI를 사용하여 [!DNL Analytics]과(와)의 소스 연결을 만드는 방법에 대한 지침은 [Analytics 소스 커넥터 자습서](../../tutorials/ui/create/adobe-applications/analytics.md)를 참조하십시오.

[!DNL Analytics]과(와) Experience Platform 간에 발생하는 필드 매핑에 대한 자세한 내용은 [Adobe Analytics 필드 매핑](./mapping/analytics.md) 안내서를 참조하십시오.

## Experience Platform에서 Analytics 데이터의 예상 대기 시간은 어떻게 됩니까?

Experience Platform의 Analytics 데이터에 대한 예상 대기 시간은 아래 표에 요약되어 있습니다. 지연은 고객 구성, 데이터 볼륨 및 소비자 애플리케이션에 따라 달라집니다. 예를 들어 Analytics 구현이 `A4T`(으)로 구성된 경우 파이프라인 지연 시간은 5~10분으로 늘어납니다.

| Analytics 데이터 | 예상 대기 시간 |
| -------------- | ---------------- |
| [!DNL Real-Time Customer Profile]에 대한 새 데이터(A4T **not** 사용) | 2분 미만 |
| [!DNL Real-Time Customer Profile]에 대한 새 데이터(A4T **is** 사용) | 최대 30분 |
| 데이터 레이크에 새 데이터 추가 | &lt; 2.25시간 |
| [결합](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) 없이 Customer Journey Analytics에 새 데이터 보내기 | &lt; 3.75시간 |
| Customer Journey Analytics에 대한 새로운 데이터 결합 | 7시간 미만 |
| 100억 개 미만의 이벤트 채우기 | &lt; 4주 |

Customer Journey Analytics 지연에 대한 자세한 내용은 [Customer Journey Analytics 보호](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en)를 참조하십시오.

프로덕션 샌드박스에 대한 Analytics 채우기는 기본적으로 13개월로 설정됩니다. 비프로덕션 샌드박스의 Analytics 데이터의 경우 채우기는 3개월로 설정됩니다. 위 표에 언급된 100억 개의 이벤트 제한은 예상되는 지연과 관련하여 엄격히 제한됩니다.

프로덕션 샌드박스의 경우 13개월 이상의 내역 채우기 데이터를 가져올 수 있는 추가 SKU에 라이선스를 부여한 경우 Adobe에 연락하여 확장된 채우기를 요청하십시오.

프로덕션 샌드박스에서 Analytics 소스 데이터 흐름을 만들면 두 개의 데이터 흐름이 만들어집니다.

* 내역 보고서 세트 데이터를 데이터 레이크로 13개월 채우도록 하는 데이터 흐름입니다. 이 데이터 흐름은 채우기가 완료되면 종료됩니다.
* 라이브 데이터를 데이터 레이크와 [!DNL Real-Time Customer Profile]&#x200B;(으)로 전송하는 데이터 흐름. 이 데이터 흐름은 지속적으로 실행됩니다.

>[!NOTE]
>
>Analytics 채우기 데이터는 [!DNL Profile]에 수집되지 않으므로 라이선스 프로필에서 설명되지 않습니다.

## [!DNL Analytics] 데이터의 기본 식별자

[!DNL Analytics] 원본 커넥터의 모든 히트에는 ECID 또는 AAID의 존재 여부에 따라 달라지는 기본 식별자가 포함되어 있습니다. ECID가 있으면 ECID가 기본 식별자로 지정됩니다. AAID가 있는 경우 AAID가 기본 AAID로 지정됩니다.

다음 표에서는 [!DNL Analytics] 데이터의 ID 필드에 대한 자세한 정보를 제공합니다.

| ID 필드 | 설명 |
| --- | --- |
| AAID | AAID는 Adobe Analytics의 기본 장치 식별자이며 [!DNL Analytics] 원본을 통해 전달되는 모든 이벤트에 존재할 수 있습니다. AAID를 *기존 Analytics ID* 또는 `s_vi` 쿠키 ID라고도 합니다. 그럼에도 불구하고 AAID는 `s_vi` 쿠키가 없는 경우에도 생성됩니다. AAID는 [[!DNL Analytics] 데이터 피드](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html)의 `post_visid_high` 및 `post_visid_low` 열에 표시됩니다. 특정 이벤트에서는 AAID 필드에 [ID ](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html)에 대한 작업 순서  [!DNL Analytics] 에 설명된 여러 다른 유형 중 하나일 수 있는 단일 ID가 포함됩니다. **참고**: 전체 보고서 세트 내에서 AAID에는 여러 이벤트에 걸쳐 혼합된 형식이 포함될 수 있습니다. |
| ECID | ECID(Experience Cloud ID)는 Experience Cloud ID 서비스를 사용하여 [!DNL Analytics]을(를) 구현할 때 Adobe Analytics에 채워지는 별도의 장치 식별자 필드입니다. ECID를 MCID(Marketing Cloud ID)라고도 합니다. 이벤트에 ECID가 존재하는 경우, AAID는 Analytics [유예 기간](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html)이 구성되었는지 여부에 따라 ECID에 기반할 수 있습니다. ECID는 Analytics 데이터 피드에서 `mcvisid`에 의해 표시됩니다. ECID에 대한 자세한 내용은 [ECID 개요](../../../identity-service/features/ecid.md)를 참조하십시오. ECID가 [!DNL Analytics]에서 작동하는 방법에 대한 자세한 내용은 [Analytics 및 Experience Cloud ID 요청](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html)에 대한 문서를 참조하십시오. |
| AACUSTOMID | AACUSTOMID는 [!DNL Analytics] 구현에서의 `s.VisitorID` 변수 사용에 따라 Adobe Analytics에 채워지는 별도의 식별자 필드입니다. AACUSTOMID는 [[!DNL Analytics] 데이터 피드](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html)의 `cust_visid` 열에 표시됩니다. AACUSTOMID가 있으면 AACUSTOMID가 [ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html)에 대한 작업 순서  [!DNL Analytics] 로 정의된 다른 모든 식별자를 우선하므로 AAID는 AACUSTOMID를 기반으로 합니다. |

### [!DNL Analytics] 원본에서 ID를 처리하는 방법

[!DNL Analytics] 원본은 다음과 같이 XDM 형식의 Experience Platform에 이러한 ID를 전달합니다.

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

이러한 필드는 ID로 표시되지 않습니다. 대신 동일한 ID(이벤트에 있는 경우)가 키-값 쌍으로 XDM의 `identityMap`에 복사됩니다.

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

ID 또는 ID가 `identityMap`에 복사되면 `endUserIDs._experience.mcid.namespace.code`도 같은 이벤트에 설정됩니다.

* AAID가 있으면 `endUserIDs._experience.aaid.namespace.code`이(가) &quot;AAID&quot;로 설정됩니다.
* ECID가 있으면 `endUserIDs._experience.mcid.namespace.code`이(가) &quot;ECID&quot;로 설정됩니다.
* AACUSTOMID가 있으면 `endUserIDs._experience.aacustomid.namespace.code`이(가) &quot;AACUSTOMID&quot;로 설정됩니다.

ID 맵에서 ECID가 있으면 이벤트의 기본 ID로 표시됩니다. 이 경우 [ID 서비스 유예 기간](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html)으로 인해 AAID는 ECID를 기반으로 할 수 있습니다. 그렇지 않으면 AAID가 이벤트의 기본 ID로 표시됩니다. AACUSTOMID는 이벤트의 기본 ID로 표시되지 않습니다. 그러나 AACUSTOMID가 있으면 Experience Cloud 작업 순서로 인해 AAID는 AACUSTOMID를 기반으로 합니다.

>[!NOTE]
>
>데이터 준비를 사용하여 AAID 및 AACUSTOMID와 같은 Analytics에서 발생하는 2차 ID를 필터링할 수 있습니다. 필터링되면 수신 Analytics 데이터에서 사용할 수 있는 경우 이러한 ID가 프로필에 수집되지 않습니다. 필터링되지 않은 데이터는 데이터 레이크로 계속 로드됩니다.
