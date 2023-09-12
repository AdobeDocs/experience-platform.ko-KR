---
title: Azure Data Lake Storage Gen2 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Azure Data Lake Storage Gen2를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: f879f2a627e55db96a89796b9f3308744bf93f67
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Azure Data Lake Storage Gen2 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform], 및 [!DNL Azure]를 사용하면 이러한 시스템에서 데이터를 가져올 수 있습니다.

클라우드 스토리지 소스는 Experience Platform, 포맷 또는 업로드 없이도 자신의 데이터를 다운로드로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. Experience Platform을 사용하면 다음 위치에서 데이터를 가져올 수 있습니다. [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) 일괄 처리를 통해

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

>[!IMPORTANT]
>
>다음 [!DNL Azure Data Lake Storage Gen2] 소스는 Experience Platform에 대한 동일 지역 연결을 지원하지 않습니다. Azure 인스턴스가 Experience Platform과 동일한 네트워크 영역을 사용하는 경우 Experience Platform 소스에 연결할 수 없습니다. 을(를) 설정할 때 Azure East US 2, Azure West Europe 및 Azure Australia East 지역을 사용하지 마십시오. [!DNL Azure Data Lake Storage Gen2] 소스. 현재는 교차 영역 연결만 지원됩니다.

## 파일 및 디렉터리에 대한 이름 지정 제약 조건

다음은 클라우드 저장소 파일 또는 디렉터리의 이름을 지정할 때 고려해야 하는 제한 사항 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`). 제공되면 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 허용되지 않습니다. `" \ / : | < > * ?`.
- 잘못된 URL 경로 문자는 허용되지 않습니다. 다음과 같은 코드 포인트 `\uE000`는 NTFS 파일 이름에서 유효하지만 은 유효한 유니코드 문자가 아닙니다. 또한 제어 문자(0x00 ~ 0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 다음을 참조하십시오. [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

## 연결 [!DNL Azure Data Lake Storage Gen2] 대상 Experience Platform

>[!NOTE]
>
>을(를) 만드는 데 사용되는 서비스 사용자 [!DNL Azure Data Lake Storage Gen2] 계정에는 최소한 다음 항목이 있어야 합니다. **저장소 Blob 데이터 Reader** 액세스 제어(IAM)에서 할당된 역할

아래 설명서는 연결 방법에 대한 정보를 제공합니다 [!DNL Azure Data Lake Storage Gen2] API 또는 Experience Platform 인터페이스를 사용하여 검색하려면 다음 작업을 수행하십시오.

### API 사용

- [만들기 [!DNL Azure Data Lake Storage Gen2] 흐름 서비스 API를 사용한 기본 연결](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스의 데이터 구조 및 콘텐츠 탐색](../../tutorials/api/explore/cloud-storage.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [만들기 [!DNL Azure Data Lake Storage Gen2] UI의 소스 연결](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
