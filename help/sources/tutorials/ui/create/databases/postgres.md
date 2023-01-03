---
keywords: Experience Platform;홈;인기 있는 주제[!DNL PostgreSQL];[!DNL PostgreSQL]PostgreSQL
solution: Experience Platform
title: UI에서 PostgreSQL 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 PostgreSQL 소스 연결을 만드는 방법을 알아봅니다.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# 만들기 [!DNL PostgreSQL] UI의 소스 연결

Adobe Experience Platform의 소스 커넥터는 예약된 방식으로 외부 소스 데이터를 수집할 수 있습니다. 이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL PostgreSQL] 소스 커넥터 [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL PostgreSQL] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/databases.md).

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL PostgreSQL] 계정 설정 [!DNL Platform], 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | 와 연결된 연결 문자열 [!DNL PostgreSQL] 계정이 필요합니다. 다음 [!DNL PostgreSQL] 연결 문자열 패턴은 다음과 같습니다. `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

시작하는 방법에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL PostgreSQL] 문서](https://www.postgresql.org/docs/9.2/app-psql.html).

#### 연결 문자열에 대해 SSL 암호화 사용

에 대해 SSL 암호화를 활성화할 수 있습니다 [!DNL PostgreSQL] 다음 속성과 함께 연결 문자열을 추가하여 연결 문자열:

| 속성 | 설명 | 예 |
| --- | --- | --- |
| `EncryptionMethod` | 에서 SSL 암호화를 활성화할 수 있습니다 [!DNL PostgreSQL] 데이터. | <uL><li>`EncryptionMethod=0`(비활성화됨)</li><li>`EncryptionMethod=1`(활성화됨)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 에서 보낸 인증서의 유효성을 검사합니다. [!DNL PostgreSQL] 데이터베이스 `EncryptionMethod` 이 적용됩니다. | <uL><li>`ValidationServerCertificate=0`(비활성화됨)</li><li>`ValidationServerCertificate=1`(활성화됨)</li></ul> |

다음은 의 예입니다 [!DNL PostgreSQL] SSL 암호화와 함께 추가된 연결 문자열: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## 연결 [!DNL PostgreSQL] account

필요한 자격 증명을 수집하면 아래 단계에 따라 를 연결할 수 있습니다 [!DNL PostgreSQL] 계정 대상 [!DNL Platform].

에 로그인합니다. [Adobe Experience Platform](https://platform.adobe.com) 그런 다음 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 **[!UICONTROL 소스]** 작업 공간. 다음 **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 **[!UICONTROL 데이터베이스]** 카테고리, 선택 **[!UICONTROL PostgreSQL DB]**. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**. 그렇지 않으면 을 선택합니다. **[!UICONTROL 데이터 추가]** 새 [!DNL PostgreSQL] 커넥터.

![](../../../../images/tutorials/create/postgresql/catalog.png)

다음 **[!UICONTROL 연결 대상[!DNL PostgreSQL]]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL PostgreSQL] 자격 증명. 완료되면 을 선택합니다 **[!UICONTROL Connect]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![](../../../../images/tutorials/create/postgresql/new.png)

### 기존 계정

기존 계정을 연결하려면 [!DNL PostgreSQL] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![](../../../../images/tutorials/create/postgresql/existing.png)

## 다음 단계

이 자습서에 따라 [!DNL PostgreSQL] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 구성하여 데이터 [!DNL Platform]](../../dataflow/databases.md).
