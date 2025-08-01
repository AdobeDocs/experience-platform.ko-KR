---
title: Didomi Source 개요
description: 사용자 인터페이스를 사용하여 Didomi를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다.
last-substantial-update: 2025-07-29T00:00:00Z
badge: Beta
exl-id: c59bcfb8-e831-4a13-8b0e-4c6d538f1059
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 1%

---

# [!DNL Didomi]

>[!AVAILABILITY]
>
>[!DNL Didomi] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 소스 개요에서 [약관](../../home.md#terms-and-conditions)을 참조하십시오.

[!DNL Didomi]은(는) 조직이 웹 사이트, 앱 및 내부 도구의 개인 데이터에 대한 사용자 선택 사항을 수집, 관리 및 적용할 수 있도록 지원하는 동의 및 환경 설정 관리 플랫폼입니다.

Adobe Experience Platform은 소스 커넥터 시스템을 통해 클라우드 저장소, 데이터베이스 및 [!DNL Didomi]과(와) 같은 응용 프로그램을 포함한 광범위한 외부 시스템의 데이터 수집을 지원합니다. 소스를 사용하여 외부 시스템을 인증하고, Experience Platform으로의 데이터 흐름을 관리하고, 고객 데이터의 일관되고 구조화된 수집을 보장합니다.

[!DNL Didomi] 소스를 사용하여 [!DNL Didomi] 동의 및 환경 설정 관리 플랫폼에서 Experience Platform으로 실시간 사용자 동의 및 환경 설정 데이터를 스트리밍합니다. [!DNL Didomi] 소스를 통해 Experience Platform의 동의 데이터를 중앙에서 관리하고 작업할 수 있으므로 고객 프로필 및 다운스트림 워크플로를 최신 상태로 유지할 수 있습니다.

![&quot;Didomi&quot; 데이터 처리 아키텍처입니다.](../../images/tutorials/create/didomi/flux.jpeg)

## 전제 조건

[!DNL Didomi] 계정을 Experience Platform에 성공적으로 연결하려면 아래에 설명된 필수 구성 요소 단계를 완료하십시오.

### 허용 목록에 추가하다 IP 주소

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

### Experience Platform에 대한 권한 구성

**[!UICONTROL 계정을 Experience Platform에 연결하려면 계정에 대해]**&#x200B;소스 보기&#x200B;**[!UICONTROL 및]**&#x200B;소스 관리[!DNL Didomi] 권한이 모두 활성화되어야 합니다. 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/ui/overview.md)를 참조하십시오.

### Adobe API 자격 증명 수집

[!DNL Didomi]을(를) Experience Platform에 안전하게 연결하려면 Adobe API 자격 증명을 사용하여 인증해야 합니다. 이러한 자격 증명은 웹후크를 설정하고 데이터 수집을 구성하는 데 필수적입니다.

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작하기](../../../landing/api-authentication.md)의 안내서를 참조하십시오.

### Experience Platform 스키마 만들기

>[!TIP]
>
>기존 XDM 스키마가 이미 있는 경우 이 단계를 건너뛸 수 있습니다.

**XDM(경험 데이터 모델) 스키마**&#x200B;은(는) [!DNL Didomi]에서 Experience Platform으로 보낼 데이터의 구조(예: 사용자 ID, 동의 목적)를 정의합니다.

스키마를 만들려면 Experience Platform UI의 왼쪽 탐색에서 [!UICONTROL 스키마]를 선택하고 **[!UICONTROL 스키마 만들기]**&#x200B;를 선택합니다. 그런 다음 스키마 유형으로 **[!UICONTROL 표준]**&#x200B;을(를) 선택한 다음 **[!UICONTROL 수동]**&#x200B;을(를) 선택하여 필드를 수동으로 만듭니다. 스키마에 대한 기본 클래스를 선택하고 스키마 이름을 제공합니다.

생성되면 필수 필드를 추가하여 스키마를 업데이트합니다. 최소 하나 이상의 필드가 [!UICONTROL ID] 필드인지 확인하여 기본 ID 값에 대해 Experience Platform에 알립니다. 마지막으로 데이터를 성공적으로 저장하려면 [!UICONTROL 프로필] 전환을 활성화해야 합니다.

![스키마 만들기](../../images/tutorials/create/didomi/create-schema.png)

자세한 내용은 [UI에서 스키마 만들기](../../../xdm/tutorials/create-schema-ui.md)에 대한 안내서를 참조하십시오.

### 데이터 세트 만들기

>[!TIP]
>
>기존 데이터 세트가 있는 경우 이 단계를 건너뛸 수 있습니다.

Experience Platform의 **dataset**&#x200B;은(는) 사용자가 정의한 스키마를 기반으로 들어오는 데이터를 저장하는 데 사용됩니다.

데이터 세트를 만들려면 Experience Platform UI의 왼쪽 탐색에서 [!UICONTROL 데이터 세트]를 선택한 다음 **[!UICONTROL 데이터 세트 만들기]**&#x200B;를 선택합니다. **[!UICONTROL 스키마에서 데이터 집합 만들기]**&#x200B;를 선택한 다음 새 데이터 집합과 연결할 스키마를 선택하십시오.

