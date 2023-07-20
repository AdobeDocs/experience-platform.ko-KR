---
keywords: Experience Platform;시작하기;고객 ai;인기 있는 주제
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Customer AI에서 시작하기
description: 이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Customer AI에서 시작하기

고객 AI 안내서에서는 고객 AI 사용과 관련된 다양한 플랫폼 서비스에 대한 작업 이해가 필요합니다. 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(경험 데이터 모델) 시스템 개요](../../xdm/home.md): XDM은 을 허용하는 기본 프레임워크입니다 [!DNL Adobe Experience Cloud]을(를) Experience Platform에서 지원하여 적절한 사람에게 적절한 메시지를 적절한 채널에서 정확한 순간에 전달할 수 있습니다. Experience Platform이 구축된 방법론인 XDM 시스템은 플랫폼 서비스에서 사용할 Experience Data Model 스키마를 운영합니다.
- [스키마 컴포지션 기본 사항](../../xdm/schema/composition.md): 이 문서에서는 XDM(Experience Data Model) 스키마와 에서 사용할 스키마를 구성하기 위한 구성 블록, 원칙 및 모범 사례에 대해 소개합니다 [!DNL Adobe Experience Platform].
- [스키마 작성 중](../../xdm/tutorials/create-schema-ui.md): 이 자습서에서는 Experience Platform 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.
- [실시간 고객 프로필 개요](../../rtcdp/overview.md): 빌드 날짜 [!DNL Adobe Experience Platform], Adobe Real-time Customer Data Platform(Real-Time CDP)는 기업이 알려진 데이터와 알 수 없는 데이터를 통합하여 고객 여정 전반에서 지능적인 의사 결정으로 고객 프로필을 활성화할 수 있도록 지원합니다. Real-Time CDP은 여러 엔터프라이즈 데이터 소스를 결합하여 실시간으로 통합 프로필을 만들어 모든 채널 및 장치에서 일대일 개인화된 고객 경험을 제공하는 데 사용할 수 있습니다.
- [세그먼테이션 서비스 개요](../../segmentation/home.md): 세그먼테이션은 프로필 하위 집합이 공유하는 특정 속성 또는 동작을 프로필 스토어와 정의하여 마케팅 가능한 사용자 그룹과 고객 기반을 구분하는 프로세스입니다. 예를 들어 &quot;운동화 구입하는 것을 잊었습니까?&quot;라는 이메일 캠페인에서 지난 30일 내에 운동화를 찾았지만 구입을 완료하지 않은 모든 사용자를 대상으로 할 수 있습니다. 다양한 세그먼트를 사용하여 다양한 대상자에 집중할 수 있으므로 보다 사용자 지정된 마케팅 경험을 제공할 수 있습니다.
- [세그먼트 빌더 사용 안내서](../../segmentation/tutorials/create-a-segment.md): 플랫폼을 사용하면 세그먼트를 쉽게 만들고 액세스할 수 있을 뿐만 아니라 다양한 기본 구성 요소를 사용하여 세그먼트를 더 특성화할 수 있습니다.

## Customer AI 스코어 다운로드

>[!NOTE]
>
>원시 점수를 다운로드할 필요가 없는 경우 이 단계를 건너뛰고 로 진행할 수 있습니다. [구성 안내서](./user-guide/configure.md).

고객 AI 점수 다운로드는 API 호출의 조합을 통해 수행됩니다. Platform API를 호출하려면 먼저 다음을 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더의 값이 제공됩니다.

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. Platform API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md).

### 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md) Experience Platform 문제 해결 안내서에서 참조하십시오.

## 다음 단계

위의 문서에 설명된 단계를 완료했으면 다음을 방문하십시오. [입력 및 출력](./data-requirements.md) 설명서를 참조하십시오. 이 문서에서는 고객 AI에서 사용 및 생성되는 데이터 유형에 대한 간략한 개요를 제공합니다.
