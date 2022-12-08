---
title: Marketo Engage 대상
description: Marketo Engage은 마케팅, 광고, 분석 및 상거래를 위한 유일한 CXM(엔드 투 엔드 고객 경험 관리) 솔루션입니다. CRM 리드 관리 및 고객 참여에서 계정 기반 마케팅 및 매출 기여도에 이르는 활동을 자동화하고 관리할 수 있습니다.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: e68bbc07f7d2e4e05b725cbef37a1810a5825742
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 2%

---

# Marketo Engage 대상 {#beta-marketo-engage-destination}

## 대상 변경 로그 {#changelog}

>[!IMPORTANT]
>
>의 [향상된 Marketo V2 대상 커넥터](/help/release-notes/2022/july-2022.md#destinations)이제 대상 카탈로그에 Marketo 카드 2개가 표시됩니다.
>* 에 데이터를 이미 활성화 중이라면 **[!UICONTROL Marketo V1]** 대상: 새 데이터 흐름 만들기 **[!UICONTROL Marketo V2]** 기존 데이터 흐름을 대상으로 대상 및 삭제 **[!UICONTROL Marketo V1]** 2023년 2월 대상. 해당 날짜의 **[!UICONTROL Marketo V1]** 대상 카드가 제거됩니다.
>* 데이터 흐름을 아직 만들지 않았다면 **[!UICONTROL Marketo V1]** 대상, 새 **[!UICONTROL Marketo V2]** 데이터를 Marketo에 연결하고 내보낼 수 있는 카드입니다.


![나란히 보기에 있는 두 Marketo 대상 카드의 이미지입니다.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Marketo V2 대상의 개선 사항은 다음과 같습니다.

* 에서 **[!UICONTROL 세그먼트 예약]** 활성화 작업 과정의 단계인 Marketo V1에서 수동으로 **매핑 ID** 데이터를 Marketo으로 성공적으로 내보내기 위해 다음을 수행하십시오. 이 수동 단계는 Marketo V2에서 더 이상 필요하지 않습니다.
* 에서 **[!UICONTROL 매핑]** 활성화 워크플로우 단계의 Marketo V1에서는 XDM 필드를 Marketo의 세 개의 대상 필드에만 매핑할 수 있었습니다. `firstName`, `lastName`, 및 `companyName`. 이제 Marketo V2 릴리스를 통해 XDM 필드를 Marketo의 더 많은 필드에 매핑할 수 있습니다. 자세한 내용은 [지원되는 특성](#supported-attributes) 섹션을 참조하십시오.

## 개요 {#overview}

[!DNL Marketo Engage] 는 마케팅, 광고, 분석 및 상거래를 위한 유일한 CXM(엔드 투 엔드 고객 경험 관리) 솔루션입니다. CRM 리드 관리 및 고객 참여에서 계정 기반 마케팅 및 매출 기여도에 이르는 활동을 자동화하고 관리할 수 있습니다.

대상을 사용하면 마케터가 Adobe Experience Platform에서 만든 세그먼트를 정적 목록으로 표시할 Marketo에 푸시할 수 있습니다.

## 지원되는 ID 및 속성 {#supported-identities-attributes}

>[!NOTE]
>
>에서 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 대상 활성화 워크플로우의 경우 *필수* id 및 를 매핑합니다. *옵션* 속성을 매핑하는 데 사용됩니다. ID 네임스페이스 탭에서 이메일 및/또는 ECID를 매핑하는 것은 Marketo에서 해당 사람이 일치하는지 확인하는 데 가장 중요한 작업입니다. 이메일을 매핑하면 가장 높은 일치율을 보장합니다.

### 지원되는 ID {#supported-identities}

| Target ID | 설명 |
|---|---|
| ECID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스를 다음 별칭으로 참조할 수도 있습니다. &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. 다음 문서를 참조하십시오. [ECID](/help/identity-service/ecid.md) 추가 정보. |
| 이메일 | 이메일 주소를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 한 사람에게 연결되므로 다른 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

### 지원되는 특성 {#supported-attributes}

Experience Platform의 속성을 Marketo에서 조직에서 액세스할 수 있는 속성에 매핑할 수 있습니다. Marketo에서 [API 요청 설명](https://developers.marketo.com/rest-api/lead-database/leads/#describe) 를 입력하여 조직에서 액세스할 수 있는 속성 필드를 검색합니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 에서 사용되는 식별자(이메일, ECID)로 세그먼트(대상)의 모든 구성원을 내보냅니다 [!DNL Marketo Engage] 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 대상 설정 및 세그먼트 활성화 {#set-up}

>[!IMPORTANT]
> 
>* 대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions).
>* 데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.


대상을 설정하고 세그먼트를 활성화하는 방법에 대한 자세한 내용은 [Marketo 정적 목록에 Adobe Experience Platform 세그먼트 푸시](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) ( Marketo 설명서)를 참조하십시오.

아래 비디오에서는 Marketo 대상을 구성하고 세그먼트를 활성화하는 방법을 보여줍니다.

>[!IMPORTANT]
>
>이 비디오는 현재 기능을 완전히 반영하지는 않습니다. 최신 정보는 위에 링크된 안내서를 참조하십시오. 비디오의 다음 부분이 구식입니다.
> 
>* Experience Platform UI에서 사용해야 하는 대상 카드는 **[!UICONTROL Marketo V2]**.
>* 비디오가 새 **[!UICONTROL 개인 만들기]** 대상에 연결 워크플로우의 선택기 필드.
>* 비디오에서 호출된 두 가지 제한 사항은 더 이상 적용되지 않습니다. 이제 비디오가 기록될 때 지원되는 세그먼트 멤버십 정보 외에 다른 여러 프로필 속성 필드를 매핑할 수 있습니다. 세그먼트 구성원을 Marketo 정적 목록에 아직 없는 Marketo으로 내보낼 수 있으며, 이러한 구성원이 목록에 추가됩니다.
>* 에서 **[!UICONTROL 세그먼트 단계 예약]** 활성화 워크플로우의 경우, Marketo V1에서 수동으로 **[!UICONTROL 매핑 ID]** 데이터를 Marketo으로 성공적으로 내보내기 위해 다음을 수행하십시오. 이 수동 단계는 Marketo V2에서 더 이상 필요하지 않습니다.


>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
