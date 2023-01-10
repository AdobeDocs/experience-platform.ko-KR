---
keywords: Experience Platform;홈;인기 항목;salesforce marketing cloud;Salesforce Marketing Cloud;마케팅 자동화
solution: Experience Platform
title: Salesforce Marketing Cloud 소스 개요
description: API 또는 사용자 인터페이스를 사용하여 Salesforce Marketing Cloud을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# (베타) [!DNL Salesforce Marketing Cloud]

>[!NOTE]
>
>다음 [!DNL Salesforce Marketing Cloud] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 에서는 타사 마케팅 자동화 시스템에서 데이터 섭취를 지원합니다. 마케팅 자동화 공급자에 대한 지원에는 다음과 같습니다 [!DNL Salesforce Marketing Cloud].

## 전제 조건

연결하기 전에 [!DNL Salesforce Marketing Cloud] 를 Platform으로 마이그레이션하는 경우 다음을 수행해야 합니다 **권한 범위** 이 [!DNL Salesforce Marketing Cloud] 클라이언트 ID 및 클라이언트 암호 조합:

* `campaign_read`
* `list_and_subscribers_read`

를 호출하여 범위를 요청할 수 있습니다 `v2/userinfo` 의 리소스 [!DNL Salesforce Marketing Cloud] API. 자세한 내용은 [[!DNL Salesforce Marketing Cloud] API 통합 권한 범위 문서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html) 범위를 요청 및 비교하는 방법에 대한 지침을 제공합니다.

관련 권한 및 동작 목록을 포함한 범위에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL Salesforce Marketing Cloud] REST API 문서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html).

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## Connect [!DNL Salesforce Marketing Cloud] API를 사용하여 플랫폼 구현

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Salesforce Marketing Cloud] api를 사용하여 플랫폼:

* [Flow Service API를 사용하여 Salesforce Marketing Cloud 기본 연결 만들기](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Flow Service API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [Flow Service API를 사용하여 마케팅 자동화 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/marketing-automation.md)

## Connect [!DNL Salesforce Marketing Cloud] UI를 사용하여 플랫폼 구현

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Salesforce Marketing Cloud] 사용자 인터페이스를 사용하여 플랫폼:

* [UI에서 Salesforce Marketing Cloud 소스 연결 만들기](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [UI에서 마케팅 자동화 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/marketing-automation.md)
