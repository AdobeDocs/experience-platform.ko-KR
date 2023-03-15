---
keywords: Experience Platform;시작하기;기여도 분석 ai;인기 있는 주제
feature: Attribution AI
title: Attribution AI에서 시작하기
description: 다음 안내서에서는 Attribution AI 사용과 관련된 다양한 Adobe Experience Platform 서비스에 대해 이해해야 합니다. 튜토리얼을 시작하기 전에 다음 문서를 검토하십시오.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Attribution AI에서 시작하기

다음 안내서에서는 다양한 내용을 이해해야 합니다 [!DNL Adobe Experience Platform] Attribution AI 사용과 관련된 서비스. 튜토리얼을 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(경험 데이터 모델) 시스템 개요](../../xdm/home.md): XDM은 을 허용하는 기본 프레임워크입니다 [!DNL Adobe Experience Cloud]을(를) Experience Platform에서 지원하여 적절한 사람에게 적절한 메시지를 적절한 채널에서 정확한 순간에 전달할 수 있습니다. Experience Platform이 구축된 방법론인 XDM 시스템은 플랫폼 서비스에서 사용할 Experience Data Model 스키마를 운영합니다.
- [스키마 컴포지션 기본 사항](../../xdm/schema/composition.md): 이 문서에서는 XDM(Experience Data Model) 스키마와 에서 사용할 스키마를 구성하기 위한 구성 블록, 원칙 및 모범 사례에 대해 소개합니다 [!DNL Adobe Experience Platform].
- [스키마 작성 중](../../xdm/tutorials/create-schema-ui.md): 이 자습서에서는 Experience Platform 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.

Attribution AI을 사용하려면 데이터 세트가 다음과 같은 CEE(Consumer Experience Event) 스키마를 준수해야 합니다. [경험 데이터 모델(XDM)](../../xdm/home.md) 스키마 필드 그룹. 이 데이터를 구현하거나 변경하려면 attributionai-support@adobe.com에서 Adobe 지원 센터에 문의하십시오. 미디어 지출 데이터가 있는 경우 증분 매출 및 ROI와 같은 추가 분석을 수행할 수 있습니다. 고객 프로필 데이터를 사용할 수 있는 경우 크레딧을 고객 프로필 수준에 추가로 연결할 수 있습니다.

## 용어

- **전환 이벤트:** 컨퍼런스 등록과 같이, 고객이 목표를 향한 이정표를 표시하기 위해 수행하는 모든 디지털 이벤트 또는 디지털 상호 작용. 추가 예에는 유료 전환, 무료 계정 등록 또는 트레이트에 대한 자격이 있습니다.

- **접점:** 고객이 목표를 향한 경로에서 수행하는 모든 디지털 이벤트 또는 디지털 상호 작용. 구매 전 관련 마케팅 활동, 본 광고 노출 횟수 표시, 유료 검색 클릭 등이 그 예입니다.

## Attribution AI 점수 다운로드

>[!NOTE]
>
>원시 점수를 다운로드할 필요가 없는 경우 이 단계를 건너뛰고 로 진행할 수 있습니다. [다음 단계](#next-steps).

Attribution AI 점수 다운로드는 API 호출의 조합을 통해 수행됩니다. Platform API를 호출하려면 먼저 다음을 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더의 값이 제공됩니다.

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

## 액세스 제어 {#access-control}

역할 기반 액세스 제어를 사용할 때 **Attribution AI 보기** 및 **Attribution AI 관리** 권한은 Attribution AI의 다양한 기능에 대한 액세스 권한을 부여합니다. 다음 **Attribution AI 관리** 다음 작업을 수행할 수 있습니다. **만들기**, **복제**, **편집**, **삭제**, **활성화**, 또는 **disable** 다음 기간 동안 인스턴스 **Attribution AI 보기** 다음 작업을 수행할 수 있습니다. **읽기** 또는 **보기** 그래. 다음 **만들기**, **편집** 및 **삭제** 작업은 감사 로그로 기록됩니다.

자세한 내용은 설명서 를 참조하십시오 [액세스 제어에 대한 권한 할당](../../../help/access-control/home.md) 또는 방법 [감사 로그를 사용하여 액세스 및 활동 모니터링](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## 다음 단계 {#next-steps}

준비가 완료되고 모든 자격 증명 및 스키마가 준비되면 다음을 수행하여 시작합니다. [Attribution AI 사용자 인터페이스 안내서](./user-guide.md). 이 안내서에서는 인스턴스를 만들고 교육 및 채점을 위해 제출하는 방법을 안내합니다.
