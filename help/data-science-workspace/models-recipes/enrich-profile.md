---
keywords: Experience Platform;기계 학습 모델;데이터 과학 작업 공간;실시간 고객 프로필;인기 항목;기계 학습 인사이트
solution: Experience Platform
title: 머신 러닝 인사이트로 실시간 고객 프로필 보강
topic-legacy: tutorial
type: Tutorial
description: 이 문서에서는 기계 학습 인사이트로 실시간 고객 프로필을 보강하는 방법에 대한 안내서를 제공합니다.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 품질 개선 [!DNL Real-Time Customer Profile] 머신 러닝 인사이트

Adobe Experience Platform [!DNL Data Science Workspace] 데이터 예측 및 인사이트를 생성하는 기계 학습 모델을 생성, 평가 및 활용할 수 있는 도구와 리소스를 제공합니다. 머신 러닝 인사이트를 [!DNL Profile]-활성화된 데이터 세트로서 동일한 데이터가 수집됩니다. [!DNL Profile] 다음으로 세그먼트화할 수 있는 레코드 [!DNL Adobe Experience Platform Segmentation Service].

이 문서에서는 다음을 보강할 수 있는 자습서에 대한 링크를 제공합니다 [!DNL Real-Time Customer Profile] 머신 러닝 인사이트 사용

## 시작하기

아래 자습서를 완료하려면 섭취에 대한 작업 이해를 해야 합니다 [!DNL Profile] 데이터 및 세그먼트 만들기 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스의 집계된 데이터를 기반으로 각 개별 고객에 대한 완전하고 통합된 표시를 제공합니다.
- [[!DNL Identity Service]](../../identity-service/home.md): 사용 [!DNL Real-Time Customer Profile] 플랫폼으로 수집되는 다양한 데이터 소스의 ID를 브리징함으로써
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

위에 언급된 문서 외에도 스키마 및 스키마 편집기에 대한 다음 안내서도 검토하는 것이 좋습니다.

- [스키마 작성 기본 사항](../../xdm/schema/composition.md): 에서 사용할 스키마를 구성하기 위한 XDM 스키마, 빌딩 블록, 원칙 및 우수 사례에 대해 설명합니다 [!DNL Experience Platform].
- [스키마 편집기 자습서](../../xdm/tutorials/create-schema-ui.md): 내에서 스키마 편집기를 사용하여 스키마를 생성하기 위한 세부 지침을 제공합니다. [!DNL Experience Platform].

## 출력 스키마 및 데이터 세트 만들기 및 구성 {#create-an-output-schema-and-dataset}

성장을 위한 첫 단계 [!DNL Real-Time Customer Profile] 점수 인사이트를 통해 데이터가 정의하는 실제 개체(예: 사람)를 알 수 있습니다. 데이터를 이해하면 관계형 데이터베이스를 디자인하는 것과 마찬가지로 의미를 추가할 구조를 설명하고 디자인할 수 있습니다.

스키마 작성은 클래스를 할당하여 시작됩니다. 클래스는 스키마에 포함할 데이터의 행동 측면(레코드 또는 시계열)을 정의합니다. 스키마를 직접 만들려면 다음 자습서의 단계를 수행하십시오. [스키마 편집기를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-ui.md). 데이터 세트를 사용하려면 먼저 [!DNL Profile]를 채울 수 있도록 데이터 세트의 스키마를 구성하여 기본 ID 필드를 만든 다음 스키마를 활성화해야 합니다 [!DNL Profile]. 데이터를에 수집할 때 [!DNL Profile]-활성화된 데이터 세트로서 동일한 데이터가 수집됩니다. [!DNL Profile] 레코드.

를 사용하여 스키마를 작성하려는 경우 [!DNL Schema Registry] API를 대신, 를 참조하여 시작하십시오. [[!DNL Schema Registry] 개발자 안내서](../../xdm/api/getting-started.md) 자습서를 시작하기 전에 [api를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md).

스키마 및 데이터 세트가 준비되면 적절한 모델을 사용하여 점수 실행을 수행하여 점수 데이터를 데이터 세트에 생성하고 수집할 수 있습니다.

## 을 사용하여 세그먼트 만들기 [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

점수 데이터 통찰력을 생성하여 자신에게 수집한 후 [!DNL Profile]-enabled 데이터 세트로, [!DNL Segment Builder].

다음 [!DNL Segment Builder] 는 상호 작용할 수 있는 풍부한 작업 공간을 제공합니다. [!DNL Profile] 데이터 요소. 작업 공간에서는 데이터 속성을 표시하는 데 사용되는 드래그 앤 드롭 타일과 같이 규칙을 만들고 편집하기 위한 직관적인 컨트롤을 제공합니다. 다음을 수행합니다 [[!DNL Segment Builder] 사용 안내서](../../segmentation/ui/segment-builder.md) 다음에 대해 자세히 알아보십시오.

- 속성, 이벤트 및 기존 대상을 빌딩 블록으로 조합하여 세그먼트 정의 만들기
- 규칙 빌더 캔버스 및 컨테이너를 사용하여 세그먼트 규칙이 실행되는 순서를 제어합니다.
- 필요에 따라 세그먼트 정의를 조정할 수 있는 예상 대상의 견적을 보는 중입니다.
- 예약된 세그먼테이션에 대해 모든 세그먼트 정의를 활성화합니다.
- 스트리밍 세그먼테이션을 위해 지정된 세그먼트 정의를 사용하도록 설정합니다.

## 다음 단계 {#next-steps}

세그먼트 및 [!DNL Segment Builder]를 읽고 [세그먼테이션 서비스 개요](../../segmentation/home.md).

에 대해 자세히 알아보려면 [!DNL Real-Time Customer Profile]를 읽고 [실시간 고객 프로필 개요](../../profile/home.md)
