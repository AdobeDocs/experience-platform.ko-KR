---
title: UI에서 Snowflake 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Snowflake 소스 연결을 만드는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 만들기 [!DNL Snowflake] UI의 소스 연결

>[!IMPORTANT]
>
>다음 [!DNL Snowflake] 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 소스 카탈로그에서 사용할 수 있습니다.

이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL Snowflake] Adobe Experience Platform 사용자 인터페이스를 사용하는 소스 커넥터입니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

### 필요한 자격 증명 수집

인증하려면 다음 자격 증명 속성에 대한 값을 제공해야 합니다. [!DNL Snowflake] 소스.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 계정 | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 계정에서 계정을 고유하게 식별해야 합니다 [!DNL Snowflake] 조직. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `orgname-account_name`. 계정 이름에 대한 자세한 내용은 [!DNL Snowflake] 설명서 [계정 식별자](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| 웨어하우스 | 다음 [!DNL Snowflake] warehouse는 애플리케이션의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] warehouse는 서로 독립적이며 데이터를 Platform으로 가져올 때 개별적으로 액세스해야 합니다. |
| 데이터베이스 | 다음 [!DNL Snowflake] 데이터베이스에는 플랫폼으로 가져올 데이터가 포함되어 있습니다. |
| 사용자 이름 | 의 사용자 이름 [!DNL Snowflake] 계정입니다. |
| 암호 | 에 대한 암호 [!DNL Snowflake] 사용자 계정입니다. |
| 역할 | 에서 사용할 기본 액세스 제어 역할 [!DNL Snowflake] 세션. 역할은 지정된 사용자에게 이미 할당된 기존 역할이어야 합니다. 기본 역할은 입니다. `PUBLIC`. |
| 연결 문자열 | 에 연결하는 데 사용되는 연결 문자열 [!DNL Snowflake] 인스턴스. 에 대한 연결 문자열 패턴입니다 [!DNL Snowflake] 은(는) `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB 키 쌍 인증]

키 쌍 인증을 사용하려면 2048비트 RSA 키 쌍을 생성한 다음 용 계정을 만들 때 다음 값을 제공해야 합니다. [!DNL Snowflake] 소스.

| 자격 증명 | 설명 |
| --- | --- |
| 계정 | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 계정에서 계정을 고유하게 식별해야 합니다 [!DNL Snowflake] 조직. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `orgname-account_name`. 계정 이름에 대한 자세한 내용은 [!DNL Snowflake] 설명서 [계정 식별자](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| 사용자 이름 | 의 사용자 이름 [!DNL Snowflake] 계정입니다. |
| 개인 키 | 다음 [!DNL Base64-]의 인코딩된 개인 키 [!DNL Snowflake] 계정입니다. 암호화되거나 암호화되지 않은 개인 키를 생성할 수 있습니다. 암호화된 개인 키를 사용하는 경우 Experience Platform에 대해 인증할 때 개인 키 암호도 제공해야 합니다. |
| 개인 키 암호 | 개인 키 암호는 암호화된 개인 키로 인증할 때 사용해야 하는 추가 보안 계층입니다. 암호화되지 않은 개인 키를 사용하는 경우에는 암호를 제공할 필요가 없습니다. |
| 데이터베이스 | 다음 [!DNL Snowflake] Experience Platform 대상으로 수집할 데이터가 포함된 데이터베이스. |
| 웨어하우스 | 다음 [!DNL Snowflake] warehouse는 애플리케이션의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] warehouse는 서로 독립적이며 데이터를 Platform으로 가져올 때 개별적으로 액세스해야 합니다. |

이러한 값에 대한 자세한 내용은 [이 Snowflake 문서](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

Experience Platform 시 Snowflake 계정에 액세스하려면 다음 인증 값을 제공해야 합니다.

>[!NOTE]
>
>다음을 설정해야 합니다. `PREVENT_UNLOAD_TO_INLINE_URL` 플래그 지정 대상 `FALSE` 에서 데이터 언로드를 허용하려면 [!DNL Snowflake] Experience Platform 대상 데이터베이스.

## Snowflake 계정 연결

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 데이터베이스] 범주, 선택 **[!UICONTROL Snowflake]** 다음을 선택합니다. **[!UICONTROL 데이터 추가]**.

![소스 카탈로그 [!DNL Snowflake] 강조 표시됨.](../../../../images/tutorials/create/snowflake/catalog.png)

다음 **[!UICONTROL Snowflake에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL Snowflake] 연결할 계정 을(를) 선택한 다음 **[!UICONTROL 다음]** 계속합니다.

![소스 워크플로우의 기존 계정 인터페이스.](../../../../images/tutorials/create/snowflake/existing.png)

### 새 계정

새 계정을 만들려면 다음을 선택합니다. **[!UICONTROL 새 계정]**&#x200B;을 클릭하고 새 항목의 이름과 설명(선택 사항)을 입력합니다 [!DNL Snowflake] 계정입니다.

![소스 워크플로우의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하려면 입력 양식에 연결 문자열을 입력한 다음 을 선택합니다. **[!UICONTROL 소스에 연결]**.

![계정 키 인증 인터페이스입니다.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB 키 쌍 인증]

키 쌍 인증을 사용하려면 계정, 사용자 이름, 개인 키, 개인 키 암호, 데이터베이스 및 웨어하우스에 대한 값을 입력한 다음 을 선택합니다 **[!UICONTROL 소스에 연결]**.

![계정 키 쌍 인증 인터페이스입니다.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## 다음 단계

이 자습서에 따라 Snowflake 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터 흐름을 구성하여 데이터 가져오기 [!DNL Platform]](../../dataflow/databases.md).
