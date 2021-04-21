---
keywords: Experience Platform;기계 학습 모델;데이터 과학 작업 공간;실시간 고객 프로필;인기 항목;기계 학습 통찰력
solution: Experience Platform
title: 머신 러닝 인사이트를 통해 실시간 고객 프로파일 강화
topic-legacy: tutorial
type: Tutorial
description: 이 문서에서는 머신 러닝 인사이트를 활용하여 실시간 고객 프로필을 향상시키는 방법에 대한 가이드를 제공합니다.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 머신 러닝 인사이트를 통해 [!DNL Real-time Customer Profile] 강화

Adobe Experience Platform [!DNL Data Science Workspace]은(는) 머신 러닝 모델을 생성, 평가 및 활용하여 데이터 예측 및 통찰력을 생성하는 도구와 리소스를 제공합니다. 머신 러닝 인사이트를 [!DNL Profile] 사용 가능한 데이터 세트에 인제스트할 때 동일한 데이터를 [!DNL Profile] 기록과 인제스트하여 [!DNL Adobe Experience Platform Segmentation Service]를 사용하여 세그먼트화할 수 있습니다. 프로필 및 시간 시리즈 데이터가 수집되면 실시간 고객 프로필은 기존 데이터와 병합하고 조합 보기를 업데이트하기 전에 스트리밍 세그먼테이션이라는 지속적인 프로세스를 통해 세그먼트에서 해당 데이터를 포함하거나 제외하기로 자동으로 결정합니다. 그 결과, 계산을 즉시 수행하고 고객이 브랜드와 상호 작용할 때 개인화된 향상된 경험을 고객에게 제공하는 결정을 내릴 수 있습니다.

이 문서에서는 기계 학습 인사이트를 바탕으로 [!DNL Real-time Customer Profile]에 대한 풍부한 기능을 제공하는 자습서 링크를 제공합니다.

## 시작하기

아래 튜토리얼을 완료하려면 [!DNL Profile] 데이터 인제스트 및 세그먼트 만들기에 대한 작업 지식이 있어야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 수집한 데이터를 기반으로 각 개별 고객을 통일하고 완벽하게 표현할 수 있습니다.
- [[!DNL Identity Service]](../../identity-service/home.md):인제스트되고  [!DNL Real-time Customer Profile] 있는 다양한 데이터 소스의 ID를 플랫폼에 브리싱하여 사용할 수 있습니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):Platform(플랫폼)이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

위에 언급된 문서 외에도 스키마 및 스키마 편집기에 대한 다음 안내서도 검토하는 것이 좋습니다.

- [스키마 컴포지션의 기본 사항](../../xdm/schema/composition.md):XDM 스키마, 구성 블록, 원리 및 사용할 스키마 구성에 대한 우수 사례를 설명합니다 [!DNL Experience Platform].
- [스키마 편집기 자습서](../../xdm/tutorials/create-schema-ui.md):내에서 스키마 편집기를 사용하여 스키마를 생성하는 자세한 지침을 제공합니다 [!DNL Experience Platform].

## 출력 스키마 및 데이터 세트 {#create-an-output-schema-and-dataset} 만들기 및 구성

채점 통찰력을 통해 [!DNL Real-time Customer Profile]을 강화하는 첫 번째 단계는 데이터가 정의하는 실제 개체(예: 사람)를 파악하는 것입니다. 데이터에 대한 이해를 통해 관계형 데이터베이스를 디자인하는 것과 같이 의미를 추가할 구조를 설명하고 디자인할 수 있습니다.

스키마 작성은 클래스를 할당하여 시작됩니다. 클래스는 스키마에 포함할 데이터의 행동 측면(레코드 또는 시간 시리즈)을 정의합니다. 스키마를 직접 만들려면 [스키마 편집기](../../xdm/tutorials/create-schema-ui.md)를 사용하여 스키마 만들기에 대한 자습서의 단계를 따릅니다. [!DNL Profile]에 대한 데이터 세트를 사용하려면 먼저 데이터 세트의 스키마를 구성하여 기본 ID 필드를 지정한 다음 [!DNL Profile]에 대한 스키마를 활성화해야 합니다. 데이터를 [!DNL Profile] 사용 가능한 데이터세트에 인제스트할 때 동일한 데이터를 [!DNL Profile] 레코드에도 인제스트됩니다.

대신 [!DNL Schema Registry] API를 사용하여 스키마를 작성하려면 [[!DNL Schema Registry] 개발자 안내서](../../xdm/api/getting-started.md)에서 API](../../xdm/tutorials/create-schema-api.md)를 사용하여 스키마를 만들기 전에 [개발자 안내서를 읽으십시오.

스키마 및 데이터 세트가 준비되면 적절한 모델을 사용하여 점수 실행을 수행하여 데이터 세트에 점수 데이터를 생성하고 인제스트할 수 있습니다.

## [!DNL Segment Builder] {#create-segments-using-the-segment-builder}을(를) 사용하여 세그먼트 만들기

점수 데이터 통찰력을 생성하여 [!DNL Profile] 사용 가능한 데이터 세트에 인사이트를 수집했으면 [!DNL Segment Builder]을(를) 사용하여 동적 세그먼트를 만들 수 있습니다.

[!DNL Segment Builder]은 [!DNL Profile] 데이터 요소와 상호 작용할 수 있는 풍부한 작업 영역을 제공합니다. 작업 영역은 데이터 속성을 나타내는 데 사용되는 드래그 앤 드롭 타일과 같이 규칙을 작성하고 편집하기 위한 직관적인 컨트롤을 제공합니다. 다음 사항에 대해 알려면 [[!DNL Segment Builder] 사용자 안내서](../../segmentation/ui/segment-builder.md)를 따르십시오.

- 특성, 이벤트 및 기존 대상을 구성 요소로 조합하여 세그먼트 정의를 만듭니다.
- 규칙 빌더 캔버스 및 컨테이너를 사용하여 세그먼트 규칙이 실행되는 순서를 제어할 수 있습니다.
- 잠재 고객의 예상 수치를 보고 필요에 따라 세그먼트 정의를 조정할 수 있습니다.
- 예약된 세그먼테이션에 대한 모든 세그먼트 정의 활성화.
- 스트리밍 세그먼테이션을 위해 지정된 세그먼트 정의를 활성화합니다.

## 다음 단계 {#next-steps}

세그먼트 및 [!DNL Segment Builder]에 대한 자세한 내용은 [세그멘테이션 서비스 개요](../../segmentation/home.md)를 참조하십시오.

[!DNL Real-time Customer Profile]에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 참조하십시오.
