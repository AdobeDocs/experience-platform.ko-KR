---
keywords: Experience Platform;홈;인기 항목;Google PubSub;google pubsub
solution: Experience Platform
title: UI에서 Google Pub 하위 소스 연결 만들기
topic: 개요
type: 자습서
description: 플랫폼 사용자 인터페이스를 사용하여 Google PubSub 소스 커넥터를 만드는 방법을 살펴봅니다.
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# UI에 [!DNL Google PubSub] 소스 연결 만들기

>[!NOTE]
>
> [!DNL Google PubSub] 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 [!DNL Google PubSub](이하 &quot;a1/>&quot;라 함)을 만드는 단계를 제공합니다.[!DNL PubSub]

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이미 유효한 [!DNL PubSub] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름](../../dataflow/batch/cloud-storage.md)을 구성하는 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL PubSub]을(를) 플랫폼에 연결하려면 다음 자격 증명에 유효한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `projectId` | [!DNL PubSub] 인증에 필요한 프로젝트 ID. |
| `credentials` | [!DNL PubSub] 인증에 필요한 자격 증명 또는 키 |

이러한 값에 대한 자세한 내용은 다음 [PubSub 인증](https://cloud.google.com/pubsub/docs/authentication) 문서를 참조하십시오.

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Blob] 계정을 플랫폼에 연결할 수 있습니다.

## [!DNL PubSub] 계정 연결

[플랫폼 UI](https://platform.adobe.com)의 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 클라우드 스토리지] 범주에서 **[!UICONTROL Google PubSub]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/google-pubsub/catalog.png)

**[!UICONTROL Google PubSub]** 페이지에 연결 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 [!DNL PubSub] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속 진행합니다.

![기존](../../../../images/tutorials/create/google-pubsub/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을 선택한 다음 입력 양식에 이름, 선택적 설명 및 [!DNL PubSub] 인증 자격 증명을 입력합니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결이 설정될 때까지 잠시 기다려 주십시오.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## 다음 단계

이 튜토리얼을 따라 [!DNL PubSub] 계정과 플랫폼 사이에 연결을 만듭니다. 이제 다음 튜토리얼을 계속 진행할 수 있으며 [데이터 흐름 구성을 통해 클라우드 스토리지의 스트리밍 데이터를 플랫폼](../../dataflow/streaming/cloud-storage-streaming.md)으로 가져올 수 있습니다.
