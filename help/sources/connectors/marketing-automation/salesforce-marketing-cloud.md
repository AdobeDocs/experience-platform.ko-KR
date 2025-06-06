---
solution: Experience Platform
title: Salesforce Marketing Cloud Source 개요
description: API 또는 사용자 인터페이스를 사용하여 Salesforce Marketing Cloud을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-04-29T00:00:00Z
source-git-commit: ce96dbc64845fddb40ebee709828c56d51a6c6ba
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud] 원본은 2026년 1월에 사용되지 않습니다. 대안으로 새로운 정보원이 올해 말 공개될 것이다. 새 소스가 릴리스되면 2026년 1월 말 이전에 새 계정 연결 및 데이터 흐름을 생성하여 새 소스로 마이그레이션할 계획이어야 합니다.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 서드파티 마케팅 자동화 시스템에서 데이터를 수집할 수 있도록 지원합니다. 마케팅 자동화 공급자에 대한 지원은 [!DNL Salesforce Marketing Cloud]입니다.

## 전제 조건

[!DNL Salesforce Marketing Cloud] 소스를 Experience Platform에 연결하려면 먼저 다음 **권한 범위**&#x200B;가 [!DNL Salesforce Marketing Cloud] 클라이언트 ID 및 클라이언트 암호 조합에 프로비저닝되어 있는지 확인해야 합니다.

* `campaign_read`
* `list_and_subscribers_read`

[!DNL Salesforce Marketing Cloud] API의 `v2/userinfo` 리소스를 호출하여 범위를 요청할 수 있습니다. 범위를 요청하고 비교하는 방법에 대한 지침은 [[!DNL Salesforce Marketing Cloud] API 통합 권한 범위 문서](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)를 참조하십시오.

관련 권한 및 동작 목록을 포함한 범위에 대한 자세한 내용은 이 [[!DNL Salesforce Marketing Cloud] REST API 문서](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>)를 참조하십시오.

>[!IMPORTANT]
>
>사용자 지정 개체 수집은 현재 [!DNL Salesforce Marketing Cloud] 원본 통합에서 지원되지 않습니다.

## 허용 목록에 추가하다 IP 주소

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

>[!WARNING]
>
>필요한 IP 주소를 허용 목록에 추가하다에 추가하지 않으면 [!DNL Salesforce Marketing Cloud] 계정이 Experience Platform에 연결되지 않습니다.

## API를 사용하여 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결

아래 설명서는 API를 사용하여 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

* [흐름 서비스 API를 사용하여 Salesforce Marketing Cloud 기본 연결 만들기](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 마케팅 자동화 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/marketing-automation.md)

## UI를 사용하여 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결

아래 설명서는 사용자 인터페이스를 사용하여 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

* [UI에서 Salesforce Marketing Cloud 소스 연결 만들기](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [UI에서 마케팅 자동화 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/marketing-automation.md)
