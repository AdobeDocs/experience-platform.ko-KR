---
title: Experience Platform 사용자 인터페이스를 사용하여 Phoenix 계정 연결
description: 사용자 인터페이스를 사용하여 Phoenix 계정을 연결하고 Phoenix 데이터베이스의 데이터를 Experience Platform으로 가져오는 방법에 대해 알아봅니다.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: a32d0d7ed7d18454099d2b55b3f6809cfbcd9b62
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# UI를 사용하여 [!DNL Phoenix] 계정을 Experience Platform에 연결

>[!IMPORTANT]
>
>[!DNL Phoenix] 원본은 2025년 5월 말에 사용되지 않습니다.

이 자습서에서는 [!DNL Phoenix] 계정을 연결하고 [!DNL Phoenix] 데이터베이스에서 데이터를 Experience Platform 상태로 만드는 방법에 대한 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

인증된 [!DNL Phoenix] 계정이 이미 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터베이스에 대한 데이터 흐름 구성](../../dataflow/databases.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

Experience Platform 시 [!DNL Phoenix] 계정에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| Host | [!DNL Phoenix] 서버의 IP 주소 또는 호스트 이름입니다. |
| 포트 | [!DNL Phoenix] 서버가 클라이언트 연결을 수신 대기하는 데 사용하는 TCP 포트입니다. [!DNL Azure HDInsights]에 연결하는 경우 포트를 443으로 지정하십시오. 이 매개 변수를 제공하지 않으면 기본값은 8765입니다. |
| HTTP 경로 | [!DNL Phoenix] 서버에 해당하는 부분 URL. [!DNL Azure HDInsights] 클러스터를 사용하는 경우 /hbasephoenix0을 지정하십시오. |
| 사용자 이름 | [!DNL Phoenix] 서버에 액세스하는 데 사용하는 사용자 이름입니다. |
| 암호 | 사용자에 해당하는 암호입니다. |
| Enable SSL | 서버 연결이 SSL을 사용하여 암호화되는지 여부를 지정하는 토글 |

시작에 대한 자세한 내용은 [이 [!DNL Phoenix] 문서](https://python-phoenixdb.readthedocs.io/en/latest/api.html)를 참조하세요.

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Phoenix] 계정을 Experience Platform에 연결할 수 있습니다.

## [!DNL Phoenix] 계정 연결

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 소스 작업 영역에 액세스합니다. *[!UICONTROL 카탈로그]* 화면에 Experience Platform 원본 카탈로그에서 사용할 수 있는 다양한 원본이 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 특정 소스를 찾을 수 있습니다.

소스 범주 목록에서 **[!UICONTROL 데이터베이스]**&#x200B;을 선택한 다음 [!DNL Phoenix] 카드에서 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

>[!TIP]
>
>소스 카탈로그의 소스는 소스 상태에 따라 다른 프롬프트를 표시할 수 있습니다.
> 
>* **[!UICONTROL 데이터 추가]**&#x200B;는 선택한 소스와 연결된 인증된 기존 계정이 있음을 의미합니다.
>
>* **[!UICONTROL 설정]**&#x200B;은(는) 선택한 원본을 사용하려면 자격 증명을 제공하고 새 계정을 인증해야 함을 의미합니다.

![Phoenix 소스 카드가 선택된 Experience Platform UI의 소스 카탈로그입니다.](../../../../images/tutorials/create/phoenix/catalog.png)

**[!UICONTROL Phoenix에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

>[!BEGINTABS]

>[!TAB 기존 Phoenix 계정 사용]

기존 계정을 사용하려면 [!UICONTROL 기존 계정]을 선택한 다음 표시되는 목록에서 사용할 계정을 선택하십시오. 완료되면 [!UICONTROL 다음]을(를) 선택하여 계속하십시오.

![이미 조직에 있는 인증된 Phoenix 데이터베이스 계정의 목록입니다.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB 새 Phoenix 계정 만들기]

새 계정을 사용하려면 [!UICONTROL 새 계정]을(를) 선택하고 이름, 설명 및 [!DNL Phoenix] 인증 자격 증명을 제공하세요. 완료되면 [!UICONTROL 소스에 연결]을 선택하고 몇 초 동안 새 연결을 설정할 수 있습니다.

![인증 자격 증명을 제공하고 Phoenix 계정을 만들 수 있는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## 다음 단계

이 자습서에 따라 [!DNL Phoenix] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 Experience Platform으로 가져오도록 데이터 흐름을 구성](../../dataflow/databases.md)할 수 있습니다.
