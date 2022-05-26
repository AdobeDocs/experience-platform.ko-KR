---
keywords: Experience Platform;홈;인기 항목;Zendesk;zendesk
solution: Experience Platform
title: Zendesk 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Zendesk을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# (베타) [!DNL Zendesk]

>[!NOTE]
>
>다음 [!DNL Zendesk] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 고객 성공 애플리케이션에서 데이터를 수집하기 위한 지원을 제공합니다. 고객 성공 공급자를 지원하는 기능에는 다음이 포함됩니다 [!DNL Zendesk].

이 Adobe Experience Platform [소스](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en) 활용 [Zendesk 검색 API > 검색 결과 내보내기](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 추가 처리를 위해 Zendesk에서 Experience Platform으로 사용자 정보를 반환합니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 인증 [!DNL Zendesk] account

[!DNL Zendesk] 는 bearer 토큰을 인증 메커니즘으로 사용하여 와 통신합니다 [!DNL Zendesk] API.

이 섹션에서는 다음을 인증하기 위해 완료해야 하는 필수 구성 요소 단계에 대해 설명합니다 [!DNL Zendesk] 계정이 필요합니다.

* 를 인증하는 첫 번째 단계 [!DNL Zendesk] 계정을 사용하는 경우 [!DNL Zendesk] 지원 계정. 아직 표시되지 않은 경우 [[!DNL Zendesk]페이지 등록](https://www.zendesk.com/register/) 을 입력하여 Zendesk 계정을 등록하고 만듭니다.
* 등록되면 다음 위치로 이동합니다 [[!DNL Zendesk] 웹 사이트](https://www.zendesk.com/login/) 그리고 **하위 도메인**.
* 다음 을 선택합니다. **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* 마지막으로 API 토큰을 **[!DNL API token]** 섹션을 참조하십시오.

![Zendesk API 토큰](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

자세한 내용은 [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) 을 참조하십시오. API 토큰 생성에 대한 자세한 내용은 [[!DNL Zendesk] 새 API 토큰 생성에 대한 안내서](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Zendesk] API 또는 사용자 인터페이스를 사용하여 플랫폼:

## Connect [!DNL Zendesk] API를 사용하여 플랫폼 구현

* [소스 연결 및 데이터 흐름 만들기 [!DNL Zendesk] 흐름 서비스 API 사용](../../tutorials/api/create/customer-success/zendesk.md)

## Connect [!DNL Zendesk] UI를 사용하여 플랫폼 구현

* [만들기 [!DNL Zendesk ]UI의 소스 연결](../../tutorials/ui/create/customer-success/zendesk.md)
* [UI에서 고객 성공 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/customer-success.md)
