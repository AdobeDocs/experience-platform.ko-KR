---
title: Salesforce Service Cloud Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Salesforce Service Cloud를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 9bebbc00-55b3-4aec-9357-4127c05844e2
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# [!DNL Salesforce Service Cloud]

[!DNL Salesforce Service Cloud]은(는) 서비스 워크플로를 자동화하고 회사와 고객 간의 커뮤니케이션을 간소화하도록 설계된 고객 성공 플랫폼입니다. 이메일, 전화, 소셜 미디어, 라이브 채팅 등 다양한 채널의 요청을 통합 에이전트 콘솔로 통합합니다. 이를 통해 지원 팀은 고객 이력을 360도 관점에서 &quot;사례&quot;를 관리할 수 있으므로 고객이 접근하는 방식에 관계없이 개인화되고 효율적입니다.

Adobe Experience Platform Sources의 [!DNL Salesforce Service Cloud] 소스 커넥터를 사용하여 [!DNL Salesforce Service Cloud] 계정을 연결하고 Experience Platform Services에서 사용할 데이터를 가져올 수 있습니다.

[!DNL Salesforce Service Cloud] 계정을 설정하고 Experience Platform에 연결하는 방법에 대해 알아보려면 이 문서를 참조하십시오.

## 전제 조건 {#prerequisites}

Experience Platform에 성공적으로 연결하기 전에 완료해야 하는 사전 요구 사항 설정에 대해서는 이 섹션을 참조하십시오.

### IP 주소 {#allowlist}

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

### 필요한 자격 증명 수집 {#credentials}

OAuth2 클라이언트 자격 증명을 사용하여 [!DNL Salesforce Service Cloud] 계정에 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 환경 URL | [!DNL Salesforce Service Cloud] 원본 인스턴스의 URL입니다. |
| 클라이언트 ID | 클라이언트 ID는 OAuth2 인증의 일부로 클라이언트 암호와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce Service Cloud]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| 클라이언트 암호 | 클라이언트 암호는 OAuth2 인증의 일부로 클라이언트 ID와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce Service Cloud]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| API 버전 | 사용 중인 [!DNL Salesforce Service Cloud] 인스턴스의 REST API 버전입니다. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전 `52`을(를) 사용하는 경우 값을 `52.0`(으)로 입력해야 합니다. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. |

[!DNL Salesforce Service Cloud]에 대한 OAuth 사용에 대한 자세한 내용은 OAuth 인증 흐름에 대한 [[!DNL Salesforce Service Cloud] 안내서](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)를 참조하십시오.

## API를 사용하여 [!DNL Salesforce Service Cloud]을(를) Experience Platform에 연결

- [흐름 서비스 API를 사용하여 Salesforce 서비스 클라우드 기반 연결 만들기](../../tutorials/api/create/customer-success/salesforce-service-cloud.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 고객 성공 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/customer-success.md)

## UI를 사용하여 [!DNL Salesforce Service Cloud]을(를) Experience Platform에 연결

- [UI에서 Salesforce Service Cloud 소스 연결 만들기](../../tutorials/ui/create/customer-success/salesforce-service-cloud.md)
- [UI에서 고객 성공 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/customer-success.md)
