---
title: 오디오 및 비디오 확장 프로그램용 Adobe Medium Analytics(3.x SDK) 개요
description: Adobe Experience Platform의 오디오 및 비디오 태그 확장용 Adobe Medium Analytics(3.x SDK)에 대해 알아봅니다.
exl-id: 7289d57d-7e7f-4832-9469-3b5a62183a32
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 76%

---

# 오디오 및 비디오 확장 프로그램용 Adobe Medium Analytics(3.x SDK) 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Adobe Media Analytics(3.x SDK) for Audio and Video 확장(Media Analytics 확장) 설치, 구성 및 구현 관련 정보에 대해서는 이 설명서를 참조합니다. 예제 및 샘플 링크와 함께 이 확장을 사용하여 규칙을 만들 때 사용할 수 있는 옵션이 포함되어 있습니다.

MA(Media Analytics) 확장은 Core JavaScript Media SDK(Media 3.x SDK)를 추가합니다. 이 확장은 `Media` 태그를 사용할 수 있는 사이트 또는 프로젝트에 대한 추적기 인스턴스. MA 확장을 사용하려면 다음 두 개의 확장이 추가로 필요합니다.

* [Analytics 확장](../analytics/overview.md)
* [Experience Cloud ID 확장](../id-service/overview.md)

>[!IMPORTANT]
>
>이 확장은 Media 2.x SDK와 이전 버전과 호환되지 않는 Media 3.x SDK와 함께 배포됩니다. 페이지에서 이미 Media 2.x SDK를 사용하고 있는 경우 이 확장 대신 [Adobe Media Analytics for Audio and Video 확장](../media-analytics/overview.md)을 사용합니다.

태그 지원 프로젝트에서 위에 언급된 확장 세 개를 모두 포함했으면 다음 두 가지 방법 중 하나를 사용하여 진행할 수 있습니다.

* 웹 앱의 `Media` API 사용
* 특정 미디어 플레이어 이벤트를 `Media` 추적기 인스턴스의 API에 매핑하는 플레이어 전용 확장을 포함하거나 빌드합니다. 이 인스턴스는 MA 확장을 통해 노출됩니다.

## MA 확장 설치 및 구성

* **설치:** MA 확장을 설치하려면 확장 속성을 열고 **[!UICONTROL Extensions > Catalog]**&#x200B;를 마우스로 가리키면 다음이 표시됩니다 **[!UICONTROL 오디오 및 비디오용 Adobe Medium Analytics(3.x SDK)]** 확장을 선택하고 **[!UICONTROL 설치]**.

* **구성:** MA 확장을 구성하려면 [!UICONTROL 확장] 탭에서 확장을 마우스로 가리킨 다음 을 선택합니다 **[!UICONTROL 구성]**:

![MA 확장 구성](../../../images/ext-ma-config.png)

### 구성 옵션:

| 옵션 | 설명 |
| :--- | :--- |
| Collection API 서버 | Media Collection API 서버 정의(이 서버를 가져오려면 Adobe 담당자에게 문의) |
| Application Version | 미디어 플레이어 앱/SDK의 버전 |
| Player Name | 사용 중인 미디어 플레이어의 이름(예: &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Channel | 채널 이름 속성입니다. |
| Debug Logging | 로깅 활성화 또는 비활성화 |
| Enable SSL | HTTPS를 통해 Ping 전송 활성화 또는 비활성화 |
| Export APIs to Window Object | 글로벌 범위로 Media Analytics API 내보내기 활성화 또는 비활성화 |
| Variable Name | `window` 개체 아래로 Media Analytics API를 내보내는 데 사용하는 변수 |

**미리 알림:** MA 확장 프로그램을 사용하려면 [Analytics](../analytics/overview.md) 및 [Experience Cloud ID](../id-service/overview.md) 확장 프로그램이 필요합니다. 확장 속성에 이러한 확장을 추가하고 구성해야 합니다.

## MA 확장 사용

### 웹 페이지/JS 앱에서 사용

MA 확장은 의 &quot;Export APIs to Window Object&quot; 설정을 활성화하여 글로벌 창 개체에서 Media API를 내보냅니다 [!UICONTROL 구성] 페이지. 구성된 변수 이름 아래에 API를 내보냅니다. 예를 들어 변수 이름이 `ADB`가 되도록 구성된 경우 Media API는 `window.ADB.Media`로 액세스할 수 있습니다.

>[!IMPORTANT]
>
>MA 확장은 `window["CONFIGURED_VARIABLE_NAME"]`가 정의되지 않고 기존 변수를 재정의하지 않는 경우에만 API를 내보냅니다.

1. **미디어 API:** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Media SDK의 모든 API 및 상수를 노출합니다. [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **미디어 추적기 인스턴스 만들기:** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **반환 값:** 미디어 세션 추적을 위한 추적기 `Media` 인스턴스입니다.

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. 미디어 추적기 인스턴스를 사용하여 [JS API 설명서](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html)에 따라 미디어 추적을 구현합니다.

여기서 샘플 플레이어는 가져올 수 있습니다. [MA 샘플 플레이어](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x). 샘플 플레이어는 MA 확장을 사용하여 웹 앱에서 바로 Media Analytics를 지원하는 방법을 소개하는 참조 역할을 합니다.


### 다른 확장에서 사용

MA 확장은 `media` 공유 모듈로 다른 확장에 추가할 수 있습니다. 공유 모듈에 대한 자세한 내용은 [공유 모듈 설명서](../../../extension-dev/web/shared.md)를 참조하십시오.

>[!IMPORTANT]
>
>공유 모듈은 다른 확장 프로그램에서만 액세스할 수 있습니다. 즉, 웹 페이지/JavaScript 앱은 공유 모듈에 액세스하거나 확장 외부에 있는 `turbine`(아래의 코드 샘플 참조)을 사용할 수 없습니다.

1. **미디어 API:** `media` 공유 모듈

   Media SDK의 모든 API 및 상수를 노출합니다. [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. 다음과 같이 Media 추적기 인스턴스를 만듭니다.

   **반환 값:** 미디어 세션 추적을 위한 추적기 `Media` 인스턴스입니다.

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. 미디어 추적기 인스턴스를 사용하여 [JS API 설명서](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html)에 따라 미디어 추적을 구현합니다.

>[!NOTE]
>
>**테스트:** 이 릴리스에서 확장을 테스트하려면 모든 종속 확장에 대한 액세스 권한이 있는 [ Platform ](../../../extension-dev/submit/upload-and-test.md)에 업로드해야 합니다.
