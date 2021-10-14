---
keywords: Experience Platform;시작하기;기여도 분석 ai;인기 항목
feature: Attribution AI
title: Attribution AI 시작하기
topic-legacy: Getting started
description: 다음 안내서에서는 Attribution AI 사용과 관련된 다양한 Adobe Experience Platform 서비스를 이해해야 합니다. 자습서를 시작하기 전에 다음 문서를 검토하십시오.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# Attribution AI 시작하기

다음 안내서에서는 Attribution AI 사용과 관련된 다양한 [!DNL Adobe Experience Platform] 서비스를 이해해야 합니다. 자습서를 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(경험 데이터 모델) 시스템 개요](../../xdm/home.md): XDM은 Experience Platform [!DNL Adobe Experience Cloud]를 통해 올바른 사용자에게 올바른 메시지를 올바른 채널에 전달하는 기본 프레임워크로서, 정확한 시점에 Experience Platform을 빌드하는 방법론인 XDM System은 Platform 서비스에서 사용하기 위해 Experience Data Model 스키마를 작동시킵니다.
- [스키마 작성 기본 사항](../../xdm/schema/composition.md): 이 문서에서는 XDM(Experience Data Model) 스키마 및 에서 사용할 스키마를 구성하기 위한 빌딩 블록, 원칙 및 모범 사례를 소개합니다 [!DNL Adobe Experience Platform].
- [스키마 작성](../../xdm/tutorials/create-schema-ui.md): 이 자습서에서는 Experience Platform 내에서 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.

Attribution AI을 사용하려면 데이터 세트가 [XDM(Experience Data Model)](../../xdm/home.md) 스키마 필드 그룹인 CEE(Consumer Experience Events) 스키마를 따르도록 해야 합니다. 이 데이터를 구현하거나 변경하려면 Adobe 지원 센터(attributionai-support@adobe.com)에 문의하십시오. 미디어 지출 데이터가 있으면 증분 매출 및 ROI와 같은 추가 분석을 수행할 수 있습니다. 고객 프로파일 데이터를 사용할 수 있는 경우 고객 프로파일 레벨에 크레딧을 추가로 지정할 수 있습니다.

## 용어

- **전환 이벤트:** 고객이 목표에 대한 이정표를 표시하기 위해 하는 모든 디지털 이벤트 또는 디지털 상호 작용(예: 전화 회의 등록) 추가적인 예로는 유료 전환, 무료 계정 등록 또는 트레이트에 대한 자격이 있습니다.

- **터치포인트:** 고객이 목표를 향해 경로에서 수행하는 모든 디지털 이벤트 또는 디지털 상호 작용. 구매 관련 마케팅 활동, 본 광고 노출 수 및 유료 검색 클릭 수를 예로 들 수 있습니다.

## Attribution AI 점수 다운로드

>[!NOTE]
>
>원시 점수를 다운로드할 필요가 없는 경우 이 단계를 건너뛰고 [다음 단계](#next-steps)로 진행할 수 있습니다.

Attribution AI 점수 다운로드는 API 호출 조합을 통해 수행됩니다. 플랫폼 API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 권한 부여: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. Platform API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 [예제 API 호출](../../landing/troubleshooting.md)를 읽는 방법 섹션을 참조하십시오.

## 다음 단계 {#next-steps}

준비가 완료되어 모든 자격 증명과 스키마가 준비되면 [Attribution AI 사용자 인터페이스 안내서](./user-guide.md)에 따라 시작하십시오. 이 안내서에서는 인스턴스를 만들고 교육 및 점수를 위해 인스턴스를 제출하는 과정을 안내합니다.
