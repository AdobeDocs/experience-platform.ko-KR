---
keywords: Experience Platform;홈;인기 항목;Azure Data Lake Storage Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Azure Data Lake Storage Gen2 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Azure Data Lake Storage Gen2를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Azure Data Lake Storage Gen2 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform], 및 [!DNL Azure]를 사용하면 이러한 시스템에서 데이터를 가져올 수 있습니다.

클라우드 스토리지 소스는 고유한 데이터를 [!DNL Platform] 를 다운로드하거나, 형식을 지정하거나, 업로드할 필요가 없습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. [!DNL Platform] 에서 데이터를 가져올 수 있습니다. [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) 를 배치(일괄 처리)로 전송합니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

>[!IMPORTANT]
>
>다음 [!DNL Azure Data Lake Storage Gen2] 소스가 Experience Platform에 대한 동일 영역 연결을 지원하지 않습니다. Azure 인스턴스가 Experience Platform과 동일한 네트워크 영역을 사용하는 경우 Experience Platform 원본에 대한 연결을 설정할 수 없습니다. Azure East US 2, Azure West Europe 및 Azure Australia East 지역을 설정할 때 사용하지 마십시오 [!DNL Azure Data Lake Storage Gen2] 소스. 현재는 교차 영역 연결만 지원됩니다.

## 파일 및 디렉터리에 대한 이름 지정 제한

클라우드 저장소 파일 또는 디렉토리의 이름을 지정할 때 고려해야 하는 제한 사항 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`). 제공된 경우 자동으로 제거됩니다.
- 다음 예약된 URL 문자를 제대로 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 사용할 수 없습니다. `" \ / : | < > * ?`.
- 잘못된 URL 경로 문자를 사용할 수 없습니다. 다음과 같은 코드 포인트 `\uE000`NTFS 파일 이름에서 사용할 수 있지만 올바른 유니코드 문자는 아닙니다. 또한 제어 문자(0x00~0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 관리하는 규칙은 다음을 참조하십시오 [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 다음 파일 이름은 허용되지 않습니다. LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, UL, CON, CLOCK$, dot 문자(..) 및 두 개의 점 문자(.)가 있습니다.

## Connect [!DNL Azure Data Lake Storage Gen2] to [!DNL Platform]

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Azure Data Lake Storage Gen2] to [!DNL Platform] api 또는 사용자 인터페이스 사용:

### API 사용

- [Flow Service API를 사용하여 ADLS-Gen2 기본 연결 만들기](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Flow Service API를 사용하여 클라우드 스토리지 소스의 데이터 구조 및 컨텐츠를 탐색합니다](../../tutorials/api/explore/cloud-storage.md)
- [Flow Service API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI에서 ADLS-Gen2 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
