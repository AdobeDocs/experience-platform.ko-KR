---
keywords: Experience Platform;홈;인기 항목;Zoho CRM;Zoho CRM;Zoho;Zoho
solution: Experience Platform
title: Zoho CRM Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Zoho CRM을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# [!DNL Zoho CRM]

>[!WARNING]
>
>[!DNL Zoho CRM] 원본은 2025년 6월 말에 사용되지 않습니다.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 서드파티 CRM 시스템에서 데이터 수집을 지원합니다. CRM 공급자에 대한 지원에는 [!DNL Zoho CRM]이(가) 포함됩니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

## [!DNL Zoho CRM]에 대한 인증 자격 증명 검색

[!DNL Zoho CRM] 계정의 데이터를 Experience Platform으로 가져오려면 먼저 자격 증명을 검색하여 [!DNL Zoho CRM] 원본을 인증해야 합니다. 클라이언트 ID, 클라이언트 암호, 액세스 토큰 및 새로 고침 토큰을 검색하려면 아래 단계를 따르십시오.

### 애플리케이션 등록

인증 자격 증명을 검색하는 첫 번째 단계는 [[!DNL Zoho CRM] 개발자 콘솔](https://accounts.zoho.com/)을 사용하여 응용 프로그램을 등록하는 것입니다. 응용 프로그램을 등록하려면 Java Script, 웹 기반, 모바일, 비브라우저 모바일 응용 프로그램 또는 자체 클라이언트에서 클라이언트 유형을 선택해야 합니다. 그런 다음 응용 프로그램 이름, 웹 페이지의 URL 및 권한 있는 리디렉션 URI에 대한 값을 제공하십시오. 이 값은 [!DNL Zoho CRM]에서 부여 토큰으로 리디렉션하는 데 사용할 수 있습니다.

등록이 완료되면 클라이언트 ID와 클라이언트 암호가 반환됩니다.

### 인증 요청 만들기

그런 다음 웹 기반 응용 프로그램이나 자체 클라이언트를 사용하여 [권한 부여 요청](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html)을 만들어야 합니다. 인증 요청은 부여 토큰을 반환하며, 이렇게 하면 액세스 토큰을 검색할 수 있습니다.

인증 요청을 만들 때 **범위** 및 **액세스 형식**&#x200B;의 값을 모두 입력해야 합니다. 범위에 대한 자세한 내용은 이 [[!DNL Zoho CRM] 문서](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html)를 참조하세요. **액세스 형식**&#x200B;은(는) 항상 `offline`(으)로 설정해야 합니다.

### 액세스 생성 및 토큰 새로 고침

부여 토큰을 검색한 후에는 클라이언트 ID, 클라이언트 암호, 부여 토큰 및 리디렉션 URI를 제공하는 동안 `{ACCOUNTS_URL}/oauth/v2/token`에 대한 POST 요청을 수행하여 [액세스 및 새로 고침 토큰](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html)을 생성할 수 있습니다. 이 단계에서는 `grant_type`도 매개 변수로 포함해야 하며 값을 `"authorization_code"`(으)로 설정해야 합니다.

성공적인 요청은 액세스 및 새로 고침 토큰을 반환하고, 이를 사용하여 인증할 수 있습니다.

자격 증명을 얻는 방법에 대한 자세한 단계는 [[!DNL Zoho CRM] 인증 안내서](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html)를 참조하십시오.

## API를 사용하여 [!DNL Zoho CRM]을(를) [!DNL Experience Platform]에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Zoho CRM]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

- [흐름 서비스 API를 사용하여  [!DNL Zoho CRM] 기본 연결 만들기](../../tutorials/api/create/crm/zoho.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 CRM 소스의 데이터 흐름 만들기](../../tutorials/api/collect/crm.md)

## UI를 사용하여 [!DNL Zoho CRM]을(를) [!DNL Experience Platform]에 연결

- [UI에서  [!DNL Zoho CRM] 소스 연결 만들기](../../tutorials/ui/create/crm/zoho.md)
- [UI에서 CRM 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/crm.md)
