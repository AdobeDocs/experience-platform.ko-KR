---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 시작하기
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Identity Service API 개발자 가이드

Adobe Experience Platform Identity Service는 Adobe Experience Platform에서 ID 그래프로 알려진 것을 통해 고객의 크로스 디바이스, 크로스채널 및 거의 실시간 ID를 관리합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [ID 서비스](../home.md):고객 프로파일 데이터의 세분화로 인한 기본적인 문제를 해결합니다. 이는 고객이 브랜드와 상호 작용하는 디바이스 및 시스템에 걸쳐 ID를 결합함으로써 이루어집니다.
- [실시간 고객 프로필](../../profile/home.md):다양한 소스의 데이터를 집계하여 실시간으로 통합된 고객 프로파일을 제공합니다.
- [XDM(Experience Data Model)](../../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

다음 섹션에서는 Identity Service API를 성공적으로 호출하기 위해 알아야 하거나 현재 보유하고 있는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

### 지역 기반 라우팅

Identity Service API는 요청 경로의 `{REGION}` 일부로 포함시켜야 하는 영역별 끝점을 사용합니다. IMS 조직 프로비전 중에 영역은 IMS 조직 프로필 내에서 결정되고 저장됩니다. 각 끝점에 올바른 영역을 사용하면 Identity Service API를 사용하여 수행한 모든 요청이 해당 영역으로 라우팅됩니다.

현재 Identity Service API에서 지원하는 두 개의 영역이 있습니다.VA7과 NLD2.

아래 표는 지역을 사용하는 경로의 예를 보여줍니다.

| 서비스 | 지역:VA7 | 지역:NLD2 |
| ------ | -------- |--------- |
| ID 서비스 API | https://</span>platform-va7.adobe</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| ID 네임스페이스 API | https://</span>platform-va7.adobe</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] 지역을 지정하지 않고 수행한 요청은 잘못된 영역에 대한 호출 라우팅이 발생하거나 호출이 예기치 않게 실패할 수 있습니다.

IMS 조직 프로필 내에서 지역을 찾을 수 없는 경우 시스템 관리자에게 지원을 요청하십시오.

## ID 서비스 API 사용

이러한 서비스에 사용되는 ID 매개 변수는 두 가지 방법 중 하나로 표현될 수 있습니다.복합 또는 XID.

복합 ID는 ID 값과 네임스페이스를 모두 포함하는 구문입니다. 복합 ID를 사용하는 경우 이름(`namespace.code`) 또는 ID(`namespace.id`)로 네임스페이스를 제공할 수 있습니다.

ID가 지속되는 경우 Identity Service는 해당 ID에 기본 ID 또는 XID라는 ID를 생성하고 할당합니다. 모든 클러스터 및 매핑 API의 변형은 요청 및 응답에서 합성 ID와 XID를 모두 지원합니다. 매개 변수 중 하나는 이러한 API `xid` 를 [`ns` 조합하거나 `nsid`] 사용해야 `id` 합니다.

응답에서 페이로드를 제한하기 위해 API는 사용된 ID 구성 유형에 대한 응답을 조정합니다. 즉, XID를 전달하면 응답에 XID가 있고 복합 ID를 전달하면 응답에 요청에 사용된 구조가 따릅니다.

이 문서의 예에서는 Identity Service API의 전체 기능을 다루지 않습니다. 전체 API는 Swagger API [참조를 참조하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE] 요청에서 기본 XID를 사용하는 경우 반환된 모든 ID는 기본 XID 형식으로 표시됩니다. ID/네임스페이스 양식을 사용하는 것이 좋습니다. 자세한 내용은 ID용 XID [가져오기에 대한 섹션을 참조하십시오](./create-custom-namespace.md).

## 다음 단계

이제 필요한 자격 증명을 수집했으므로 개발자 가이드의 나머지 부분을 계속 읽을 수 있습니다. 각 섹션에서는 끝점에 대한 중요한 정보를 제공하며 CRUD 작업 수행을 위한 예제 API 호출을 보여줍니다. 각 호출에는 일반 API **형식**, 필요한 헤더와 올바른 형식의 페이로드를 표시하는 샘플 **요청** 및 성공적인 호출을 위한 샘플 **응답이** 포함됩니다.
