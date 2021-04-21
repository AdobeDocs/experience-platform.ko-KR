---
keywords: Experience Platform;홈;인기 항목;ID 서비스 api;ID 서비스 개발자 안내서;지역
solution: Experience Platform
title: ID 서비스 API 안내서
topic-legacy: API guide
description: 개발자는 Identity Service API를 사용하여 Adobe Experience Platform에서 ID 그래프를 사용하여 디바이스 간, 크로스 채널 및 거의 실시간으로 고객 ID를 관리할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보려면 이 안내서를 따르십시오.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# [!DNL Identity Service] API 안내서

Adobe Experience Platform [!DNL Identity Service]은 Adobe Experience Platform 내의 ID 그래프라고 하는 것을 통해 고객을 거의 실시간으로 식별하면서 디바이스 간, 크로스 채널을 관리합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [[!DNL Identity Service]](../home.md):고객 프로파일 데이터의 세분화로 인한 기본적인 문제를 해결합니다. 고객이 브랜드와 상호 작용하는 장치 및 시스템 간의 ID를 연결함으로써 이렇게 됩니다.
- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 실시간으로 제공합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크

다음 섹션에서는 [!DNL Identity Service] API를 성공적으로 호출하기 위해 알아야 하거나 현재 가지고 있는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:Bearer `{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

### 지역 기반 라우팅

[!DNL Identity Service] API는 요청 경로의 일부로 `{REGION}`을(를) 포함해야 하는 지역 특정 끝점을 사용합니다. IMS 조직을 프로비저닝하는 동안 IMS 조직 프로필 내에서 영역이 결정 및 저장됩니다. 각 끝점에서 올바른 영역을 사용하면 [!DNL Identity Service] API를 사용하여 수행한 모든 요청이 해당 영역으로 라우팅됩니다.

현재 [!DNL Identity Service] API에서 지원하는 두 개의 영역이 있습니다.VA7과 NLD2.

아래 표는 영역을 사용하는 경로의 예를 보여줍니다.

| 서비스 | 지역:VA7 | 지역:NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>영역을 지정하지 않은 요청은 잘못된 영역에 대한 호출 라우팅이 발생하거나 호출이 예기치 않게 실패할 수 있습니다.

IMS 조직 프로필 내에서 지역을 찾을 수 없는 경우 시스템 관리자에게 지원을 요청하십시오.

## [!DNL Identity Service] API 사용

이러한 서비스에 사용되는 ID 매개 변수는 두 가지 방법 중 하나로 나타낼 수 있습니다.합성 또는 XID로 생성할 수 있습니다.

합성 ID는 ID 값과 네임스페이스를 모두 포함하는 구문입니다. 복합 ID를 사용할 때 이름(`namespace.code`) 또는 ID(`namespace.id`)로 네임스페이스를 제공할 수 있습니다.

ID가 지속되는 경우 [!DNL Identity Service]은(는) 기본 ID 또는 XID라는 ID를 생성하고 할당합니다. 클러스터 및 매핑 API의 모든 변형은 요청 및 응답에서 합성 ID와 XID를 모두 지원합니다. 이러한 API를 사용하려면 `xid` 또는 [`ns` 또는 `nsid`] 및 `id`의 조합이 필요합니다.

응답에서 페이로드를 제한하기 위해 API는 사용되는 ID 구문 유형에 대한 응답을 조정합니다. 즉, XID를 전달하면 응답에 XID가 있고 복합 ID를 전달하면 응답에 요청에 사용된 구조가 따릅니다.

이 문서의 예에는 [!DNL Identity Service] API의 전체 기능이 포함되지 않습니다. 전체 API에 대해서는 [Swagger API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)를 참조하십시오.

>[!NOTE]
>
>요청에서 기본 XID를 사용하면 반환된 모든 ID는 기본 XID 형태로 유지됩니다. ID/네임스페이스 양식을 사용하는 것이 좋습니다. 자세한 내용은 ID](./create-custom-namespace.md)에 대한 XID 가져오기의 섹션을 참조하십시오.[

## 다음 단계

이제 필요한 자격 증명을 수집했으므로 개발자 가이드의 나머지 부분을 계속 읽을 수 있습니다. 각 섹션은 해당 끝점에 대한 중요한 정보를 제공하며 CRUD 작업을 수행하기 위한 API 호출 예를 보여줍니다. 각 호출에는 일반 API 형식, 필수 헤더와 올바른 형식의 페이로드를 표시하는 샘플 요청 및 성공적인 호출을 위한 샘플 응답이 포함됩니다.
