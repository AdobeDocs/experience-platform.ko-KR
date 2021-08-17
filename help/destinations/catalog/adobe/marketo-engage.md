---
title: Marketo Engage 대상
description: Marketo Engage은 마케팅, 광고, 분석 및 상거래를 위한 유일한 CXM(엔드 투 엔드 고객 경험 관리) 솔루션입니다. CRM 리드 관리 및 고객 참여에서 계정 기반 마케팅 및 매출 기여도에 이르는 활동을 자동화하고 관리할 수 있습니다.
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---


# (베타) Marketo Engage 대상 {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform의 Marketo Engage 대상은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

Marketo Engage은 마케팅, 광고, 분석 및 상거래를 위한 유일한 CXM(엔드 투 엔드 고객 경험 관리) 솔루션입니다. CRM 리드 관리 및 고객 참여에서 계정 기반 마케팅 및 매출 기여도에 이르는 활동을 자동화하고 관리할 수 있습니다.

세그먼트 커넥터를 사용하면 마케터가 Adobe Experience Platform에서 만든 세그먼트를 정적 목록으로 표시되는 Marketo에 푸시할 수 있습니다.

## 지원되는 ID {#supported-identities}

| Target ID | 설명 |
|---|---|
| ECID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스를 다음 별칭으로 참조할 수도 있습니다. &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. 자세한 내용은 [ECID](/help/identity-service/ecid.md)에서 다음 문서를 참조하십시오. |
| 이메일 | 이메일 주소를 나타내는 네임스페이스입니다. 이러한 유형의 네임스페이스는 종종 한 사람에게 연결되므로 다른 채널에서 해당 사용자를 식별하는 데 사용할 수 있습니다. |

## 내보내기 유형 {#export-type}

세그먼트 내보내기 - Marketo Engage 대상에 사용되는 식별자(이름, 전화번호 또는 기타)로 세그먼트(대상)의 모든 구성원을 내보냅니다.

## 설정 {#set-up}

대상 [을 설정하는 방법에 대한 지침은 여기](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en)에 있습니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모든 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)를 참조하십시오.

## 세그먼트를 이 대상에 활성화 {#activate}

대상으로 대상 세그먼트를 활성화하는 방법에 대한 지침은 [대상 세그먼트 활성화](../../ui/activate-destinations.md)를 참조하십시오.
