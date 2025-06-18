---
title: Salesforce Marketing Cloud Source 개요
description: API 또는 사용자 인터페이스를 사용하여 Salesforce Marketing Cloud을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud] 원본은 2026년 1월에 사용되지 않습니다. 대안으로 새로운 정보원이 올해 말 공개될 것이다. 새 소스가 릴리스되면 2026년 1월 말 이전에 새 계정 연결 및 데이터 흐름을 생성하여 새 소스로 마이그레이션할 계획이어야 합니다.

[!DNL Salesforce Marketing Cloud]을(를) 사용하면 하나의 플랫폼에서 이메일, 모바일, 소셜 미디어 및 광고 전반에 걸친 고객 참여를 관리하고 자동화할 수 있습니다. Email Studio, 여정 빌더 및 대상 빌더와 같은 도구를 사용하여 대상에 맞게 개인화된 캠페인과 고객 여정을 만들 수 있습니다.

[!DNL Salesforce Marketing Cloud] 원본을 사용하여 계정을 연결하고 데이터를 Adobe Experience Platform으로 가져올 수 있습니다.

## 전제 조건

[!DNL Salesforce Marketing Cloud] 소스를 Experience Platform에 연결하려면 먼저 다음 **권한 범위**&#x200B;가 [!DNL Salesforce Marketing Cloud] 클라이언트 ID 및 클라이언트 암호 조합에 프로비저닝되어 있는지 확인해야 합니다.

* `campaign_read`
* `list_and_subscribers_read`

[!DNL Salesforce Marketing Cloud] API의 `v2/userinfo` 리소스를 호출하여 범위를 요청할 수 있습니다. 범위를 요청하고 비교하는 방법에 대한 지침은 [[!DNL Salesforce Marketing Cloud] API 통합 권한 범위 문서](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)를 참조하십시오.

관련 권한 및 동작 목록을 포함한 범위에 대한 자세한 내용은 이 [[!DNL Salesforce Marketing Cloud] REST API 문서](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>)를 참조하십시오.

>[!IMPORTANT]
>
>사용자 지정 개체 수집은 현재 [!DNL Salesforce Marketing Cloud] 원본 통합에서 지원되지 않습니다.

### 허용 목록에 추가하다 IP 주소

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

>[!WARNING]
>
>필요한 IP 주소를 허용 목록에 추가하다에 추가하지 않으면 [!DNL Salesforce Marketing Cloud] 계정이 Experience Platform에 연결되지 않습니다.

### Azure에서 Experience Platform 인증 {#azure}

[!DNL Azure]의 Experience Platform에 [!DNL Salesforce Marketing Cloud]을(를) 연결하려면 다음 자격 증명의 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| Host | 응용 프로그램의 호스트 서버입니다. 이는 종종 하위 도메인입니다. **참고:** `host` 값을 입력할 때 `{subdomain}.rest.marketingcloudapis.com`을(를) 지정해야 합니다. 예를 들어 호스트 URL이 `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`인 경우 `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/`을(를) 호스트 값으로 입력해야 합니다. |
| 클라이언트 ID | [!DNL Salesforce Marketing Cloud] 응용 프로그램과 연결된 클라이언트 ID입니다. |
| 클라이언트 암호 | [!DNL Salesforce Marketing Cloud] 응용 프로그램과 연결된 클라이언트 암호입니다. |
| 연결 사양 ID | **연결 사양**&#x200B;은(는) 데이터 원본의 커넥터 속성을 제공합니다. 여기에는 **기본** 및 **소스** 연결을 모두 만들기 위한 인증 사양 및 요구 사항과 같은 세부 정보가 포함됩니다. [!DNL Salesforce Marketing Cloud]의 경우 연결 사양 ID는 `ea1c2a08-b722-11eb-8529-0242ac130003`입니다. **참고:** 이 자격 증명은 API를 통해 연결할 때만 필요합니다. |

### Amazon Web Services(AWS)에서 Experience Platform 인증 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../landing/multi-cloud.md)를 참조하세요.

AWS에서 Experience Platform에 [!DNL Salesforce Marketing Cloud]을(를) 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 하위 도메인 | API 끝점을 만드는 데 사용되는 [!DNL Salesforce Marketing Cloud] 인스턴스 URL의 고유한 부분입니다. |
| 클라이언트 ID | [!DNL Salesforce Marketing Cloud]에 설치된 패키지를 만들 때 생성되는 응용 프로그램의 공용 식별자입니다. |
| 클라이언트 암호 | 클라이언트 ID와 연결된 기밀 키로서 설치된 패키지도 생성됩니다. |
| 연결 사양 ID | **연결 사양**&#x200B;은(는) 데이터 원본의 커넥터 속성을 제공합니다. 여기에는 **기본** 및 **소스** 연결을 모두 만들기 위한 인증 사양 및 요구 사항과 같은 세부 정보가 포함됩니다. [!DNL Salesforce Marketing Cloud]의 경우 연결 사양 ID는 `ea1c2a08-b722-11eb-8529-0242ac130003`입니다. **참고:** 이 자격 증명은 API를 통해 연결할 때만 필요합니다. |

자세한 내용은 서버 간 통합을 위한 액세스 토큰에 대한 [[!DNL Salesforce] 설명서](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html)를 참조하십시오.

## API를 사용하여 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결

아래 설명서는 API를 사용하여 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

* [흐름 서비스 API를 사용하여  [!DNL Salesforce Marketing Cloud] 을(를) Experience Platform에 연결](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 마케팅 자동화 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/marketing-automation.md)

## UI를 사용하여 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결

아래 설명서는 사용자 인터페이스를 사용하여 [!DNL Salesforce Marketing Cloud]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

* [UI에서  [!DNL Salesforce Marketing Cloud] 을(를) Experience Platform에 연결](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [UI에서 마케팅 자동화 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/marketing-automation.md)
