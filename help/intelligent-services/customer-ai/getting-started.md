---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: 고객 AI 시작하기
topic: Getting started
description: 이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# 고객 AI 시작하기

고객 AI를 위한 가이드는 고객 AI 사용과 관련된 다양한 플랫폼 서비스에 대해 자세히 알고 있어야 합니다. 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(Experience Data Model) 시스템 개요](../../xdm/home.md):XDM은 Experience Platform [!DNL Adobe Experience Cloud]를 기반으로 올바른 고객에게 정확한 타이밍에 적합한 채널을 통해 올바른 메시지를 전달할 수 있는 기본 프레임워크입니다. XDM System은 Experience Platform이 구축되는 방법론을 통해 플랫폼 서비스에서 사용하기 위해 경험 데이터 모델 스키마를 운영합니다.
- [스키마 컴포지션의 기본 사항](../../xdm/schema/composition.md):이 문서에서는 XDM(Experience Data Model) 스키마 및 사용할 스키마 작성에 대한 기본 블록, 원칙 및 모범 사례에 대해 소개합니다 [!DNL Adobe Experience Platform].
- [스키마 빌드](../../xdm/tutorials/create-schema-ui.md):이 자습서에서는 Experience Platform 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.
- [실시간 고객 프로필 개요](../../rtcdp/overview.md):실시간 CDP(Customer Data Platform)를 기반으로 구축된 실시간 고객 데이터 플랫폼 [!DNL Adobe Experience Platform]을 사용하면 알려진 데이터와 알려지지 않은 데이터를 결합하여 고객 여정 전반에서 지능적인 의사 결정을 통해 고객 프로파일을 활성화할 수 있습니다. 실시간 CDP는 여러 엔터프라이즈 데이터 소스를 통합하여 실시간으로 통합 프로파일을 생성하므로 모든 채널과 디바이스에서 개인화된 고객 경험을 제공하는 데 사용할 수 있습니다.
- [세그멘테이션 서비스 개요](../../segmentation/home.md):세그먼테이션은 프로필 하위 세트가 공유한 특정 특성 또는 행동을 프로필 스토어와 비교하여 마케팅 가능한 사용자 그룹을 고객 기반과 구분하는 프로세스입니다. 예를 들어 &quot;운동화 구입을 잊으셨습니까?&quot;라는 이메일 캠페인에서 지난 30일 이내에 운동화를 검색했지만 구매를 완료하지 않은 모든 사용자가 운동화를 구매해야 할 수 있습니다. 다양한 세그먼트를 사용하여 다양한 고객에 초점을 맞춰 보다 맞춤화된 마케팅 경험을 제공할 수 있습니다.
- [세그먼트 빌더 사용 안내서](../../segmentation/tutorials/create-a-segment.md):플랫폼을 사용하면 세그먼트를 쉽게 만들고 액세스할 수 있을 뿐만 아니라, 다양한 기본 요소를 사용하여 세그먼트를 더욱 구체화할 수 있습니다.

## 고객 AI 점수 다운로드

>[!NOTE]
>
>Raw 점수를 다운로드할 필요가 없는 경우 이 단계를 건너뛰고 [구성 안내서로 진행할 수 있습니다](./user-guide/configure.md).

고객 AI 점수 다운로드는 API 호출 조합을 통해 이루어집니다. 플랫폼 API를 호출하려면 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 예제 API 호출 [](../../landing/troubleshooting.md) 읽기 방법에 대한 섹션을 참조하십시오.

## 다음 단계

위의 문서에 설명된 단계를 완료하면 [입력 및 출력](./input-output.md) 설명서를 참조하십시오. 이 문서에서는 고객 AI에서 사용 및 생성되는 데이터 유형에 대한 간략한 개요를 제공합니다.