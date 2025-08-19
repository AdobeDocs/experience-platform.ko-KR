---
title: Azure Blob Source 커넥터 개요
description: Azure Blob 계정을 Experience Platform에 연결하는 방법 알아보기
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: f659d78eebc1c5e74021f9a41a2a489389a6588e
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---

# [!DNL Azure Blob Storage] 원본

[!DNL Azure Blob Storage]은(는) [!DNL Microsoft Azure]에서 제공하는 클라우드 기반 개체 저장소 서비스입니다. 텍스트, 이미지, 비디오, 백업 및 로그와 같은 대량의 비정형 데이터를 저장하도록 설계되었습니다. [!DNL Azure Blob Storage]을(를) 사용하여 문서, 이미지, 비디오 및 오디오 파일과 같은 대량의 구조화되지 않은 데이터를 저장하고 관리할 수 있습니다. 데이터 백업 및 아카이빙, 재해 복구 지원, 분석을 위한 빅 데이터 워크로드 처리에 이상적입니다.

[!DNL Azure Blob Storage] 원본을 사용하여 계정을 연결하고 [!DNL Azure Blob Storage]에서 Adobe Experience Platform으로 데이터를 수집합니다.

## 전제 조건 {#prerequisites}

[!DNL Azure Blob Storage] 계정을 Experience Platform에 연결하기 전에 필수 구성 요소 설정을 완료하려면 다음 섹션을 참조하십시오.

### 허용 목록에 추가하다 IP 주소

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

>[!IMPORTANT]
>
>[!DNL Azure Blob] 원본은 Experience Platform에 대한 동일 지역 연결을 지원하지 않습니다. [!DNL Azure] 인스턴스가 Experience Platform과 동일한 네트워크 영역을 사용하는 경우 Experience Platform 소스에 연결할 수 없습니다. 현재는 교차 영역 연결만 지원됩니다.

### 파일 및 디렉터리에 대한 이름 지정 제약 조건

다음은 클라우드 저장소 파일 또는 디렉터리의 이름을 지정할 때 고려해야 하는 제한 사항 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공되면 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- `" \ / : | < > * ?` 문자는 사용할 수 없습니다.
- 잘못된 URL 경로 문자는 허용되지 않습니다. `\uE000` 같은 코드 포인트는 NTFS 파일 이름에서 사용할 수 있지만 올바른 유니코드 문자가 아닙니다. 또한 제어 문자(0x00 ~ 0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)을 참조하십시오.
- LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

### Experience Platform에 [!DNL Azure Blob Storage] 인증 {#authentication}

다음 인증 유형을 사용하여 [!DNL Azure Blob Storage] 계정을 Experience Platform에 연결할 수 있습니다.

- **계정 키 인증**: 저장소 계정의 액세스 키를 사용하여 인증하고 [!DNL Azure Blob Storage] 계정에 연결합니다.
- **SAS(공유 액세스 서명)**: SAS URI를 사용하여 [!DNL Azure Blob Storage] 계정의 리소스에 위임되고 제한된 시간 제한 액세스를 제공합니다.
- **서비스 사용자 기반 인증**: Azure Active Directory(AAD) 서비스 사용자(클라이언트 ID 및 암호)를 사용하여 Azure Blob 저장소 계정을 안전하게 인증합니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하여 [!DNL Azure Blob Storage] 계정을 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `connectionString` | 저장소 계정의 [!DNL Azure Blob Storage] 연결 문자열입니다. 이 문자열에는 [!DNL Azure Blob Storage] 인스턴스를 인증하고 연결하는 데 필요한 정보가 포함되어 있습니다. 예제 형식: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | 데이터 파일이 저장된 [!DNL Azure Blob Storage] 컨테이너의 이름입니다. 컨테이너는 파일 시스템의 디렉토리와 유사하게 블롭 세트를 구성합니다. |
| `folderPath` | 파일이 있는 지정된 컨테이너 내의 경로입니다. 컨테이너 내부의 선택적 하위 디렉터리 경로(가상 폴더)입니다. 비워 두면 컨테이너의 루트가 사용됩니다. |
| `connectionSpec.id` | 연결 사양 ID는 기본 및 소스 연결 생성과 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Azure Blob Storage]의 연결 사양 ID는 `4c10e202-c428-4796-9208-5f1f5732b1cf`입니다. **참고**: 이 자격 증명은 [!DNL Flow Service] API를 통해 연결할 때만 필요합니다. |

