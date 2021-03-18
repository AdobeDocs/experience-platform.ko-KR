---
title: Adobe Experience Platform 웹 SDK를 사용하여 고객 동의 기본 설정 지원
description: Adobe Experience Platform 웹 SDK를 사용하여 동의 기본 설정을 지원하는 방법을 알아봅니다.
keywords: 동의;defaultConsent;default consent;setConsent;프로필 개인 정보 혼합;경험 이벤트 개인 정보 혼합;개인 정보 혼합
translation-type: tm+mt
source-git-commit: dd9101079a1093c109f43b268a78c07770221156
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 0%

---


# 고객 동의 환경 설정 지원

사용자의 개인 정보를 존중하기 위해 SDK가 특정 목적을 위해 사용자별 데이터를 사용하도록 허용하기 전에 사용자의 동의를 요청할 수 있습니다. 현재, SDK는 사용자가 모든 목적에 한해서만 가입 또는 가입을 하도록 허용하지만, 향후 Adobe은 특정 목적에 대한 보다 세밀한 제어를 제공하기를 희망하고 있습니다.

사용자가 모든 목적으로 액세스하는 경우 SDK는 다음 작업을 수행할 수 있습니다.

* Adobe 서버에서 데이터를 전송합니다.
* 쿠키 또는 웹 저장소 항목을 읽고 씁니다.

사용자가 모든 목적을 벗어나는 경우 SDK는 이러한 작업을 수행하지 않습니다.

## 동의 구성

기본적으로 사용자는 모든 목적으로 옵트인됩니다. 사용자가 로그인할 때까지 SDK가 위 작업을 수행하지 않도록 하려면 다음과 같이 SDK 구성 중에 `"defaultConsent": "pending"`을(를) 전달합니다.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

일반적인 용도의 기본 동의를 보류 중으로 설정하면 사용자 옵트인 기본 설정(예: `sendEvent` 명령)에 의존하는 명령을 실행하려고 하면 SDK 내에서 명령이 큐에 오르게 됩니다. 이러한 명령은 사용자의 옵트인 기본 설정을 SDK에 전달해야만 처리됩니다.

>[!NOTE]
>
>명령은 메모리에서 큐에 있습니다. 페이지 로드 간에 저장되지 않습니다.

사용자의 옵트인 환경 설정이 설정되기 전에 발생한 이벤트를 수집하지 않으려면 SDK 구성 중에 `"defaultConsent": "out"`을(를) 전달할 수 있습니다. 사용자 옵트인 기본 설정에 따라 다른 명령을 실행하려 해도 사용자의 옵트인 기본 설정이 SDK에 전달되기 전에는 아무런 효과가 없습니다.

>[!NOTE]
>
>현재 SDK는 단일 전체 또는 아무 목적만 지원합니다. 서로 다른 Adobe 기능 및 제품 오퍼링에 해당하는 더 강력한 목적 또는 카테고리 세트를 구축할 계획이지만, 현재 구현은 옵트인에 대한 전체 또는 전혀 도움이 되지 않습니다.  이는 Adobe Experience Platform [!DNL Web SDK]에만 적용되며 다른 Adobe JavaScript 라이브러리는 해당되지 않습니다.

이 시점에서 사용자에게 사용자 인터페이스 내 특정 위치에서 옵트인하도록 요청할 수 있습니다. 사용자의 기본 설정이 수집되면 SDK에 이러한 기본 설정을 알립니다.

## Adobe Experience Platform 표준을 통해 동의 기본 설정 전달

SDK는 Adobe Experience Platform 동의 표준의 버전 1.0 및 2.0을 지원합니다. 현재, 1.0 및 2.0 표준은 전체 또는 아무것도 동의 기본 설정의 자동 실행만 지원합니다. 1.0 표준은 2.0 표준에 찬성하여 단계적으로 폐지되고 있다. 2.0 표준에서는 동의 기본 설정을 수동으로 적용하는 데 사용할 수 있는 추가 동의 기본 설정을 추가할 수 있습니다.

### Adobe 표준 버전 2.0 사용

