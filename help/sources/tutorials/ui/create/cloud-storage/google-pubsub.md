---
title: UI에서 Google PubSub 소스 연결 만들기
description: 플랫폼 사용자 인터페이스를 사용하여 Google PubSub 소스 커넥터를 만드는 방법을 알아봅니다.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: f56cdc2dc67f2d4820d80d8e5bdec8306d852891
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 1%

---

# 만들기 [!DNL Google PubSub] UI의 소스 연결

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Google PubSub] (이하 &quot;라 한다)[!DNL PubSub]&quot;) 플랫폼 사용자 인터페이스를 사용합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이미 유효한 [!DNL PubSub] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md).

### 필요한 자격 증명 수집

연결하려면 [!DNL PubSub] 플랫폼에 다음 자격 증명에 유효한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 프로젝트 ID | 인증하는 데 필요한 프로젝트 ID [!DNL PubSub]. |
| 자격 증명 | 인증하는 데 필요한 자격 증명 또는 개인 키 ID입니다 [!DNL PubSub]. |
| 항목 ID | 의 ID입니다 [!DNL PubSub] 메시지 피드를 나타내는 리소스입니다. 의 특정 데이터 스트림에 대한 액세스 권한을 제공하려면 항목 ID를 지정해야 합니다 [!DNL Google PubSub] 소스. |

이러한 값에 대한 자세한 내용은 다음을 참조하십시오 [PubSub 인증](https://cloud.google.com/pubsub/docs/authentication) 문서. 서비스 계정 기반 인증을 사용하는 경우 다음을 참조하십시오 [PubSub 안내서](https://cloud.google.com/docs/authentication/production#create_service_account) 을 참조하십시오.

>[!TIP]
>
>서비스 계정 기반 인증을 사용 중인 경우, 자격 증명을 복사하여 붙여넣을 때 서비스 계정에 대한 충분한 사용자 액세스 권한을 부여했는지 및 JSON에 추가 공백이 없는지 확인하십시오.

필요한 자격 증명을 수집하면 아래 단계에 따라 를 연결할 수 있습니다 [!DNL PubSub] Platform에 계정을 설정합니다.

## 연결 [!DNL PubSub] account

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 클라우드 스토리지] 카테고리, 선택 **[!UICONTROL Google PubSub]**&#x200B;를 선택한 다음 을 선택합니다. **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/google-pubsub/catalog.png)

다음 **[!UICONTROL Google PubSub에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL PubSub] 새 데이터 흐름을 만들 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/google-pubsub/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**, 그런 다음 이름, 선택적 설명 및 을 입력합니다. [!DNL PubSub] 입력 양식의 인증 자격 증명입니다. 이 단계에서는 주제 ID를 제공하여 계정이 액세스할 수 있는 데이터를 정의할 수 있습니다. 해당 주제 ID와 연결된 구독만 액세스할 수 있습니다.

>[!NOTE]
>
>게시 프로젝트에 지정된 주체(역할)는 [!DNL PubSub] 프로젝트. 특정 주제에 액세스할 수 있도록 주체(역할)를 추가하려면 해당 주체(역할)도 해당 주제의 해당 구독에도 추가해야 합니다. 자세한 내용은 [[!DNL PubSub] 액세스 제어 설명서](https://cloud.google.com/pubsub/docs/access-control).

완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![새](../../../../images/tutorials/create/google-pubsub/new.png)

## 다음 단계

이 자습서에 따라 [!DNL PubSub] 계정 및 플랫폼. 이제 다음 자습서를 계속 진행하고 [클라우드 저장소에서 플랫폼으로 스트리밍 데이터를 가져오도록 데이터 흐름 구성](../../dataflow/streaming/cloud-storage-streaming.md).
