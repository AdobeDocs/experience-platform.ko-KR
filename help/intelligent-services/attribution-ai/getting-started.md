---
keywords: Experience Platform;시작하기;attribution ai;인기 있는 주제
feature: Attribution AI
title: Attribution AI 시작하기
description: 다음 안내서에서는 기여도 AI 사용과 관련된 다양한 Adobe Experience Platform 서비스에 대해 이해해야 합니다. 튜토리얼을 시작하기 전에 다음 문서를 검토하십시오.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 6%

---

# Attribution AI 시작하기

다음 안내서에서는 Attribution AI 사용과 관련된 다양한 [!DNL Adobe Experience Platform] 서비스를 이해해야 합니다. 튜토리얼을 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(Experience Data Model) 시스템 개요](../../xdm/home.md): XDM은 Experience Platform에서 제공하는 [!DNL Adobe Experience Cloud]이(가) 올바른 사람에게 올바른 메시지를 올바른 채널에서 정확한 순간에 전달할 수 있도록 하는 기본 프레임워크입니다. Experience Platform이 구축된 방법론인 XDM 시스템은 Experience Platform 서비스에서 사용할 Experience Data Model 스키마를 운영합니다.
- [스키마 작성의 기본 사항](../../xdm/schema/composition.md): 이 문서에서는 XDM(Experience Data Model) 스키마와 [!DNL Adobe Experience Platform]에서 사용할 스키마를 작성하기 위한 기본 구성 요소, 원칙 및 모범 사례에 대해 소개합니다.
- [스키마 빌드](../../xdm/tutorials/create-schema-ui.md): 이 자습서에서는 Experience Platform 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 다룹니다.

기여도 AI를 사용하려면 데이터 세트가 [XDM(경험 데이터 모델)](../../xdm/home.md) 스키마 필드 그룹인 CEE(소비자 경험 이벤트) 스키마를 준수해야 합니다. 이 데이터를 구현하거나 변경하려면 attributionai-support@adobe.com에서 Adobe 지원 센터에 문의하십시오. 미디어 지출 데이터가 있는 경우 증분 매출 및 ROI와 같은 추가 분석을 수행할 수 있습니다. 고객 프로필 데이터를 사용할 수 있는 경우 크레딧을 고객 프로필 수준에 추가로 연결할 수 있습니다.

## 용어

- **전환 이벤트:** 전화 회의 등록과 같이 고객이 목표에 대한 이정표를 표시하기 위해 수행하는 모든 디지털 이벤트 또는 디지털 상호 작용입니다. 추가 예에는 유료 전환, 무료 계정 등록 또는 트레이트에 대한 자격이 있습니다.

- **접점:** 고객이 목표를 향한 경로에서 수행하는 모든 디지털 이벤트 또는 디지털 상호 작용입니다. 구매 전 관련 마케팅 활동, 본 광고 노출 횟수 표시, 유료 검색 클릭 등이 그 예입니다.

## Attribution AI 점수 다운로드

>[!NOTE]
>
>원시 점수를 다운로드할 필요가 없는 경우 이 단계를 건너뛰고 [다음 단계](#next-steps)로 진행할 수 있습니다.

기여도 AI 점수 다운로드는 API 호출의 조합을 통해 수행됩니다. Experience Platform API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더에 대한 값이 제공됩니다.

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. Experience Platform API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

### 샘플 API 호출 읽기

이 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md)에 대한 섹션을 참조하십시오.

## 액세스 제어 {#access-control}

역할 기반 액세스 제어를 사용하는 경우 **기여도 AI 보기** 및 **기여도 AI 관리** 권한은 기여도 AI의 다양한 기능에 대한 액세스 권한을 부여합니다. **기여도 분석 AI 관리**&#x200B;를 통해 인스턴스를 **생성**, **복제**, **편집**, **삭제**, **활성화** 또는 **비활성화**&#x200B;할 수 있고 **기여도 분석 AI 보기**&#x200B;를 통해 인스턴스를 **읽기** 또는 **보기**&#x200B;할 수 있습니다. **만들기**, **편집** 및 **삭제** 작업이 감사 로그에 기록됩니다.

[액세스 제어에 대한 권한 할당](../../../help/access-control/home.md) 또는 [감사 로그를 사용하여 액세스 및 활동을 모니터링하는 방법](../../../help/landing/governance-privacy-security/audit-logs/overview.md)에 대해 알아보려면 설명서를 참조하세요.

## 다음 단계 {#next-steps}

준비가 완료되고 모든 자격 증명 및 스키마를 준비한 후에는 [Attribution AI 사용자 인터페이스 안내서](./user-guide.md)를 따라 시작합니다. 이 안내서에서는 인스턴스를 만들고 교육 및 채점을 위해 제출하는 방법을 안내합니다.
