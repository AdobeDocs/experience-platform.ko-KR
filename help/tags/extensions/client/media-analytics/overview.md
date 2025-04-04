---
title: Adobe Media Analytics for Audio 및 Video 확장 개요
description: Adobe Experience Platform의 Adobe Media Analytics for Audio 및 Video 태그 확장 기능에 대해 알아봅니다.
exl-id: 426cfd08-aead-4b35-824c-45494bca2fc8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 81%

---

# Adobe Media Analytics for Audio 및 Video 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Adobe Media Analytics for Audio 및 Video 확장(Media Analytics 확장) 설치, 구성 및 구현 관련 정보에 대해서는 이 설명서를 참조합니다. 예제 및 샘플 링크와 함께 이 확장을 사용하여 규칙을 만들 때 사용할 수 있는 옵션이 포함되어 있습니다.

MA(Media Analytics) 확장은 Core JavaScript Media SDK(Media 2.x SDK)를 추가합니다. 이 확장은 태그 사이트 또는 프로젝트에 `MediaHeartbeat` 추적기 인스턴스를 추가하는 기능을 제공합니다. MA 확장을 사용하려면 다음 두 개의 확장이 추가로 필요합니다.

* [Analytics 확장](../analytics/overview.md)
* [Experience Cloud ID 확장](../id-service/overview.md)

>[!IMPORTANT]
>
> 오디오 추적을 사용하려면 Analytics 확장 v1.6 이상이 필요합니다.

태그 프로젝트에서 위에 언급된 확장 세 개를 모두 포함했으면 다음 두 가지 방법 중 하나를 사용하여 진행할 수 있습니다.

* 웹 앱의 `MediaHeartbeat` API 사용
* 특정 미디어 플레이어 이벤트를 `MediaHeartbeat` 추적기 인스턴스의 API에 매핑하는 플레이어 전용 확장을 포함하거나 빌드합니다. 이 인스턴스는 MA 확장을 통해 노출됩니다.

## MA 확장 설치 및 구성

* **설치 -** MA 확장을 설치하려면 확장 속성을 열고 **[!UICONTROL 확장 > 카탈로그]**&#x200B;를 선택하고 **[!UICONTROL 오디오 및 비디오용 Adobe Media Analytics]** 확장을 마우스로 가리킨 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

* **구성 -** MA 확장을 구성하려면 [!UICONTROL 확장] 탭을 열고 확장을 마우스로 가리킨 다음 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![MA 확장 구성](../../../images/ext-va-config.jpg)

### 구성 옵션:

