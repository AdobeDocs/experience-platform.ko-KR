---
keywords: Experience Platform;머신 러닝 모델;Data Science Workspace;실시간 고객 프로필;인기 주제;머신 러닝 통찰력
solution: Experience Platform
title: 머신 러닝 통찰력을 통해 실시간 고객 프로필 강화
type: Tutorial
description: 이 문서에서는 머신 러닝 통찰력을 통해 실시간 고객 프로필을 보강하는 방법에 대한 안내서를 제공합니다.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# 강화 [!DNL Real-Time Customer Profile] 머신 러닝 인사이트 사용

Adobe Experience Platform [!DNL Data Science Workspace] 는 머신 러닝 모델을 생성, 평가 및 활용하여 데이터 예측 및 통찰력을 생성하는 도구 및 리소스를 제공합니다. 머신 러닝 통찰력이 [!DNL Profile]-활성화된 데이터 세트, 동일한 데이터도 [!DNL Profile] 다음을 사용하여 세그먼트화할 수 있는 레코드 [!DNL Adobe Experience Platform Segmentation Service].

이 문서에서는 강화 가능한 튜토리얼 링크를 제공합니다 [!DNL Real-Time Customer Profile] 머신 러닝 통찰력을 통해.

## 시작하기

아래 튜토리얼을 완료하려면 수집에 대한 작업 이해가 필요합니다 [!DNL Profile] 데이터 및 세그먼트 만들기 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계한 데이터를 기반으로 각 개별 고객을 완전히 통합하여 표시합니다.
- [[!DNL Identity Service]](../../identity-service/home.md): 사용 [!DNL Real-Time Customer Profile] 서로 다른 데이터 소스의 ID를 Platform으로 가져와서 브리징합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

위에서 언급한 문서 외에도 스키마 및 스키마 편집기에 대해 다음 안내서도 검토하는 것이 좋습니다.

- [스키마 컴포지션 기본 사항](../../xdm/schema/composition.md): 에서 사용할 스키마를 구성하기 위한 XDM 스키마, 빌딩 블록, 원칙 및 모범 사례를 설명합니다. [!DNL Experience Platform].
- [스키마 편집기 튜토리얼](../../xdm/tutorials/create-schema-ui.md): 내의 스키마 편집기를 사용하여 스키마를 만드는 자세한 지침을 제공합니다. [!DNL Experience Platform].

## 출력 스키마 및 데이터 세트 만들기 및 구성 {#create-an-output-schema-and-dataset}

풍요를 위한 첫 번째 단계 [!DNL Real-Time Customer Profile] 채점 통찰력을 사용하면 데이터가 정의하는 실제 개체(예: 개인)를 알 수 있습니다. 데이터를 이해하면 관계형 데이터베이스를 디자인하는 것과 같이 의미를 추가할 구조를 설명하고 디자인할 수 있습니다.

스키마 작성은 클래스를 할당하는 것부터 시작됩니다. 클래스는 스키마가 포함할 데이터의 동작 측면(레코드 또는 시계열)을 정의합니다. 자신만의 스키마 만들기를 시작하려면 다음 자습서의 단계를 따르십시오. [스키마 편집기를 사용하여 스키마 생성](../../xdm/tutorials/create-schema-ui.md). 다음에 대한 데이터 세트를 활성화하려면 먼저 [!DNL Profile]: 기본 id 필드를 갖도록 데이터 세트의 스키마를 구성한 다음 를 위해 스키마를 활성화해야 합니다 [!DNL Profile]. 데이터가 로 수집되는 경우 [!DNL Profile]-활성화된 데이터 세트, 동일한 데이터도 [!DNL Profile] 레코드.

를 사용하여 스키마를 구성하려는 경우 [!DNL Schema Registry] API를 참조하려면 먼저 [[!DNL Schema Registry] 개발자 안내서](../../xdm/api/getting-started.md) 에 대한 자습서를 시도하기 전에 [api를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md).

스키마와 데이터 세트가 준비되면 적절한 모델을 사용하여 채점 실행을 수행함으로써 채점 데이터를 생성하고 데이터 세트에 수집할 수 있습니다.

## 를 사용하여 세그먼트 만들기 [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

채점 데이터 인사이트를 생성하여 로 수집한 후 [!DNL Profile]-enabled dataset을 사용하여 동적 세그먼트를 만들 수 있습니다. [!DNL Segment Builder].

다음 [!DNL Segment Builder] 에서는 상호 작용할 수 있는 다양한 작업 영역을 제공합니다. [!DNL Profile] 데이터 요소. 작업 공간에서는 데이터 속성을 표시하는 데 사용되는 드래그 앤 드롭 타일과 같은 규칙을 작성하고 편집할 수 있는 직관적인 컨트롤을 제공합니다. 다음 [[!DNL Segment Builder] 사용 안내서](../../segmentation/ui/segment-builder.md) 에 대해 알아보려면 다음을 수행하십시오.

- 속성, 이벤트 및 기존 대상의 조합을 빌딩 블록으로 사용하여 세그먼트 정의 작성.
- 규칙 빌더 캔버스 및 컨테이너를 사용하여 세그먼트 규칙이 실행되는 순서를 제어합니다.
- 예상 대상의 예상치를 보고 필요에 따라 세그먼트 정의를 조정할 수 있습니다.
- 예약된 세분화에 대해 모든 세그먼트 정의를 활성화합니다.
- 스트리밍 세분화에 대해 지정된 세그먼트 정의를 사용하도록 설정하는 중입니다.

## 다음 단계 {#next-steps}

세그먼트 및 [!DNL Segment Builder], 다음을 읽습니다 [세그먼테이션 서비스 개요](../../segmentation/home.md).

에 대해 자세히 알아보기 [!DNL Real-Time Customer Profile], 다음을 읽습니다 [실시간 고객 프로필 개요](../../profile/home.md)
