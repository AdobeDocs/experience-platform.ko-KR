---
title: Edge 확장 모듈의 컨텍스트
description: 컨텍스트 개체와 이 개체가 Edge 속성의 태그 확장에서 라이브러리 모듈과 상호 작용할 때 수행하는 역할에 대해 알아봅니다.
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 77%

---

# Edge 확장 모듈의 컨텍스트

>[!NOTE]
>
> Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

Edge 확장의 모든 라이브러리 모듈은 실행될 때 `context` 개체가 제공됩니다. 이 문서에서는 `context` 개체에서 제공하는 속성과 라이브러리 모듈에서 수행하는 역할에 대해 설명합니다.

## Adobe 요청 컨텍스트(arc)

`arc` 속성은 규칙을 트리거하는 이벤트에 대한 정보를 제공하는 개체입니다. 아래 섹션은 이 개체에 포함된 다양한 하위 속성을 설명합니다.

### [!DNL event]

다음 `event` object 는 규칙을 트리거한 이벤트를 나타내며 다음 값을 포함합니다.

```js
logger.log(context.arc.event);
```

| 속성 | 설명 |
| --- | --- |
| `xdm` | 이벤트의 XDM 개체입니다. |
| `data` | 사용자 지정 데이터 레이어입니다. |

### [!DNL request]

클라이언트 장치의 요청과 혼동하지 않도록 하십시오. `request`는 Adobe Experience Platform Edge Network에서 가져오는 약간 수정된 개체입니다.

```js
logger.log(context.arc.request)
```

`request` 개체에는 두 개의 최상위 속성이 있습니다. `body` 및 `head`. 다음 `body` 속성에는 XDM(경험 데이터 모델) 정보가 포함되어 있으며 로 이동할 때 Adobe Experience Platform Debugger에서 검사할 수 있습니다. **[!UICONTROL 시작]** 및 선택 **[!UICONTROL 에지 추적]** 탭.

### [!DNL ruleStash] {#rulestash}

`ruleStash`는 작업 모듈에서 모든 결과를 수집하는 개체입니다.

```js
logger.log(context.arc.ruleStash);
```

각 확장에는 고유한 네임스페이스가 있습니다. 예를 들어, 확장의 이름이 `send-beacon`인 경우 `send-beacon` 작업의 모든 결과가 `ruleStash['send-beacon']` 네임스페이스에 저장됩니다.

이 네임스페이스는 각 확장에 대해 고유하며 시작 부분에 `undefined` 값이 있습니다.

네임스페이스는 각 작업에서 반환된 결과로 재정의됩니다. 예를 들어, 다음 두 가지 작업을 포함하는 `transform` 확장이 있다고 가정해 보십시오. `generate-fullname` 및 `generate-fulladdress`. 그런 다음 이 두 작업을 규칙에 추가합니다.

`generate-fullname` 작업의 결과가 `Firstname Lastname`이면 작업이 완료된 후 규칙 스태시가 다음과 같이 표시됩니다.

```js
{
  transform: 'Firstname Lastname'
}
```

`generate-address` 작업의 결과가 `3900 Adobe Way`이면 작업이 완료된 후 규칙 스태시가 다음과 같이 표시됩니다.

```js
{
  transform: '3900 Adobe Way'
}
```

`generate-address` 작업이 새 값으로 재정의되었으므로 &quot;Firstname Lastname&quot;이 규칙 스태시에 더 이상 없습니다.

`ruleStash`에서 `transform` 네임스페이스 안에 있는 두 작업의 결과를 저장하게 하려면 다음 예제와 비슷한 작업 모듈을 작성할 수 있습니다.

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

이 작업을 처음 실행할 때 `ruleStash`는 `undefined`로 시작되므로 빈 개체로 초기화됩니다. 다음 번에 작업이 실행되면 작업을 이전에 호출할 때 반환된 `ruleStash`이 수신됩니다. 개체를 `ruleStash`로 사용하면 Adobe의 확장에서 이전에 설정한 다른 작업에 의해 데이터 손실 없이 새 데이터를 추가할 수 있습니다.

>[!NOTE]
>
>이 전략을 사용할 때는 항상 전체 확장 규칙 스태시를 반환하도록 주의하십시오. 대신 값만 반환하는 경우 설정한 다른 속성을 덮어씁니다.

## 유틸리티

다음 `utils` 속성은 태그 런타임과 관련된 유틸리티를 제공하는 개체를 나타냅니다.

### [!DNL logger]

다음 `logger` 유틸리티를 사용하면 를 사용할 때 디버깅 세션 중에 표시되는 메시지를 기록할 수 있습니다 [Adobe Experience Platform 디버거](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

```js
context.utils.logger.error('Error!');
```

이 로거에는 다음과 같은 메서드가 있습니다. 여기서 `message`는 기록할 메시지입니다.

| 메서드 | 설명 |
| --- | --- |
| `log(message)` | 콘솔에 메시지를 기록합니다. |
| `info(message)` | 콘솔에 정보 메시지를 기록합니다. |
| `warn(message)` | 콘솔에 경고 메시지를 기록합니다. |
| `error(message)` | 콘솔에 오류 메시지를 기록합니다. |
| `debug(message)` | 콘솔에 디버그 메시지를 기록합니다. 브라우저 콘솔 내에서 `verbose` 로깅이 활성화될 때만 표시됩니다. |

### [!DNL fetch]

이 유틸리티는 [FETCH API](https://developer.mozilla.org/ko-KR/docs/Web/API/Fetch_API)를 구현합니다. 이 함수를 사용하여 타사 엔드포인트에 대한 요청을 수행할 수 있습니다.

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

이 유틸리티는 현재 태그 런타임 라이브러리의 빌드에 대한 정보가 포함된 개체를 반환합니다.

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

개체에는 다음 값이 포함되어 있습니다.

| 속성 | 설명 |
| --- | --- |
| `turbineVersion` | 현재 라이브러리 내에서 사용되는 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) 버전입니다. |
| `turbineBuildDate` | 컨테이너 내에 사용된 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) 버전이 빌드된 ISO 8601 날짜입니다. |
| `buildDate` | 현재 라이브러리가 빌드된 ISO 8601 날짜입니다. |
| `environment` | 이 라이브러리가 빌드된 환경입니다. 가능한 값은 `development`, `staging` 및 `production.`을 포함합니다. |

다음은 반환되는 값을 보여 주는 예제 `getBuildInfo` 개체입니다.

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

[확장 구성](../configuration.md) 보기에서 마지막으로 저장한 `settings` 개체를 반환합니다.

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

이 유틸리티는 해당 라이브러리 모듈 보기에서 마지막으로 저장한 `settings` 개체를 반환합니다.

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

이 유틸리티는 모듈을 트리거하는 규칙에 대한 정보가 포함된 개체를 반환합니다.

```js
logger.log(context.utils.getRule());
```

이 개체에는 다음 값이 포함됩니다.

| 속성 | 설명 |
| --- | --- |
| `id` | 규칙 ID. |
| `name` | 규칙 이름. |
