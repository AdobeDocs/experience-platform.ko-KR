---
title: 위치 힌트
description: 이 문서에서는 최종 사용자 요청이 항상 동일한 서버로 라우팅될 수 있도록 Edge Network Server API에서 위치 힌트가 작동하는 방식을 설명합니다.
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 80c527ab3c82e01fe19e5003e224d63e79b23bdc
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 위치 힌트

## 개요 {#overview}

다음 [!DNL Adobe Experience Platform Edge Network] 은 여러 개의 전역으로 분산된 서버를 사용하여 최종 사용자 위치에 관계없이 빠른 응답 시간을 보장합니다. 또한 DNS 기반 라우팅을 사용하여 요청이 항상 최종 사용자에게 가장 가까운 Edge Network 위치로 라우팅되도록 합니다.

최종 사용자가 VPN에 연결하거나 세션 중에 모바일 장치의 네트워크 유형을 전환하는 경우 Edge Network 요청을 종종 다른 위치로 라우팅할 수 있습니다. Adobe Experience Platform 및 Adobe Experience Cloud 솔루션은 Edge Network에 최종 사용자 프로필 정보를 저장하기 때문에 서버 간 중간 세션 라우팅이 문제가 될 수 있습니다.

여기에서 위치 힌트가 작동합니다.

최종 사용자가 항상 현재 프로필 데이터가 포함된 Edge Network 지역 서버와 상호 작용하도록 하기 위해, 위치 힌트 기능은 Edge Network에 대한 모든 요청이 세션의 첫 번째 요청이 이루어진 동일한 서버로 전송되도록 합니다. 따라서 사용자는 세션 과정에서 발생할 수 있는 네트워크 변경 사항에 관계없이 일관된 경험을 유지할 수 있습니다.

## 위치 힌트 사용

위치 힌트는 아래 예와 같이, 초기 Edge Network 요청의 응답과 모든 후속 요청에 포함됩니다.

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

다음 `EdgeNetwork` 범위에는 Edge Network가 그에 따라 후속 요청을 라우팅하는 데 필요한 모든 관련 정보가 포함되어 있습니다. Edge 네트워크에 대한 초기 요청과 각 후속 요청에 대한 응답으로 핸들에는 다음 유형의 섹션이 있습니다. `locationHint:result`.

와 관련된 힌트 `EdgeNetwork` 범위는 다음 값 중 하나를 포함할 수 있습니다.

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API 형식**

후속 요청이 올바로 라우팅되도록 하려면 기본 경로 사이에 있는 후속 API 호출의 URL 경로에 위치 힌트를 삽입합니다(일반적으로) `ee`, 및 `v2` API 버전.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## 쿠키에 위치 힌트 저장 {#storing-hints-in-cookies}

Edge Network에서 반환되는 위치 힌트가 세션 기간 동안 지속되도록 하기 위해 쿠키에 포함된 쿠키 수명과 함께 위치 힌트 값을 저장할 수 있습니다. `ttlSeconds` 필드(일반적으로 1,800초).

대부분의 쿠키와 마찬가지로 Edge Network의 응답이 있을 때마다 이 쿠키의 수명을 연장해야 합니다. 웹 SDK와의 호환성을 최대한 보장하려면 쿠키 이름을 사용하십시오 `kndctr_{IMSORG}_AdobeOrg_cluster`. IMS 조직 ID는 일반적으로 다음으로 끝남 `@AdobeOrg`. 다음 `@` 쿠키가 올바른 형식인지 확인하려면 값을 밑줄로 변환해야 합니다.
