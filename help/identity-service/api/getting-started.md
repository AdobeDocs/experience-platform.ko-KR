---
keywords: Experience Platform;홈;인기 항목;ID 서비스 api;ID 서비스 개발자 안내서;지역
solution: Experience Platform
title: Identity Service API 안내서
topic-legacy: API guide
description: Identity 서비스 API를 사용하여 개발자는 Adobe Experience Platform에서 ID 그래프를 사용하여 교차 장치, 교차 채널 및 거의 실시간 고객 ID를 관리할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 2%

---

# [!DNL Identity Service] API 안내서

Adobe Experience Platform [!DNL Identity Service] Adobe Experience Platform 내에서 ID 그래프라고 하는 것에서 고객을 교차 장치, 교차 채널 및 거의 실시간 식별하도록 관리합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Identity Service]](../home.md): 고객 프로필 데이터 조각화에 의해 발생하는 근본적인 문제를 해결합니다. 고객이 브랜드와 상호 작용하는 장치 및 시스템에서 ID를 브리징하여 이를 수행합니다.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 실시간으로 제공합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.

다음 섹션에서는 를 성공적으로 호출하기 위해 알고 있거나 현재 상태여야 하는 추가 정보를 제공합니다 [!DNL Identity Service] API.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- 권한 부여: 베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

### 지역 기반 라우팅

다음 [!DNL Identity Service] API는 `{REGION}` 를 요청 경로의 일부로 포함했습니다. IMS 조직을 프로비저닝하는 동안 영역은 IMS 조직 프로필 내에서 결정 및 저장됩니다. 각 종단점에 올바른 영역을 사용하면 [!DNL Identity Service] API는 해당 영역으로 라우팅됩니다.

현재 지원되는 두 개의 지역이 있습니다. [!DNL Identity Service] API: VA7와 NLD2입니다.

아래 표는 지역을 사용하는 경로의 예를 보여줍니다.

| 서비스 | 지역: VA7 | 지역: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>지역을 지정하지 않고 요청을 수행하면 잘못된 지역으로 라우팅이 전송되거나 호출이 예기치 않게 실패할 수 있습니다.

IMS 조직 프로필 내에서 해당 지역을 찾을 수 없는 경우 시스템 관리자에게 문의하여 지원을 받으십시오.

## 사용 [!DNL Identity Service] API

이러한 서비스에 사용되는 ID 매개 변수는 두 가지 방법 중 하나로 표시할 수 있습니다. XID 또는 XID를 조합합니다.

복합 ID는 ID 값과 네임스페이스를 모두 포함하는 구문입니다. 복합 ID를 사용할 때 이름(`namespace.code`) 또는 ID(`namespace.id`).

ID가 유지되면 [!DNL Identity Service] 는 기본 ID 또는 XID라고 하는 해당 ID에 ID를 생성하여 할당합니다. 클러스터 및 매핑 API의 모든 변형은 해당 요청과 응답에서 복합 ID와 XID를 모두 지원합니다. 매개 변수 중 하나가 필요합니다. `xid` 또는 조합 [`ns` 또는 `nsid`] 및 `id` 를 사용하십시오.

응답에서 페이로드를 제한하기 위해 API는 사용된 ID 구성 유형에 대한 응답을 조정합니다. 즉, XID를 전달하는 경우 응답에 XID가 있고 복합 ID를 전달하는 경우 응답에는 요청에 사용된 구조를 따릅니다.

이 문서의 예제는 [!DNL Identity Service] API. 전체 API에 대해서는 [Swagger API 참조](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>요청에서 네이티브 XID를 사용하는 경우 반환되는 모든 ID는 기본 XID 양식에 표시됩니다. ID/네임스페이스 양식을 사용하는 것이 좋습니다. 자세한 내용은 [id에 대한 XID 가져오기](./create-custom-namespace.md).

## 다음 단계

이제 필요한 자격 증명을 수집했으므로 개발자 가이드의 나머지 부분을 계속 읽을 수 있습니다. 각 섹션에서는 종단점에 대한 중요한 정보를 제공하며 CRUD 작업을 수행하기 위한 예제 API 호출을 보여줍니다. 각 호출에는 일반 API 형식, 필수 헤더와 올바른 형식의 페이로드를 보여주는 샘플 요청 및 성공적인 호출을 위한 샘플 응답이 포함되어 있습니다.
