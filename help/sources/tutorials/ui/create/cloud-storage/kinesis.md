---
title: UI에서 Amazon Kinesis 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Amazon Kinesis 소스 연결을 만드는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# 만들기 [!DNL Amazon Kinesis] UI의 소스 연결

>[!IMPORTANT]
>
>다음 [!DNL Amazon Kinesis] 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 소스 카탈로그에서 사용할 수 있습니다.

Adobe Experience Platform의 소스 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 다음을 인증하는 단계를 제공합니다. [!DNL Amazon Kinesis] (이하 &quot;&quot;라 한다) [!DNL "Kinesis"]) 소스 커넥터 [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   - [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 을(를) 가지고 있는 경우 [!DNL Kinesis] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/streaming/cloud-storage-streaming.md).

### 필요한 자격 증명 수집

을(를) 인증하려면 [!DNL Kinesis] 소스 커넥터에서는 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `accessKeyId` | 에 대한 액세스 키 ID [!DNL Kinesis] 계정입니다. |
| `Secret access key` | 에 대한 비밀 액세스 키 [!DNL Kinesis] 계정입니다. |
| `region` | AWS 서버의 지역입니다. |

이러한 값에 대한 자세한 내용은 [이 [!DNL Kinesis] 문서](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## 연결 [!DNL Kinesis] account

필요한 자격 증명을 수집했으면 아래 단계에 따라 를 연결할 수 있습니다. [!DNL Kinesis] 계정 위치: [!DNL Platform].

에 로그인 [Adobe Experience Platform](https://platform.adobe.com) 다음을 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: **[!UICONTROL 소스]** 작업 영역. 다음 **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 **[!UICONTROL 클라우드 스토리지]** 범주, 선택 **[!UICONTROL Amazon Kinesis]**. 이 커넥터를 처음 사용하는 경우 다음을 선택합니다. **[!UICONTROL 구성]**. 그렇지 않으면 를 선택합니다. **[!UICONTROL 데이터 추가]** 새로 만들려면 [!DNL Kinesis] 커넥터.

![](../../../../images/tutorials/create/kinesis/catalog.png)

다음 **[!UICONTROL Amazon Kinesis에 연결]** 대화 상자가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 설명(선택 사항) 및 [!DNL Kinesis] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![](../../../../images/tutorials/create/kinesis/new.png)

### 기존 계정

기존 계정을 연결하려면 [!DNL Kinesis] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속합니다.

![](../../../../images/tutorials/create/kinesis/existing.png)

## 다음 단계

이 자습서를 따라 을(를) [!DNL Kinesis] 계정 위치: [!DNL Platform]. 이제 다음 튜토리얼을 계속 진행하여 [클라우드 스토리지에서 로 데이터를 가져오도록 데이터 흐름 구성 [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
