---
keywords: Experience Platform;시작하기;고객 ai;인기 항목;;getting started;customer ai;popular topics
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 고객 AI에서 시작하기
topic-legacy: Getting started
description: 이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# 고객 AI에서 시작하기

고객 AI를 위한 가이드는 고객 AI 사용과 관련된 다양한 플랫폼 서비스에 대한 충분한 지식이 있어야 합니다. 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(Experience Data Model) 시스템 개요](../../xdm/home.md):XDM은 Experience Platform [!DNL Adobe Experience Cloud]를 기반으로 올바른 고객에게 올바른 메시지를 정확한 타이밍에 적합한 채널에 전달할 수 있는 기본 프레임워크입니다. Experience Platform이 구축되는 방법론, XDM 시스템은 플랫폼 서비스에서 사용하기 위해 경험 데이터 모델 스키마를 운영합니다.
- [스키마 컴포지션의 기본 사항](../../xdm/schema/composition.md):이 문서에서는 XDM(Experience Data Model) 스키마 및 사용할 스키마를 작성하기 위한 기본 블록, 원칙 및 모범 사례에 대해 설명합니다 [!DNL Adobe Experience Platform].
- [스키마 작성](../../xdm/tutorials/create-schema-ui.md):이 자습서에서는 Experience Platform 내에서 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.
- [실시간 고객 프로필 개요](../../rtcdp/overview.md):실시간  [!DNL Adobe Experience Platform]CDP(Customer Data Platform)를 기반으로 구축된 실시간 고객 데이터 플랫폼(CDP)을 사용하면 널리 알려진 데이터와 알려지지 않은 데이터를 결합하여 고객 여정 전반에 걸쳐 지능적인 의사 결정을 통해 고객 프로파일을 활성화할 수 있습니다. 실시간 CDP는 여러 엔터프라이즈 데이터 소스를 통합하여 실시간으로 통합 프로파일을 생성하여 모든 채널과 디바이스에서 개인화된 고객 경험을 제공하는 데 사용할 수 있습니다.
- [세그멘테이션 서비스 개요](../../segmentation/home.md):세그먼테이션은 프로필 하위 세트가 프로필 스토어와 공유한 특정 특성 또는 행동을 정의하여 마케팅 가능한 사람 그룹을 고객 기반과 구별하는 프로세스입니다. 예를 들어 &quot;운동화 구입을 잊으셨습니까?&quot;라는 이메일 캠페인에서는 지난 30일 이내에 운동화를 검색했지만 구매를 완료하지 않은 모든 사용자를 원할 수 있습니다. 세그먼트가 다른 경우 다양한 대상에 집중할 수 있으므로 보다 맞춤화된 마케팅 경험을 제공할 수 있습니다.
- [세그먼트 빌더 사용 안내서](../../segmentation/tutorials/create-a-segment.md):플랫폼을 사용하면 세그먼트를 쉽게 만들고 액세스할 수 있을 뿐만 아니라, 다양한 기본 요소를 사용하여 세그먼트를 더욱 구체화할 수 있습니다.

## 고객 AI 점수 다운로드

>[!NOTE]
>
>원시 점수를 다운로드할 필요가 없는 경우 이 단계를 건너뛰고 [구성 안내서](./user-guide/configure.md)로 진행할 수 있습니다.

고객 AI 점수 다운로드는 API 호출 조합을 통해 수행됩니다. 플랫폼 API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:Bearer `{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md)를 읽는 방법을 참조하십시오.

## 다음 단계

위의 문서에 설명된 단계를 완료했으면 [입력 및 출력](./input-output.md) 설명서를 방문하십시오. 이 문서에서는 고객 AI에서 사용 및 생성되는 데이터 유형에 대한 간략한 개요를 제공합니다.
