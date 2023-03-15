---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 데이터 랜딩 영역 소스
description: 데이터 랜딩 영역을 Adobe Experience Platform에 연결하는 방법 알아보기
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: d57060ddeed64d3863f71ac1ea34ccc5c97265ea
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>이 페이지는 다음에 한정됩니다. [!DNL Data Landing Zone] *소스* Experience Platform의 커넥터입니다. 에 연결하는 방법에 대한 자세한 내용은 [!DNL Data Landing Zone] *대상* 커넥터를 참조하려면 [[!DNL Data Landing Zone] 대상 설명서 페이지](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] 은(는) [!DNL Azure Blob] Adobe Experience Platform에서 프로비저닝한 스토리지 인터페이스로, 파일을 플랫폼으로 가져올 수 있는 안전한 클라우드 기반 파일 스토리지 시설에 액세스할 수 있습니다. 액세스 권한이 있습니다. [!DNL Data Landing Zone] 샌드박스당 컨테이너 및 모든 컨테이너의 총 데이터 볼륨은 Platform 제품 및 서비스 라이선스와 함께 제공되는 총 데이터로 제한됩니다. Platform 및 해당 애플리케이션 서비스의 모든 고객: [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], 및 [!DNL Adobe Real-Time Customer Data Platform] 이(가) 하나로 프로비저닝됨 [!DNL Data Landing Zone] 샌드박스당 컨테이너. 다음을 통해 파일을 읽고 컨테이너에 쓸 수 있습니다. [!DNL Azure Storage Explorer] 또는 명령줄 인터페이스입니다.

[!DNL Data Landing Zone] 는 SAS 기반 인증을 지원하며 데이터는 표준으로 보호됩니다 [!DNL Azure Blob] 중단 및 전송 중인 스토리지 보안 메커니즘. SAS 기반 인증을 통해 [!DNL Data Landing Zone] 공용 인터넷 연결을 통한 컨테이너. 에 액세스하는 데 필요한 네트워크 변경 사항이 없습니다. [!DNL Data Landing Zone] 즉, 네트워크에 대한 허용 목록 또는 교차 영역 설정을 구성할 필요가 없습니다. Platform은에 업로드된 모든 파일에 엄격한 7일 만료 시간을 적용합니다. [!DNL Data Landing Zone] 컨테이너. 모든 파일은 7일 후에 삭제됩니다.

## 파일 및 디렉터리에 대한 이름 지정 제약 조건

