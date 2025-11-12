---
title: Zendesk Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Zendesk를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 8%

---

# [!DNL Zendesk]

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집하는 동시에 Experience Platform 서비스를 사용하여 수신 데이터를 구조화하고 레이블을 지정하며 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 고객 성공 애플리케이션에서 데이터를 수집하는 데 대한 지원을 제공합니다. 고객 성공 공급자에 대한 지원은 [!DNL Zendesk]입니다.

이 Adobe Experience Platform [소스](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ko)는 추가 처리를 위해 Zendesk에서 Experience Platform으로 사용자 정보를 반환하는 [Zendesk 검색 API > 검색 결과 내보내기](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results)를 활용합니다.

## 허용 목록에 추가하다 IP 주소

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

## [!DNL Zendesk] 계정 인증

[!DNL Zendesk]은(는) 전달자 토큰을 인증 메커니즘으로 사용하여 [!DNL Zendesk] API와 통신합니다.

이 섹션에서는 [!DNL Zendesk] 계정을 인증하기 위해 완료해야 하는 필수 조건 단계를 간략하게 설명합니다.

* [!DNL Zendesk] 계정을 인증하는 첫 번째 단계는 [!DNL Zendesk] 지원 계정이 있는지 확인하는 것입니다. 아직 등록하지 않은 경우 [[!DNL Zendesk] 등록 페이지](https://www.zendesk.com/register/)를 참조하여 Zendesk 계정을 등록하고 만드십시오.
* 등록했으면 [[!DNL Zendesk] 웹 사이트](https://www.zendesk.com/login/)로 이동하여 **하위 도메인**&#x200B;을 제공하세요.
* 그런 다음 **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**&#x200B;을(를) 선택합니다.
* 마지막으로 **[!DNL API token]** 섹션에서 API 토큰을 검색합니다.

![Zendesk API 토큰](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

하위 도메인을 검색하는 방법에 대한 자세한 내용은 [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->)을(를) 참조하십시오. API 토큰 생성에 대한 자세한 내용은 [[!DNL Zendesk] 새 API 토큰 생성에 대한 안내서](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>)를 참조하십시오.

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Zendesk]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

## API를 사용하여 [!DNL Zendesk]을(를) Experience Platform에 연결

* [흐름 서비스 API를 사용하여  [!DNL Zendesk] 에 대한 소스 연결 및 데이터 흐름을 만듭니다.](../../tutorials/api/create/customer-success/zendesk.md)

## UI를 사용하여 [!DNL Zendesk]을(를) Experience Platform에 연결

* [UI에서  [!DNL Zendesk &#x200B;]소스 연결 만들기](../../tutorials/ui/create/customer-success/zendesk.md)
* [UI에서 고객 성공 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/customer-success.md)
