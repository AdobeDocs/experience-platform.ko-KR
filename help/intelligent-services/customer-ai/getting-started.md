---
keywords: Experience Platform;시작하기;고객 ai;인기 항목
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 고객 AI에서 시작하기
topic-legacy: Getting started
description: 이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# 고객 AI에서 시작하기

고객 AI 안내서를 사용하려면 Customer AI 사용과 관련된 다양한 플랫폼 서비스를 이해하고 있어야 합니다. 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(경험 데이터 모델) 시스템 개요](../../xdm/home.md): XDM은 [!DNL Adobe Experience Cloud]은(는) Experience Platform을 통해 올바른 사용자에게 올바른 메시지를 전달하는 데 필요한 최적의 시간을 제공하기 위해 노력하고 있습니다. Experience Platform을 빌드하는 방법론인 XDM System은 Platform 서비스에서 사용하기 위해 Experience Data Model 스키마를 작동시킵니다.
- [스키마 작성 기본 사항](../../xdm/schema/composition.md): 이 문서에서는 XDM(Experience Data Model) 스키마 및 사용할 스키마를 구성하기 위한 빌딩 블록, 원칙 및 모범 사례를 소개합니다 [!DNL Adobe Experience Platform].
- [스키마 작성](../../xdm/tutorials/create-schema-ui.md): 이 자습서에서는 Experience Platform 내에서 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.
- [실시간 고객 프로필 개요](../../rtcdp/overview.md): 기본 제공 [!DNL Adobe Experience Platform], Adobe Real-time Customer Data Platform (Real-Time CDP)은 회사에서 알려진 데이터와 알 수 없는 데이터를 결합하여 고객 여정 전체에서 지능형 의사 결정을 사용하여 고객 프로필을 활성화하도록 지원합니다. Real-Time CDP은 여러 엔터프라이즈 데이터 소스를 결합하여 실시간으로 통합 프로필을 만듭니다. 이 통합을 통해 모든 채널 및 장치에서 개인화된 고객 경험을 일대일로 제공할 수 있습니다.
- [세그먼테이션 서비스 개요](../../segmentation/home.md): 세그먼테이션은 마케팅 가능한 사람 그룹을 고객 기반과 구분하기 위해 프로필 저장소의 프로필 하위 집합에 의해 공유되는 특정 속성 또는 동작을 정의하는 프로세스입니다. 예를 들어 &quot;운동화 구입을 잊으셨습니까?&quot;라는 이메일 캠페인에서 지난 30일 이내에 운동화 구매를 검색했지만 구매를 완료하지 않은 모든 사용자의 청중을 원할 수 있습니다. 다양한 세그먼트를 사용하여 다양한 대상에 집중하여 보다 맞춤형 마케팅 경험을 제공할 수 있습니다.
- [세그먼트 빌더 사용 안내서](../../segmentation/tutorials/create-a-segment.md): Platform을 사용하면 세그먼트를 쉽게 만들고 액세스할 수 있을 뿐만 아니라 다른 구성 요소를 사용하여 세그먼트를 더 규명할 수 있습니다.

## Customer AI 점수 다운로드

>[!NOTE]
>
>원시 점수를 다운로드할 필요가 없는 경우 이 단계를 건너뛰고 다음 단계로 진행할 수 있습니다. [구성 안내서](./user-guide/configure.md).

Customer AI 점수를 다운로드하는 것은 API 호출 조합을 통해 수행됩니다. 플랫폼 API를 호출하려면 먼저 를 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 권한 부여: 베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. Platform API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md).

### 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md) Experience Platform 문제 해결 안내서에서 을 참조하십시오.

## 액세스 제어 {#access-control}

액세스 제어를 사용하는 경우 **고객 AI 보기** 및 **고객 AI 관리** 권한은 고객 AI의 다양한 기능에 대한 액세스 권한을 부여합니다. 다음 **고객 AI 관리** 사용 권한 을 통해 **만들기**,**업데이트**, **delete**, **활성화**, 또는 **disable** 다음 기간 동안 인스턴스 **고객 AI 보기** 이를 읽거나 볼 수 있습니다. 다음 **만들기**, **업데이트** 및 **delete** 작업은 감사 로그에 기록됩니다.

자세한 내용은 설명서 를 참조하십시오 [액세스 제어 권한 할당](../../../help/access-control/home.md) 또는 방법 [감사 로그를 사용하여 액세스 및 활동 모니터링](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## 다음 단계

위의 문서에 설명된 단계를 완료하면 [입력 및 출력](./input-output.md) 설명서. 이 문서에서는 고객 AI에서 사용 및 생성되는 데이터 유형에 대한 간단한 개요를 제공합니다.
