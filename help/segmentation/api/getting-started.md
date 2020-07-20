---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 세그멘테이션 서비스 개발자 가이드
topic: developer guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Adobe Experience Platform 세그멘테이션 서비스를 사용하면 세그먼트를 작성하고 [!DNL Real-time Customer Profile] 데이터로부터 Adobe Experience Platform에서 대상을 생성할 수 있습니다.

개발자 가이드는 사용과 관련된 다양한 Experience Platform 서비스에 대한 작업 이해를 필요로 합니다 [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): 실시간 고객 프로필 데이터를 통해 고객 세그먼트를 만들 수 있습니다.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [!DNL Real-time Customer Profile](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [샌드박스](../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 Platform 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Segmentation] API를 사용하여 성공적으로 작업하기 위해 알아야 할 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

API 설명서는 요청의 서식을 지정하는 방법을 시연하기 위한 예제 API 호출을 제공합니다. [!DNL Segmentation Service] 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 예제 API 호출 [](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기 방법에 대한 섹션을 참조하십시오.

## 필요한 헤더

또한 API 설명서는 Platform 끝점에 대한 호출을 성공적으로 수행하려면 [인증 자습서를](../../tutorials/authentication.md) 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스 작업에 대한 자세한 내용 [!DNL Experience Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

## 다음 단계

API를 사용하여 [!DNL Segmentation Service] 호출을 하려면 왼쪽 탐색 또는 [개발자 가이드 개요 내에서 사용 가능한 끝점 가이드 중 하나를 선택합니다](./overview.md)