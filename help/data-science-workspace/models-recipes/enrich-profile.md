---
keywords: Experience Platform;머신 러닝 모델;Data Science Workspace;실시간 고객 프로필;인기 주제;머신 러닝 통찰력
solution: Experience Platform
title: 머신 러닝 인사이트를 통해 실시간 고객 프로필 강화
type: Tutorial
description: 이 문서에서는 머신 러닝 통찰력을 통해 실시간 고객 프로필을 보강하는 방법에 대한 안내서를 제공합니다.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 기계 학습 통찰력을 사용하여 [!DNL Real-Time Customer Profile] 강화

Adobe Experience Platform [!DNL Data Science Workspace]은(는) 데이터 예측 및 통찰력을 생성하기 위해 머신 러닝 모델을 만들고, 평가하고, 활용할 수 있는 도구와 리소스를 제공합니다. 머신 러닝 인사이트가 [!DNL Profile]을(를) 사용할 수 있는 데이터 세트로 수집되면 동일한 데이터도 [!DNL Profile] 레코드로 수집되어 [!DNL Adobe Experience Platform Segmentation Service]을(를) 사용하여 세그먼트화할 수 있습니다.

이 문서에서는 기계 학습 통찰력을 통해 [!DNL Real-Time Customer Profile]을(를) 보강할 수 있는 자습서에 대한 링크를 제공합니다.

## 시작하기

아래 튜토리얼을 완료하려면 [!DNL Profile] 데이터를 수집하고 세그먼트를 만드는 방법에 대해 잘 알고 있어야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 각 개별 고객에 대한 완전한 통합 표현을 제공합니다.
- [[!DNL Identity Service]](../../identity-service/home.md): 플랫폼에 수집되는 서로 다른 데이터 원본의 ID를 연결하여 [!DNL Real-Time Customer Profile]을(를) 사용하도록 설정합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

위에서 언급한 문서 외에도 스키마 및 스키마 편집기에 대해 다음 안내서도 검토하는 것이 좋습니다.

- [스키마 작성의 기본 사항](../../xdm/schema/composition.md): [!DNL Experience Platform]에서 사용할 스키마를 작성하기 위한 XDM 스키마, 빌딩 블록, 원칙 및 모범 사례를 설명합니다.
- [스키마 편집기 자습서](../../xdm/tutorials/create-schema-ui.md): [!DNL Experience Platform] 내에서 스키마 편집기를 사용하여 스키마를 만드는 자세한 지침을 제공합니다.

## 출력 스키마 및 데이터 세트 만들기 및 구성 {#create-an-output-schema-and-dataset}

채점 통찰력을 통해 [!DNL Real-Time Customer Profile]을(를) 보강하는 첫 번째 단계는 데이터가 정의하는 실제 개체(예: 사용자)를 파악하는 것입니다. 데이터를 이해하면 관계형 데이터베이스를 디자인하는 것과 같이 의미를 추가할 구조를 설명하고 디자인할 수 있습니다.

스키마 작성은 클래스를 할당하는 것부터 시작됩니다. 클래스는 스키마가 포함할 데이터의 동작 측면(레코드 또는 시계열)을 정의합니다. 자신만의 스키마를 만들려면 [스키마 편집기를 사용하여 스키마를 만드는 방법](../../xdm/tutorials/create-schema-ui.md)에 대한 자습서의 단계를 따르십시오. [!DNL Profile]에 대해 데이터 집합을 활성화하려면 먼저 기본 ID 필드를 갖도록 데이터 집합의 스키마를 구성한 다음 [!DNL Profile]에 대해 스키마를 활성화해야 합니다. 데이터를 [!DNL Profile]이(가) 활성화된 데이터 세트로 수집하면 동일한 데이터도 [!DNL Profile] 레코드로 수집됩니다.

대신 [!DNL Schema Registry] API를 사용하여 스키마를 작성하려는 경우 [API를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md)에 대한 자습서를 시도하기 전에 [[!DNL Schema Registry] 개발자 안내서](../../xdm/api/getting-started.md)를 읽는 것부터 시작하십시오.

스키마와 데이터 세트가 준비되면 적절한 모델을 사용하여 채점 실행을 수행함으로써 채점 데이터를 생성하고 데이터 세트에 수집할 수 있습니다.

## [!DNL Segment Builder]을(를) 사용하여 세그먼트 만들기 {#create-segments-using-the-segment-builder}

[!DNL Profile]이(가) 활성화된 데이터 세트에 대한 채점 데이터 인사이트를 생성하고 수집한 후 [!DNL Segment Builder]을(를) 사용하여 동적 세그먼트를 만들 수 있습니다.

[!DNL Segment Builder]은(는) [!DNL Profile] 데이터 요소와 상호 작용할 수 있는 풍부한 작업 영역을 제공합니다. 작업 공간에서는 데이터 속성을 표시하는 데 사용되는 드래그 앤 드롭 타일과 같은 규칙을 작성하고 편집할 수 있는 직관적인 컨트롤을 제공합니다. 자세한 내용은 [[!DNL Segment Builder] 사용 안내서](../../segmentation/ui/segment-builder.md)를 참조하세요.

- 속성, 이벤트 및 기존 대상의 조합을 빌딩 블록으로 사용하여 세그먼트 정의 작성.
- 규칙 빌더 캔버스 및 컨테이너를 사용하여 세그먼트 규칙이 실행되는 순서를 제어합니다.
- 예상 대상의 예상치를 보고 필요에 따라 세그먼트 정의를 조정할 수 있습니다.
- 예약된 세분화에 대해 모든 세그먼트 정의를 활성화합니다.
- 스트리밍 세분화에 대해 지정된 세그먼트 정의를 사용하도록 설정하는 중입니다.

## 다음 단계 {#next-steps}

세그먼트 및 [!DNL Segment Builder]에 대한 자세한 내용은 [세그먼테이션 서비스 개요](../../segmentation/home.md)를 참조하세요.

[!DNL Real-Time Customer Profile]에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md)를 참조하세요.
