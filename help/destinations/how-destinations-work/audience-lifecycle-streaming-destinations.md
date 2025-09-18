---
title: Experience Platform 및 스트리밍 대상의 고객 라이프사이클
description: Experience Platform의 대상 이름 및 매핑이 스트리밍 대상 플랫폼에 어떻게 반영되는지 알아봅니다.
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---


# 스트리밍 대상의 대상 라이프사이클

이 페이지에서는 Experience Platform의 대상 이름 업데이트 및 매핑을 스트리밍 대상 플랫폼과 동기화하는 방법을 설명합니다. Experience Platform에서 대상 이름을 수정하거나 대상 매핑을 제거하면 대상 플랫폼의 기능에 따라 동작이 달라집니다.

이러한 차이점을 이해하는 것은 대상 라이프사이클 작업을 관리하고 대상 플랫폼이 Experience Platform 대상의 현재 상태를 반영하도록 하는 데 중요합니다.

## 대상자 이름 전달 동작 {#audience-name-propagation}

스트리밍 대상에 대상을 활성화하면 초기 활성화 중에 대상 이름이 대상으로 전송됩니다. 그러나 대상 이름 업데이트 동작은 대상에 따라 다릅니다.

* **[대상 이름 업데이트를 지원하는 대상](#name-update-supported)**: Experience Platform에서 대상 이름을 변경하면 업데이트된 이름이 이러한 대상으로 자동으로 전파됩니다.
* **[대상 이름 업데이트를 지원하지 않는 대상](#name-update-not-supported)**: Experience Platform에서 대상 이름을 변경하면 대상은 초기 활성화에서 원래 이름을 계속 사용합니다.

### 대상자 이름 업데이트를 지원하는 대상 {#name-update-supported}

다음 스트리밍 대상은 Experience Platform에서 대상 이름을 수정할 때 자동 대상 이름 업데이트를 지원합니다.

* [Acxiom 대상 연결](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [봄보라](../catalog/advertising/bombora.md)
* [크리테오](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Demandbase 사용자](../catalog/advertising/demandbase-people.md)
* [Experience Cloud 대상자](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook 사용자 지정 대상자](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [(회사) LinkedIn 일치하는 대상](../catalog/social/linkedin-b2b.md)
* [LinkedIn 일치하는 대상](../catalog/social/linkedin.md)
* [(기존) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [스냅](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Twitter 사용자 지정 대상](../catalog/social/twitter.md)
* [야후 데이터 X](../catalog/advertising/datax.md)

### 대상자 이름 업데이트를 지원하지 않는 대상 {#name-update-not-supported}

위에 나열되지 않은 대상의 경우 대상 이름은 초기 활성화 후 정적으로 유지됩니다. 이러한 대상의 대상 이름을 업데이트해야 하는 경우 다음을 수행해야 합니다.

1. 원하는 이름으로 Experience Platform에서 새 대상 만들기
2. 대상에 대한 새 대상 활성화

>[!TIP]
>
>혼동을 방지하려면 첫 번째 활성화의 수사적 대상 이름을 사용하십시오. 특히 대상 이름 업데이트를 지원하지 않는 대상으로 활성화할 때 더욱 그러합니다.

## 대상자 제거를 지원하는 대상 {#support-removal}

스트리밍 대상에서 대상을 제거(매핑 해제)하면 Experience Platform은 대상 플랫폼에서 해당 대상을 제거하려고 합니다. 그러나 모든 대상이 이 기능을 지원하는 것은 아닙니다.

다음 스트리밍 대상은 대상에서 대상을 매핑 해제할 때 자동 대상 제거를 지원합니다.

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [(회사) LinkedIn 일치하는 대상](../catalog/social/linkedin-b2b.md)
* [(기존) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora 계정 대상자](../catalog/advertising/bombora.md)
* [크리테오](../catalog/advertising/criteo.md)
* [Experience Cloud 대상자](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [LinkedIn 일치하는 대상](../catalog/social/linkedin.md)
* [LiveRamp - 배포](../catalog/advertising/liveramp-distribution.md)
* [Mailchimp 관심 범주](../catalog/email-marketing/mailchimp-interest-categories.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [Salesforce Marketing Cloud 계정 참여](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [스냅](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Twitter 사용자 지정 대상](../catalog/social/twitter.md)
* [야후 데이터 X](../catalog/advertising/datax.md)

### 대상자 제거를 지원하지 않는 대상

위에 나열되지 않은 대상의 경우 대상에서 대상을 매핑 해제하면 Experience Platform에서는 매핑만 제거합니다. 대상 플랫폼의 대상은 파트너 플랫폼에서 수동으로 삭제할 때까지 활성 상태로 유지됩니다.
