---
title: 이벤트 전달 개요
description: 태그 구현을 변경하지 않고 Platform Edge Network를 사용하여 작업을 실행할 수 있는 Adobe Experience Platform의 이벤트 전달에 대해 알아보십시오.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 42%

---

# 이벤트 전달 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

Adobe Experience Platform의 이벤트 전달은 Adobe Experience Platform Edge Network를 사용하여 클라이언트에서 일반적으로 수행된 작업을 실행함으로써 웹 페이지 및 앱 가중치를 줄입니다. 이벤트 전달 규칙은 클라이언트측 구현을 변경하지 않고 데이터를 새로운 대상으로 변환하고 전송할 수 있습니다.

Adobe Experience Platform Web 및 Mobile SDK와 결합된 이벤트 전달을 통해 다음을 수행할 수 있습니다.

* 데이터 페이로드가 포함된 페이지에서 한 번 호출합니다. 그런 다음 데이터를 서버측을 병합하여 클라이언트측 네트워크 트래픽을 줄이고 고객을 위한 더 빠른 경험을 제공합니다.
* 웹 페이지를 로드하는 데 걸리는 시간을 줄여 사사이트가 성능에 대한 업계 모범 사례를 준수하게 됩니다.
* 투명도를 높이고 모든 태그 속성에서 전송되는 데이터 유형을 제어합니다.
* 이전에 추적한 데이터를 새 대상에 전송하는 이벤트 전달 규칙을 만듭니다.

## 향상된 성능

경쟁이 날로 치열해지는 환경에서 기업은 시장 점유율을 유지하고 확장하기 위해 성능을 가장 우선시해야 합니다. 이벤트 전달을 통해 모바일, IoT 및 OTT 장치 간의 웹 사이트 및 앱 성능이 향상됩니다. 더 빨라진 로드 시간 덕분에 웹 사이트 전환율이 증가하고,모바일 앱은 배터리를 빨리 소진하지 않으며 OTT 앱은 모바일 디바이스에서 실행되는 앱과 같은 속도로 반응합니다. 성능이 향상되면 전환율이 증가하는 것이 일반적입니다.

## 데이터 거버넌스 향상

기술 스택이 증가하고 데이터가 점점 더 많은 대상으로 전송됨에 따라 어떤 데이터를 어디로 전송할지 제어하는 것이 점점 더 어려워지고 있습니다. GDPR 및 CCPA와 같은 규정의 표준화는 기업이 점점 더 어려워지고 있는 데이터 문제에 대해 더 많은 통제력을 발휘하도록 하고 있습니다.

이벤트 전달을 통해 마케팅 팀은 데이터를 제어하면서 비즈니스를 성장시킵니다. 이를 통해 마케터가 타겟 시장에 진출하고 Adobe가 아닌 대상으로 데이터를 전송하는 데 필요한 클라이언트측 기술의 개수를 줄일 수 있습니다. 따라서 구현 팀이 클라이언트에서 다양한 대상으로 이동하는 데이터를 보다 쉽게 관리할 수 있습니다. 

## 이벤트 전달과 태그 간의 차이점

이벤트 전달과 태그 간의 다음 차이점을 참고하십시오.

* 데이터 요소 토큰화

   * 태그: 규칙에서 데이터 요소는 `%` at the first and end of the data element name. 예: `%viewportHeight%`.

   * 이벤트 전달: 규칙에서 데이터 요소는 `{{` 시작 및 `}}` at the end of the data element name. 예: `{{viewportHeight}}`.

* 데이터 참조 방법

   Edge 네트워크의 데이터를 참조하려면 데이터 요소 경로가 `arc.event._<element>_`여야 합니다.

   `arc`는 Adobe 응답 컨텍스트를 나타냅니다.

   예: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >이 경로를 잘못 지정하면 데이터가 수집되지 않습니다.


* 규칙 작업 순서

   규칙의 작업 섹션에서 이벤트 전달 규칙이 항상 순차적으로 실행됩니다. 규칙을 저장할 때 작업 순서가 올바른지 확인합니다. 이 실행 시퀀스는 태그를 사용할 때처럼 선택할 수 없습니다.

<!--doc Adobe Cloud Connector extension, get from Jon-->
