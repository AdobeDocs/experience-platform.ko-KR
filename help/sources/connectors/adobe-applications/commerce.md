---
title: Adobe Commerce Source 커넥터
description: Adobe Commerce 소스를 사용하여 상거래 데이터를 Experience Platform으로 가져오는 방법에 대해 알아봅니다.
last-substantial-update: 2023-12-13T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: 506f33e03dea5d5879808bccb82948209714926a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Adobe Commerce

Adobe Commerce은 온라인 및 물리적 공간에서 고객 중심의 디지털 상거래 경험을 통해 가맹점과 브랜드가 매출을 가속화할 수 있도록 하는 애자일 B2B 및 B2C 상거래 플랫폼입니다.

Adobe Experience Platform Sources는 Adobe Commerce 통합을 지원하므로 판매자가 Experience Platform Edge Network에 상점 및 백오피스 데이터를 보낼 수 있으므로 Adobe Analytics 및 Adobe Target과 같은 다른 Adobe Experience Cloud 제품에서 [!DNL Commerce] 데이터를 사용할 수 있습니다.

* **Storefront 이벤트**: `View Page`, `View Product` 및 `Add to Cart`과(와) 같은 쇼핑객 상호 작용을 캡처합니다. B2B 판매자의 경우 상점 이벤트도 [구매요청 목록](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>)을 캡처합니다.
* **사무실 뒷면 이벤트**: 주문, 취소, 환불, 배송 또는 완료 여부 등 주문 상태에 대한 정보를 캡처합니다.

>[!NOTE]
>
>Adobe Commerce에서 캡처된 데이터에는 PII(개인 식별 정보)가 포함되지 않습니다. 쿠키 ID 및 IP 주소와 같은 모든 사용자 식별자는 엄격히 익명으로 처리됩니다.

## 전제 조건

Adobe Commerce을 Experience Platform에 연결하려면 다음 조건을 충족해야 합니다.

* Adobe Commerce 2.4.3 이상
* 유효한 Adobe ID 및 조직 ID.
* [Adobe 클라이언트 데이터 레이어 확장](../../../tags/extensions/client/client-data-layer/overview.md)에 액세스합니다. 이 확장은 상점 이벤트 데이터를 수집하는 데 필요합니다.
* 다른 Adobe DX 제품에 대한 자격.

## 온보딩 단계

Adobe Commerce 소스 계정을 완전히 온보딩하려면 해당 설명서와 함께 아래에 설명된 단계를 수행합니다.

* Adobe Commerce용 [확장 [!DNL Data Connection] 설치](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) [Adobe 마켓플레이스](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html)에서 커넥터 확장을 다운로드할 수 있습니다.
* Connector 확장을 설치했으면 Experience Cloud에서 Adobe 계정에 로그인하고 [조직 ID를 확인](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255)합니다. 이 ID는 공급된 Experience Cloud 회사와 연결되어 있습니다. 이 ID는 24자의 영숫자 문자열로 형식이 지정되며 필수 `@AdobeOrg`을(를) 포함합니다.
* 그런 다음 Commerce 관련 필드 그룹으로 XDM(Experience Data Model) 스키마를 만들거나 업데이트합니다. XDM 스키마에 Commerce 관련 필드 그룹을 추가하는 방법에 대한 자세한 단계는 [XDM 스키마에 필드 그룹 추가](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html)에 대한 안내서를 참조하십시오.
* 스키마가 구성되면 새 스키마를 기반으로 하여 데이터 세트를 만들어야 합니다. 그러면 이 데이터 세트에는 보내는 [!DNL Commerce] 데이터가 포함됩니다. [!DNL Commerce] 데이터에 대한 데이터 집합을 만드는 방법에 대한 자세한 단계는 [Experience Platform에 데이터 보내기](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset)에 대한 안내서를 참조하십시오.
* 그런 다음 데이터 스트림을 만들고 Commerce 관련 필드 그룹이 포함된 XDM 스키마를 선택합니다. 데이터스트림에 대한 자세한 내용은 [데이터스트림 개요](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html)를 참조하십시오.
* 그런 다음 Adobe Commerce 인스턴스를 [Commerce 서비스 커넥터](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html)에 연결해야 합니다. 이를 통해 Commerce 인스턴스를 SaaS(Software as a Service)로 배포할 수 있습니다.
* 위에서 설명한 모든 구성을 완료하면 이제 [!DNL Commerce Admin]을(를) 사용하여 Commerce 서비스 커넥터와 [!DNL Data Connection] 확장을 모두 구성하여 Experience Platform에 연결할 수 있습니다. 이 마지막 단계에 대한 자세한 내용은 [Commerce 데이터를 Experience Platform에 연결](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html)에 대한 안내서를 참조하십시오.
