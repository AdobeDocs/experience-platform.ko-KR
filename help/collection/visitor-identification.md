---
title: 방문자 식별
description: Adobe Experience Platform Edge Network Server API가 방문자를 식별하는 방법을 알아봅니다
seo-description: Learn how Adobe Experience Platform Edge Network Server API identifies visitors
keywords: 에지 네트워크;게이트웨이;api;방문자;식별
exl-id: aa2f3b83-5cc8-4e02-9119-edfd5e212588
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 5%

---

# 방문자 식별

Edge Network Server API는 [자사 ID를 통한 방문자 식별([!DNL FPID])](visitor-identification-fpid.md).

모든 사용자 ID는 `identityMap` 필드 그룹. 이 필드 그룹은 AEP 웹 SDK에 포함되어 있습니다 `ExperienceEvent` 믹신

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"55613368189701342632255821452918751312",
            "authenticatedState":"ambiguous"
         }
      ],
      "CRM":[
         {
            "id":"2394509340-30453470347",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

## 장치 식별자 {#identifiers}

Edge Network에서 장치를 식별할 수 있는 방법은 여러 가지가 있습니다. 지원되는 ID에 대한 개요를 알려면 아래 표를 참조하십시오.

| ID 네임스페이스 | 에서 관리 | 설명 |
| --- | --- | --- |
| `FPID` | Customer | `FPID` 은(는) 자동으로 `ECID` Edge Network에 의해 `ECID` 도 잘 될 겁니다.  <br><br> 일관된 장치 식별을 위해 이러한 ID는 장치에서 유지되어야 하며 각 요청 시 제공되어야 합니다. 웹 상호 작용의 경우 브라우저 쿠키로 저장하는 작업이 포함됩니다. |
| `IDFA`/`GAID` | Experience Platform | 여러 애플리케이션에서 사용자를 식별할 수 있으므로 이러한 ID가 로 인코딩되지 않습니다 `ECID` 에지 네트워크에서 액세스 |

<!--
| `ECID` | Adobe | `ECID` is required when leveraging and integrating with Adobe Analytics and Adobe Audience Manager. <br><br> For consistent device identification, these IDs must be persisted on the device and supplied on each request. For web interactions, this involves storing them as browser cookies. |
-->

<!--
## Experience Edge Identity Protocol {#experience-edge-identity-protocol}

Device identities like `ECID` must be persisted on the client device and supplied on each request in the session and across sessions. Having stable device identities across multiple sessions improves the accuracy levels in your reports and allows delivering a consistent experience to the visitors.

For all non-server interactions, the Edge Network will automatically perform the following actions:

* Generate a new `ECID` when none is found on the request. This will automatically enhance the collected event with the new identity.
* Return a `state:store` instruction to the caller with the `kndctr_{$IMS_ORG_ID|url-safe}_identity` entry, which contains:
  * The [ID value](#ee-identity-format)
  * A `maxAge` value, in seconds, indicating how long the client persist the ID for

For example, let's consider the following request:

```json
{
   "events":[
      {
         "xdm":{
            "eventType":"web.webpagedetails.pageViews",
            "eventMergeId":"0772675a-1e24-44ea-a92b-0138c1d03a38",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page",
                  "pageViews":{
                     "value":1
                  }
               }
            },
            "device":{
               "screenHeight":1120,
               "screenWidth":1792,
               "screenOrientation":"landscape"
            },
            "environment":{
               "type":"browser",
               "browserDetails":{
                  "viewportWidth":1792,
                  "viewportHeight":481
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z"
         }
      }
   ]
}
```

The Edge Network response includes a `state:store` handle, which, in turn, includes an entry with the following name format: `kndctr_{$IMS_ORG_ID|url-safe}_identity`.

```json
{
   "requestId":"f5abf988-15d1-4463-a3b8-59aa0709a808",
   "handle":[
      {
         "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
         "value":"CiYzOTMyMzQ5NzU1MDY0MzIxNzc3NDEzMjY2NDA4OTIzOTExNDgyMlIRCIbghtqyLxABGAEqBElSTDHwAYbghtqyLw==",
         "maxAge":34128000
      }
   ],
   "type":"state:store"
}
```

>[!NOTE]
>
>The `kndctr_{$IMS_ORG_ID|url-safe}_` prefix is also used for other entries stored on the client device, and enables state isolation for complex integrations, which could involve multiple/different IMS organizations. While the Edge Network will filter the entries which can be used for a given datastream, in order to minimize the payload, the caller (SDK) should ideally ensure that only the relevant entries are sent.

The caller must:

* Store this value on the client device
* Supply it on subsequent calls from that device in the request `meta.state.entries[]`, as shown below:

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYzOTMyMzQ5NzU1MDY0MzIxNzc3NDEzMjY2NDA4OTIzOTExNDgyMlIRCIbghtqyLxABGAEqBElSTDHwAYbghtqyLw=="
            }
         ]
      }
   }
}
```

## Identity Protocol via cookies (web)

When using first-party domain CNAMEs for interacting with the Edge Network, the client state can be managed automatically via first-party cookies.

The caller must explicitly activate this functionality via the `meta.state.cookiesEnabled` flag:

```json
{
   "meta":{
      "state":{
         "domain":"alloystore.dev",
         "cookiesEnabled":true
      }
   }
}
```

>[!NOTE]
>
>The `meta.state.domain` is an optional value which a caller could supply, specifying the exact domain on which the cookies should be stored. When this is missing, Experience Edge can automatically infer the top-level domain from the request. Automatic client state management via browser cookies **should never be used** in a `server` interaction.

-->
