---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 셀프 서비스 소스(배치 SDK) API 안내서
topic-legacy: overview
description: 이 문서에서는 Flow Service API를 사용하여 새 연결 사양을 검색, 쓰기 및 제출하는 단계 등 새 소스를 생성하는 프로세스에 대한 개요를 제공합니다.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 셀프 서비스 소스(배치 SDK) API 안내서

이 문서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] 는 플랫폼 내에서 다양한 서로 다른 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다. 이러한 소스 연결을 통해 타사 시스템을 인증하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

다음 [!DNL Flow Service] API는 셀프 서비스 소스(배치 SDK)를 통해 통합하는 새 소스에 대한 연결 및 흐름 사양을 프로그래밍 방식으로 관리할 수 있도록 해주는 몇 가지 엔드포인트를 제공합니다.

## 새 연결 사양 만들기

새 소스를 구성하는 첫 번째 단계는 새 연결 사양을 만드는 것입니다.

연결 사양은 소스의 커넥터 속성을 반환합니다. 여기에는 기본 및 소스 연결 생성과 관련된 인증 사양과 특정 소스에 할당된 고정 연결 사양 ID가 포함됩니다. 연결 사양은 테넌트 및 IMS 조직에 관계 없습니다. 일반적인 연결 사양은 특정 소스에 대한 기본 정보와 세 개의 개별 섹션을 포함합니다. `authSpec`, `sourceSpec`, 및 `exploreSpec`.

자세한 지침은 [새 연결 사양 생성](./create.md). 인증, 소스 및 탐색 사양 구성에 대한 세부 정보를 비롯하여 연결 사양에 사용되는 속성 및 값에 대한 자세한 내용은 [구성 옵션 문서](../config/config.md).

## 플로우 사양 업데이트

연결 사양을 성공적으로 생성한 후에는 `RestStorageToAEP` 소스가 데이터 흐름을 작성할 수 있도록 하기 위한 흐름 사양

흐름 사양은 지원되는 소스 및 대상 연결 ID, 데이터에 적용해야 하는 변환 사양, 흐름 생성에 필요한 스케줄링 매개 변수 등 흐름을 정의하는 정보를 포함합니다.

자세한 지침은 [흐름 사양 업데이트](./update-flow-specs.md).

## 연결 사양 업데이트

에 PUT 요청을 수행하여 연결 사양을 업데이트할 수 있습니다 [!DNL Flow Service] API. 다음 안내서를 참조하십시오. [연결 사양 업데이트](./update-connection-specs.md) 추가 정보.

## 소스 제출

Experience Platform에 통합할 소스를 제출하려면 먼저 전체 보고서를 완료해야 합니다 [!DNL Flow Service] 소스가 성공적으로 작동하는지 확인하는 소스에 대한 API 워크플로우입니다. 소스가 성공적으로 실행되면 을 진행하여 확인 및 프로모션을 위해 Adobe 담당자에게 문의하십시오. 다음 안내서를 참조하십시오. [소스 테스트 및 제출](./submit.md) 자세한 정보

## 다음 단계

를 사용하려면 [!DNL Flow Service] API를 실행하고 셀프 서비스 소스(배치 SDK)를 통해 새 소스를 만들려면 다음을 참조하십시오. [시작 안내서](./getting-started.md) 그런 다음 엔드포인트 가이드 중 하나를 선택하여 특정 엔드포인트를 사용하는 방법을 알아봅니다.
