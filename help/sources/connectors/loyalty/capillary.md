---
title: 모세관 스트리밍 이벤트 개요
description: Capillary에서 Experience Platform으로 데이터를 스트리밍하는 방법에 대해 알아봅니다.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 4%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>[!DNL Capillary Streaming Events] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 소스 개요에서 [약관](../../home.md#terms-and-conditions)을 참조하십시오.

[!DNL Capillary Technologies]은(는) 전 세계 300개 이상의 브랜드에서 신뢰하는 선도적인 충성도 및 참여 플랫폼입니다. 비즈니스에서 [!DNL Capillary Streaming Events]의 고객 프로필, 충성도 데이터 및 트랜잭션 이벤트를 Adobe Experience Platform으로 원활하게 스트리밍할 수 있도록 하려면 [!DNL Capillary] 소스를 사용하십시오. [!DNL Capillary] 소스를 연결하여 실시간 개인화, 고급 대상자 세분화 및 옴니채널 캠페인 오케스트레이션을 사용할 수 있습니다.

[!DNL Capillary]을(를) Experience Platform과 통합하여 다음과 같은 작업을 수행할 수 있습니다.

* **충성도 포인트, 계층 및 보상**&#x200B;을 실시간으로 동기화합니다.
* 분석 및 활성화를 위해 **트랜잭션 데이터**&#x200B;를 Experience Platform으로 보냅니다.
* 세그멘테이션, 여정 오케스트레이션 및 개인화를 위해 Real-Time CDP, Experience Platform 및 Adobe Journey Optimizer을 활용합니다.

## 전제 조건

[!DNL Capillary]을(를) Adobe Experience Platform에 연결하기 전에 다음을 확인하십시오.

* 유효한 **Adobe 조직 ID** 및 활성화된 Experience Platform 샌드박스에 대한 액세스 권한.
* **[!DNL Capillary]원본 자격 증명**(클라이언트 ID 및 클라이언트 암호).
* Adobe Admin Console에서 소스 및 데이터 흐름을 만드는 데 필요한 권한입니다.

### 필요한 자격 증명 수집

[!DNL Capillary] 계정을 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 클라이언트 ID | [!DNL Capillary] 원본의 클라이언트 식별자입니다. | `321c8a8fee0d4a06838d46f9d3109e8a` |
| 클라이언트 암호 | 클라이언트 ID로 발급된 클라이언트 암호 | `xxxxxxxxxxxxxxxxxx` |
| 조직 ID | Adobe 조직 ID | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

액세스 토큰 생성에 대한 자세한 내용은 [Adobe 인증 안내서](https://developer.adobe.com/developer-console/docs/guides/authentication/)를 참조하십시오.

### 액세스 토큰 생성

그런 다음 클라이언트 ID와 클라이언트 암호를 사용하여 Adobe에서 액세스 토큰을 생성합니다.

**요청**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**응답**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## 다음 단계

[!DNL Capillary]에 대한 필수 구성 요소 설정을 완료했으면 다음 설명서를 읽어 계정을 연결하고 [!DNL Capillary]에서 Experience Platform으로 데이터 스트리밍을 시작하는 방법에 대해 알아보십시오.

* [API를 사용하여  [!DNL Capillary Streaming Events] 을(를) Experience Platform에 연결](../../tutorials/api/create/loyalty/capillary.md)
* [UI를 사용하여  [!DNL Capillary Streaming Events] 을(를) Experience Platform에 연결](../../tutorials/ui/create/loyalty/capillary.md)
