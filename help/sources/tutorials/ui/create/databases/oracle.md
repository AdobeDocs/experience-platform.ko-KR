---
title: Ui를 사용하여 Oracle DB를 Experience Platform에 연결
description: UI를 사용하여 Oracle DB 인스턴스를 Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# UI에서 [!DNL Oracle DB] 소스 연결 만들기

Experience Platform 사용자 인터페이스의 소스 작업 영역을 사용하여 [!DNL Oracle DB] 인스턴스를 Adobe Experience Platform에 연결하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 [!DNL Oracle DB] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/databases.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL Oracle DB] 개요](../../../../connectors/databases/oracle.md#prerequisites)를 읽어 보십시오.

## 소스 카탈로그 탐색

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 *[!UICONTROL 소스]* 작업 영역에 액세스합니다. 카테고리를 선택하거나 검색 창을 사용하여 소스를 찾습니다.

[!DNL Oracle DB]에 연결하려면 *[!UICONTROL 데이터베이스]* 범주로 이동하여 **[!UICONTROL Oracle DB]** 원본 카드를 선택한 다음 **[!UICONTROL 설정]**&#x200B;을 선택하십시오.

>[!TIP]
>
>소스에 새 연결에 대한 **[!UICONTROL 설정]** 및 계정이 이미 있는 경우 **[!UICONTROL 데이터 추가]**&#x200B;가 표시됩니다.

![&quot;Oracle DB&quot;가 있는 원본 카탈로그를 선택했습니다.](../../../../images/tutorials/create/oracle/catalog.png)

## 기존 계정 사용 {#existing}

기존 계정을 사용하려면 **[!UICONTROL 기존 계정]**&#x200B;을(를) 선택한 다음 사용할 [!DNL Oracle DB] 계정을 선택하십시오.

![&quot;기존 계정&quot;이 선택된 원본 워크플로의 기존 계정 인터페이스입니다.](../../../../images/tutorials/create/oracle/existing.png)

## 새 계정 만들기 {#new}

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을 선택한 다음 이름을 입력하고 필요에 따라 계정에 대한 설명을 추가하십시오.

### Azure에서 Experience Platform에 연결 {#azure}

연결 문자열을 사용하여 [!DNL Oracle DB] 데이터베이스를 Azure의 Experience Platform에 연결할 수 있습니다.

연결 문자열 인증을 사용하려면 [연결 문자열](../../../../connectors/databases/oracle.md#azure)을 제공하고 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하십시오.

![연결 문자열 인증이 선택된 원본 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/oracle/azure.png)

### Amazon Web Services(AWS)에서 Experience Platform에 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

새 [!DNL Oracle DB] 계정을 만들고 AWS의 Experience Platform에 연결하려면 VA6 샌드박스에 있는지 확인한 다음 인증에 필요한 [자격 증명을 제공](../../../../connectors/databases/oracle.md#aws)합니다.

![AWS에 연결할 소스 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/oracle/aws.png)

## [!DNL Oracle DB] 데이터에 대한 데이터 흐름 만들기

[!DNL Oracle DB] 데이터베이스를 연결했으므로 이제 [데이터 흐름을 만들고 데이터베이스에서 Experience Platform으로 데이터를 수집](../../dataflow/databases.md)할 수 있습니다.
