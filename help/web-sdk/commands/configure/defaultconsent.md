---
title: defaultConsent
description: 웹 속성에 대한 기본 동의 수집 방법을 설정합니다.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 5%

---


# `defaultConsent`

`defaultConsent` 속성은 [`setConsent`](../setconsent.md) 명령을 호출하기 전에 데이터 수집 동의를 처리하는 방법을 결정합니다. 이 속성은 데이터를 수집하기 전에 동의가 필요한 영역에 거주하는 개인의 데이터를 실수로 수집하지 않으려는 경우 유용합니다.

기본적으로 사용자는 모든 용도로 옵트인되며 Web SDK는 다음 작업을 수행할 수 있습니다.

* Adobe 서버에 데이터를 보내고 받습니다.
* 쿠키 또는 웹 저장소 항목을 읽고 씁니다.

사용자가 모든 목적을 옵트아웃하는 경우 Web SDK는 이러한 작업을 수행하지 않습니다.

`defaultConsent` 속성은 다음 세 가지 값을 지원합니다.

* **`in`**: 사용자가 옵트아웃할 때까지 데이터 수집이 정상적으로 진행됩니다.
* **`out`**: 사용자가 옵트인할 때까지 데이터가 영구적으로 삭제됩니다.
* **`pending`**: 사용자가 [`setConsent`](../setconsent.md) 명령을 사용하여 옵트인할 때까지 데이터가 로컬에 저장됩니다. 일반적인 목적의 기본 동의가 `pending`(으)로 설정된 경우 사용자 옵트인 환경 설정에 따라 다른 명령(예: [`sendEvent`](../sendevent/overview.md) 명령)을 실행하려고 하면 웹 SDK에서 명령이 대기됩니다. 대기열에 추가된 명령은 사용자의 옵트인 환경 설정을 웹 SDK에 전달할 때까지 처리되지 않습니다.

>[!NOTE]
>
> 동의 데이터는 페이지 로드 간에 지속되지 않습니다.

방문자가 GDPR(일반 데이터 보호 규정)의 적용을 받지 않는 경우 기본 동의를 `in`(으)로 설정할 수 있습니다. GDPR 관할권 내의 방문자는 기본 동의를 `pending`(으)로 설정할 수 있습니다. CMP(동의 관리 플랫폼)가 고객의 지역을 감지하고 `gdprApplies` 플래그를 IAB TCF 2.0에 제공할 수 있습니다. 이 플래그는 기본 동의를 설정하는 데 사용할 수 있습니다.

사용자의 옵트인 환경 설정이 지정되기 전에 발생한 이벤트를 수집하지 않으려면 웹 SDK 구성 중에 `"defaultConsent": "out"`을(를) 전달할 수 있습니다. 사용자 옵트인 환경 설정에 의존하는 명령을 실행하려고 시도해도 사용자의 옵트인 환경 설정을 웹 SDK에 전달할 때까지 효과가 없습니다.

>[!NOTE]
>
>현재 Web SDK는 단일 전체 또는 무목적 기능만 지원합니다. 다양한 Adobe 기능 및 제품 오퍼링에 해당하는 보다 강력한 목적 또는 카테고리 세트를 구축할 계획이지만 현재 구현은 옵트인에 대한 양자택일의 접근 방식입니다.  이는 [!DNL Web SDK]에만 적용되며 다른 Adobe JavaScript 라이브러리에는 적용되지 않습니다.

## `setConsent`과(와) 함께 `defaultConsent` 사용 {#using-consent}

Web SDK는 두 개의 상호 보완적인 동의 구성 명령을 제공합니다.

* [`defaultConsent`](defaultconsent.md): 이 명령은 Web SDK를 사용하는 Adobe 고객의 동의 환경 설정을 캡처하기 위한 것입니다.
* [`setConsent`](../setconsent.md): 이 명령은 사이트 방문자의 동의 환경 설정을 캡처하기 위한 것입니다.

이러한 설정을 함께 사용하면 구성된 값에 따라 데이터 수집 및 쿠키 설정 결과가 달라질 수 있습니다.

동의 설정을 기반으로 데이터 수집이 발생하는 시점과 쿠키가 설정되는 시점을 이해하려면 아래 표를 참조하십시오.

| defaultConsent | setConsent | 데이터 수집 발생 | Web SDK가 브라우저 쿠키를 설정합니다. |
|---------|----------|---------|---------|
| `in` | `in` | 예 | 예 |
| `in` | `out` | 아니요 | 예 |
| `in` | 설정되지 않음 | 예 | 예 |
| `pending` | `in` | 예 | 예 |
| `pending` | `out` | 아니요 | 예 |
| `pending` | 설정되지 않음 | 아니요 | 아니요 |
| `out` | `in` | 예 | 예 |
| `out` | `out` | 아니요 | 예 |
| `out` | 설정되지 않음 | 아니요 | 아니요 |

다음 쿠키는 동의 구성이 허용하면 설정됩니다.

| 이름 | 최대 나이 | 설명 |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000(395일) | [`idMigrationEnabled`](../configure/idmigrationenabled.md)이(가) 활성화된 경우 표시됩니다. 사이트의 일부 부분이 `visitor.js`을(를) 사용하는 동안 Web SDK로 전환하는 데 도움이 됩니다. |
| **Demdex 쿠키** | 15552000(180일) | ID 동기화가 활성화된 경우 표시됩니다. Audience Manager은 사이트 방문자에게 고유 ID를 할당하도록 이 쿠키를 설정합니다. demdex 쿠키는 Audience Manger 가 방문자 식별, ID 동기화, 세그먼테이션, 모델링, 보고 등과 같은 기본 기능을 수행하는 데 도움이 됩니다. |
| **kndctr_orgid_cluster** | 1800(30분) | 현재 사용자의 요청을 처리하는 Edge Network 영역을 저장합니다. Edge Network이 요청을 올바른 영역으로 라우팅할 수 있도록 URL 경로에 영역이 사용됩니다. 사용자가 다른 IP 주소 또는 다른 세션에 연결하는 경우 요청이 다시 가장 가까운 영역으로 라우팅됩니다. |
| **kndct_orgid_identity** | 34128000(395일) | ECID 및 ECID와 관련된 기타 정보를 저장합니다. |
| **kndctr_orgid_consent** | 15552000(180일) | 웹 사이트에 대한 사용자 동의 환경 설정을 저장합니다. |
| **s_ecid** | 63115200(2년) | Experience Cloud ID([!DNL ECID]) 또는 MID의 복사본을 포함합니다. MID는 `s_ecid=MCMID\|<ECID>` 구문 뒤에 오는 키-값 쌍에 저장됩니다. |

## 웹 SDK 태그 확장을 사용하여 기본 동의 설정

[태그 확장을 구성](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)할 때 **[!UICONTROL 기본 동의]**&#x200B;에서 원하는 라디오 단추를 선택합니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 확장]**(으)로 이동한 다음 [!UICONTROL Adobe Experience Platform Web SDK] 카드에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.
1. [!UICONTROL 개인 정보] 섹션까지 아래로 스크롤한 다음 원하는 **[!UICONTROL 기본 동의]**&#x200B;를 선택합니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 변경 내용을 게시합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 기본 동의 설정

`configure` 명령을 실행할 때 `defaultConsent` 문자열 속성을 원하는 동의 수준으로 설정하십시오. 이 속성은 대/소문자를 구분하며 `"in"`, `"out"` 및 `"pending"` 세 가지 값만 지원합니다. 다른 값을 사용하려고 하면 라이브러리에서 오류가 발생합니다.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
