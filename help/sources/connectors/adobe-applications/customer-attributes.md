---
keywords: Experience Platform;홈;인기 항목;고객 속성 커넥터
solution: Experience Platform
title: 고객 속성 소스 커넥터 개요
topic-legacy: overview
description: API 또는 사용자 인터페이스를 사용하여 고객 속성을 Adobe Experience Platform에 연결하는 방법을 알아봅니다
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 8%

---

# 고객 속성 커넥터

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) Experience Cloud에서 고객 관계 관리(CRM) 데이터베이스에서 캡처한 엔터프라이즈 데이터를 업로드할 수 있습니다. 데이터를 Experience Cloud의 고객 속성 데이터 소스에 업로드한 다음 Adobe Analytics 및 Adobe Target에서 데이터를 사용할 수 있습니다.

Experience Platform은 [!DNL Customer Attributes] 프로필 데이터를 Adobe Experience Platform에 수집하는 데 대한 지원을 제공합니다.

## 데이터 세트 및 스키마

[!DNL Customer Attributes] 소스는 랜딩할 데이터에 대한 데이터 집합을 자동으로 만듭니다. 이 자동 생성된 데이터 세트는 수정되었으며 수동으로 선택할 수 없습니다. 또한 소스는 입력 데이터 소스를 기반으로 데이터 세트에 대한 스키마를 자동으로 만듭니다. 이 프로세스에는 스키마와 소스 데이터 간에 필요한 매핑을 자동으로 만드는 작업도 포함됩니다.

## ID

데이터 세트의 기본 ID는 소스 데이터의 CSV 파일의 첫 번째 열에 포함됩니다. [!DNL Customer Attributes] 소스는 ID가 항상 [[!DNL Identity Service]](../../../identity-service/home.md)에서 지원하는 시스템에서 생성한 네임스페이스인 [`CORE` 네임스페이스](../../../identity-service/namespaces.md)에 매핑된다고 가정합니다.

[!DNL Customer Attributes] 소스를 사용할 때에는 ID에 대한 기존 네임스페이스를 선택할 수 없습니다. [!DNL Customer Attributes] 에서는 스키마의 기본 ID가 항상 ID 맵에 있다고 간주하기 때문입니다. [!DNL Customer Attributes] 그런 다음 자동화된 방식으로 소스 ID를 id 맵 UUID에 매핑합니다.

[!DNL Customer Attributes] 데이터를 다른 [!DNL Profile] 데이터 세트에 연결하려면 해당 데이터와 ID가 Experience Cloud ID에 일치할 수 있어야 합니다.

[웹 SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [Mobile SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity) 또는 [Experience Cloud ID 서비스 API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=ko-KR)를 사용하여 방문자에 대한 Experience Cloud ID를 설정하여 `CORE` 네임스페이스를 설정할 수 있습니다.

[!DNL Customer Attributes] 파일은 더 이상 다른 ID 관계를 채우지 않습니다. 예를 들어 [!DNL Customer Attributes] 소스 데이터 세트에 **이메일** 및 **충성도 ID** 필드가 포함된 경우 이러한 필드를 [!DNL Identity Service]로 처리하려면 스키마에서 ID 필드로 레이블이 지정되어야 합니다.

자세한 내용은 [UI에서 [!DNL Customer Attributes] 소스 연결 만들기에 대한 자습서를 참조하십시오.](../../tutorials/ui/create/adobe-applications/customer-attributes.md)
