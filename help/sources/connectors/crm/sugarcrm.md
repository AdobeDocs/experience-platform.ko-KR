---
title: SugarCRM 소스 개요
description: API 또는 사용자 인터페이스를 사용하여 SugarCRM을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# [!DNL SugarCRM]

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 타사 CRM 애플리케이션에서 데이터를 수집하는 기능을 지원합니다. CRM 공급자에 대한 지원은 다음과 같습니다 [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) 는 CRM(고객 관계 관리) 시스템입니다. [!DNL SugarCRM]의 기능에는 영업 자동화, 마케팅 캠페인, 고객 지원, 공동 작업, Mobile CRM, Social CRM 및 보고가 포함됩니다.

다음 [!DNL SugarCRM] 소스를 사용하면 다음 API 끝점에서 계정, 연락처 및 이벤트 데이터를 수집할 수 있습니다.

* [계정](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [연락처](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [이벤트](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] 전달자 토큰을 인증 메커니즘으로 사용하여 [!DNL SugarCRM] 계정 및 연락처 API 및 [!DNL SugarCRM] 이벤트 API.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

## 전제 조건

다음을 만들기 전에 [!DNL SugarCRM] 소스 연결에서 먼저 다음을 확인해야 합니다.

* A [!DNL SugarMarket] 계정입니다. 다음으로 문의해야 합니다. [!DNL SugarCRM] 계정 관리자가 유효한 값을 얻음 [!DNL SugarMarket] 아직 계정이 없다면 계정을 만듭니다.

* 마케팅 또는 판매 프로세스와 연결된 사용자 계정과 별도의 고유한 API 사용자 이름 및 계정입니다. 이 고유한 사용자 이름 및 계정 조합에는 API 액세스 권한이 있어야 합니다. 계정을 설정하는 프로세스에 대한 자세한 내용은 [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) 설명서를 참조하십시오.

## 연결 [!DNL SugarCRM Accounts & Contacts] 대상 플랫폼

* [가져올 소스 연결 만들기 [!DNL SugarCRM Accounts & Contacts] API를 사용하여 데이터를 플랫폼에 전송](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [가져올 소스 연결 만들기 [!DNL SugarCRM Accounts & Contacts] 사용자 인터페이스를 사용하여 Platform에 데이터 전송](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [흐름 서비스 API를 사용하여 CRM 소스의 데이터 흐름 만들기](../../tutorials/api/collect/crm.md)


## 연결 [!DNL SugarCRM Events] 대상 플랫폼

* [가져올 소스 연결 만들기 [!DNL SugarCRM Events] API를 사용하여 데이터를 플랫폼에 전송](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [가져올 소스 연결 만들기 [!DNL SugarCRM Events] 사용자 인터페이스를 사용하여 Platform에 데이터 전송](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [UI에서 CRM 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/crm.md)