다음은 클라우드 저장소 파일 또는 디렉터리의 이름을 지정할 때 고려해야 하는 제약 조건 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`). 제공되면 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 허용되지 않습니다. `" \ / : | < > * ?`.
- 잘못된 URL 경로 문자는 허용되지 않습니다. 다음과 같은 코드 포인트 `\uE000`는 NTFS 파일 이름에서 유효하지만 은 유효한 유니코드 문자가 아닙니다. 또한 제어 문자(예: `0x00` 끝 `0x1F`, `\u0081`등)도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 다음을 참조하십시오. [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

## 의 콘텐츠 관리 [!DNL Data Landing Zone]

다음을 사용할 수 있습니다. [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 의 콘텐츠를 관리하려면 [!DNL Data Landing Zone] 컨테이너.

다음에서 [!DNL Azure Storage Explorer] UI에서, 왼쪽 탐색에서 연결 아이콘을 선택합니다. 다음 **리소스 선택** 연결 옵션을 제공하는 창이 나타납니다. 선택 **[!DNL Blob container]** 에 연결하려면 [!DNL Data Landing Zone].

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

그런 다음 을 선택합니다. **SAS(공유 액세스 서명 URL)** 을 연결 방법으로 선택한 다음 을 선택합니다. **다음**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

연결 방법을 선택한 후 다음을 제공해야 합니다. **표시 이름** 및 **[!DNL Blob]컨테이너 SAS URL** 에 해당하는 [!DNL Data Landing Zone] 컨테이너.

>[!TIP]
>
>다음을 검색할 수 있습니다. [!DNL Data Landing Zone] platform UI의 소스 카탈로그의 자격 증명입니다.

다음을 제공하십시오. [!DNL Data Landing Zone] SAS URL을 선택한 다음 **다음**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

다음 **요약** 창에 설정에 대한 정보를 포함하여 설정의 개요를 제공합니다. [!DNL Blob] 엔드포인트 및 권한. 준비가 되면 다음을 선택합니다. **연결**.

![요약](../../images/tutorials/create/dlz/summary.png)

연결에 성공하면 다음 항목이 업데이트됩니다. [!DNL Azure Storage Explorer] 을 통한 UI [!DNL Data Landing Zone] 컨테이너.

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

(으)로 [!DNL Data Landing Zone] 컨테이너 연결됨 [!DNL Azure Storage Explorer]이제 파일에 대한 업로드를 시작할 수 있습니다. [!DNL Data Landing Zone] 컨테이너. 업로드하려면 다음을 선택합니다 **업로드** 다음을 선택합니다. **파일 업로드**.

![업로드](../../images/tutorials/create/dlz/upload.png)

업로드할 파일을 선택한 다음 를 식별해야 합니다. [!DNL Blob] 업로드하려는 이름을 입력하고 원하는 대상 디렉토리를 지정합니다. 완료되면 다음을 선택합니다. **업로드**.

| [!DNL Blob] 유형 | 설명 |
| --- | --- |
| 차단 [!DNL Blob] | 차단 [!DNL Blobs] 대량의 데이터를 효율적으로 업로드하도록 최적화되었습니다. 차단 [!DNL Blobs] 의 기본 옵션입니다. [!DNL Data Landing Zone]. |
| 추가 [!DNL Blob] | 추가 [!DNL Blobs] 는 파일 끝에 데이터를 추가하도록 최적화되었습니다. |

![업로드 파일](../../images/tutorials/create/dlz/upload-files.png)

## 에 파일 업로드 [!DNL Data Landing Zone] 명령줄 인터페이스 사용

또한 장치의 명령줄 인터페이스를 사용하여 업로드 파일에 액세스할 수 있습니다. [!DNL Data Landing Zone].

### Bash를 사용하여 파일 업로드

다음 예제에서는 Bash 및 cURL을 사용하여 파일을 [!DNL Data Landing Zone] (으)로 [!DNL Azure Blob Storage] REST API:

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

다음 예제에서는 를 사용합니다 [!DNL Microsoft's] 파일을 업로드할 Python v12 SDK [!DNL Data Landing Zone]:

>[!TIP]
>
>그러나 아래 예에서는 전체 SAS URI를 사용하여 [!DNL Azure Blob] 컨테이너에서 다른 방법 및 작업을 사용하여 인증할 수 있습니다. 이 항목 보기 [[!DNL Microsoft] python v12 SDK에 대한 문서](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) 추가 정보.

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

### 다음을 사용하여 파일 업로드 [!DNL AzCopy]

다음 예제에서는 를 사용합니다 [!DNL Microsoft's] [!DNL AzCopy] 파일을 업로드하는 유틸리티 [!DNL Data Landing Zone]:

>[!TIP]
>
>아래 예제는 `copy` 명령, 다른 명령 및 옵션을 사용하여 파일을 [!DNL Data Landing Zone], 사용 [!DNL AzCopy]. 이 항목 보기 [[!DNL Microsoft AzCopy] 문서](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) 추가 정보.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## 연결 [!DNL Data Landing Zone] 끝 [!DNL Platform]

아래 설명서에서는 에서 데이터를 가져오는 방법에 대한 정보를 제공합니다. [!DNL Data Landing Zone] api 또는 사용자 인터페이스를 사용하여 Adobe Experience Platform에 컨테이너

### API 사용

- [만들기 [!DNL Data Landing Zone] 흐름 서비스 API를 사용한 소스 연결](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [연결 [!DNL Data Landing Zone] UI를 사용하여 플랫폼에 연결](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
