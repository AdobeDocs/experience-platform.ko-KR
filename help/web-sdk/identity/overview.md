---
title: 웹 SDK의 ID 데이터
description: Adobe Experience Platform Web SDK를 사용하여 Adobe Experience Cloud ID(ECID)를 검색하고 관리하는 방법에 대해 알아봅니다.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: c99831cf2bb1b862d65851701b38c6d3dfe99000
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---


# 웹 SDK의 ID 데이터

Adobe Experience Platform Web SDK는 [ECID(Adobe Experience Cloud ID)](../../identity-service/features/ecid.md)를 사용하여 방문자 행동을 추적합니다. [!DNL ECIDs]을(를) 사용하면 각 디바이스에 여러 세션에서 지속될 수 있는 고유 식별자가 있는지 확인하여 웹 세션 중 및 여러 세션에서 발생하는 모든 히트를 특정 디바이스에 연결할 수 있습니다.

이 문서에서는 웹 SDK를 사용하여 [!DNL ECIDs] 및 [!DNL CORE IDs]을(를) 관리하는 방법에 대한 개요를 제공합니다.

## Web SDK를 사용하여 ECID 추적 {#tracking-ecids-web-sdk}

Web SDK는 쿠키를 사용하여 [!DNL ECIDs]을(를) 할당하고 추적하며, 이러한 쿠키가 생성되는 방식을 구성하는 데 사용 가능한 여러 메서드를 사용합니다.

새 사용자가 웹 사이트에 도달하면 [Adobe Experience Cloud Identity 서비스](../../identity-service/home.md)에서 해당 사용자에 대한 장치 ID 쿠키를 설정하려고 시도합니다.

* 처음 방문하는 사용자의 경우 [!DNL ECID]이(가) 생성되어 Experience Platform Edge Network의 첫 번째 응답에서 반환됩니다.
* 재방문자의 경우 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` 쿠키에서 [!DNL ECID]을(를) 검색하고 Edge Network이 요청 페이로드에 추가합니다.

[!DNL ECID]이(가) 포함된 쿠키가 설정되면 Web SDK에서 생성한 각 후속 요청에는 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` 쿠키에 인코딩된 [!DNL ECID]이(가) 포함됩니다.

장치 식별을 위해 쿠키를 사용하는 경우 Edge Network과 상호 작용하는 두 가지 방법이 있습니다.

