---
keywords: Experience Platform;홈;인기 항목;[!DNL PostgreSQL];[!DNL PostgreSQL];PostgreSQL
solution: Experience Platform
title: UI에서 PostgreSQL Source 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 PostgreSQL 소스 연결을 만드는 방법을 알아봅니다.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 2%

---

# UI에서 [!DNL PostgreSQL] 소스 연결 만들기

Adobe Experience Platform의 Source 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 [!DNL Experience Platform] 사용자 인터페이스를 사용하여 [!DNL PostgreSQL] 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 올바른 [!DNL PostgreSQL] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/databases.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL Experience Platform]에서 [!DNL PostgreSQL] 계정에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | [!DNL PostgreSQL] 계정과 연결된 연결 문자열입니다. [!DNL PostgreSQL] 연결 문자열 패턴은 `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`입니다. |

시작에 대한 자세한 내용은 이 [[!DNL PostgreSQL] 문서](https://www.postgresql.org/docs/9.2/app-psql.html)를 참조하세요.

#### 연결 문자열에 SSL 암호화 사용

다음 속성을 사용하여 연결 문자열을 추가하여 [!DNL PostgreSQL] 연결 문자열에 SSL 암호화를 사용하도록 설정할 수 있습니다.

| 속성 | 설명 | 예 |
| --- | --- | --- |
| `EncryptionMethod` | [!DNL PostgreSQL] 데이터에 대해 SSL 암호화를 사용하도록 설정할 수 있습니다. | <uL><li>`EncryptionMethod=0`(사용 안 함)</li><li>`EncryptionMethod=1`(활성화됨)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | `EncryptionMethod`이(가) 적용되면 [!DNL PostgreSQL] 데이터베이스에서 보낸 인증서의 유효성을 검사합니다. | <uL><li>`ValidationServerCertificate=0`(사용 안 함)</li><li>`ValidationServerCertificate=1`(활성화됨)</li></ul> |

다음은 SSL 암호화가 추가된 [!DNL PostgreSQL] 연결 문자열의 예입니다. `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## [!DNL PostgreSQL] 계정 연결

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL PostgreSQL] 계정을 [!DNL Experience Platform]에 연결할 수 있습니다.

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 **[!UICONTROL 소스]** 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**[!UICONTROL 데이터베이스]** 범주에서 **[!UICONTROL PostgreSQL DB]**&#x200B;를 선택합니다. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**&#x200B;을 선택하세요. 그렇지 않으면 **[!UICONTROL 데이터 추가]**&#x200B;를 선택하여 새 [!DNL PostgreSQL] 커넥터를 만드십시오.

![](../../../../images/tutorials/create/postgresql/catalog.png)

**[!UICONTROL [!DNL PostgreSQL]]**&#x200B;에 연결 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택하십시오. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL PostgreSQL] 자격 증명을 제공합니다. 완료되면 **[!UICONTROL 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 시간을 허용합니다.

![](../../../../images/tutorials/create/postgresql/new.png)

### 기존 계정

기존 계정에 연결하려면 연결할 [!DNL PostgreSQL] 계정을 선택한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![](../../../../images/tutorials/create/postgresql/existing.png)

## 다음 단계

이 자습서에 따라 [!DNL PostgreSQL] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 가져올 데이터 흐름을 구성 [!DNL Experience Platform]](../../dataflow/databases.md)할 수 있습니다.
