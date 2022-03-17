---
title: Marketo Engage 대상
description: Marketo Engage은 마케팅, 광고, 분석 및 상거래를 위한 유일한 CXM(엔드 투 엔드 고객 경험 관리) 솔루션입니다. CRM 리드 관리 및 고객 참여에서 계정 기반 마케팅 및 매출 기여도에 이르는 활동을 자동화하고 관리할 수 있습니다.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# Marketo Engage 대상 {#beta-marketo-engage-destination}

## 개요 {#overview}

Marketo Engage은 마케팅, 광고, 분석 및 상거래를 위한 유일한 CXM(엔드 투 엔드 고객 경험 관리) 솔루션입니다. CRM 리드 관리 및 고객 참여에서 계정 기반 마케팅 및 매출 기여도에 이르는 활동을 자동화하고 관리할 수 있습니다.

대상을 사용하면 마케터가 Adobe Experience Platform에서 만든 세그먼트를 정적 목록으로 표시할 Marketo에 푸시할 수 있습니다.

## 지원되는 ID {#supported-identities}

| Target ID | 설명 |
|---|---|
| ECID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스를 다음 별칭으로 참조할 수도 있습니다. &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. 다음 문서를 참조하십시오. [ECID](/help/identity-service/ecid.md) 추가 정보. |
| 이메일 | 이메일 주소를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 한 사람에게 연결되므로 다른 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>에서 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 대상 활성화 워크플로우의 경우 *필수* id 및 를 매핑합니다. *옵션* 속성을 매핑하는 데 사용됩니다. ID 네임스페이스 탭에서 이메일 및/또는 ECID를 매핑하는 것은 Marketo에서 해당 사람이 일치하는지 확인하는 데 가장 중요한 작업입니다. 이메일을 매핑하면 가장 높은 일치율을 보장합니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | Marketo Engage 대상에 사용되는 식별자(이메일, ECID)로 세그먼트(대상)의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 대상 설정 및 세그먼트 활성화 {#set-up}

대상을 설정하고 세그먼트를 활성화하는 방법에 대한 자세한 내용은 [Marketo 정적 목록에 Adobe Experience Platform 세그먼트 푸시](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) ( Marketo 설명서)를 참조하십시오.

아래 비디오에서는 Marketo 대상을 구성하고 세그먼트를 활성화하는 방법을 보여줍니다.

>[!NOTE]
>
>Experience Platform 사용자 인터페이스는 자주 업데이트되며 이 비디오를 기록한 후 변경되었을 수 있습니다. 최신 정보는 위에 링크된 안내서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
