---
title: Oracle NetSuite Source 개요
description: API 또는 사용자 인터페이스를 사용하여 Oracle NetSuite를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 2%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>[!DNL Oracle NetSuite] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 데이터 수집 서드파티 마케팅 자동화 시스템에 대한 지원을 제공합니다. 마케팅 자동화 공급자에 대한 지원에는 [!DNL Oracle NetSuite]이(가) 포함됩니다.

[[!DNL Oracle NetSuite]](https://www.netsuite.com/)은(는) ERP/재무, CRM 및 전자 상거래 솔루션을 포함하는 클라우드 기반 비즈니스 관리 세트입니다.

두 개의 다른 소스를 사용하여 [!DNL Oracle NetSuite]에서 Experience Platform으로 데이터를 수집할 수 있습니다.

* [!DNL Oracle NetSuite Activities] 원본을 사용하여 이벤트 데이터를 수집하십시오.
* [!DNL Oracle NetSuite Entities] 원본을 사용하여 고객 및 연락처 데이터를 수집하십시오.

두 [!DNL Oracle NetSuite] 원본에 대한 자세한 내용은 다음 표를 참조하십시오.

| 소스 | 유형 | 설명 |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | 이벤트 | 캘린더에 추가된 예약된 활동을 검색합니다. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 고객 | 고객 이름, 주소 및 키 식별자와 같은 세부 정보를 포함한 특정 고객 데이터를 검색합니다. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | 연락처 | 연락처 이름, 이메일, 전화 번호 및 고객과 연결된 모든 사용자 지정 연락처 관련 필드를 검색합니다. |

## IP 주소 허용 목록 {#ip-allow-list}

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 할 수 있습니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

## 전제 조건 {#prerequisites}

[!DNL Oracle NetSuite] 데이터를 Experience Platform으로 가져오려면 먼저 다음 사항을 확인해야 합니다.

* **[!DNL Oracle NetSuite] 계정**&#x200B;입니다.
   * 올바른 계정이 아직 없는 경우 [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml)에 문의하세요.
* [!DNL Oracle NetSuite] 제품에 대한 **활성 구독**.
* **계정 ID**.
   * [!DNL Oracle NetSuite] 원본은 OAuth 2.0을 사용하여 [!DNL Oracle NetSuite] API와 통신합니다. 계정 ID가 없는 경우 [계정 ID를 검색하는 방법](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID)의 [!DNL Oracle] 설명서를 참조하세요.
* **클라이언트 ID** 및 **클라이언트 암호** 조합입니다.
   * [!DNL Oracle NetSuite] API에 액세스하려면 클라이언트 ID 및 클라이언트 암호가 필요합니다. 이 단계에서 관리자는 또한 다음을 수행해야 합니다.
      * OAuth 2.0 기능을 활성화하고 적절한 OAuth 2.0 역할을 설정합니다.
      * OAuth 2.0 역할에 사용자를 할당하고 필요한 통합 레코드를 만들었습니다.
* **액세스 토큰** 및 **새로 고침 토큰**&#x200B;입니다.
   * 액세스 및 토큰 새로 고침 방법에 대한 자세한 내용은 [OAuth 2.0 인증 코드 부여 흐름](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow)의 [!DNL Oracle] 안내서를 참조하십시오.

### 필요한 자격 증명 수집 {#gather-credentials}

[!DNL Oracle NetSuite]을(를) Experience Platform에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 클라이언트 ID | [!DNL Oracle NetSuite]에서 통합 레코드를 만들 때 생성되는 클라이언트 ID 값입니다. 자세한 내용은 [통합 레코드를 만드는 방법](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)에 대한 [!DNL Oracle] 안내서를 참조하십시오. | `7fce.....b42f`<br>값이 64자로 이루어진 문자열입니다. |
| 클라이언트 암호 | 통합 레코드를 만들 때 생성되는 클라이언트 암호 값입니다. 자세한 내용은 [통합 레코드를 만드는 방법](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)에 대한 [!DNL Oracle] 안내서를 참조하십시오. | `5c98.....1b46`<br>값이 64자로 이루어진 문자열입니다. |
| 인증 테스트 URL | (선택 사항) [!DNL NetSuite] 인증 테스트 URL입니다. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| 액세스 토큰 | 액세스 토큰은 JSON 웹 토큰(JWT) 형식이며 60분 동안만 유효합니다. 액세스 토큰을 검색하는 방법에 대한 자세한 내용은 [NetSuite에 대한 OAuth 2.0 권한 부여](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint)에 대한 [!DNL Oracle] 안내서를 참조하십시오. | `eyJr......f4V0`<br> 값이 JSON 웹 토큰(JWT) 형식의 1024자 문자열입니다. |
| 토큰 새로 고침 | 액세스 토큰이 만료된 후 새로 고침을 사용하여 새 액세스 토큰을 생성합니다. 새로 고침 토큰은 7일 동안 유효합니다. 액세스 토큰을 검색하는 방법에 대한 자세한 내용은 [NetSuite에 대한 OAuth 2.0 권한 부여](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint)에 대한 [!DNL Oracle] 안내서를 참조하십시오. | `eyJr......dmxM`<br> 값이 JSON 웹 토큰(JWT) 형식의 1024자 문자열입니다. |
| 토큰 URL 액세스 | 애플리케이션이 POST 요청을에 전송하는 토큰 종단점입니다. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>새로 고침 토큰이 만료되면 업데이트된 토큰으로 Experience Platform에서 새 계정을 만들어야 합니다.

## Experience Platform에 [!DNL Oracle NetSuite Activities] 연결 {#oracle-netsuite-activities}

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Oracle NetSuite Activities]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

* [API를 사용하여  [!DNL Oracle NetSuite Activities] 데이터를 Experience Platform으로 가져오기](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md)할 원본 연결 및 데이터 흐름을 만듭니다.
* [UI를 사용하여  [!DNL Oracle NetSuite Activities] 계정을 Experience Platform에 연결](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [UI를 사용하여 원본 연결에 대한 데이터 흐름을 만듭니다](../../tutorials/ui/dataflow/marketing-automation.md).

## Experience Platform에 [!DNL Oracle NetSuite Entities] 연결 {#oracle-netsuite-entities}

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Oracle NetSuite Entities]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

* [API를 사용하여  [!DNL Oracle NetSuite Entities] 데이터를 Experience Platform으로 가져오기](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md)할 원본 연결 및 데이터 흐름을 만듭니다.
* [UI를 사용하여  [!DNL Oracle NetSuite Entities] 계정을 Experience Platform에 연결](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [UI를 사용하여 원본 연결에 대한 데이터 흐름을 만듭니다](../../tutorials/ui/dataflow/marketing-automation.md).
