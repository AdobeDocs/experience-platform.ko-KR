---
title: BrightCove 비디오 추적 확장 개요
description: Adobe Experience Platform의 BrightCove 비디오 추적 태그 확장에 대해 알아봅니다.
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 35%

---

# BrightCove 비디오 추적 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

## 전제 조건

Adobe Experience Platform의 각 태그 속성에는 확장 화면에 다음과 같은 확장이 설치 및 구성되어 있어야 합니다.

* Adobe Analytics
* Experience Cloud Visitor ID 서비스
* 핵심 확장이 설치됨

비디오 플레이어를 렌더링할 각 웹 페이지의 HTML에 있는 &quot;In-Page embed code (Advanced)&quot; 코드 조각을 사용하십시오. &quot;In-Page Embed Code(Advanced)&quot; HTML 코드 조각은 [Brightcove 설명서](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage)에서 찾을 수 있습니다. 다음 링크에서는 [미리 보기와 게시된 비디오 플레이어 모두에 대해 포함된 코드를 생성하는 방법](https://studio.support.brightcove.com/players/generating-player-embed-code.html)에 대한 자세한 정보를 제공합니다.

이 확장 버전 1.1.0은 여러 개의 BrightCove 비디오를 단일 웹 페이지에 포함할 수 있습니다. 고급 포함 태그 내에 `id` 속성이 여러 개 있는 경우 각각 고유한 값이 있는지 확인하십시오. 예: `player1`, `player2` 등.

>[!NOTE]
>
>여러 비디오가 있는 페이지의 경우 각 비디오는 해당 페이지에서 실행되는 태그 규칙에 동일한 구성 세트를 사용합니다. 예를 들어, 50% 완료된 비디오에서 완료되는 이벤트를 트리거하는 규칙을 만드는 경우 페이지의 각 비디오가 50% 큐 포인트에서 규칙을 트리거합니다.

관련 스크립트가 완전히 로드되기 전에 비디오와 상호 작용하는 이 확장을 사용하는 웹 페이지에 두 가지 작업을 수행하여 문제를 해결할 수 있습니다. 먼저 태그 라이브러리를 동기식으로 로드할 수 있고, 두 번째로 페이지의 비디오 포함 앞에 `<script type="text/javascript">\_satellite.pageBottom();\</script\>` 요소를 배치합니다.

이 확장에서 사용되는 구성 요소 메서드 및 이벤트에 대한 자세한 내용은 [BrightCove API 설명서](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer)를 참조하십시오.

## 데이터 요소

확장에는 7개의 데이터 요소가 있으며 그 중 어느 것도 구성을 필요로 하지 않습니다.

* **재생 헤드 위치:** 태그 규칙 내에서 이 데이터 요소가 호출되면 비디오 타임라인에서 재생 헤드 위치의 위치를 초 단위로 기록합니다.
* **비디오 계정 ID:** 이 데이터 요소는 비디오를 게시한 Brightcove 계정의 ID를 기록합니다.
* **비디오 지속 시간:** 이 데이터 요소는 비디오 컨텐츠의 총 지속 시간을 초 단위로 기록합니다. 또한 Analytics 내에 계산된 지표를 만들어 초 단위의 숫자를 분 또는 시간으로 변환할 수 있습니다.
* **비디오 광고 지원:** 이 데이터 요소는 광고가 비디오 내에서 지원되는지 여부를 지정합니다.
* **비디오 ID:** 이 데이터 요소는 비디오와 연결된 BrightCove ID를 지정합니다.
* **비디오 이름:** 이 데이터 요소는 비디오의 설명적이거나 친숙한 이름을 지정합니다.
* **비디오 태그:** 이 데이터 요소는 비디오와 연결된 특정 스크립트를 지정합니다.

## 이벤트

확장에는 7개의 이벤트를 사용할 수 있으며, 사용자 지정 큐 포인트 추적에만 구성이 필요합니다.

* **사용자 지정 큐 포인트 추적:** 이 이벤트는 비디오가 지정된 비디오 임계값 비율에 도달하면 트리거됩니다. 예를 들어, 비디오의 길이가 60초이고 지정된 큐 포인트가 50%인 경우 이벤트가 30초 표시에서 트리거됩니다.

>[!NOTE]
>
>이 이벤트는 이 큐 포인트에 도달할 때마다 트리거됩니다. 예를 들어 사용자가 50% 표시에 도달하고 50% 표시 전에 비디오를 찾은 다음 50% 표시에 다시 도달하면 트리거가 다시 발생합니다.

* **비디오 완료:** 비디오가 완전히 완료되면 이 이벤트가 트리거됩니다.
* **비디오 로드된 메타데이터:** 플레이어가 초기 기간 및 차원 정보를 수신하면 이 이벤트가 실행됩니다.
* **비디오 일시 중지:** 이 이벤트는 비디오가 일시 중지되면 트리거됩니다.
* **비디오 다시 시작:** 이 이벤트는 일시 중지 이벤트 후에 비디오 컨텐츠가 다시 시작될 때 트리거됩니다.
* **비디오 화면 변경:** 비디오가 전체 화면 모드로 전환되거나 전체 화면 모드로 전환될 때 이벤트가 트리거됩니다.
* **비디오 시작:** 이 이벤트는 비디오 컨텐츠가 처음 시작될 때 트리거됩니다.

## 사용

각 비디오 이벤트(위에 나열된 7개 이벤트)에 대해 하나의 태그 규칙을 설정할 수 있습니다. 추적할 각 이벤트에 대한 특정 태그 규칙을 만듭니다. 이벤트를 추적하지 않으려면 를 생략하여 규칙을 만듭니다.

규칙에는 다음의 세 가지 작업이 있습니다.

1. Adobe Analytics 변수 설정. (위에 나열된 데이터 요소의 전체 또는 일부에 대한 데이터 요소를 만듭니다.)
1. Adobe Analytics 비콘 보내기.
1. Adobe Analytics 변수 지우기.

## &quot;비디오 시작&quot;에 대한 태그 규칙 예

다음 비디오 확장 개체가 포함될 예정입니다.

* **이벤트**

   1. &quot;비디오 시작&quot;: 이 이벤트는 방문자가 BrightCove 비디오를 재생하기 시작할 때 규칙이 실행됩니다.

* **조건**

   1. None

* **작업**

   1. Analytics &quot;변수 설정&quot; 작업에서 다음을 설정합니다.

      * **비디오 시작** 이벤트(예: event17)
      * **비디오 이름** 데이터 요소에 대한 prop/eVar(예: eVar10)
      * **비디오 지속 시간** 데이터 요소에 대한 prop/eVar(예: eVar11)
      * **현재 비디오 장소** 데이터 요소에 대한 prop/eVar(예: eVar12)

   1. Analytics &quot;비콘 전송&quot; 작업(`s.tl`)
   1. Analytics &quot;변수 지우기&quot; 작업

>[!TIP]
>
>각 비디오 요소에 대해 여러 개의 eVar 또는 prop을 제공하기를 원하지 않는 사용자의 경우, 데이터 요소 값이 대체 방법으로 연결됩니다. 그런 다음 분류 규칙 빌더 도구를 사용하여 분류 보고서로 구문 분석합니다. 자세한 내용은 [분류 규칙 빌더 도구](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=ko) 설명서를 참조하십시오. 마지막으로 Analysis Workspace에서 세그먼트로 적용됩니다.
>
>이렇게 하려면 &quot;비디오 메타데이터&quot;와 같은 새로운 데이터 요소를 만들고 이를 프로그래밍하여 모든 비디오 데이터 요소(위에 나열됨)를 가져와서 함께 연결합니다.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
