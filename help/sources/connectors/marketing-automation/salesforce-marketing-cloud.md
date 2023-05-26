---
solution: Experience Platform
title: Salesforce Marketing Cloud 소스 개요
description: API 또는 사용자 인터페이스를 사용하여 Salesforce Marketing Cloud을 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: bc37d41d0f7b0ff0cf4d52242f41467f2891d613
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 서드파티 마케팅 자동화 시스템에서 데이터를 수집하는 기능을 지원합니다. 마케팅 자동화 공급자에 대한 지원은 다음과 같습니다 [!DNL Salesforce Marketing Cloud].

## 사전 요구 사항

연결하기 전에 [!DNL Salesforce Marketing Cloud] source to Platform에서 다음을 확인해야 합니다. **권한 범위** 이(가) 다음에 프로비저닝되었습니다. [!DNL Salesforce Marketing Cloud] 클라이언트 ID 및 클라이언트 암호 조합:

* `campaign_read`
* `list_and_subscribers_read`

을 호출하여 범위를 요청할 수 있습니다. `v2/userinfo` 의 리소스 [!DNL Salesforce Marketing Cloud] API. 다음을 참조하십시오. [[!DNL Salesforce Marketing Cloud] API 통합 권한 범위 문서](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) 범위를 요청하고 비교하는 방법에 대한 지침을 제공합니다.

관련 권한 및 동작 목록을 포함하여 범위에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL Salesforce Marketing Cloud] REST API 문서](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>사용자 지정 개체 수집은 현재 [!DNL Salesforce Marketing Cloud] 소스 통합.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

## 연결 [!DNL Salesforce Marketing Cloud] API를 사용하여 플랫폼으로

아래 설명서는 연결 방법에 대한 정보를 제공합니다 [!DNL Salesforce Marketing Cloud] API를 사용하여 플랫폼에 다음을 수행합니다.

* [흐름 서비스 API를 사용하여 Salesforce Marketing Cloud 기본 연결 만들기](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 마케팅 자동화 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/marketing-automation.md)

## 연결 [!DNL Salesforce Marketing Cloud] UI를 사용하여 플랫폼에 연결

아래 설명서는 연결 방법에 대한 정보를 제공합니다 [!DNL Salesforce Marketing Cloud] 사용자 인터페이스를 사용하여 Platform으로:

* [UI에서 Salesforce Marketing Cloud 소스 연결 만들기](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [UI에서 마케팅 자동화 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/marketing-automation.md)
