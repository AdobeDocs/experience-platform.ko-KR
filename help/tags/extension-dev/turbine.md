---
title: Turbine 자유 변수
description: Adobe Experience Platform 태그 런타임과 관련된 정보 및 유틸리티를 제공하는 자유 변수인 turbine 개체에 대해 알아봅니다.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 27dd38cc509040ea9dc40fc7030dcdec9a182d55
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 49%

---

# Turbine 자유 변수

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../term-updates.md)를 참조하십시오.

`turbine` 객체는 확장의 라이브러리 모듈 범위 내에 있는 &quot;자유 변수&quot;입니다. Adobe Experience Platform 태그 런타임과 관련된 정보 및 유틸리티를 제공하며 를 사용하지 않고도 라이브러리 모듈에서 항상 사용할 수 있습니다 `require()`.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` 는 현재 태그 런타임 라이브러리에 대한 빌드 정보를 포함하는 객체입니다.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| 속성 | 설명 |
| --- | --- |
| `turbineVersion` | 현재 라이브러리 내에서 사용되는 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 버전입니다. |
| `turbineBuildDate` | 컨테이너 내에 사용된 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 버전이 빌드된 ISO 8601 날짜입니다. |
| `buildDate` | 현재 라이브러리가 빌드된 ISO 8601 날짜입니다. |

{style="table-layout:auto"}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` 는 라이브러리가 배포되는 환경에 대한 정보가 포함된 객체입니다.

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 환경의 ID입니다. |
| `stage` | 이 라이브러리가 빌드된 환경입니다. 가능한 값은 다음과 같습니다 `development`, `staging`, 및 `production`. |

{style="table-layout:auto"}

## `debugEnabled`

태그 디버깅이 현재 활성화되어 있는지 여부를 나타내는 부울 값입니다.

단순히 메시지를 기록하려는 경우에는 이 기능을 사용할 필요가 없습니다. 대신, 항상 를 사용하여 메시지를 기록합니다. `turbine.logger` 태그 디버깅이 활성화된 경우에만 메시지가 콘솔에 인쇄되도록 합니다.

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

데이터 요소의 값을 반환합니다.

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

[확장 구성](./configuration.md) 보기에서 마지막으로 저장한 설정 객체를 반환합니다.

반환된 설정 객체 내의 값은 데이터 요소에서 제공될 수 있습니다. 따라서 데이터 요소의 값이 변경되면 다른 시간에 `getExtensionSettings()`를 호출하는 경우 다른 결과가 발생할 수 있습니다. 최신 값을 얻으려면 를 호출하기 전에 가능한 한 오래 기다리십시오 `getExtensionSettings()`.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

다음 [hostedLibFiles](./manifest.md) 속성은 태그 런타임 라이브러리와 함께 다양한 파일을 호스팅하기 위해 확장 매니페스트 내에서 정의할 수 있습니다. 이 모듈은 주어진 라이브러리 파일이 호스팅되는 URL을 반환합니다.

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

다른 확장에서 공유된 모듈을 검색합니다. 일치하는 모듈이 없으면 `undefined`가 반환됩니다. 공유 모듈에 대한 자세한 내용은 [공유 모듈 구현](./web/shared.md)을 참조하십시오.

## `logger`

```js
turbine.logger.error('Error!');
```

로깅 유틸리티는 콘솔에 메시지를 기록하는 데 사용됩니다. 사용자가 디버깅을 사용하는 경우에만 콘솔에 메시지가 표시됩니다. 디버깅을 설정하는 데 권장되는 방법은 [Adobe Experience Cloud 디버거](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda). 또는 다음 명령을 실행할 수도 있습니다 `_satellite.setDebug(true)` 브라우저 개발자 콘솔 내에서 로거는 다음 메서드를 사용합니다.

* `logger.log(message: string)`: 콘솔에 메시지를 기록합니다.
* `logger.info(message: string)`: 콘솔에 정보 메시지를 기록합니다.
* `logger.warn(message: string)`: 콘솔에 경고 메시지를 기록합니다.
* `logger.error(message: string)`: 콘솔에 오류 메시지를 기록합니다.
* `logger.debug(message: string)`: 콘솔에 디버그 메시지를 기록합니다. (브라우저 콘솔 내에서 `verbose` 로깅이 활성화될 때만 표시됩니다.)
* `logger.deprecation(message: string)`: 사용자가 태그 디버깅을 활성화했는지 여부에 관계없이 콘솔에 경고 메시지를 기록합니다.

## `onDebugChanged`

콜백 함수를 로 전달하여 `turbine.onDebugChanged`, 디버깅이 전환될 때마다 태그가 콜백을 호출합니다. 태그는 디버깅이 활성화된 경우 true이고, 디버깅이 비활성화된 경우 false인 콜백 함수에 부울을 전달합니다.

단순히 메시지를 기록하려는 경우에는 이 기능을 사용할 필요가 없습니다. 대신, 항상 를 사용하여 메시지를 기록합니다. `turbine.logger` 및 태그는 태그 디버깅이 활성화된 경우에만 메시지가 콘솔에 인쇄되도록 합니다.

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

현재 태그 런타임 라이브러리의 속성에 대해 사용자가 정의하는 다음 설정을 포함하는 객체입니다.

* `propertySettings.domains: Array<String>`

   속성이 다루는 도메인의 배열입니다.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   확장 개발자는 이 설정에 관여하지 않아야 합니다.
