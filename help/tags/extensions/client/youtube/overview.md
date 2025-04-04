---
title: YouTube 비디오 추적 확장 개요
description: Adobe Experience Platform의 YouTube 비디오 추적 태그 확장에 대해 알아봅니다.
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 35%

---

# YouTube 비디오 추적 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

**전제 조건**

Adobe Experience Platform의 각 태그 속성을 사용하려면 확장 화면에서 다음 확장을 설치하고 구성해야 합니다.

* Adobe Analytics
* Experience Cloud Visitor ID 서비스
* 코어 확장

비디오 플레이어를 렌더링할 각 웹 페이지의 HTML에 있는 Google 개발자 문서에서 \&lt;iframe\> 태그&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) 코드 조각을 사용하여 [&quot;플레이어 포함&quot;을 사용하십시오.

이 확장 버전 2.0.1은 iframe 스크립트 태그에 고유한 값이 있는 `id` 특성을 삽입하고 아직 포함되지 않은 경우 `src` 특성 값의 끝에 `enablejsapi=1` 및 `rel=0`을(를) 추가하여 단일 웹 페이지에 하나 이상의 YouTube 비디오를 포함하도록 지원합니다. 예:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

또한 이 확장은 `enablejsapi` 및 `rel` 쿼리 문자열 매개 변수의 존재 여부 및 예상 값이 올바른지 여부에 관계없이 `player1`과(와) 같은 고유한 ID 특성 값을 동적으로 확인하도록 설계되었습니다. 따라서 `id` 특성을 사용하거나 사용하지 않고 `enablejsapi` 및 `rel` 쿼리 문자열 매개 변수의 포함 여부에 관계없이 YouTube 스크립트 태그를 웹 페이지에 추가할 수 있습니다.

>[!NOTE]
>
>둘 이상의 비디오가 있는 페이지의 경우 각 비디오는 해당 페이지에서 실행되는 태그 규칙에 동일한 구성 세트를 사용합니다. 예를 들어, 비디오 50%에서 완료되는 이벤트를 트리거하는 규칙을 만드는 경우 페이지의 각 비디오가 50% 큐 포인트에서 규칙을 트리거합니다.

확장은 다음 논리를 사용하여 iFrame을 다시 작성합니다.

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

따라서 페이지가 로드된 후 약간 깜박임이 발생합니다. 이 동작은 예상되었습니다.

## 데이터 요소

확장에는 6개의 데이터 요소가 있으며 그 중 어느 것도 구성을 필요로 하지 않습니다.

* **재생 헤드 위치:** 태그 규칙 내에서 호출될 때 비디오 타임라인에서 재생 헤드 위치의 위치를 초 단위로 기록합니다.
* **비디오 ID:** 비디오와 연결된 YouTube ID를 지정합니다.
* **비디오 이름:** 비디오의 설명적이거나 친숙한 이름을 지정합니다.
* **비디오 URL:** 현재 로드되거나 재생되는 비디오에 대한 YouTube.com URL을 반환합니다.
* **비디오 지속 시간:** 비디오 컨텐츠의 총 지속 시간을 초 단위로 기록합니다.
* **확장 버전:** 이 데이터 요소는 &quot;Video Tracking_YouTube_2.0.0&quot;과 같은 YouTube 추적 확장 버전을 기록합니다.

## 이벤트

확장에는 8개의 이벤트를 사용할 수 있으며, 사용자 지정 큐 포인트 추적에만 구성이 필요합니다.

* **비디오 준비:** 비디오가 시작될 때 트리거되며 재생할 준비가 되었습니다.
* **비디오 시작:** 비디오가 처음 시작될 때와 `player.getCurrentTime() === 0`의 경우 트리거됩니다.
* **비디오 재생:** 비디오가 시작될 때 트리거되고 초기 시작 후 재생됩니다. 이 트리거는 재생 때마다 실행됩니다.
* **비디오 일시 중지:** 비디오가 일시 중지되면 트리거됩니다.
* **비디오 다시 시작:** 비디오가 다시 시작될 때와 `player.getCurrentTime() !== 0`의 경우 트리거됩니다.
* **사용자 지정 큐 추적:** 비디오가 지정된 비디오 임계값 비율에 도달하면 트리거됩니다. 예를 들어 비디오가 60초이고 지정된 큐 포인트가 50%인 경우 재생 헤드 위치가 30초일 때 이벤트가 트리거됩니다. 큐 포인트 추적은 초기 재생과 재생 모두에 적용됩니다. 사용자가 큐 포인트를 검색하는 경우 이벤트가 실행되지 않습니다. 큐 포인트 이벤트는 재생 헤드가 타임라인에서 계산된 큐 포인트 위치를 교차하고 비디오 플레이어가 재생되는 경우에만 발생합니다.
* **비디오 버퍼:** 플레이어가 비디오 재생을 시작하기 전에 일정 양의 데이터를 다운로드하는 경우 트리거됩니다.
* **비디오 종료:** 비디오가 완전히 완료되는 경우 트리거됩니다.

## 사용

각 비디오 이벤트(위에 나열된 7개 이벤트)에 대해 하나의 태그 규칙을 설정할 수 있습니다. 추적할 각 이벤트에 대한 특정 태그 규칙을 만듭니다. 이벤트를 추적하지 않으려면 를 생략하여 규칙을 만듭니다.

규칙에는 다음의 세 가지 작업이 있습니다.

* **변수 설정:** Adobe Analytics 변수를 설정합니다(일부 포함 데이터 요소에 매핑).
* **비콘 보내기:** Adobe Analytics 비콘을 사용자 지정 링크 추적 호출로 보내고 &quot;링크 이름&quot; 값을 제공하십시오.
* **변수 지우기:** Adobe Analytics 변수를 지웁니다.

## &quot;비디오 시작&quot;에 대한 태그 규칙 예

다음 비디오 확장 개체가 포함될 예정입니다.

* **이벤트**: &quot;비디오 시작&quot;(이 이벤트는 방문자가 YouTube 비디오를 재생하기 시작할 때 규칙이 실행됩니다.)

* **조건**: 없음

* **작업**: **Analytics 확장**&#x200B;을 사용하여 &quot;변수 설정&quot; 작업을 매핑합니다.

   * 비디오 시작 이벤트,
   * 비디오 지속 시간 데이터 요소에 대한 prop/eVar
   * 비디오 ID 데이터 요소에 대한 prop/eVar
   * 비디오 이름 데이터 요소에 대한 prop/eVar
   * 비디오 URL 데이터 요소에 대한 prop/eVar

  그런 다음 링크 이름이 &quot;비디오 시작&quot;인 &quot;비콘 보내기&quot; 작업(`s.tl`) 다음에 &quot;변수 지우기&quot; 작업을 포함합니다.

>[!TIP]
> 
>각 비디오 요소에 대해 여러 개의 eVar 또는 prop을 사용할 수 없는 구현의 경우, 데이터 요소 값을 Experience Platform 내에서 연결하고, 분류 규칙 빌더 도구를 사용하여 분류 보고서로 구문 분석한 다음, [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html)에 설명된 대로 Analysis Workspace에서 세그먼트로 적용할 수 있습니다.

비디오 정보 값을 연결하려면 &quot;비디오 메타데이터&quot;라는 새 데이터 요소를 만들고 이를 프로그래밍하여 모든 비디오 데이터 요소(위에 나열됨)를 가져와서 함께 조합합니다. 예:

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```

Experience Platform 내에서 데이터 요소를 효과적으로 만들고 활용하는 방법에 대한 자세한 내용은 [데이터 요소](../../../ui/managing-resources/data-elements.md) 설명서를 참조하십시오.
