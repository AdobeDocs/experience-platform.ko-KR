---
keywords: Experience Platform;홈;인기 항목;Azure HDInsights;Apache Spark
solution: Experience Platform
title: UI에서 Azure HDInsights 소스 연결에서 Apache 스파크 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Azure HDInsights 소스 연결에서 Apache 스파크를 만드는 방법을 알아봅니다.
exl-id: 30d0b740-cec4-486f-9c9b-1579fd04f28b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# 만들기 [!DNL Apache Spark] on [!DNL Azure HDInsights] UI의 소스 연결

>[!NOTE]
>
> 다음 [!DNL Apache Spark] on [!DNL Azure HDInsights] 커넥터가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 커넥터 사용에 대한 자세한 정보.

Adobe Experience Platform의 소스 커넥터는 예약된 방식으로 외부 소스 데이터를 수집할 수 있습니다. 이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Apache Spark] on [!DNL Azure HDInsights] 소스 커넥터 [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [XDM(경험 데이터 모델) 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [실시간 고객 프로필](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Spark] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/databases.md)

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Spark] 계정 설정 [!DNL Platform], 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 의 IP 주소 또는 호스트 이름 [!DNL Spark] server. |
| `username` | 액세스하기 위해 사용하는 사용자 이름 [!DNL Spark] server. |
| `password` | 사용자에게 해당하는 암호입니다. |

시작하는 방법에 대한 자세한 내용은 [이 Spark 문서](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

## 연결 [!DNL Spark] account

필요한 자격 증명을 수집하면 아래 단계에 따라 를 연결할 수 있습니다 [!DNL Spark] 연결할 계정 [!DNL Platform].

에 로그인합니다. [Adobe Experience Platform](https://platform.adobe.com) 그런 다음 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 **[!UICONTROL 소스]** 작업 공간. 다음 **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 **[!UICONTROL 데이터베이스]** 카테고리, 선택 **[!UICONTROL 스파크]**. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**. 그렇지 않으면 을 선택합니다. **[!UICONTROL 데이터 추가]** 새 [!DNL Spark] 커넥터.

![카탈로그](../../../../images/tutorials/create/spark/catalog.png)

다음 **[!UICONTROL Spark에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL Spark] 자격 증명. 완료되면 을 선택합니다 **[!UICONTROL Connect]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![새](../../../../images/tutorials/create/spark/new.png)

### 기존 계정

기존 계정을 연결하려면 [!DNL Spark] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/spark/existing.png)

## 다음 단계

이 자습서에 따라 [!DNL Spark] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 구성하여 데이터 [!DNL Platform]](../../dataflow/databases.md).
