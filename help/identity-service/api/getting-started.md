---
keywords: Experience Platform;home;popular topics;identity service api;identity service developer guide;region
solution: Experience Platform
title: 시작하기
topic: API guide
description: 'Adobe Experience Platform ID 서비스는 Adobe Experience Platform에서 ID 그래프라고 하는 것을 통해 고객의 크로스 디바이스, 크로스채널 및 거의 실시간 ID를 관리합니다. '
translation-type: tm+mt
source-git-commit: fa667d86c089c692f22cfd1b46f3f11b6e9a68d7
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 1%

---


# [!DNL Identity Service] API 개발자 가이드

Adobe Experience Platform [!DNL Identity Service] 는 Adobe Experience Platform 내에서 고객을 거의 실시간으로 식별하는 크로스 디바이스, 크로스채널을 관리합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

- [[!DNL Identity Service]](../home.md):고객 프로필 데이터 세분화로 인한 기본적인 문제를 해결합니다. 이는 고객이 브랜드와 상호 작용하는 장치 및 시스템 간의 ID를 결합함으로써 이루어집니다.
- [[!DNL 실시간 고객 프로필]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 실시간으로 제공합니다.
- [[!DNL 경험 데이터 모델(XDM)]](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

다음 섹션에서는 [!DNL Identity Service] API를 성공적으로 호출하기 위해 알아야 하거나 현 상태로 두어야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

### 지역 기반 라우팅

API는 [!DNL Identity Service] 요청 경로의 일부로서 항목을 포함시켜야 하는 지역 특정 끝점 `{REGION}` 을 사용합니다. IMS 조직 제공 중 IMS 조직 프로필 내에서 영역이 결정 및 저장됩니다. 각 끝점이 있는 올바른 영역을 사용하면 [!DNL Identity Service] API를 사용하여 수행한 모든 요청이 해당 지역으로 라우팅됩니다.

현재 API에서 지원하는 두 개의 영역이 [!DNL Identity Service] 있습니다.VA7과 NLD2.

아래 표는 영역을 사용하는 방법의 예를 보여줍니다.

| 서비스 | 지역:VA7 | 지역:NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>지역을 지정하지 않은 요청은 잘못된 영역에 대한 호출 라우팅을 초래하거나 예기치 않게 호출이 실패할 수 있습니다.

IMS 조직 프로필 내에서 지역을 찾을 수 없는 경우 시스템 관리자에게 지원을 문의하십시오.

## API [!DNL Identity Service] 사용

이러한 서비스에 사용되는 ID 매개 변수는 두 가지 방법 중 하나로 나타낼 수 있습니다.합성 또는 XID.

복합 ID는 ID 값과 네임스페이스를 모두 포함하는 구문입니다. 복합 ID를 사용하는 경우 이름(`namespace.code`) 또는 ID(`namespace.id`)로 네임스페이스를 제공할 수 있습니다.

ID가 유지되면 기본 ID 또는 XID라는 ID를 생성하여 해당 ID에 할당합니다. [!DNL Identity Service] 클러스터 및 매핑 API의 모든 변형은 요청 및 응답에서 합성 ID와 XID를 모두 지원합니다. 매개 변수 중 하나는 이러한 API를 `xid` 사용하거나 [`ns` 조합하여 사용해야 `nsid`]`id` 합니다.

응답에서 페이로드를 제한하기 위해 API는 사용되는 ID 구문 유형에 대한 응답을 조정합니다. 즉, XID를 전달하면 응답에 XID가 있고 복합 ID를 전달하면 응답에 요청에 사용된 구조가 따릅니다.

이 문서의 예제는 [!DNL Identity Service] API의 전체 기능을 포함하지 않습니다. 전체 API는 [Swagger API 참조를 참조하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE]
>
>요청에서 기본 XID를 사용하는 경우 반환되는 모든 ID는 기본 XID 양식으로 설정됩니다. ID/네임스페이스 양식을 사용하는 것이 좋습니다. 자세한 내용은 ID용 XID [가져오기에 대한 섹션을 참조하십시오](./create-custom-namespace.md).

## 다음 단계

이제 필요한 자격 증명을 수집했으므로 개발자 가이드의 나머지 부분을 계속 읽을 수 있습니다. 각 섹션은 해당 끝점과 관련된 중요한 정보를 제공하며 CRUD 작업을 수행하기 위한 예제 API 호출을 보여줍니다. 각 호출에는 일반 API 형식, 필요한 헤더와 올바른 형식의 페이로드를 보여주는 샘플 요청 및 성공적인 호출을 위한 샘플 응답이 포함됩니다.
