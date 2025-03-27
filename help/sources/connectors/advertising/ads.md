---
title: Google Ads Source 개요
description: API 또는 사용자 인터페이스를 사용하여 Google 광고를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# [!DNL Google Ads] 원본

>[!NOTE]
>
>[!DNL Google Ads] 원본이 Beta 버전입니다. 베타 레이블 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 서드파티 광고 시스템에서 데이터를 수집하는 기능을 지원합니다. 광고 공급자에 대한 지원은 [!DNL Google Ads]입니다.

## 전제 조건 {#prerequisites}

### IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

### Experience Platform에 대한 권한 구성

[!DNL Google Ads] 계정을 Experience Platform에 연결하려면 계정에 대해 **[!UICONTROL 소스 보기]** 및 **[!UICONTROL 소스 관리]** 권한이 모두 활성화되어야 합니다. 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/ui/overview.md)를 참조하십시오.

### 필요한 자격 증명 수집

[!DNL Google Ads] 계정을 Experience Platform에 연결하려면 다음 자격 증명에 적절한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `clientCustomerId` | 클라이언트 고객 ID는 [!DNL Google Ads] API로 관리할 [!DNL Google Ads] 클라이언트 계정에 해당하는 계정 번호입니다. 이 ID는 `123-456-7890`의 템플릿을 따릅니다. |
| `loginCustomerId` | 로그인 고객 ID는 [!DNL Google Ads] 관리자 계정에 해당하는 계정 번호이며 특정 운영 고객으로부터 보고서 데이터를 가져오는 데 사용됩니다. 로그인 고객 ID에 대한 자세한 내용은 [[!DNL Google Ads] API 설명서](https://developers.google.com/search-ads/reporting/concepts/login-customer-id)를 참조하세요. |
| `developerToken` | 개발자 토큰을 사용하면 [!DNL Google Ads] API에 액세스할 수 있습니다. 모든 [!DNL Google Ads] 계정에 대해 동일한 개발자 토큰을 사용하여 요청을 수행할 수 있습니다. [관리자 계정에 로그인](https://ads.google.com/home/tools/manager-accounts/)한 다음 [!DNL API Center] 페이지로 이동하여 개발자 토큰을 검색하십시오. |
| `refreshToken` | 새로 고침 토큰은 [!DNL OAuth2] 인증의 일부입니다. 이 토큰을 사용하면 액세스 토큰이 만료된 후 다시 생성할 수 있습니다. |
| `clientId` | 클라이언트 ID는 [!DNL OAuth2] 인증의 일부로 클라이언트 암호와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Google]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| `clientSecret` | 클라이언트 암호는 [!DNL OAuth2] 인증의 일부로 클라이언트 ID와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Google]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| `googleAdsApiVersion` | [!DNL Google Ads]에서 지원하는 현재 API 버전입니다. 최신 버전은 `v18`이지만 Experience Platform에서 지원되는 최신 버전은 `v17`입니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Google Ads]의 연결 사양 ID는 `d771e9c1-4f26-40dc-8617-ce58c4b53702`입니다. [!DNL Flow Service] API를 사용하여 [!DNL Google Ads] 계정에 연결하는 경우 이 값이 필요합니다. |

## Experience Platform에 [!DNL Google Ads] 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Google Ads]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

* [흐름 서비스 API를 사용하여 Google 광고 기본 연결 만들기](../../tutorials/api/create/advertising/ads.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 광고 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/advertising.md)

### UI 사용

* [UI에서 Google Ads 소스 연결 만들기](../../tutorials/ui/create/advertising/ads.md)
* [UI에서 광고 소스 연결에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/advertising.md)