| 옵션 | 설명 |
| :--- | :--- |
| Tracking Server | 미디어 하트비트를 추적할 서버 정의(Analytics 추적 서버와 동일한 서버 아님) |
| Application Version | 미디어 플레이어 앱/SDK의 버전 |
| Player Name | 사용 중인 미디어 플레이어의 이름(예: &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Channel | 채널 이름 속성입니다. |
| Online Video Provider | 콘텐츠가 배포되는 온라인 비디오 플랫폼의 이름입니다 |
| Debug Logging | 로깅 활성화 또는 비활성화 |
| Enable SSL | HTTPS를 통해 Ping 전송 활성화 또는 비활성화 |
| Export APIs to Window Object | 글로벌 범위로 Media Analytics API 내보내기 활성화 또는 비활성화 |
| Variable Name | `window` 개체 아래로 Media Analytics API를 내보내는 데 사용하는 변수 |

**미리 알림:** MA 확장 프로그램을 사용하려면 [Analytics](../analytics/overview.md) 및 [Experience Cloud ID](../id-service/overview.md) 확장 프로그램이 필요합니다. 확장 속성에 이러한 확장을 추가하고 구성해야 합니다.

## MA 확장 사용

### 웹 페이지/JS 앱에서 사용

MA 확장은 [!UICONTROL 구성] 페이지에서 &quot;Export APIs to Window Object&quot; 설정을 활성화하여 글로벌 창 개체에서 MediaHeartbeat API를 내보냅니다. 구성된 변수 이름 아래에 API를 내보냅니다. 예를 들어 변수 이름이 `ADB`가 되도록 구성된 경우 MediaHeartbeat는 `window.ADB.MediaHeartbeat`로 액세스할 수 있습니다.

>[!IMPORTANT]
>
>MA 확장은 `window["CONFIGURED_VARIABLE_NAME"]`가 정의되지 않고 기존 변수를 재정의하지 않는 경우에만 API를 내보냅니다.

1. **MediaHeartbeat 인스턴스 만들기:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

   **매개 변수:** 다음 함수를 노출하는 유효한 위임 개체

   | 메서드 |  설명   |
   | :--- | :--- |
   | `getQoSObject()` | 현재 QoS 정보가 포함된 `theMediaObject` 인스턴스를 반환합니다. 이 메서드는 재생 세션 중에 여러 번 호출됩니다. 플레이어 구현은 항상 최근에 사용 가능한 QoS 데이터를 반환해야 합니다. |
   | `getCurrentPlaybackTime()` | 플레이헤드의 현재 위치를 반환합니다. VOD 추적의 경우 이 값은 미디어 항목이 시작된 후 현재까지의 시간(초)으로 지정됩니다. LIVE/LIVE 추적의 경우 이 값은 프로그램이 시작된 후 현재까지의 시간(초)으로 지정됩니다. |

   **반환 값:** `MediaHeartbeat` 인스턴스로 해결되거나 오류 메시지가 표시되고 거부되는 약속입니다.

1. **MediaHeartbeat 상수에 액세스:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat`

   이렇게 하면 [`MediaHeartbeat`](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) 클래스의 모든 상수 및 정적 메서드가 노출됩니다.

   여기서 샘플 플레이어는 가져올 수 있습니다. [MA 샘플 플레이어](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/2.x). 샘플 플레이어는 MA 확장을 사용하여 웹 앱에서 바로 Media Analytics를 지원하는 방법을 소개하는 참조 역할을 합니다.

1. 다음과 같이 MediaHeartbeat 추적기 인스턴스를 만듭니다.

   ```javascript
   var MediaHeartbeat = window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat;
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   };
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   };
   
   var self = this;
   MediaHeartbeat.getInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   ```

### 다른 확장에서 사용

MA 확장은 `get-instance` 및 `media-heartbeat` 공유 모듈을 다른 확장에 노출합니다. 공유 모듈에 대한 자세한 내용은 [공유 모듈 설명서](../../../extension-dev/web/shared.md)를 참조하십시오.

>[!IMPORTANT]
>
>공유 모듈은 다른 확장 프로그램에서만 액세스할 수 있습니다. 즉, 웹 페이지/JS 앱은 공유 모듈에서 액세스하거나 확장 외부에 있는 `turbine`(아래의 코드 샘플 참조)을 사용할 수 없습니다.

1. **MediaHeartbeat 인스턴스 만들기:** `get-instance` 공유 모듈

   **매개 변수:**

   * 다음 함수를 노출하는 유효한 위임 개체

     | 메서드 |  설명   |
     | :--- | :--- |
     | `getQoSObject()` | 현재 QoS 정보가 포함된 `MediaObject` 인스턴스를 반환합니다. 이 메서드는 재생 세션 중에 여러 번 호출됩니다. 플레이어 구현은 항상 최근에 사용 가능한 QoS 데이터를 반환해야 합니다. |
     | `getCurrentPlaybackTime()` | 플레이헤드의 현재 위치를 반환합니다. VOD 추적의 경우 이 값은 미디어 항목이 시작된 후 현재까지의 시간(초)으로 지정됩니다. LIVE/LIVE 추적의 경우 이 값은 프로그램이 시작된 후 현재까지의 시간(초)으로 지정됩니다. |

   * 다음 속성을 노출하는 옵션 구성 개체

     | 속성 | 설명 | 필수 여부 |
     | :--- | :--- | :--- |
     | Online Video Provider | 콘텐츠가 배포되는 온라인 비디오 플랫폼의 이름입니다. | 아니요. 있는 경우 확장 구성 중에 정의된 값을 재정의합니다. |
     | Player Name | 사용 중인 미디어 플레이어의 이름(예: &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) | 아니요. 있는 경우 확장 구성 중에 정의된 값을 재정의합니다. |
     | Channel | 채널 이름 속성입니다. | 아니요. 있는 경우 확장 구성 중에 정의된 값을 재정의합니다. |

   **반환 값:** `MediaHeartbeat` 인스턴스로 해결되거나 오류 메시지가 표시되고 거부되는 약속입니다.

1. **MediaHeartbeat 상수에 액세스:** `media-heartbeat` 공유 모듈

   이 모듈은 이 클래스의 모든 상수 및 정적 메서드를 노출합니다. [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

1. 다음과 같이 MediaHeartbeat 추적기 인스턴스를 만듭니다.

   ```javascript
   var getMediaHeartbeatInstance =
     turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   
   var MediaHeartbeat =
     turbine.getSharedModule('adobe-video-analytics', 'media-heartbeat');
     ...
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   }
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   }
   ...
   
   var self = this;
   getMediaHeartbeatInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       ...
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   
   ...
   ```

1. 미디어 하트비트 인스턴스를 사용하여 [미디어 SDK JS 설명서](https://experienceleague.adobe.com/docs/media-analytics/using/legacy-implementations/legacy-media-sdks/setup-javascript/set-up-js-2.html) 및 [JS API 설명서](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)에 따라 미디어 추적을 구현합니다.

>[!NOTE]
>
>**테스트:** 이 릴리스에서 확장을 테스트하려면 모든 종속 확장에 대한 액세스 권한이 있는 [Experience Platform](../../../extension-dev/submit/upload-and-test.md)에 업로드해야 합니다.


<!--
## Leveraging the sample HTML5 player

You can obtain the MA extension sample HTML5 player here: [HTML5 Sample Player](https://github.com/adobe/reactor-adobe-va-sample-player). The sample player acts as a reference to create video player extensions and to showcase using the MA extension to support media tracking.

### Sample player extension action types

This section describes the action types available in the Sample Player extension.

#### Open Video

The _Open Video_ action provides various configurations for creating and customizing an HTML5 player, providing a video to play and enabling/disabling Adobe Video Analytics tracking.

**Action Configuration / Player Settings:** Note the CSS Selector setting which specifics the `<div>` in the web page where the player is added. Note also that the _Enable Adobe Analytics_ checkbox is checked in the Analytics Settings pane.

![Player Extension Action Configuration](../../../images/ext-va-sp-action.png)

![Player Extension Action Configuration](../../../images/ext-va-sp-action1.png)

* [\[...\]/openVideo/openVideo.jsx](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/view/actions/openVideo/openVideo.jsx) -

  UI Code to configure the Action is defined here.

* [\[...\]/actions/openVideo.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/actions/openVideo.js) - This file exports a function that gets executed when the Action is triggered as part of the tag rule.

  This is a code snippet from `openVideo.js` where the `openVideo` Action is executed:

  ```javascript
    function openVideo(settings) {
        let player;
        try {
            Logger.info(LOG_TAG, `Executing action with ${JSON.stringify(settings)}`);

            player = new PlayerFacade(settings);
            PlayerStore.registerPlayer(player);
            player.load(settings.media);
        } catch (ex) {
            Logger.error(LOG_TAG, `Creating player for action openVideo failed with error ${ex.message}`);

            // Cleanup from DOM.
            if (player) {
                player.destroy();
            }
        }
    }
    ...
  ```

* [\[...\]/analytics/adobeAnalyticsProvider.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/helpers/analytics/adobeAnalyticsProvider.js) - This file implements Video Analytics tracking by using Shared Modules exposed by the VA extension.

### Sample player extension basic deployment

Once the Sample Player extension is installed, you'll need to create at least one rule to properly deploy it. The Image below shows a sample rule that opens the specified video when the core extension fires the `DOMLoaded` event.

![Player Extension Sample Rule](../../../images/ext-va-sp-rule.png)

After you have saved this rule, you will need to add it to a Library, and then build and deploy so that you can test the behavior.

-->
