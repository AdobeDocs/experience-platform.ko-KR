---
keywords: Experience Platform;홈;인기 항목;Azure Blob;azure blob;Azure Blob 커넥터
solution: Experience Platform
title: UI에서 Azure Blob 소스 연결 만들기
type: Tutorial
description: 플랫폼 사용자 인터페이스를 사용하여 Azure Blob 소스 커넥터를 만드는 방법을 알아봅니다.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---

# 만들기 [!DNL Azure Blob] UI의 소스 연결

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Azure Blob] (이하 &quot;라 한다)[!DNL Blob]&quot;) 플랫폼 사용자 인터페이스를 사용합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Blob] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md).

### 지원되는 파일 형식

[!DNL Experience Platform] 에서는 외부 저장소에서 수집할 다음 파일 형식을 지원합니다.

- 구분 기호로 구분된 값(DSV): DSV 형식 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다. DSV 형식 파일 내의 필드 헤더 값은 영숫자 문자 및 밑줄로만 구성되어야 합니다. 일반적인 DSV 파일에 대한 지원은 향후에 제공됩니다.
- JavaScript 개체 표기법(JSON): JSON 형식 데이터 파일은 XDM 규격 파일이어야 합니다.
- Apache Parquet: Parquet 형식 데이터 파일은 XDM 규격 파일이어야 합니다.

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Blob] 플랫폼의 저장소는 다음 자격 증명에 유효한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | 인증에 필요한 인증 정보가 들어 있는 문자열입니다 [!DNL Blob] Experience Platform에 연결할 수도 있습니다. 다음 [!DNL Blob] 연결 문자열 패턴은 다음과 같습니다. `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 연결 문자열에 대한 자세한 내용은 다음을 참조하십시오 [!DNL Blob] 문서 [연결 문자열 구성](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | 다른 인증 유형으로 사용하여 연결할 수 있는 공유 액세스 서명 URI [!DNL Blob] 계정이 필요합니다. 다음 [!DNL Blob] SAS URI 패턴: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 자세한 내용은 다음을 참조하십시오 [!DNL Blob] 문서 [공유 액세스 서명 URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## 연결 [!DNL Blob] account

필요한 자격 증명을 수집하면 아래 단계에 따라 를 연결할 수 있습니다 [!DNL Blob] Platform에 계정을 설정합니다.

에서 [플랫폼 UI](https://platform.adobe.com), 선택 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 클라우드 스토리지] 카테고리, 선택 **[!UICONTROL Azure Blob 저장소]**&#x200B;를 선택한 다음 을 선택합니다. **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/blob/catalog.png)

다음 **[!UICONTROL Azure Blob 저장소에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL Blob] 새 데이터 흐름을 만들 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/blob/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**, 그런 다음 이름 및 옵션 설명을 새로 추가합니다 [!DNL Blob] 계정이 필요합니다.

**연결 문자열을 사용하여 인증**

다음 [!DNL Blob] 커넥터는 액세스를 위한 다양한 인증 유형을 제공합니다. 아래 [!UICONTROL 계정 인증] 선택 **[!UICONTROL ConnectionString]** 연결 문자열 기반 자격 증명을 사용하려면 다음을 수행하십시오.

![연결 문자열](../../../../images/tutorials/create/blob/connectionstring.png)

**공유 액세스 서명 URI를 사용하여 인증**

SAS(공유 액세스 서명) URI를 사용하면 사용자에게 안전한 위임된 권한 부여가 허용됩니다 [!DNL Blob] 계정이 필요합니다. SAS 기반 인증을 사용하면 권한, 시작 및 만료 날짜 및 특정 리소스에 대한 규정을 설정할 수 있으므로 다양한 액세스 수준을 갖는 인증 자격 증명을 만들 수 있습니다.

선택 **[!UICONTROL SasURIAuthentication]** 그런 다음 [!DNL Blob] SAS URI. 선택 **[!UICONTROL 소스에 연결]** 계속 진행합니다.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## 다음 단계

이 자습서에 따라 [!DNL Blob] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [클라우드 저장소에서 플랫폼으로 데이터를 가져오도록 데이터 흐름 구성](../../dataflow/batch/cloud-storage.md).
