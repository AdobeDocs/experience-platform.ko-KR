---
title: 데이터 수집에서의 ID
description: 데이터 수집이 웹 구현 간에 ECID, 코어 ID, 자사 지속성 및 identityMap을 사용하는 방법에 대해 알아봅니다.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# 데이터 수집에서의 ID

Adobe 데이터 수집은 ID 신호를 사용하여 재방문자를 인식하고 경험을 통해 컨텍스트를 전달합니다. 방문자가 사이트에 도달하면 Edge Network은 ECID(Experience Cloud ID)를 생성하고 자사 쿠키에서 유지합니다. 해당 ECID는 Adobe Experience Cloud 애플리케이션에서 사용되는 기본 디바이스 식별자이며 분석, 개인화 및 대상자 활성화가 기반으로 하는 기반입니다. 구현에서는 [`getIdentity`](/help/collection/js/commands/getidentity.md) 명령을 통해 클라이언트측에서 방문자의 ECID에 액세스할 수 있습니다. 데이터 스트림 수준에서 [데이터 수집을 위한 데이터 준비](/help/datastreams/data-prep.md)를 사용하여 ECID가 다운스트림 서비스에 도달하기 전에 사용자 지정 XDM 필드에 매핑할 수 있습니다.

ECID는 개인이 아닌 장치를 식별합니다. 활동을 알려진 사용자에게 연결하기 위해 XDM [`identityMap`](./identity-map.md)을(를) 사용하여 ECID와 함께 CRM ID 또는 해시된 이메일과 같은 추가 식별자를 보낼 수 있습니다. Adobe에서는 사용 가능한 개인 수준 네임스페이스를 [기본 id](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map)(으)로 설정하는 것이 좋습니다.

데이터 수집은 기본 ECID 외에도 구현에 따라 추가 ID 신호를 지원합니다.

* **FPID(자사 디바이스 ID)**: 사용자가 제어하는 인프라에서 생성하고 관리하는 디바이스 식별자. Edge Network은 FPID를 사용하여 ECID를 [시드](./fpid.md)합니다. 이렇게 하면 브라우저 제한 사항으로 Adobe 관리 쿠키의 수명이 단축될 때 소유한 속성에 대한 쿠키 지속성이 강화됩니다.
* **코어 ID**: 서드파티 쿠키를 사용할 수 있을 때 서드파티 ID 워크플로에 참여하는 별도의 demdex 기반 식별자입니다. 코어 ID는 ECID와 다르며 [`getIdentity`](/help/collection/js/commands/getidentity.md)을(를) 통해 검색할 수 있습니다. 자사 및 타사 ID 컨텍스트가 함께 작동하는 방법에 대한 자세한 내용은 [통합 ID 지원](./unified-identity-support.md)을 참조하십시오.

방문자 API에서 업그레이드하거나 이전 ID 동작을 조정하는 경우 기존 AMCV 쿠키를 마이그레이션하려면 [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md)을(를) 참조하십시오.

## 자사 및 타사 컬렉션 {#first-party-and-third-party-collection}

웹 SDK은 데이터 수집 요청을 수신하는 끝점에 관계없이 항상 ID [쿠키](https://experienceleague.adobe.com/ko/docs/core-services/interface/data-collection/cookies/web-sdk)&#x200B;(예: `kndctr_` 쿠키)를 도메인의 자사 쿠키로 설정합니다. 수집 끝점(구현이 데이터를 보내는 도메인)은 브라우저와 네트워크 정책이 요청 자체를 처리하는 방식에 영향을 주는 별도의 선택입니다.

**자사 컬렉션**&#x200B;은(는) Adobe의 Edge Network을 가리키는 CNAME를 사용하여 조직이 제어하는 도메인(예: `data.example.com`)을 통해 데이터 수집 요청을 라우팅합니다. 요청이 도메인에 유지되므로 광고 차단기 또는 브라우저 네트워크 제한에 의해 차단될 가능성이 줄어듭니다. 또한 자사 수집은 자체 서버 인프라에서 [자사 장치 ID](./fpid.md)을(를) 설정하기 위한 전제 조건이며, 이는 가장 지속적인 ID 전략입니다. Adobe에서는 [Adobe 관리 인증서 프로그램](https://experienceleague.adobe.com/ko/docs/core-services/interface/data-collection/adobe-managed-cert)을 사용하여 구현에 대한 자사 컬렉션을 구성하는 것이 좋습니다.

**타사 컬렉션**&#x200B;에서 Adobe 소유 [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md)(예: `example.data.adobedc.net`)에 직접 요청을 보냅니다. ID 쿠키가 여전히 도메인에서 자사 쿠키로 설정되어 있는 동안 요청 자체는 서드파티 도메인으로 이동하며, 일부 브라우저 및 광고 차단기가 이를 제한할 수 있습니다.

## 올바른 ID 패턴 선택 {#choose-your-path}

* **소유한 속성에 대한 ID 지속성 강화**: 브라우저 제한 사항으로 인해 쿠키 수명이 단축되고 사용자가 제어하는 사이트에 대한 분석 및 개인화에 대해 더 강력한 연속성이 필요한 경우 [자사 장치 ID를 사용](./fpid.md)합니다.
* **앱에서 모바일 웹으로 ID 전달**: 방문자가 모바일 앱에서 시작하여 WebView 또는 모바일 웹 페이지에서 계속되는 경우 [모바일-웹 ID 공유](./mobile-to-web.md)를 사용합니다.
* **도메인 간에 ID 연속성을 유지하세요**: 방문자가 조직이 소유하는 웹 속성 간에 이동할 때 일관된 보고 및 개인화를 원할 경우 [도메인 간 공유](./cross-domain-sharing.md)를 사용합니다.
* **퍼스트 파티 지속성과 타사 활성화를 결합합니다**: 지원되는 타사 활성화 흐름과 함께 지속적인 자사 식별이 필요한 경우 [통합 ID 지원](./unified-identity-support.md)을 사용합니다.
* **개인 수준 식별자 보내기**: [`identityMap`](./identity-map.md)을(를) 사용하여 CRM ID, 해시된 전자 메일 및 기타 개인 수준 식별자를 ECID와 함께 전송하여 다운스트림 서비스가 활동을 알려진 사용자에게 연결할 수 있도록 합니다.
* **동의가 ID에 미치는 영향 이해**: [동의 및 ID](./consent.md)를 읽고 `defaultConsent` 및 `setConsent`이(가) ECID를 생성하고 쿠키를 설정하며 데이터를 전송할 때 제어하는 방법을 알아보세요.

방문자 인플레이션, ECID 불일치 또는 FPID 문제와 같은 ID 문제를 진단하는 데 도움이 필요하면 [ID 문제 해결](./troubleshooting.md)을 참조하십시오.
