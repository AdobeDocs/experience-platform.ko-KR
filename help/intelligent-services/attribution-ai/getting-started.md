---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Attribution AI 시작하기
topic: Getting started
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Attribution AI 시작하기

다음 가이드는 Attribution AI 사용과 관련된 다양한 [!DNL Adobe Experience Platform] 서비스를 이해해야 합니다. 자습서를 시작하기 전에 다음 문서를 검토하십시오.

- [XDM(Experience Data Model) 시스템 개요](../../xdm/home.md): XDM은 Experience Platform [!DNL Adobe Experience Cloud]를 기반으로 올바른 고객에게 정확한 타이밍에 적합한 채널을 통해 올바른 메시지를 전달할 수 있는 기본 프레임워크입니다. Platform이 구축되는 방법론인 XDM System은 Experience Platform 서비스에서 사용하기 위해 경험 데이터 모델 스키마를 운영합니다.
- [스키마 컴포지션의 기본 사항](../../xdm/schema/composition.md): 이 문서에서는 XDM(Experience Data Model) 스키마 및 사용할 스키마 작성에 대한 기본 블록, 원칙 및 모범 사례에 대해 소개합니다 [!DNL Adobe Experience Platform].
- [스키마 빌드](../../xdm/tutorials/create-schema-ui.md): 이 자습서에서는 Experience Platform 내의 스키마 편집기를 사용하여 스키마를 만드는 단계를 설명합니다.

Attribution AI은 XDM( [Experience Data Model](../../xdm/home.md) )의 혼합인 CEE(Consumer Experience Events) 스키마를 따라야 합니다. 이 데이터를 구현하거나 변경하려면 attributionai-support@adobe.com의 Adobe 지원에 문의하십시오. 미디어 지출 데이터가 있는 경우 매출 및 ROI와 같은 추가 분석을 수행할 수 있습니다. 고객 프로파일 데이터를 사용할 수 있는 경우 크레딧을 고객 프로파일 레벨에 더 적용할 수 있습니다.

## 용어

- **전환 이벤트:** 고객이 목표를 향해 이정표를 나타내기 위해 수행하는 모든 디지털 이벤트 또는 디지털 인터랙션(예: 컨퍼런스 등록) 추가 예로는 유료 전환, 무료 계정 등록 또는 트레이트 자격증이 있습니다.

- **터치포인트:** 고객이 목표를 향해 가는 모든 디지털 이벤트 또는 디지털 인터랙션 구매 전 관련 마케팅 노력, 열람한 광고 노출 수, 유료 검색 클릭 수 등이 그 예입니다.

## Attribution AI 스코어 다운로드

>[!NOTE]
>
>Raw 점수를 다운로드할 필요가 없는 경우 이 단계를 건너뛰고 [다음 단계를 진행할 수 있습니다](#next-steps).

Attribution AI 스코어 다운로드는 API 호출 조합을 통해 수행됩니다. Platform API를 호출하려면 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증: 무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. Platform API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 예제 API 호출 [](../../landing/troubleshooting.md) 읽기 방법에 대한 섹션을 참조하십시오.

## 다음 단계 {#next-steps}

모든 자격 증명 및 스키마를 준비했으면 [Attribution AI 사용자 인터페이스 가이드](./user-guide.md)따라가십시오. 이 안내서에서는 인스턴스를 만들고 교육 및 채점용으로 제출하는 과정을 안내합니다.