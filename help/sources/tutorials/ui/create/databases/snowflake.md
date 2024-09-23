---
title: UI에서 Snowflake Source 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Snowflake 소스 연결을 만드는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 3%

---

# UI에서 [!DNL Snowflake] 소스 연결 만들기

>[!IMPORTANT]
>
>[!DNL Snowflake] 원본은 Real-time Customer Data Platform Ultimate를 구입한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 [!DNL Snowflake] 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Snowflake] 원본을 인증하려면 다음 자격 증명 속성에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 계정 | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 [!DNL Snowflake] 조직에서 계정을 고유하게 식별해야 합니다. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `orgname-account_name`. 추가 지침은 [계정 식별자 검색 [!DNL Snowflake] 에 대한 안내서를 참조하십시오](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier). 자세한 내용은 [[!DNL Snowflake] 설명서](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)를 참조하세요. |
| 웨어하우스 | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이며 데이터를 플랫폼으로 가져올 때 개별적으로 액세스해야 합니다. |
| 데이터베이스 | [!DNL Snowflake] 데이터베이스에 플랫폼에 가져올 데이터가 있습니다. |
| 사용자 이름 | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| 암호 | [!DNL Snowflake] 사용자 계정의 암호입니다. |
| 역할 | [!DNL Snowflake] 세션에서 사용할 기본 액세스 제어 역할입니다. 역할은 지정된 사용자에게 이미 할당된 기존 역할이어야 합니다. 기본 역할은 `PUBLIC`입니다. |
| 연결 문자열 | [!DNL Snowflake] 인스턴스에 연결하는 데 사용되는 연결 문자열입니다. [!DNL Snowflake]에 대한 연결 문자열 패턴은 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`입니다. |

>[!TAB 키 쌍 인증]

키 쌍 인증을 사용하려면 2048비트 RSA 키 쌍을 생성한 다음 [!DNL Snowflake] 소스에 대한 계정을 만들 때 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 계정 | 계정 이름은 조직 내에서 계정을 고유하게 식별합니다. 이 경우 서로 다른 [!DNL Snowflake] 조직에서 계정을 고유하게 식별해야 합니다. 이렇게 하려면 계정 이름 앞에 조직 이름을 추가해야 합니다. 예: `orgname-account_name`. 추가 지침은 [계정 식별자 검색 [!DNL Snowflake] 에 대한 안내서를 참조하십시오](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier). 자세한 내용은 [[!DNL Snowflake] 설명서](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)를 참조하세요. |
| 사용자 이름 | [!DNL Snowflake] 계정의 사용자 이름입니다. |
| 개인 키 | [!DNL Snowflake] 계정의 [!DNL Base64-]인코딩된 개인 키입니다. 암호화되거나 암호화되지 않은 개인 키를 생성할 수 있습니다. 암호화된 개인 키를 사용하는 경우 Experience Platform에 대해 인증할 때 개인 키 암호도 제공해야 합니다. 자세한 내용은 [개인 키 검색 [!DNL Snowflake] 2}에 대한 안내서를 참조하십시오.](../../../../connectors/databases/snowflake.md) |
| 개인 키 암호 | 개인 키 암호는 암호화된 개인 키로 인증할 때 사용해야 하는 추가 보안 계층입니다. 암호화되지 않은 개인 키를 사용하는 경우에는 암호를 제공할 필요가 없습니다. |
| 데이터베이스 | Experience Platform 대상으로 수집할 데이터가 포함된 [!DNL Snowflake] 데이터베이스입니다. |
| 웨어하우스 | [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 [!DNL Snowflake] 웨어하우스는 서로 독립적이며 데이터를 플랫폼으로 가져올 때 개별적으로 액세스해야 합니다. |

이러한 값에 대한 자세한 내용은 [이 Snowflake 문서](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)를 참조하세요.

>[!ENDTABS]

>[!NOTE]
>
>[!DNL Snowflake] 데이터베이스에서 Experience Platform으로 데이터를 언로드하려면 `PREVENT_UNLOAD_TO_INLINE_URL` 플래그를 `FALSE`(으)로 설정해야 합니다.

## Snowflake 계정 연결

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 데이터베이스] 범주에서 **[!UICONTROL Snowflake]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![강조 표시된 [!DNL Snowflake]의 원본 카탈로그입니다.](../../../../images/tutorials/create/snowflake/catalog.png)

**[!UICONTROL Snowflake에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 연결할 [!DNL Snowflake] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![원본 워크플로의 기존 계정 인터페이스입니다.](../../../../images/tutorials/create/snowflake/existing.png)

### 새 계정

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 새 [!DNL Snowflake] 계정에 대한 이름과 선택적 설명을 입력하십시오.

![원본 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하려면 입력 양식에 연결 문자열을 입력한 다음 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하십시오.

![계정 키 인증 인터페이스입니다.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB 키 쌍 인증]

키 쌍 인증을 사용하려면 계정, 사용자 이름, 개인 키, 개인 키 암호, 데이터베이스 및 웨어하우스에 대한 값을 제공한 다음 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하십시오.

![계정 키 쌍 인증 인터페이스](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

### 샘플 데이터의 미리 보기 건너뛰기 {#skip-preview-of-sample-data}

데이터 선택 단계에서 큰 테이블 또는 데이터 파일을 수집할 때 시간 초과가 발생할 수 있습니다. 샘플 데이터가 없어도 데이터 미리 보기를 건너뛰어 시간 초과를 우회하고 스키마를 볼 수 있습니다. 데이터 미리 보기를 건너뛰려면 **[!UICONTROL 샘플 데이터 미리 보기 건너뛰기]** 전환을 사용하도록 설정하십시오.

워크플로우의 나머지 부분은 그대로 유지됩니다. 유일한 주의 사항은 데이터 미리보기를 건너뛰면 매핑 단계에서 계산된 필드 및 필수 필드의 자동 유효성 검사를 방지할 수 있으므로 매핑 중에 이러한 필드의 유효성을 수동으로 검사해야 한다는 것입니다.

## 다음 단계

이 자습서에 따라 Snowflake 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 가져올 데이터 흐름을 구성 [!DNL Platform]](../../dataflow/databases.md)할 수 있습니다.
