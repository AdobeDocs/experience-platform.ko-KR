---
keywords: Experience Platform;홈;인기 항목;identity service api;identity service 개발자 안내서;지역
solution: Experience Platform
title: ID 서비스 API 안내서
description: ID 서비스 API를 사용하면 개발자가 Adobe Experience Platform의 ID 그래프를 사용하여 크로스 디바이스, 크로스 채널 및 거의 실시간으로 고객을 식별할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 14%

---

# [!DNL Identity Service] API 안내서

Adobe Experience Platform [!DNL Identity Service]은(는) Adobe Experience Platform 내에서 id 그래프로 알려진 것을 통해 고객의 크로스 디바이스, 크로스 채널 및 거의 실시간으로 식별하여 관리합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

- [[!DNL Identity Service]](../home.md): 고객 프로필 데이터의 단편화로 인해 발생하는 기본적인 문제를 해결합니다. 이는 고객이 브랜드와 상호 작용하는 디바이스 및 시스템 간에 ID를 연결하여 수행됩니다.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 원본에서 집계한 데이터를 기반으로 통합 소비자 프로필을 실시간으로 제공합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): [!DNL Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

다음 단원에서는 [!DNL Identity Service] API를 성공적으로 호출하기 위해 알고 있어야 하거나 현재 보유하고 있어야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

### 지역 기반 라우팅

[!DNL Identity Service] API는 요청 경로의 일부로 `{REGION}`을(를) 포함해야 하는 지역별 끝점을 사용합니다. 조직을 프로비저닝하는 동안 영역은 조직 프로필 내에서 결정되고 저장됩니다. 각 끝점에 올바른 영역을 사용하면 [!DNL Identity Service] API를 사용하여 만든 모든 요청이 적절한 영역으로 라우팅됩니다.

현재 [!DNL Identity Service] API에서 지원하는 두 개의 지역(VA7 및 NLD2)이 있습니다.

아래 표는 영역을 사용하는 경로의 예를 보여줍니다.

| 서비스 | 지역: VA7 | 지역: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>영역을 지정하지 않고 요청하면 잘못된 영역으로 라우팅되는 호출이 발생하거나 예기치 않게 호출이 실패할 수 있습니다.

조직 프로필 내에서 지역을 찾을 수 없는 경우 시스템 관리자에게 지원을 요청하십시오.

## [!DNL Identity Service] API 사용

이러한 서비스에 사용되는 ID 매개 변수는 복합 또는 XID 중 한 가지 방법으로 표현할 수 있습니다.

복합 ID는 ID 값과 네임스페이스를 모두 포함하는 구문입니다. 복합 ID를 사용하는 경우 이름(`namespace.code`) 또는 ID(`namespace.id`)로 네임스페이스를 제공할 수 있습니다.

ID가 지속되면 [!DNL Identity Service]에서 해당 ID에 네이티브 ID 또는 XID라고 하는 ID를 생성하여 할당합니다. 모든 클러스터 및 매핑 API 변형은 해당 요청 및 응답에서 복합 ID와 XID를 모두 지원합니다. 이러한 API를 사용하려면 매개 변수 중 하나(`xid` 또는 [`ns` 또는 `nsid`]과(와) `id`의 조합)가 필요합니다.

응답에서 페이로드를 제한하기 위해 API는 사용한 ID 구문 유형에 대한 응답을 조정합니다. 즉, XID를 전달하는 경우 응답에는 XID가 생기고, 복합 ID를 전달하는 경우 응답은 요청에 사용된 구조를 따릅니다.

이 문서의 예제에서는 [!DNL Identity Service] API의 전체 기능을 다루지 않습니다. 전체 API에 대해서는 [Swagger API 참조](https://www.adobe.io/experience-platform-apis/references/identity-service)를 참조하십시오.

>[!NOTE]
>
>요청에 네이티브 XID를 사용하면 반환되는 모든 ID가 네이티브 XID 형식으로 표시됩니다. ID/네임스페이스 양식을 사용하는 것이 좋습니다. 자세한 내용은 [ID에 대한 XID 가져오기](./create-custom-namespace.md)에 대한 섹션을 참조하십시오.

## 다음 단계

필요한 자격 증명을 수집했으므로 이제 나머지 개발자 안내서를 계속 읽을 수 있습니다. 각 섹션에서는 해당 끝점에 대한 중요한 정보를 제공하고 CRUD 작업을 수행하기 위한 예제 API 호출을 보여줍니다. 각 호출에는 일반 API 형식, 필요한 헤더와 올바른 형식의 페이로드를 보여주는 샘플 요청 및 성공적인 호출을 위한 샘플 응답이 포함됩니다.
