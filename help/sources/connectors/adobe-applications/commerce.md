---
title: Adobe Commerce 소스 커넥터
description: Adobe Commerce 소스를 사용하여 상거래 데이터를 Experience Platform으로 가져오는 방법에 대해 알아봅니다.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: 8249de4c78810a4cee245fa9c48b91c210aeb0a4
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# Adobe Commerce

Adobe Commerce은 온라인 및 물리적 공간에서 고객 중심의 디지털 상거래 경험을 통해 가맹점과 브랜드가 매출을 가속화할 수 있도록 하는 애자일 B2B 및 B2C 상거래 플랫폼입니다.

Adobe Experience Platform 소스는 Adobe Commerce 통합을 지원하여 판매자가 Experience Platform 에지 네트워크로 상점 및 백오피스 데이터를 전송하여 Adobe Analytics 및 Adobe Target과 같은 다른 Adobe Experience Cloud 제품에서 사용할 수 있도록 합니다 [!DNL Commerce] 데이터.

* **Storefront 이벤트**: 다음과 같은 쇼핑객 상호 작용 캡처 `View Page`, `View Product`, 및 `Add to Cart`. B2B 판매자를 위해 상점 이벤트도 캡처합니다. [구매요청 목록](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **백오피스 이벤트**: 주문, 취소, 환불, 배송 또는 완료 여부 등 주문 상태에 대한 정보를 캡처합니다.

>[!NOTE]
>
>Adobe Commerce에서 캡처된 데이터에는 PII(개인 식별 정보)가 포함되지 않습니다. 쿠키 ID 및 IP 주소와 같은 모든 사용자 식별자는 엄격히 익명으로 처리됩니다.

## 전제 조건

Adobe Commerce을 Experience Platform에 연결하려면 다음 조건을 충족해야 합니다.

* Adobe Commerce 2.4.3 이상
* 유효한 Adobe ID 및 조직 ID.
* 액세스 권한: [Adobe 클라이언트 데이터 레이어 확장](../../../tags/extensions/client/client-data-layer/overview.md). 이 확장은 상점 이벤트 데이터를 수집하는 데 필요합니다.
* 다른 Adobe DX 제품에 대한 자격.

## 온보딩 단계

Adobe Commerce 소스 계정을 완전히 온보딩하려면 해당 설명서와 함께 아래에 설명된 단계를 수행합니다.

* [Experience Platform 커넥터 확장 설치](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html) Adobe Commerce용 에서 커넥터 확장을 다운로드할 수 있습니다. [Adobe 마켓플레이스](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Connector 확장을 성공적으로 설치한 후 Experience Cloud에서 Adobe 계정에 로그인하고 [조직 ID 확인](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). 이 ID는 공급된 Experience Cloud 회사와 연결되어 있습니다. 24자 영숫자 문자열로 포맷되며 필수 항목이 포함됩니다 `@AdobeOrg`.
* 다음으로, Commerce별 필드 그룹으로 XDM(Experience Data Model) 스키마를 만들거나 업데이트합니다. XDM 스키마에 상거래 특정 필드 그룹을 추가하는 방법에 대한 자세한 단계는 의 안내서를 참조하십시오 [xdm 스키마에 필드 그룹 추가](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html).
* 스키마가 구성되면 새 스키마를 기반으로 하여 데이터 세트를 만들어야 합니다. 그러면 이 데이터 세트에는 [!DNL Commerce] 전송하는 데이터입니다. 의 데이터 세트를 만드는 방법에 대한 자세한 단계 [!DNL Commerce] 데이터, 다음에 대한 안내서 읽기 [Experience Platform에 데이터 보내기](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* 그런 다음 데이터 스트림을 만들고 Commerce 관련 필드 그룹이 포함된 XDM 스키마를 선택합니다. 데이터스트림에 대한 자세한 내용은 [데이터스트림 개요](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=ko-KR).
* 그런 다음 Adobe Commerce 인스턴스를 [Commerce Services 커넥터](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). 이를 통해 상거래 인스턴스를 SaaS(Software as a Service)로 배포할 수 있습니다.
* 앞에서 설명한 모든 구성이 완료되면 이제 를 사용하여 Commerce Services 커넥터와 Experience Platform 커넥터를 모두 구성하여 Experience Platform에 연결할 수 있습니다. [!DNL Commerce Admin]. 이 마지막 단계에 대한 자세한 내용은 의 안내서를 참조하십시오 [Experience Platform에 상거래 데이터 연결](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html).
