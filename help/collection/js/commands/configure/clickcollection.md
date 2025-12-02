---
title: clickCollection
description: 클릭 컬렉션 설정을 미세 조정합니다.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

`clickCollection` 개체에는 자동으로 수집된 링크 데이터를 제어하는 데 도움이 되는 여러 변수가 포함되어 있습니다. 데이터 수집에서 링크 유형을 포함하거나 제외하려면 다음 변수를 사용하십시오. 웹 SDK 버전 2.25.0 이상에서 지원됩니다.

이 변수를 사용하려면 다음 조건을 모두 충족해야 합니다.

* [`clickCollectionEnabled`](clickcollectionenabled.md)을(를) 사용하도록 설정해야 합니다.
* `clickCollection.filterClickDetails`을(를) 사용하는 경우 사용되지 않는 [`onBeforeLinkClickSend`](onbeforelinkclicksend.md) 메서드는 비어 있어야 합니다.
* 이벤트 페이로드에는 방문자의 방문 중 특정 시점에 `xdm.web.webPageDetails.name`의 값이 있어야 합니다.

구현이 위의 요구 사항을 모두 충족하지 않는 경우 이 객체는 아무 작업도 하지 않습니다.

`clickCollection` 개체에서 다음 속성을 사용할 수 있습니다.

| 속성 | 유형 | 설명 |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | 현재 도메인 내의 링크가 자동으로 추적되는지 여부를 결정합니다. 예를 들어 `https://example.com/index.html`에 대한 `https://example.com/product.html`은(는) 내부 링크로 간주됩니다. |
| **`downloadLinkEnabled`** | `boolean` | 라이브러리가 [`downloadLinkQualifier`](downloadlinkqualifier.md) 속성을 기반으로 다운로드로 적합한 링크를 추적하는지 여부를 결정합니다. |
| **`externalLinkEnabled`** | `boolean` | 외부 도메인에 대한 링크가 자동으로 추적되는지 여부를 결정합니다. 예를 들어 `https://example.com`에서 `https://example.net`까지는 외부 링크로 간주됩니다. |
| **`eventGroupingEnabled`** | `boolean` | 라이브러리가 다음 &quot;페이지 보기&quot; 이벤트까지 대기하여 링크 추적 데이터를 전송할지 여부를 결정합니다. 다음 요소가 페이로드에 포함될 때 라이브러리는 이벤트를 &quot;페이지 보기&quot;로 간주합니다.<ul><li>`xdm.web.webPageDetails.name`에 문자열 값이 있습니다.</li><li>`xdm.web.webPageDetails.pageViews.value`이(가) `0`보다 큽니다.</li></ul>페이지 보기 이벤트가 로드되면 라이브러리는 저장된 링크 추적 데이터를 해당 이벤트의 나머지 데이터와 결합합니다. 이 옵션을 활성화하면 Adobe으로 전송하는 총 이벤트 수가 줄어듭니다. `internalLinkEnabled`이(가) 비활성화되어 있으면 이 변수는 아무 작업도 하지 않습니다. |
| **`sessionStorageEnabled`** | `boolean` | 링크 추적 데이터가 로컬 변수 대신 세션 저장소에 저장되는지 여부를 결정합니다. `internalLinkEnabled` 또는 `eventGroupingEnabled`이(가) 비활성화된 경우 이 변수는 아무 작업도 하지 않습니다.Adobe <br>단일 페이지 응용 프로그램 외부에서 `eventGroupingEnabled`을(를) 사용할 때는 이 변수를 사용하도록 설정하는 것이 좋습니다. `eventGroupingEnabled`이(가) 비활성화되어 있는 동안 `sessionStorageEnabled`이(가) 활성화된 경우 새 페이지를 클릭하면 링크 추적 데이터가 세션 저장소에 유지되지 않으므로 손실됩니다. 단일 페이지 애플리케이션은 일반적으로 새 페이지로 이동하지 않으므로 SPA 페이지에는 세션 스토리지가 필요하지 않습니다. |
| **`filterClickDetails`** | `function` | 수집한 링크 추적 데이터에 대한 전체 제어를 제공하는 콜백 함수입니다. 이 콜백 함수를 사용하여 링크 추적 데이터 전송을 변경, 난독화 또는 중단할 수 있습니다. 이 콜백은 링크 내의 개인 식별 정보와 같은 특정 정보를 생략하려는 경우 유용합니다. |

[`configure`](overview.md) 명령에서 이 개체를 설정하지 않으면 이 개체의 기본 설정은 [`clickCollectionEnabled`](clickcollectionenabled.md)의 값에 따라 달라집니다.

* `internalLinkEnabled`: `clickCollectionEnabled`과(와) 일치
* `downloadLinkEnabled`: `clickCollectionEnabled`과(와) 일치
* `externalLinkEnabled`: `clickCollectionEnabled`과(와) 일치
* `eventGroupingEnabled`: 기본값은 `false`입니다. 명시적으로 사용하도록 설정해야 합니다.
* `sessionStorageEnabled`: 기본값은 `false`입니다. 명시적으로 사용하도록 설정해야 합니다.
* `filterClickDetails`: 함수를 포함하지 않습니다. 명시적으로 등록해야 합니다.

>[!TIP]
>
>Adobe에서는 계약상 사용에 포함되는 이벤트 수를 줄이기 때문에 `eventGroupingEnabled`이(가) 활성화된 경우 `internalLinkEnabled`을(를) 활성화할 것을 권장합니다.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```

## 웹 SDK 태그 확장에 대한 클릭 컬렉션 구성

이러한 설정은 [데이터 수집 구성 설정](/help/tags/extensions/client/web-sdk/configure/data-collection.md)을 사용하여 웹 SDK 태그 확장에서 구성할 수 있습니다.