Adobe Experience Platform을 사용하는 경우 프로필 스키마에 개인 정보 혼합을 포함해야 합니다. Adobe 표준 버전 2.0에 대한 자세한 내용은 Adobe Experience Platform](../../landing/governance-privacy-security/overview.md)의 [거버넌스, 개인 정보 및 보안을 참조하십시오. 동의 및 기본 설정 프로필 혼합의 `consents` 필드의 스키마에 해당하는 아래 값 개체 내에 데이터를 추가할 수 있습니다.

사용자가 옵션을 선택하는 경우 다음과 같이 컬렉션 환경 설정이 `y`으로 설정된 `setConsent` 명령을 실행합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    }]
});
```

시간 필드는 사용자가 마지막으로 동의 기본 설정을 업데이트한 시기를 지정해야 합니다. 사용자가 옵트아웃하도록 선택한 경우 다음과 같이 컬렉션 환경 설정이 `n`으로 설정된 `setConsent` 명령을 실행합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

>[!NOTE]
>
>사용자가 옵트아웃한 후 SDK에서는 사용자가 `y`에 대한 동의를 수집하는 것을 허용하지 않습니다.

### Adobe 표준 버전 1.0 사용

사용자가 옵션을 선택하는 경우 다음과 같이 `general` 옵션이 `in`로 설정된 `setConsent` 명령을 실행합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

사용자가 그만두기로 선택한 경우 다음과 같이 `general` 옵션이 `out`로 설정된 `setConsent` 명령을 실행합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

>[!NOTE]
>
>사용자가 옵트아웃한 후에는 SDK에서 사용자가 `in`에 대한 동의를 설정할 수 없습니다.

## IAB TCF 표준을 통해 동의 환경 설정을 통신합니다.

SDK는 IAB(Interactive Advertising Bureau Europe) TCF(Transparency and Consent Framework) 표준을 통해 제공되는 사용자의 동의 기본 설정을 기록하는 것을 지원합니다. 동의 문자열은 위와 동일한 `setConsent` 명령을 통해 다음과 같이 설정할 수 있습니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

이러한 방식으로 동의가 설정되면, 실시간 고객 프로필은 동의 정보로 업데이트됩니다. 이 작업을 수행하려면 프로필 XDM 스키마에는 [프로필 개인 정보 혼합](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md)이 포함되어야 합니다. 이벤트를 전송할 때 IAB 동의 정보를 이벤트 XDM 개체에 수동으로 추가해야 합니다. SDK는 이벤트에 동의 정보를 자동으로 포함하지 않습니다. 이벤트에서 동의 정보를 보내려면 [경험 이벤트 개인 정보 혼합](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md)을 경험 이벤트 스키마에 추가해야 합니다.

## 하나의 요청에서 여러 표준 전송

또한 SDK는 요청에서 두 개 이상의 동의 개체 전송을 지원합니다.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## 동의 기본 사항 지속성

`setConsent` 명령을 사용하여 SDK에 대한 사용자 환경 설정을 전달한 후 SDK는 사용자의 환경 설정을 쿠키에 유지합니다. 다음에 사용자가 브라우저에서 웹 사이트를 로드할 때 SDK는 이러한 지속적인 환경 설정을 검색하고 사용하여 이벤트를 Adobe으로 보낼 수 있는지 여부를 결정합니다.

현재 기본 설정으로 동의 대화 상자를 표시할 수 있으려면 사용자 환경 설정을 별도로 저장해야 합니다. SDK에서 사용자 환경 설정을 검색할 수 없습니다. 사용자 환경 설정이 SDK와 동기화되어 있는지 확인하려면 페이지를 로드할 때마다 `setConsent` 명령을 호출할 수 있습니다. 환경 설정이 변경된 경우에만 SDK에서 서버 호출을 수행합니다.

## 동의를 설정하는 동안 ID 동기화

기본 동의가 보류 중이거나 종료될 때, `setConsent`은 외부로 이동하여 ID를 설정하는 첫 번째 요청일 수 있습니다. 따라서 첫 번째 요청에서 ID를 동기화하는 것이 중요할 수 있습니다. ID 맵은 `sendEvent` 명령에서처럼 `setConsent` 명령에 추가할 수 있습니다. [Experience Cloud ID 검색](../identity/overview.md) 참조

