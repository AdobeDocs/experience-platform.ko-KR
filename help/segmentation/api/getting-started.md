---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;api;
solution: Experience Platform
title: 세그멘테이션 서비스 API 시작하기
topic-legacy: developer guide
description: 다음 설명서는 세그멘테이션 API를 성공적으로 사용하기 위해 알아야 하는 추가 정보를 제공합니다.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 세그멘테이션 서비스 API 시작 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service]을(를) 사용하면 [!DNL Real-time Customer Profile] 데이터에서 세그먼트를 작성하고 Adobe Experience Platform에서 대상을 생성할 수 있습니다.

개발자 가이드는 [!DNL Segmentation Service] 사용과 관련된 다양한 [!DNL Experience Platform] 서비스에 대한 작업 이해를 필요로 합니다.

- [[!DNL Segmentation]](../home.md):데이터에서 대상 세그먼트를 만들 수  [!DNL Real-time Customer Profile] 있습니다.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Segmentation] API를 사용하여 성공적으로 작업하기 위해 알아야 할 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

[!DNL Segmentation Service] API 설명서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

## 필수 헤더

또한 API 설명서는 [!DNL Platform] 끝점을 성공적으로 호출하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스 작업에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

## 다음 단계

[!DNL Segmentation Service] API를 사용하여 호출을 하려면 왼쪽 탐색 또는 [개발자 안내서 개요](./overview.md) 내에서 사용 가능한 끝점 안내선 중 하나를 선택합니다.