![create-dataset](../../images/tutorials/create/didomi/create-dataset.png)

## [!DNL Didomi] 콘솔에서 HTTP Webhook 구성

[!DNL Webhooks]을(를) 사용하면 사용자가 동의 환경 설정과 상호 작용할 때 [!DNL Didomi] 플랫폼에서 트리거되는 이벤트를 구독할 수 있습니다. 관련 이벤트가 발생할 때(예: 사용자가 동의를 제공하거나 철회할 때) [!DNL Didomi]이(가) JSON 페이로드가 포함된 실시간 HTTP POST 요청을 구성된 [!DNL webhook] 끝점으로 보냅니다.

![didomi-console](../../images/tutorials/create/didomi/didomi-console.png)

Experience Platform과의 호환성을 보장하려면 웹후크가 다음 요구 사항을 충족해야 합니다.

| 필드 | 설명 | 예 |
| --- | --- | --- | 
| 클라이언트 암호 | Adobe API 자격 증명과 연결된 비밀 키. | `d8f3b2e1-4c9a-4a7f-9b2e-8f1c3d2a1b6e` |
| API 키 | Adobe 서비스에 대한 요청을 인증하는 데 사용되는 공개 API 키입니다. |
| 권한 유형 | 응용 프로그램이 인증 서버에서 액세스 토큰을 가져오는 방법입니다. 이 값을 `client_credentials`(으)로 설정하십시오. | `client_credentials` |
| 범위 | 인증 범위는 응용 프로그램이 API 공급자로부터 요청하는 특정 권한 또는 액세스 수준을 정의합니다. | `openid,AdobeID,read_organizations,additional_info.projectedProductContext,session` |
| 인증 헤더 | Adobe 토큰 요청에 필요한 추가 헤더입니다. | `{"Content-type": "application/x-www-form-urlencoded"}` |
| 토큰 URL | Adobe 토큰 엔드포인트. | `https://ims-na1.adobelogin.com/ims/token/v3` |
| 엔드포인트 URL | 최종 Adobe 커넥터 URL(설정 끝에 제공됨)입니다. | `https://dcs.adobedc.net/collection/your-adobe-endpoint-id` |

{style="table-layout:auto"}

[!DNL webhook]에 대해 다음 옵션을 구성합니다.

| 필드 | 설명 | 값 |
| ---| --- | --- | 
| 요청 헤더 | [!DNL webhook]에 대한 사용자 지정 헤더입니다. `x-adobe-flow-id`을(를) 포함해야 합니다. [데이터 흐름이 만들어진](../../tutorials/ui/create/consent-and-preferences/didomi.md#retrieve-the-streaming-endpoint-url) 후에 이 값을 검색할 수 있습니다. | `{"Content-Type": "application/json", "Cache-Control": "no-cache", "x-adobe-flow-id": "{DATAFLOW_ID}"}` |
| 평면화 | 이 속성은 [!DNL webhook] 데이터가 플랫 개체로 전송될 수 있도록 하기 때문에 확인해야 합니다. | 활성화됨 |
| 이벤트 유형 | [!DNL Didomi]을(를) 트리거해야 하는 특정 `event.*` 이벤트 그룹(`user.*` 또는 [!DNL webhook])을 선택하십시오. `event.*`을(를) 사용하여 동의 또는 환경 설정 변경을 추적하고 `user.*`을(를) 사용하여 사용자 프로필 업데이트를 추적합니다. 이 선택은 호환 가능한 이벤트만 Adobe으로 전송하는 데 필요합니다. Adobe은 데이터 흐름당 하나의 스키마만 지원하므로 두 이벤트 유형을 모두 선택하면 수집 오류가 발생할 수 있습니다. | 지원되는 이벤트 유형 목록은 다음과 같습니다. <ul><li>`Event.created`</li><li>`Event.updated`</li><li>`Event.deleted`</li><li>`User.created`</li><li>`User.updated`</li><li>`User.deleted`</li></ul> |

### 샘플 페이로드 파일 다운로드 {#download-the-sample-payload-file}

선택한 이벤트 그룹을 기반으로 **콘솔에서 적절한**&#x200B;샘플 페이로드 파일[!DNL Didomi]을(를) 직접 다운로드합니다. 이 파일은 데이터 구조를 나타내며 Adobe의 스키마 및 매핑 단계 중에 사용됩니다.

| **이벤트 그룹** | **다운로드할 샘플 파일** | **필터링 옵션** |
| --- | ---| --- |
| `event.*` | `event.created`에 대한 샘플 다운로드 | `event.*`개 이벤트만 필터링 |
| `user.*` | `user.created`에 대한 샘플 다운로드 | `user.*`개 이벤트만 필터링 |

## [!DNL Didomi] 계정을 Experience Platform에 연결

소스 연결을 만들고 동의 및 환경 설정 데이터를 [에서 Experience Platform으로 수집하는 방법을 알아보려면  [!DNL Didomi] 연결](../../tutorials/ui/create/consent-and-preferences/didomi.md)에서 Experience Platform[!DNL Didomi]에 대한 안내서를 읽어 보십시오.
