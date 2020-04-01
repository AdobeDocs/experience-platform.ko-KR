---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: 고객 AI에서 시작하기
topic: Getting started
translation-type: tm+mt
source-git-commit: 0eeb41fa06864cc28b3a76c2a69c76ea5430d45a

---


# 고객 AI에서 시작하기

고객 AI에 대한 가이드는 고객 AI 사용과 관련된 다양한 플랫폼 서비스에 대한 충분한 지식이 있어야 합니다. 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(Experience Data Model) 시스템 개요](../../xdm/home.md):XDM은 Adobe Experience Cloud가 Adobe Experience Platform을 기반으로 정확한 타이밍에 적합한 고객에게 올바른 메시지를 전달할 수 있는 기본 프레임워크입니다. XDM System은 경험 플랫폼을 구축하는 방법론을 통해 경험 데이터 모델 스키마를 플랫폼 서비스에서 사용할 수 있도록 운영했습니다.
- [스키마 컴포지션의](../../xdm/schema/composition.md)기본 사항:이 문서에서는 XDM(Experience Data Model) 스키마와 Adobe Experience Platform에서 사용할 스키마를 작성하기 위한 기본 요소, 원칙 및 모범 사례에 대해 소개합니다.
- [스키마 작성](../../xdm/tutorials/create-schema-ui.md):이 자습서에서는 경험 플랫폼 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.
- [실시간 고객 프로필 개요](../../rtcdp/overview.md):Adobe Experience Platform(실시간 고객 데이터 플랫폼)을 기반으로 구축된 Adobe 실시간 CDP(Customer Data Platform)를 통해 알려진 데이터와 알려지지 않은 데이터를 통합하여 고객 여정 전반에 걸쳐 지능적인 의사 결정을 통해 고객 프로파일을 활성화할 수 있습니다. 실시간 CDP는 여러 엔터프라이즈 데이터 소스를 통합하여 실시간으로 프로파일을 통합함으로써 모든 채널과 디바이스에서 개인화된 고객 경험을 제공할 수 있습니다.
- [세그멘테이션 서비스 개요](../../segmentation/home.md):세그먼테이션은 프로필 하위 세트가 프로필 스토어와 공유한 특정 특성 또는 행동을 정의하여 마케팅 가능한 사용자 그룹과 고객 기반을 구별하는 프로세스입니다. 예를 들어 &quot;운동화 구입을 잊으셨습니까?&quot;라는 이메일 캠페인에서 지난 30일 이내에 운동화를 검색했지만 구매를 완료하지 않은 모든 사용자를 원할 수 있습니다. 다양한 세그먼트를 사용하여 다양한 고객에 초점을 맞춰 보다 맞춤화된 마케팅 경험을 제공할 수 있습니다.
- [세그먼트 빌더 사용 안내서](../../segmentation/tutorials/create-a-segment.md):플랫폼을 사용하면 세그먼트를 쉽게 만들고 액세스할 수 있을 뿐만 아니라, 다른 구성 요소를 사용하여 세그먼트를 더 자세히 특정할 수 있습니다.

## 고객 AI 점수 다운로드

>[!NOTE] Raw 점수를 다운로드할 필요가 없는 경우 이 단계를 건너뛰고 사용자 인터페이스 가이드로 진행할 수 있습니다.

고객 AI 점수 다운로드는 API 호출 조합을 통해 이루어집니다. 플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md) 방법에 대한 섹션을 참조하십시오.

## 다음 단계

모든 자격 증명과 스키마를 준비했으면 고객 AI [사용자 인터페이스 가이드를](./user-guide.md)따라 시작하십시오. 이 안내서에서는 인스턴스를 만들고 이를 교육 및 점수 책정용으로 제출하는 과정을 안내합니다.