[!DNL Azure Blob Storage]에서 계정 키 인증을 사용하는 방법에 대한 자세한 내용은 공식 [Microsoft Azure 인증 안내서](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication)를 참조하세요.

>[!TAB 공유 액세스 서명]

공유 액세스 서명을 사용하여 [!DNL Azure Blob Storage] 계정을 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `SasURI` | 계정을 연결하는 데 대체 인증 유형으로 사용할 수 있는 공유 액세스 서명 URI입니다. SAS URI 패턴: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. 자세한 내용은 [!DNL Azure]공유 액세스 서명 URI[에서 이 ](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication) 문서를 참조하십시오. |
| `container` | 데이터 파일이 저장된 [!DNL Azure Blob Storage] 컨테이너의 이름입니다. 컨테이너는 파일 시스템의 디렉토리와 유사하게 블롭 세트를 구성합니다. |
| `folderPath` | 파일이 있는 지정된 컨테이너 내의 경로입니다. 컨테이너 내부의 선택적 하위 디렉터리 경로(가상 폴더)입니다. 비워 두면 컨테이너의 루트가 사용됩니다. |
| `connectionSpec.id` | 연결 사양 ID는 기본 및 소스 연결 생성과 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Azure Blob Storage]의 연결 사양 ID는 `4c10e202-c428-4796-9208-5f1f5732b1cf`입니다. **참고**: 이 자격 증명은 [!DNL Flow Service] API를 통해 연결할 때만 필요합니다. |

[!DNL Azure Blob Storage]에서 공유 액세스 서명을 사용하는 방법에 대한 자세한 내용은 공식 [Microsoft Azure 인증 안내서](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)를 참조하세요.

>[!TAB 서비스 사용자 기반 인증]

서비스 사용자 기반 인증을 사용하여 [!DNL Azure Blob Storage] 계정을 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `serviceEndpoint` | [!DNL Azure Blob Storage] 계정의 끝점 URL입니다. 일반적으로 형식은 `https://{ACCOUNT_NAME}.blob.core.windows.net`입니다. |
| `accountKind` | [!DNL Azure Blob Storage] 계정의 형식입니다. 일반적인 값은 `StorageV2`, `BlobStorage` 또는 `Storage`입니다. |
| `servicePrincipalId` | 인증에 사용되는 Azure Active Directory(AAD) 서비스 사용자의 클라이언트/응용 프로그램 ID입니다. |
| `servicePrincipalKey` | Azure 서비스 주체와 연결된 클라이언트 암호 또는 암호입니다. |
| `tenant` | 서비스 주체가 등록된 Azure Active Directory(AAD) 테넌트 ID입니다. |
| `container` | 데이터 파일이 저장된 Azure Blob 저장소 컨테이너의 이름입니다. |
| `folderPath` | 파일이 있는 지정된 컨테이너 내의 경로입니다. 컨테이너 내부의 선택적 하위 디렉터리 경로(가상 폴더)입니다. 비워 두면 컨테이너의 루트가 사용됩니다. |
| `connectionSpec.id` | 연결 사양 ID는 기본 및 소스 연결 생성과 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. Azure Blob 저장소의 연결 사양 ID는 `4c10e202-c428-4796-9208-5f1f5732b1cf`입니다. **참고**: 이 자격 증명은 [!DNL Flow Service] API를 통해 연결할 때만 필요합니다. |

[!DNL Azure Blob Storage]과(와) 함께 서비스 사용자 기반 인증을 사용하는 방법에 대한 자세한 내용은 공식 [Microsoft Azure 인증 안내서](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication)를 참조하세요.

>[!ENDTABS]

## [!DNL Azure Blob Storage]을(를) [!DNL Experience Platform]에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 Azure Blob를 Adobe Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

- [Experience Platform에  [!DNL Azure Blob Storage] 연결](../../tutorials/api/create/cloud-storage/blob.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스의 데이터 구조 및 콘텐츠 탐색](../../tutorials/api/explore/cloud-storage.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [Experience Platform에  [!DNL Azure Blob Storage] 연결](../../tutorials/ui/create/cloud-storage/blob.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
