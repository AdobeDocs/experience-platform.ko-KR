---
keywords: Experience Platform;홈;인기 항목;Zoho CRM;Zoho CRM;Zoho;Zoho
solution: Experience Platform
title: Zoho CRM 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Zoho CRM을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 을 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 서드파티 CRM 시스템에서 데이터 수집을 지원합니다. CRM 공급자에 대한 지원은 다음과 같습니다 [!DNL Zoho CRM].

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

## 다음에 대한 인증 자격 증명 검색 [!DNL Zoho CRM]

에서 데이터를 가져오기 전에 [!DNL Zoho CRM] 계정을 Platform으로 가져왔습니다. 인증하려면 먼저 자격 증명을 검색해야 합니다. [!DNL Zoho CRM] 소스. 클라이언트 ID, 클라이언트 암호, 액세스 토큰 및 새로 고침 토큰을 검색하려면 아래 단계를 따르십시오.

### 애플리케이션 등록

인증 자격 증명을 검색하는 첫 번째 단계는 [[!DNL Zoho CRM] 개발자 콘솔](https://accounts.zoho.com/). 응용 프로그램을 등록하려면 Java Script, 웹 기반, 모바일, 비브라우저 모바일 응용 프로그램 또는 자체 클라이언트에서 클라이언트 유형을 선택해야 합니다. 그런 다음 애플리케이션 이름, 웹 페이지의 URL 및 [!DNL Zoho CRM] 그런 다음 을 사용하여 권한 부여 토큰으로 리디렉션할 수 있습니다.

등록이 완료되면 클라이언트 ID와 클라이언트 암호가 반환됩니다.

### 인증 요청 만들기

다음으로, 다음을 만들어야 합니다. [인증 요청](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) 웹 기반 애플리케이션이나 자체 클라이언트 사용 인증 요청은 부여 토큰을 반환하며, 이렇게 하면 액세스 토큰을 검색할 수 있습니다.

인증 요청을 만들 때 두 요청에 대한 값을 모두 입력해야 합니다. **범위** 및 **액세스 유형**. 다음을 참조하십시오. [[!DNL Zoho CRM] 문서](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) 을(를) 클릭하는 동안 범위에 대한 자세한 내용을 보려면 **액세스 유형** 은(는) 항상 로 설정해야 합니다. `offline`.

### 액세스 생성 및 토큰 새로 고침

부여 토큰을 검색한 후에는 다음을 생성할 수 있습니다. [토큰 액세스 및 새로 고침](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) 에 POST 요청 수행 `{ACCOUNTS_URL}/oauth/v2/token` 클라이언트 ID, 클라이언트 암호, 부여 토큰 및 리디렉션 URI를 제공하는 동안. 이 단계에서 다음을 포함해야 합니다. `grant_type` 을 매개 변수로 설정하고 값을 로 설정합니다. `"authorization_code"`.

성공적인 요청은 액세스 및 새로 고침 토큰을 반환하고, 이를 사용하여 인증할 수 있습니다.

자격 증명을 얻는 방법에 대한 자세한 단계는 [[!DNL Zoho CRM] 인증 안내서](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## 연결 [!DNL Zoho CRM] 끝 [!DNL Platform] api 사용

아래 설명서는 연결 방법에 대한 정보를 제공합니다 [!DNL Zoho CRM] API 또는 사용자 인터페이스를 사용하여 Platform으로

- [만들기 [!DNL Zoho CRM] 흐름 서비스 API를 사용한 기본 연결](../../tutorials/api/create/crm/zoho.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 CRM 소스의 데이터 흐름 만들기](../../tutorials/api/collect/crm.md)

## 연결 [!DNL Zoho CRM] 끝 [!DNL Platform] UI 사용

- [만들기 [!DNL Zoho CRM] UI의 소스 연결](../../tutorials/ui/create/crm/zoho.md)
- [UI에서 CRM 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/crm.md)
