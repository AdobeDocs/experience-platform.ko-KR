---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 데이터 랜딩 영역 Source
description: 데이터 랜딩 영역을 Adobe Experience Platform에 연결하는 방법 알아보기
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: cb37eda87b8fcc0d0284db7a0bab8d48eab5aae6
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>이 페이지는 Experience Platform의 [!DNL Data Landing Zone] *source* 커넥터에 한정됩니다. [!DNL Data Landing Zone] *대상* 커넥터에 연결하는 방법에 대한 자세한 내용은 [[!DNL Data Landing Zone] 대상 설명서 페이지](/help/destinations/catalog/cloud-storage/data-landing-zone.md)를 참조하세요.

[!DNL Data Landing Zone]은(는) Adobe Experience Platform에서 프로비저닝한 [!DNL Azure Blob] 저장소 인터페이스로서, 파일을 플랫폼으로 가져올 수 있는 안전한 클라우드 기반 파일 저장소 기능에 액세스할 수 있도록 허용합니다. 샌드박스당 하나의 [!DNL Data Landing Zone] 컨테이너에 액세스할 수 있으며 모든 컨테이너의 총 데이터 볼륨은 Platform 제품 및 서비스 라이선스와 함께 제공되는 총 데이터로 제한됩니다. [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] 및 [!DNL Adobe Real-Time Customer Data Platform]과(와) 같은 플랫폼과 해당 애플리케이션의 모든 고객에게 샌드박스당 하나의 [!DNL Data Landing Zone] 컨테이너가 제공됩니다. [!DNL Azure Storage Explorer] 또는 명령줄 인터페이스를 통해 컨테이너에 파일을 읽고 쓸 수 있습니다.

[!DNL Data Landing Zone]은(는) SAS 기반 인증을 지원하며, 전송 중이거나 사용하지 않는 표준 [!DNL Azure Blob] 저장소 보안 메커니즘을 통해 데이터를 보호합니다. SAS 기반 인증을 사용하면 공용 인터넷 연결을 통해 [!DNL Data Landing Zone] 컨테이너에 안전하게 액세스할 수 있습니다. [!DNL Data Landing Zone] 컨테이너에 액세스하는 데 필요한 네트워크 변경 내용이 없습니다. 따라서 네트워크에 대한 허용 목록 또는 교차 지역 설정을 구성할 필요가 없습니다. Platform은 [!DNL Data Landing Zone] 컨테이너에 업로드된 모든 파일에 엄격한 7일 만료 시간을 적용합니다. 모든 파일은 7일 후에 삭제됩니다.

## 파일 및 디렉터리에 대한 이름 지정 제약 조건

다음은 클라우드 저장소 파일 또는 디렉터리의 이름을 지정할 때 고려해야 하는 제약 조건 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공되면 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- `" \ / : | < > * ?` 문자는 사용할 수 없습니다.
- 잘못된 URL 경로 문자는 허용되지 않습니다. `\uE000` 같은 코드 포인트는 NTFS 파일 이름에서 사용할 수 있지만 올바른 유니코드 문자가 아닙니다. 또한 컨트롤 문자(예: `0x00` ~ `0x1F`, `\u0081` 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)을 참조하십시오.
- LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

## 데이터 랜딩 영역의 콘텐츠 관리{#manage-the-contents-of-your-data-landing-zone}

