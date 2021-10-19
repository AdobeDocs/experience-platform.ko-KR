---
keywords: Experience Platform;홈;인기 항목;Snowflake
title: UI에서 Snowflake 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Snowflake 소스 연결을 만드는 방법을 알아봅니다.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 76b3e3e9bcb27eb2bd6981ae6eb109410ae16336
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# 만들기 [!DNL Snowflake] UI의 소스 연결

>[!NOTE]
>
> 다음 [!DNL Snowflake] 커넥터가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 커넥터 사용에 대한 자세한 정보.

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Snowflake] Adobe Experience Platform 사용자 인터페이스를 사용한 소스 커넥터.

## 시작하기

이 자습서에서는 Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

### 필요한 자격 증명 수집

Snowflake 계정에 액세스하려면 [!DNL Platform], 다음 인증 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 계정 | 와 연결된 전체 계정 이름 [!DNL Snowflake] 계정이 필요합니다. 충분한 자격이 있는 [!DNL Snowflake] 계정 이름에는 계정 이름, 지역 및 클라우드 플랫폼이 포함됩니다. 예, `cj12345.east-us-2.azure`. 계정 이름에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| 웨어하우스 | 다음 [!DNL Snowflake] 웨어하우스는 응용 프로그램에 대한 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] warehouse는 서로 독립적이므로 Platform으로 데이터를 전송할 때 개별적으로 액세스해야 합니다. |
| 데이터베이스 | 다음 [!DNL Snowflake] 데이터베이스에 Platform을 가져올 데이터가 포함되어 있습니다. |
| 사용자 이름 | 사용자 이름 [!DNL Snowflake] 계정이 필요합니다. |
| 암호 | 의 암호 [!DNL Snowflake] 사용자 계정. |
| 연결 문자열 | 에 연결하는 데 사용되는 연결 문자열입니다 [!DNL Snowflake] 인스턴스. 에 대한 연결 문자열 패턴 [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

이러한 값에 대한 자세한 내용은 [이 Snowflake 문서](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Snowflake 계정 연결

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 데이터베이스] 카테고리, 선택 **[!UICONTROL Snowflake]** 그런 다음 **[!UICONTROL 데이터 추가]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

다음 **[!UICONTROL Snowflake에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 연결할 Snowflake 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![](../../../../images/tutorials/create/snowflake/existing.png)

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 Snowflake 자격 증명을 제공합니다. 완료되면 을 선택합니다 **[!UICONTROL Connect]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![](../../../../images/tutorials/create/snowflake/new.png)

## 다음 단계

이 자습서에 따라 Snowflake 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 구성하여 데이터 [!DNL Platform]](../../dataflow/databases.md).
