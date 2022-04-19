---
keywords: advertising; criteo;
title: Criteo connection
description: Criteo powers trusted and impactful advertising to bring richer experiences to every consumer across the open internet. With the world's largest commerce data set and best-in-class AI, Criteo ensures each touchpoint across the shopping journey is personalized to reach customers with the right ad, at the right time.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 36da42b184450cfaf12b097f982234d628681430
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 3%

---

# (Beta) Criteo connection

## 개요 {#overview}

>[!IMPORTANT]
>
>This documentation page was created by Criteo. This is currently a beta product and functionality is subject to change. [](mailto:criteoTechnicalPartnerships@criteo.com)

Criteo powers trusted and impactful advertising to bring richer experiences to every consumer across the open internet. With the world&#39;s largest commerce data set and best-in-class AI, Criteo ensures each touchpoint across the shopping journey is personalized to reach customers with the right ad, at the right time.

## 전제 조건 {#prerequisites}

* [](https://marketing.criteo.com)
* You&#39;ll need your Criteo Advertiser ID (ask your Criteo contact if you don&#39;t have this ID).

## 제한 사항 {#limitations}

* Criteo does not currently support removing users from audiences.
* [!DNL SHA-256][!DNL SHA-256] Please do not send any PII (Personal Identifiable Information, such as individual&#39;s names or phone numbers).

![전제 조건](../../assets/catalog/advertising/criteo/prerequisites.png)

## Supported identities {#supported-identities}

Criteo supports the activation of identities described in the table below. [](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)

| Target Identity | 설명 | 고려 사항 |
| --- | --- | --- |
| `email_sha256` | Email addresses hashed with the SHA-256 algorithm | Both plain text and SHA-256-hashed email addresses are supported by Adobe Experience Platform.  |

## Export type and frequency {#export-type-frequency}

Refer to the table below for information about the destination export type and frequency.

| 항목 | 유형 | 참고 |
| --- | --- | --- |
| Export type | 세그먼트 내보내기 | [!DNL Criteo] |
| Export frequency | Streaming | Streaming destinations are &quot;always on&quot; API-based connections. As soon as a profile is updated in Experience Platform based on segment evaluation, the connector sends the update downstream to the destination platform. [](../../destination-types.md#streaming-destinations) |

## 사용 사례 {#use-cases}

[!DNL Criteo][!DNL Criteo]

### Use case 1 : Get traffic

Showcase your business with relevant product offers and flexible creatives. With intelligent product recommendations, your ads will automatically feature the products most likely to trigger visits and engagement. Flexible targeting allows you to build audiences from Criteo&#39;s commerce data set or from your own prospect lists and Adobe CDP segments.

### Use case 2 : Increase website conversions

When visitors leave your website, remind them what they&#39;re missing with retargeting ads that increase conversions by showing special deals and hyper-relevant offers, wherever they go next. Connect your Adobe CDP segment to re-engage existing customers or target consumers similar to your most loyal shoppers.

## Connect to Criteo {#connect}

[](../../ui/connect-destination.md)

### Authenticate to Criteo

Steps to connect are as follows:

1. Log in to Adobe Experience Platform and connect to the Criteo destination.

   ![로그인합니다](../../assets/catalog/advertising/criteo/connect-destination.png)

1. You will be redirected to Criteo to authorize the connection. You may need to first log in with your Criteo credentials:

   ![](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![](../../assets/catalog/advertising/criteo/log-in-3.png)


### Connection parameters {#connection-parameters}

After authenticating to the destination, please fill in the following connection parameters.

![](../../assets/catalog/advertising/criteo/connection-parameters.png)

| 필드 | 설명 | 필수 여부 |
| --- | --- | --- |
| 이름 | A name to help you recognize this destination in the future. [!DNL Audience] | 예 |
| 설명 | A description to help you identify this destination in the future. | 아니요 |
| API Version | Criteo API Version. Please select Preview. | 예 |
| Advertiser ID | Criteo Advertiser ID of your organization. Please contact your Criteo account manager to obtain this information. | 예 |

## Activate segments to this destination {#activate-segments}

[](../../ui/activate-segment-streaming-destinations.md)

## Exported data {#exported-data}

[](https://marketing.criteo.com/audience-manager/dashboard)

[!DNL Criteo]

```json
{ 
  "data": { 
    "type": "ContactlistWithUserAttributesAmendment", 
    "attributes": { 
      "operation": "add", 
      "identifierType": "sha256email", 
      "identifiers": [ 
        { 
          "identifier": "1c8494bbc4968277345133cca6ba257b9b3431b8a84833a99613cf075a62a16d", 
          "attributes": [{ "key": "customValue", "value": "1" }] 
        } 
      ] 
    } 
  } 
} 
```

## Data usage and governance {#data-usage}

All Adobe Experience Platform destinations are compliant with data usage policies when handling your data. [](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en)

## 추가 리소스

* [](https://help.criteo.com/kb/en)
* [](https://developers.criteo.com/marketing-solutions/v2022.04/reference/modifyaudienceuserswithattributes)