[[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/)을(를) 사용하여 [!DNL Data Landing Zone] 컨테이너의 콘텐츠를 관리할 수 있습니다.

[!DNL Azure Storage Explorer] UI의 왼쪽 탐색에서 연결 아이콘을 선택합니다. 연결할 수 있는 옵션을 제공하는 **리소스 선택** 창이 나타납니다. [!DNL Data Landing Zone]에 연결하려면 **[!DNL Blob container]**&#x200B;을(를) 선택하십시오.

![리소스 선택](../../images/tutorials/create/dlz/select-resource.png)

다음으로 연결 방법으로 **SAS(공유 액세스 서명 URL)**&#x200B;을(를) 선택한 후 **다음**&#x200B;을(를) 선택합니다.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

연결 방법을 선택한 후 [!DNL Data Landing Zone] 컨테이너에 해당하는 **표시 이름** 및 **[!DNL Blob]컨테이너 SAS URL**&#x200B;을(를) 제공해야 합니다.

>[!TIP]
>
>Platform UI의 소스 카탈로그에서 [!DNL Data Landing Zone] 자격 증명을 검색할 수 있습니다.

[!DNL Data Landing Zone] SAS URL을 입력한 다음 **다음**&#x200B;을(를) 선택하십시오.

![연결 정보 입력](../../images/tutorials/create/dlz/enter-connection-info.png)

[!DNL Blob] 끝점 및 사용 권한에 대한 정보를 포함하여 설정에 대한 개요를 제공하는 **요약** 창이 나타납니다. 준비가 되면 **연결**&#x200B;을 선택합니다.

![요약](../../images/tutorials/create/dlz/summary.png)

연결에 성공하면 [!DNL Azure Storage Explorer] UI가 [!DNL Data Landing Zone] 컨테이너로 업데이트됩니다.

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

[!DNL Data Landing Zone] 컨테이너가 [!DNL Azure Storage Explorer]에 연결되어 있으므로 이제 [!DNL Data Landing Zone] 컨테이너에 파일을 업로드할 수 있습니다. 업로드하려면 **업로드**&#x200B;를 선택한 다음 **파일 업로드**&#x200B;를 선택하십시오.

![업로드](../../images/tutorials/create/dlz/upload.png)

업로드할 파일을 선택했으면 업로드할 [!DNL Blob] 유형과 원하는 대상 디렉터리를 확인해야 합니다. 완료되면 **업로드**&#x200B;를 선택합니다.

| [!DNL Blob]개 유형 | 설명 |
| --- | --- |
| [!DNL Blob] 차단 | 블록 [!DNL Blobs]은(는) 대량의 데이터를 효율적인 방식으로 업로드하도록 최적화되었습니다. [!DNL Blobs] 블록은 [!DNL Data Landing Zone]의 기본 옵션입니다. |
| [!DNL Blob] 추가 | [!DNL Blobs] 추가는 파일 끝에 데이터를 추가하도록 최적화되었습니다. |

![업로드 파일](../../images/tutorials/create/dlz/upload-files.png)

## 명령줄 인터페이스를 사용하여 [!DNL Data Landing Zone]에 파일 업로드

장치의 명령줄 인터페이스를 사용하여 [!DNL Data Landing Zone]에 대한 업로드 파일에 액세스할 수도 있습니다.

### Bash를 사용하여 파일 업로드

다음 예제에서는 Bash 및 cURL을 사용하여 [!DNL Azure Blob Storage] REST API를 사용하여 [!DNL Data Landing Zone]에 파일을 업로드합니다.

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### Python을 사용하여 파일 업로드

다음 예제에서는 [!DNL Microsoft's] Python v12 SDK를 사용하여 파일을 [!DNL Data Landing Zone]에 업로드합니다.

>[!TIP]
>
>아래 예제에서는 전체 SAS URI를 사용하여 [!DNL Azure Blob] 컨테이너에 연결하지만 다른 방법 및 작업을 사용하여 인증할 수 있습니다. 자세한 내용은 Python v12 SDK에 대한 이 [[!DNL Microsoft] 문서](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python)를 참조하십시오.

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### [!DNL AzCopy]을(를) 사용하여 파일 업로드

다음 예제에서는 [!DNL Microsoft's] [!DNL AzCopy] 유틸리티를 사용하여 파일을 [!DNL Data Landing Zone]에 업로드합니다.

>[!TIP]
>
>아래 예제에서는 `copy` 명령을 사용하는 동안 다른 명령 및 옵션을 사용하여 [!DNL AzCopy]을(를) 사용하여 파일을 [!DNL Data Landing Zone]에 업로드할 수 있습니다. 자세한 내용은 이 [[!DNL Microsoft AzCopy] 문서](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json)를 참조하세요.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## [!DNL Data Landing Zone]을(를) [!DNL Platform]에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Data Landing Zone] 컨테이너에서 Adobe Experience Platform으로 데이터를 가져오는 방법에 대한 정보를 제공합니다.

### API 사용

- [흐름 서비스 API를 사용하여  [!DNL Data Landing Zone] 소스 연결 만들기](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI를 사용하여  [!DNL Data Landing Zone] 을(를) 플랫폼에 연결](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>[!DNL Data Landing Zone]을(를) 사용하여 Experience Platform에 연결할 때 개인 링크는 현재 지원되지 않습니다. 액세스가 지원되는 메서드는 [여기](#manage-the-contents-of-your-data-landing-zone)에 나열된 메서드뿐입니다.

