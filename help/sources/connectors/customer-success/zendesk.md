---
keywords: Experience Platform;홈;인기 항목;Zendesk;zendesk
solution: Experience Platform
title: Zendesk 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Zendesk를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 61b694ca5fbd3548243663b3f1bff06aaca72434
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# (베타) [!DNL Zendesk]

>[!NOTE]
>
>다음 [!DNL Zendesk] 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 서드파티 고객 성공 애플리케이션에서 데이터를 수집하는 데 대한 지원을 제공합니다. 고객 성공 공급업체에 대한 지원은 다음과 같습니다 [!DNL Zendesk].

이 Adobe Experience Platform [소스](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ko) 을 활용합니다. [Zendesk 검색 API > 검색 결과 내보내기](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 추가 처리를 위해 Zendesk의 Experience Platform으로 사용자 정보를 반환합니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

## 인증 [!DNL Zendesk] account

[!DNL Zendesk] 전달자 토큰을 인증 메커니즘으로 사용하여 [!DNL Zendesk] API.

이 섹션에서는 다음을 인증하기 위해 완료해야 하는 사전 요구 사항에 대해 설명합니다. [!DNL Zendesk] 계정입니다.

* 인증의 첫 번째 단계 [!DNL Zendesk] 계정은 다음을 확인할 수 있습니다. [!DNL Zendesk] 지원 계정입니다. 아직 없는 경우 [[!DNL Zendesk] 페이지 등록](https://www.zendesk.com/register/) 등록하여 Zendesk 계정을 만듭니다.
* 등록했으면 다음으로 이동합니다. [[!DNL Zendesk] 웹 사이트](https://www.zendesk.com/login/) 및 제공 **하위 도메인**.
* 그런 다음 을 선택합니다. **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* 마지막으로,에서 API 토큰 검색 **[!DNL API token]** 섹션.

![Zendesk API 토큰](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

다음을 참조하십시오. [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) 을 참조하십시오. API 토큰 생성에 대한 자세한 내용은 [[!DNL Zendesk] 새 API 토큰 생성에 대한 안내서](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

아래 설명서는 연결 방법에 대한 정보를 제공합니다 [!DNL Zendesk] API 또는 사용자 인터페이스를 사용하여 Platform으로

## 연결 [!DNL Zendesk] API를 사용하여 플랫폼으로

* [소스 연결 및 데이터 흐름 만들기 [!DNL Zendesk] 흐름 서비스 API 사용](../../tutorials/api/create/customer-success/zendesk.md)

## 연결 [!DNL Zendesk] UI를 사용하여 플랫폼에 연결

* [만들기 [!DNL Zendesk ]UI의 소스 연결](../../tutorials/ui/create/customer-success/zendesk.md)
* [UI에서 고객 성공 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/customer-success.md)
