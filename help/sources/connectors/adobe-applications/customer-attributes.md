---
keywords: Experience Platform;홈;인기 항목;고객 속성 커넥터
solution: Experience Platform
title: 고객 속성 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 고객 속성을 Adobe Experience Platform에 연결하는 방법을 알아봅니다
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 139d6a6632532b392fdf8d69c5c59d1fd779a6d1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 10%

---

# 고객 속성 커넥터

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) Experience Cloud에서 고객 관계 관리(CRM) 데이터베이스에서 캡처한 엔터프라이즈 데이터를 업로드할 수 있습니다. 데이터를 Experience Cloud의 고객 속성 데이터 소스에 업로드한 다음 Adobe Analytics 및 Adobe Target에서 데이터를 사용할 수 있습니다.

Experience Platform은 수집을 지원합니다 [!DNL Customer Attributes] 프로필 데이터를 Adobe Experience Platform에 넣습니다.

## 데이터 세트 및 스키마

다음 [!DNL Customer Attributes] 소스는 데이터를 연결할 데이터 세트를 자동으로 만듭니다. 이 자동 생성된 데이터 세트는 고정되며 수동으로 선택할 수 없습니다. 소스는 또한 입력 데이터 소스를 기반으로 데이터 세트에 대한 스키마를 자동으로 만듭니다. 이 프로세스에는 스키마와 소스 데이터 간에 필요한 매핑을 자동으로 만드는 작업도 포함됩니다.

## ID

데이터 세트의 기본 ID는 소스 데이터의 CSV 파일의 첫 번째 열에 포함되어 있습니다. 다음 [!DNL Customer Attributes] 소스는 id가 항상 [`CORE` 네임스페이스](../../../identity-service/namespaces.md)에서 지원하는 시스템 생성 네임스페이스 [[!DNL Identity Service]](../../../identity-service/home.md).

을 사용할 때는 ID에 대한 기존 네임스페이스를 선택할 수 없습니다. [!DNL Customer Attributes] 소스 이유 [!DNL Customer Attributes] 스키마에 대한 기본 id가 항상 id 맵에 있다고 가정합니다. [!DNL Customer Attributes] 그런 다음 자동화된 방식으로 소스 ID와 ID 맵 UUID의 매핑을 생성합니다.

대상 [!DNL Customer Attributes] 다른 항목에 연결할 데이터 [!DNL Profile] 데이터 세트, 데이터 및 id는 Experience Cloud ID와 일치시킬 수 있어야 합니다.

다음을 설정할 수 있습니다. `CORE` 네임스페이스: 을 사용하여 방문자의 Experience Cloud ID를 설정하는 경우 [웹 SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/)또는 [Experience Cloud ID 서비스 API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

다음 [!DNL Customer Attributes] 파일이 다른 id 관계를 더 이상 채우지 않습니다. 예를 들어 [!DNL Customer Attributes] 소스 데이터 세트에 포함된 **이메일** 및 a **고객 충성도 ID** 필드를 선택한 다음 스키마에서 해당 필드를 id 필드로 레이블 지정하여 [!DNL Identity Service].

다음 튜토리얼 참조: [만들기 [!DNL Customer Attributes] UI의 소스 연결](../../tutorials/ui/create/adobe-applications/customer-attributes.md) 추가 정보.
