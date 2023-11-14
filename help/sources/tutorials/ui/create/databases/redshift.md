---
title: UI에서 Amazon Redshift 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Amazon Redshift 소스 연결을 만드는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---

# 연결 [!DNL Amazon Redshift] 소스 작업 영역을 사용하는 계정

>[!IMPORTANT]
>
>다음 [!DNL Amazon Redshift] 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 소스 카탈로그에서 사용할 수 있습니다.

이 튜토리얼에서는 을(를) 연결하는 방법에 대한 단계를 제공합니다. [!DNL Amazon Redshift] (이하 &quot;라고 한다)[!DNL Redshift]&quot;) 사용자 인터페이스를 사용하여 Adobe Experience Platform에 계정을 추가합니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 을(를) 가지고 있는 경우 [!DNL Redshift] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/databases.md).

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Redshift] Experience Platform 시 계정에서 다음 값을 제공해야 합니다.

| **자격 증명** | **설명** |
| -------------- | --------------- |
| 서버 | 와(과) 연계된 서버 [!DNL Redshift] 계정입니다. |
| 포트 | 이(가) 지원하는 TCP 포트 [!DNL Redshift] 서버는 를 사용하여 클라이언트 연결을 수신합니다. |
| 사용자 이름 | 와(과) 연계된 사용자 이름 [!DNL Redshift] 계정입니다. |
| 암호 | 과(와) 연계된 암호 [!DNL Redshift] 계정입니다. |
| 데이터베이스 | 다음 [!DNL Redshift] 액세스 중인 데이터베이스입니다. |

시작하기에 대한 자세한 내용은 을(를) 참조하십시오. [이 [!DNL Redshift] 문서](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

필요한 자격 증명을 수집했으면 아래 단계에 따라 를 연결할 수 있습니다. [!DNL Redshift] Experience Platform 계정.

## 연결 [!DNL Redshift] account

>[!NOTE]
>
>의 기본 인코딩 표준 [!DNL Redshift] 유니코드입니다. 이는 변경할 수 없습니다.

에 로그인 [Adobe Experience Platform](https://platform.adobe.com) 다음을 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: **[!UICONTROL 소스]** 작업 영역. 다음 **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 **[!UICONTROL 데이터베이스]** 범주, 선택 **[!UICONTROL Amazon Redshift]**. 이 커넥터를 처음 사용하는 경우 다음을 선택합니다. **[!UICONTROL 구성]**. 그렇지 않으면 를 선택합니다. **[!UICONTROL 데이터 추가]** 새로 만들려면 [!DNL Redshift] 커넥터.

![](../../../../images/tutorials/create/redshift/catalog.png)

다음 **[!UICONTROL Amazon Redshift에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 설명(선택 사항) 및 [!DNL Redshift] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![](../../../../images/tutorials/create/redshift/new.png)

### 기존 계정

기존 계정을 연결하려면 [!DNL Redshift] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속합니다.

![](../../../../images/tutorials/create/redshift/existing.png)

## 다음 단계

이 자습서를 따라 [!DNL Redshift] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터를 Experience Platform 상태로 전환하도록 데이터 흐름 구성](../../dataflow/databases.md).
