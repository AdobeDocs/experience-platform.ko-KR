---
title: Experience Platform 사용자 인터페이스를 사용하여 Phoenix 계정 연결
description: 사용자 인터페이스를 사용하여 Phoenix 계정을 연결하고 Phoenix 데이터베이스의 데이터를 Experience Platform으로 가져오는 방법에 대해 알아봅니다.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# 연결 [!DNL Phoenix] UI를 사용하여 Experience Platform 할 계정

이 튜토리얼에서는 을(를) 연결하는 방법에 대한 단계를 제공합니다. [!DNL Phoenix] 계정 및 에서 데이터 가져오기 [!DNL Phoenix] Experience Platform 대상 데이터베이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 인증된 사용자가 있는 경우 [!DNL Phoenix] 그러면 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [데이터베이스에 대한 데이터 흐름 구성](../../dataflow/databases.md).

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Phoenix] Experience Platform 시 계정에서 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| Host | 의 IP 주소 또는 호스트 이름 [!DNL Phoenix] 서버입니다. |
| 포트 | 이 작동하는 TCP 포트 [!DNL Phoenix] 서버는 를 사용하여 클라이언트 연결을 수신합니다. 을(를) 연결하는 경우 [!DNL Azure HDInsights]을 클릭한 다음 포트를 443으로 지정합니다. 이 매개 변수를 제공하지 않으면 기본값은 8765입니다. |
| HTTP 경로 | 에 해당하는 부분 URL [!DNL Phoenix] 서버입니다. 다음을 사용하는 경우 /hbasephoenix0 을 지정합니다. [!DNL Azure HDInsights] 클러스터. |
| 사용자 이름 | 에 액세스하는 데 사용하는 사용자 이름 [!DNL Phoenix] 서버입니다. |
| 암호 | 사용자에 해당하는 암호입니다. |
| Enable SSL | 서버 연결이 SSL을 사용하여 암호화되는지 여부를 지정하는 토글 |

시작하기에 대한 자세한 내용은 을(를) 참조하십시오. [이 [!DNL Phoenix] 문서](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

필요한 자격 증명을 수집했으면 아래 단계에 따라 연결할 수 있습니다. [!DNL Phoenix] Experience Platform 계정.

## 연결 [!DNL Phoenix] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색에서 소스 작업 영역에 액세스합니다. 다음 *[!UICONTROL 카탈로그]* 화면에는 Experience Platform 소스 카탈로그에서 사용할 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 특정 소스를 찾을 수 있습니다.

선택 **[!UICONTROL 데이터베이스]** 소스 범주 목록에서 을 선택한 다음 **[!UICONTROL 데이터 추가]** 다음에서 [!DNL Phoenix] 카드.

>[!TIP]
>
>소스 카탈로그의 소스는 소스 상태에 따라 다른 프롬프트를 표시할 수 있습니다.
> 
>* **[!UICONTROL 데이터 추가]** 은(는) 선택한 소스와 연결된 인증된 기존 계정이 있음을 의미합니다.
>
>* **[!UICONTROL 설정]** 은(는) 선택한 소스를 사용하기 위해 자격 증명을 제공하고 새 계정을 인증해야 함을 의미합니다.

![Phoenix 소스 카드가 선택된 Experience Platform UI의 소스 카탈로그.](../../../../images/tutorials/create/phoenix/catalog.png)

다음 **[!UICONTROL 피닉스에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

>[!BEGINTABS]

>[!TAB 기존 Phoenix 계정 사용]

기존 계정을 사용하려면 [!UICONTROL 기존 계정] 그런 다음 나타나는 목록에서 사용할 계정을 선택합니다. 완료되면 다음을 선택합니다. [!UICONTROL 다음] 계속합니다.

![조직에 이미 존재하는 인증된 Phoenix 데이터베이스 계정의 목록입니다.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB 새 Phoenix 계정 만들기]

새 계정을 사용하려면 다음을 선택합니다. [!UICONTROL 새 계정] 이름, 설명 및 [!DNL Phoenix] 인증 자격 증명입니다. 완료되면 다음을 선택합니다. [!UICONTROL 소스에 연결] 새 연결이 설정되도록 몇 초 동안 기다립니다.

![인증 자격 증명을 제공하고 Phoenix 계정을 만들 수 있는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## 다음 단계

이 자습서를 따라 [!DNL Phoenix] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터를 Experience Platform 상태로 전환하도록 데이터 흐름 구성](../../dataflow/databases.md).
