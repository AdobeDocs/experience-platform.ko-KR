---
title: Ui를 사용하여 PostgreSQL을 Experience Platform에 연결
description: Experience Platform 사용자 인터페이스의 소스 작업 영역을 사용하여 PostgreSQL 데이터베이스를 Experience Platform에 연결하는 방법에 대해 알아봅니다.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: 8cabf1cb86993fdde37d0b9d957f6c8ec23bb237
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# UI를 사용하여 [!DNL PostgreSQL]을(를) Experience Platform에 연결

Experience Platform 사용자 인터페이스의 소스 작업 영역을 사용하여 [!DNL PostgreSQL] 데이터베이스를 Adobe Experience Platform에 연결하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 올바른 [!DNL PostgreSQL] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/databases.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL PostgreSQL] 개요](../../../../connectors/databases/postgres.md)를 참조하세요.

### 연결 문자열에 SSL 암호화 사용

다음 속성을 사용하여 연결 문자열을 추가하여 [!DNL PostgreSQL] 연결 문자열에 SSL 암호화를 사용하도록 설정할 수 있습니다.

| 속성 | 설명 | 예 |
| --- | --- | --- |
| `EncryptionMethod` | [!DNL PostgreSQL] 데이터에 대해 SSL 암호화를 사용하도록 설정할 수 있습니다. | <uL><li>`EncryptionMethod=0`(사용 안 함)</li><li>`EncryptionMethod=1`(활성화됨)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | `EncryptionMethod`이(가) 적용되면 [!DNL PostgreSQL] 데이터베이스에서 보낸 인증서의 유효성을 검사합니다. | <uL><li>`ValidationServerCertificate=0`(사용 안 함)</li><li>`ValidationServerCertificate=1`(활성화됨)</li></ul> |

다음은 SSL 암호화가 추가된 [!DNL PostgreSQL] 연결 문자열의 예입니다. `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## 소스 카탈로그 탐색 {#navigate}

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 *[!UICONTROL 소스]* 작업 영역에 액세스합니다. *[!UICONTROL 범주]* 패널에서 적절한 범주를 선택합니다. 또는 검색 창을 사용하여 사용할 특정 소스로 이동합니다.

[!DNL PostgreSQL]을(를) 사용하려면 *[!UICONTROL 데이터베이스]*&#x200B;에서 **[!UICONTROL PostgreSQL]** 원본 카드를 선택한 다음 **[!UICONTROL 설정]**&#x200B;을 선택하십시오.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL 설정]** 옵션이 표시됩니다. 인증된 계정을 만들면 이 옵션이 **[!UICONTROL 데이터 추가]**(으)로 변경됩니다.



## 기존 계정 사용 {#existing}

기존 계정을 사용하려면 **[!UICONTROL 기존 계정]**&#x200B;을(를) 선택한 다음 사용할 [!DNL PostgreSQL] 계정을 선택하십시오.

![원본 워크플로의 기존 계정 인터페이스입니다.](../../../../images/tutorials/create/postgresql/catalog.png)

## 새 계정 만들기 {#create}

기존 계정이 없는 경우 소스와 일치하는 필요한 인증 자격 증명을 제공하여 새 계정을 만들어야 합니다.

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을 선택한 다음 이름을 입력하고 필요에 따라 계정에 대한 설명을 추가하십시오.

![계정 이름과 선택적 설명을 제공하는 원본 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/postgresql/existing.png)

### Azure에서 Experience Platform에 연결 {#azure}

계정 키 또는 기본 인증을 사용하여 [!DNL PostgreSQL] 계정을 Azure의 Experience Platform에 연결할 수 있습니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하려면 **[!UICONTROL 계정 키 인증]**&#x200B;을 선택하고 [연결 문자열](../../../../connectors/databases/postgres.md#azure)을 제공한 다음 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하십시오.

![&quot;계정 키 인증&quot;이 선택된 원본 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/postgresql/account-key.png)

>[!TAB 기본 인증]

기본 인증을 사용하려면 **[!UICONTROL 기본 인증]**&#x200B;을 선택하고 [인증 자격 증명](../../../../connectors/databases/postgres.md#azure)의 값을 제공한 다음 **[!UICONTROL 소스에 연결]**&#x200B;을 선택하십시오.

![기본 인증을 선택한 원본 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/postgresql/basic-auth.png)

>[!ENDTABS]

### Amazon Web Services(AWS)에서 Experience Platform에 연결 {#aws}

>[!AVAILABILITY]
>
>이 섹션은 Amazon Web Services(AWS)에서 실행되는 Experience Platform 구현에 적용됩니다. AWS에서 실행되는 Experience Platform은 현재 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../../../landing/multi-cloud.md)를 참조하세요.

새 [!DNL PostgreSQL] 계정을 만들고 AWS의 Experience Platform에 연결하려면 VA6 샌드박스에 있는지 확인한 다음 인증에 필요한 [자격 증명을 제공](../../../../connectors/databases/postgres.md#aws)합니다.

![AWS에 연결할 소스 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/postgresql/basic-auth.png)

## [!DNL PostgreSQL] 데이터에 대한 데이터 흐름 만들기

이 자습서에 따라 [!DNL MariaDB] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 Experience Platform으로 가져오도록 데이터 흐름을 구성](../../dataflow/databases.md)할 수 있습니다.