1. `adobedc.net`을(를) 가리키는 자체 도메인에 CNAME을 만듭니다. 이 메서드를 [자사 데이터 수집](#first-party)이라고 합니다.
1. 데이터를 Edge Network 도메인 `adobedc.net`(으)로 직접 보냅니다. 이 메서드를 [타사 데이터 수집](#third-party)이라고 합니다.

아래 섹션에 설명된 대로 사용하도록 선택하는 데이터 수집 방법은 전체 브라우저에서 쿠키 수명에 직접적인 영향을 줍니다.

## Web SDK를 사용한 코어 ID 추적 {#tracking-coreid-web-sdk}

서드파티 쿠키가 활성화된 Google Chrome을 사용할 때 `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` Edge Network이 설정되어 있지 않으면 첫 번째 쿠키 요청은 demdex 쿠키를 설정하는 `demdex.net` 도메인을 거칩니다. 이 쿠키에는 [!DNL CORE ID]이(가) 포함되어 있습니다. [!DNL ECID]과(와) 다른 고유한 사용자 ID입니다.

구현에 따라 [액세스 [!DNL CORE ID]](#retrieve-coreid)할 수 있습니다.

### 자사 데이터 수집 {#first-party}

자사 데이터 수집에는 `adobedc.net`을(를) 가리키는 자체 도메인에서 `CNAME`을(를) 통해 쿠키를 설정하는 작업이 포함됩니다.

브라우저에서 사이트 소유 끝점에 의해 설정된 쿠키와 유사한 방식으로 `CNAME` 끝점에 의해 설정된 쿠키를 오랫동안 처리했지만, 브라우저에 의해 구현된 최근 변경 사항으로 인해 `CNAME` 쿠키가 처리되는 방식이 구분되었습니다. 현재 기본적으로 자사 `CNAME` 쿠키를 차단하는 브라우저가 없지만 일부 브라우저에서는 `CNAME`을(를) 사용하여 설정된 쿠키 수명을 7일로 제한합니다.

### 타사 데이터 수집 {#third-party}

타사 데이터 수집에는 Edge Network 도메인 `adobedc.net`(으)로 직접 데이터를 보내는 작업이 포함됩니다.

최근 몇 년 동안 웹 브라우저는 제3자가 설정한 쿠키를 처리하는 데 점점 더 제한을 받고 있습니다. 일부 브라우저는 기본적으로 서드파티 쿠키를 차단합니다. 서드파티 쿠키를 사용하여 사이트 방문자를 식별하는 경우, 이러한 쿠키의 수명은 거의 항상 자사 쿠키를 대신 사용하여 사용할 수 있는 수명보다 짧습니다. 경우에 따라 서드파티 쿠키가 7일 후에 만료됩니다.

또한 서드파티 데이터 수집을 사용하는 경우 일부 광고 차단기는 트래픽을 제한하여 데이터 수집 엔드포인트를 완전히 Adobe 합니다.

### 쿠키 수명이 Adobe Experience Cloud 애플리케이션에 미치는 영향 {#lifespans}

자사 데이터 수집을 선택하는지 또는 서드파티 데이터 수집을 선택하는지에 관계없이, 쿠키가 지속될 수 있는 시간은 [Adobe Analytics](https://experienceleague.adobe.com/ko/docs/analytics) 및 [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/customer-journey-analytics)의 방문자 수에 직접적인 영향을 줍니다. 또한 사이트에서 [Adobe Target](https://experienceleague.adobe.com/en/docs/target) 또는 [Offer decisioning](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision)을(를) 사용하면 최종 사용자에게 일관되지 않은 개인화 경험이 있을 수 있습니다.

예를 들어 사용자가 지난 7일 동안 항목을 3번 본 경우 항목을 홈 페이지로 홍보하는 개인화 경험을 만든 상황을 생각해 보겠습니다.

최종 사용자가 일주일에 세 번 사이트를 방문한 후 7일 동안 사이트로 돌아오지 않는 경우, 해당 사용자는 브라우저 정책(사이트를 방문했을 때 사용 중인 브라우저에 따라)에 의해 쿠키가 삭제되었을 수 있으므로 사이트로 돌아올 때 새 사용자로 간주될 수 있습니다. 이 경우 Analytics 도구는 7일 조금 전에 방문자가 사이트를 방문했더라도 해당 방문자를 새 사용자로 취급합니다. 또한 사용자를 위해 경험을 개인화하려는 노력이 다시 시작됩니다.

### 자사 디바이스 ID(FPID) {#fpid}

위에 설명된 대로 쿠키 수명의 효과를 고려하기 위해 대신 고유한 장치 식별자를 설정하고 관리하도록 선택할 수 있습니다. 자세한 내용은 [자사 장치 ID](./first-party-device-ids.md)의 안내서를 참조하십시오.

## 현재 사용자의 ECID 및 지역 검색 {#retrieve-ecid}

사용 사례에 따라 [!DNL ECID]에 액세스할 수 있는 두 가지 방법이 있습니다.

* [데이터 수집을 위한 데이터 준비를 통해  [!DNL ECID] 을(를) 검색합니다](#retrieve-ecid-data-prep): 이 방법은 권장되는 방법입니다.
* [`getIdentity()` 명령을 통해  [!DNL ECID] 검색](#retrieve-ecid-getidentity): 클라이언트측에서 [!DNL ECID] 정보가 필요한 경우에만 이 메서드를 사용하십시오.

### 데이터 수집을 위한 데이터 준비를 통해 [!DNL ECID] 검색 {#retrieve-ecid-data-prep}

[데이터 수집에 대한 데이터 준비](../../datastreams/data-prep.md)를 사용하여 [!DNL ECID]을(를) [!DNL XDM] 필드에 매핑합니다. [!DNL ECID]에 액세스하는 데 권장되는 방법입니다.

이렇게 하려면 소스 필드를 다음 경로로 설정합니다.

```js
xdm.identityMap.ECID[0].id
```

그런 다음 대상 필드를 필드가 `string` 유형인 XDM 경로로 설정합니다.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### `getIdentity()` 명령을 통해 [!DNL ECID] 검색 {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>클라이언트측에서 [!DNL ECID]이(가) 필요한 경우에만 `getIdentity()` 명령을 통해 ECID를 검색해야 합니다. ECID를 XDM 필드에만 매핑하려면 대신 [데이터 수집을 위한 데이터 준비](#retrieve-ecid-data-prep)를 사용하십시오.

현재 방문자에 대한 고유한 ECID를 검색하려면 `getIdentity` 명령을 사용하십시오. 아직 [!DNL ECID]이(가) 없는 처음 방문자의 경우 이 명령은 새 [!DNL ECID]을(를) 생성합니다. `getIdentity`은(는) 방문자에 대한 지역 ID도 반환합니다.

>[!NOTE]
>
>이 메서드는 일반적으로 [!DNL Experience Cloud] ID를 읽거나 Adobe Audience Manager에 대한 위치 힌트가 필요한 사용자 지정 솔루션에 사용됩니다. 표준 구현에서는 사용되지 않습니다.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## 현재 사용자의 코어 ID 검색 {#retrieve-coreid}

사용자에 대한 CORE ID를 검색하려면 아래와 같이 [`getIdentity()`](../commands/getidentity.md) 명령을 사용할 수 있습니다.

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```


## `identityMap` 사용 중 {#using-identitymap}

XDM [`identityMap` 필드](../../xdm/schema/composition.md#identityMap)을(를) 사용하여 여러 ID를 사용하는 장치/사용자를 식별하고, 인증 상태를 설정하고, 기본 ID로 간주되는 식별자를 결정할 수 있습니다. 식별자가 `primary`(으)로 설정되지 않은 경우 기본 값은 `ECID`입니다.

`identityMap` 필드가 `sentEvent` 명령을 사용하여 업데이트됩니다.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>Adobe은 `CRMID`과(와) 같은 사용자를 나타내는 네임스페이스를 기본 ID로 보낼 것을 권장합니다.


`identityMap` 내의 각 속성은 특정 [ID 네임스페이스](../../identity-service/features/namespaces.md)에 속하는 ID를 나타냅니다. 속성 이름은 ID 네임스페이스 기호여야 합니다. 이 기호는 &quot;[!UICONTROL ID]&quot; 아래의 Adobe Experience Platform 사용자 인터페이스에 나열되어 있습니다. 속성 값은 해당 ID 네임스페이스와 관련된 ID 배열이어야 합니다.

>[!IMPORTANT]
>
>`identityMap`에서 전달된 네임스페이스 ID는 대/소문자를 구분합니다. 데이터 수집이 불완전하지 않도록 올바른 네임스페이스 ID를 사용해야 합니다.

ID 배열의 각 ID 개체에는 다음 속성이 포함되어 있습니다.

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `id` | 문자열 | **(필수)** 특정 네임스페이스에 대해 설정할 ID입니다. |
| `authenticatedState` | 문자열 | **(필수)** ID의 인증 상태입니다. 가능한 값은 `ambiguous`, `authenticated` 및 `loggedOut`입니다. |
| `primary` | 부울 | 이 ID를 프로필의 기본 조각으로 사용할지 여부를 결정합니다. 기본적으로 ECID는 사용자의 기본 식별자로 설정됩니다. 생략하면 이 값의 기본값은 `false`입니다. |

`identityMap` 필드를 사용하여 장치 또는 사용자를 식별하면 [!DNL ID Service API]에서 [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) 메서드를 사용하는 것과 동일한 결과가 발생합니다. 자세한 내용은 [ID 서비스 API 설명서](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html)를 참조하세요.

## 방문자 API에서 ECID로 마이그레이션 {#migrating-visitor-api-ecid}

방문자 API를 사용하여에서 마이그레이션할 때 기존 AMCV 쿠키를 마이그레이션할 수도 있습니다. ECID 마이그레이션을 사용하려면 구성에서 `idMigrationEnabled` 매개 변수를 설정하십시오. ID 마이그레이션을 통해 다음과 같은 사용 사례를 사용할 수 있습니다.

* 도메인의 일부 페이지가 방문자 API를 사용하고 다른 페이지가 이 SDK를 사용하는 경우. 이 경우를 지원하기 위해 SDK는 기존 AMCV 쿠키를 읽고 기존 ECID로 새 쿠키를 기록합니다. 또한 SDK는 AMCV 쿠키를 기록하여 SDK로 계측된 페이지에서 ECID를 먼저 획득하는 경우 방문자 API로 계측된 후속 페이지가 동일한 ECID를 갖도록 합니다.
* 방문자 API가 있는 페이지에서 Adobe Experience Platform Web SDK가 설정된 경우. 이 경우를 지원하기 위해 AMCV 쿠키가 설정되지 않은 경우 SDK는 페이지에서 방문자 API를 찾아 호출하여 ECID를 가져옵니다.
* 전체 사이트에서 Adobe Experience Platform Web SDK를 사용하고 있고 방문자 API가 없는 경우 반환된 방문자 정보가 유지되도록 ECID를 마이그레이션하는 것이 유용합니다. 대부분의 방문자 쿠키가 마이그레이션되도록 SDK를 `idMigrationEnabled`과(와) 함께 배포한 후 설정을 끌 수 있습니다.

### 마이그레이션할 트레이트 업데이트

XDM 형식의 데이터를 Audience Manager으로 보낼 때 마이그레이션 시 이 데이터를 신호로 변환해야 합니다. XDM에서 제공하는 새 키를 반영하도록 트레이트를 업데이트해야 합니다. 이 프로세스는 Audience Manager이 만든 [BAAAM 도구](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)를 사용하여 쉽게 수행할 수 있습니다.

## 이벤트 전달에 사용

현재 [이벤트 전달](../../tags/ui/event-forwarding/overview.md)이 활성화되어 있고 `appmeasurement.js` 및 `visitor.js`을(를) 사용 중인 경우 이벤트 전달 기능을 활성화 상태로 유지할 수 있으며 이로 인해 문제가 발생하지 않습니다. 백 엔드에서 Adobe은 모든 AAM 세그먼트를 가져와 Analytics 호출에 추가합니다. Analytics에 대한 호출에 이러한 세그먼트가 포함되어 있는 경우 Analytics는 Audience Manager을 호출하여 데이터를 전달하지 않으므로 이중 데이터 수집은 없습니다. 동일한 세그멘테이션 종단점이 백엔드에서 호출되므로 Web SDK를 사용할 때도 위치 힌트가 필요하지 않습니다.
