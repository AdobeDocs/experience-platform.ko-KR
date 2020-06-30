---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 Azure Blob 또는 Amazon S3 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---


# UI에서 [!DNL Azure Blob] 또는 [!DNL Amazon] S3 소스 커넥터 만들기

Adobe Experience Platform의 소스 커넥터는 외부에서 가져온 데이터를 예약된 기준으로 인제스트하는 기능을 제공합니다. 이 자습서에서는 [!DNL Azure Blob] 사용자 인터페이스를 사용하여 소스 커넥터(이하 &quot;Blob&quot;) 또는 [!DNL Amazon] [!DNL Platform] S3(이하 &quot;S3&quot;이라 한다)을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [실시간 고객 프로필](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 Blob 또는 S3 기본 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성 자습서로 진행할 수 있습니다](../../dataflow/batch/cloud-storage.md).

### 지원되는 파일 형식

[!DNL Experience Platform] 는 외부 저장소에서 인제스트할 다음 파일 형식을 지원합니다.

- 구분 기호 구분 값(DSV): DSV 형식 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다. DSV 형식 파일 내의 필드 헤더 값은 영숫자 및 밑줄로만 구성되어야 합니다. 일반 DSV 파일에 대한 지원이 나중에 제공될 예정입니다.
- JSON(JavaScript Object Notation): JSON 형식 데이터 파일은 XDM과 호환되어야 합니다.
- Apache Pariter: 쪽모이 세공된 형식의 데이터 파일은 XDM과 호환되어야 합니다.

### 필요한 자격 증명 수집

Blob 저장소에 액세스하려면 다음 자격 증명 [!DNL Platform]에 유효한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | Blob 저장소의 데이터에 액세스하는 데 필요한 연결 문자열입니다. 물방울 연결 문자열 패턴은 다음과 같습니다. `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

시작하는 방법에 대한 자세한 내용은 [이 Azure Blob 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

마찬가지로 S3 버킷에 액세스하려면 다음 자격 증명에 대한 유효한 값을 제공해야 [!DNL Platform] 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `s3AccessKey` | S3 저장소의 액세스 키 ID입니다. |
| `s3SecretKey` | S3 저장소의 비밀 키 ID입니다. |

시작하는 방법에 대한 자세한 내용은 [이 AWS 문서를 참조하십시오](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/).

## Blob 또는 S3 계정 연결

필요한 자격 증명을 수집했으면 아래 절차에 따라 연결할 새 Blob 또는 S3 계정을 만들 수 있습니다 [!DNL Platform].

Adobe Experience Platform에 [로그인한](https://platform.adobe.com) 다음 왼쪽 탐색 **[!UICONTROL 모음에서]** 소스 *[!UICONTROL 를 선택하여]* 소스 작업 영역에액세스합니다. [ *[!UICONTROL 카탈로그]* ] 화면에는 인바운드 계정을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 계정과 연결된 기존 데이터 흐름 수가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 해당 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[ *[!UICONTROL Azure Blob 저장소]* ] 범주 아래에서 **[!UICONTROL Amazon S3를]** 선택하거나 **[!UICONTROL Amazon S3를]** 클릭하여 + 아이콘(+)을 **** [!DNL Blob] 클릭하여 새 Azure 또는 S3 커넥터를 만듭니다.

![카탈로그](../../../../images/tutorials/create/blob/catalog.png)

Azure Blob 저장소 *[!UICONTROL 에 연결]* 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **[!UICONTROL 새 계정을 선택합니다]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 사용자 [!DNL Blob] 또는 S3 자격 증명을 사용하여 연결을 제공합니다. 완료되면 **[!UICONTROL Connect를]** 선택한 다음 새 계정이 설정되기까지 약간의 시간이 소요됩니다.

![connect](../../../../images/tutorials/create/blob/new.png)

### 기존 계정

기존 계정을 연결하려면 연결할 [!DNL Blob] 또는 S3 계정을 선택한 다음 **[!UICONTROL 다음을]** 선택하여 진행하십시오.

![기존](../../../../images/tutorials/create/blob/existing.png)

## 다음 단계

이 튜토리얼을 따라 사용자 [!DNL Blob] 또는 S3 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼로 계속 진행하여 데이터 흐름을 [구성하여 클라우드 스토리지의 데이터를 Platform으로 가져올 수 있습니다](../../dataflow/batch/cloud-storage.md).