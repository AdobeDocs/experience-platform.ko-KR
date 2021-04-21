---
keywords: Experience Platform;홈;인기 항목;Azure Blob;azure blob;Azure Blob 커넥터
solution: Experience Platform
title: UI에서 Azure Blob 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: 플랫폼 사용자 인터페이스를 사용하여 Azure Blob 소스 커넥터를 만드는 방법을 알아봅니다.
exl-id: 0e54569b-7305-4065-981e-951623717648
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# UI에 [!DNL Azure Blob] 소스 연결 만들기

이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 [!DNL Azure Blob](이하 &quot;a1/>&quot;라 함)을 만드는 단계를 제공합니다.[!DNL Blob]

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Blob] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름](../../dataflow/batch/cloud-storage.md)을 구성하는 자습서로 진행할 수 있습니다.

### 지원되는 파일 형식

[!DNL Experience Platform] 외부 저장소에서 인제스트할 다음 파일 형식을 지원합니다.

- 구분 기호 구분 값(DSV):DSV 형식 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다. DSV 형식 파일 내의 필드 헤더 값은 영숫자 문자와 밑줄로만 구성되어야 합니다. 일반 DSV 파일에 대한 지원은 나중에 제공될 예정입니다.
- JavaScript 개체 표기법(JSON):JSON 형식 데이터 파일은 XDM 규격이어야 합니다.
- Apache Parided:쪽모이 세공된 형식의 데이터 파일은 XDM 규격이어야 합니다.

### 필요한 자격 증명 수집

플랫폼에서 [!DNL Blob] 스토리지에 액세스하려면 다음 자격 증명에 유효한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | Experience Platform에 대해 [!DNL Blob]을(를) 인증하는 데 필요한 인증 정보를 포함하는 문자열입니다. [!DNL Blob] 연결 문자열 패턴은 다음과 같습니다.`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 연결 문자열에 대한 자세한 내용은 [연결 문자열 구성](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)의 이 [!DNL Blob] 문서를 참조하십시오. |
| `sasUri` | 대체 인증 유형으로 사용하여 [!DNL Blob] 계정을 연결할 수 있는 공유 액세스 서명 URI입니다. [!DNL Blob] SAS URI 패턴은 다음과 같습니다.`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 자세한 내용은 [공유 액세스 서명 URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)에 있는 이 [!DNL Blob] 문서를 참조하십시오. |

## [!DNL Blob] 계정 연결

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Blob] 계정을 플랫폼에 연결할 수 있습니다.

[플랫폼 UI](https://platform.adobe.com)의 왼쪽 탐색 막대에서 **[!UICONTROL Sources]**&#x200B;를 선택하여 [!UICONTROL Sources] 작업 영역에 액세스합니다. [!UICONTROL Catalog] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL Cloud storage] 범주에서 **[!UICONTROL Azure Blob Storage]**&#x200B;을 선택한 다음 **[!UICONTROL Add data]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/blob/catalog.png)

**[!UICONTROL Connect to Azure Blob Storage]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 [!DNL Blob] 계정을 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택하여 계속 진행합니다.

![기존](../../../../images/tutorials/create/blob/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL New account]**&#x200B;을 선택한 다음 새 [!DNL Blob] 계정에 대한 이름과 옵션 설명을 입력합니다.

**연결 문자열을 사용하여 인증**

[!DNL Blob] 커넥터는 액세스할 수 있는 다른 인증 유형을 제공합니다. [!UICONTROL Account authentication] 아래에서 **[!UICONTROL ConnectionString]** 을 선택하여 연결 문자열 기반 자격 증명을 사용합니다.

![연결 문자열](../../../../images/tutorials/create/blob/connectionstring.png)

**공유 액세스 서명 URI를 사용하여 인증**

SAS(Shared Access Signature) URI를 사용하면 [!DNL Blob] 계정에 대한 보안 위임 인증을 허용합니다. SAS 기반 인증을 통해 특정 리소스에 대한 규정 및 권한, 시작 및 만료 날짜를 설정할 수 있으므로 SAS를 사용하여 액세스 수준이 다른 인증 자격 증명을 만들 수 있습니다.

**[!UICONTROL SasURIAuthentication]**&#x200B;을 선택한 다음 [!DNL Blob] SAS URI를 제공합니다. 계속하려면 **[!UICONTROL Connect to source]**&#x200B;을 선택합니다.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## 다음 단계

이 자습서를 따라 [!DNL Blob] 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행할 수 있으며 [데이터 흐름 구성을 통해 클라우드 스토리지의 데이터를 플랫폼](../../dataflow/batch/cloud-storage.md)으로 가져올 수 있습니다.
