---
keywords: Experience Platform;홈;인기 항목;FTP;ftp;
solution: Experience Platform
title: FTP 소스 커넥터 개요
topic-legacy: overview
description: API 또는 사용자 인터페이스를 사용하여 FTP 서버를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: a6186fad-8a7b-4103-80c7-a522ff69fe9e
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# (베타) FTP 커넥터

>[!NOTE]
>
>FTP 커넥터는 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions) 를 참조하십시오.

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform] 및 [!DNL Azure]과 같은 클라우드 제공업체를 위한 네이티브 연결을 제공하므로 이러한 시스템에서 데이터를 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 고유한 데이터를 [!DNL Platform]로 가져올 수 있습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. [!DNL Platform] 을(를) 사용하면 배치를 통해 FTP 또는 SFTP 서버에서 데이터를 가져올 수 있습니다.

>[!IMPORTANT]
>
>FTP 소스 커넥터를 사용하여 데이터 플로우를 만들 때 FTP 서버 내에서 발생하는 증분 업데이트에 대한 느린 문제로 인해 1회 수집 일정을 설정하는 것이 좋습니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 파일 및 디렉터리에 대한 이름 지정 제한

클라우드 저장소 파일 또는 디렉토리의 이름을 지정할 때 고려해야 하는 제한 사항 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공된 경우 자동으로 제거됩니다.
- 다음 예약된 URL 문자를 제대로 이스케이프해야 합니다.`! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 사용할 수 없습니다.`" \ / : | < > * ?`
- 잘못된 URL 경로 문자를 사용할 수 없습니다. `\uE000` 같은 코드 포인트는 NTFS 파일 이름에서 유효하지만 올바른 유니코드 문자는 아닙니다. 또한 제어 문자(0x00~0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙은 [RFC 2616, 섹션 2.2를 참조하십시오.기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 다음 파일 이름은 허용되지 않습니다.LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, UL, CON, CLOCK$, dot 문자(..) 및 두 개의 점 문자(.)가 있습니다.

## FTP를 [!DNL Platform]에 연결

아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 FTP 서버를 [!DNL Platform]에 연결하는 방법에 대해 설명합니다.

### API 사용

- [Flow Service API를 사용하여 FTP 기본 연결 만들기](../../tutorials/api/create/cloud-storage/ftp.md)
- [Flow Service API를 사용하여 클라우드 스토리지 소스의 데이터 구조 및 컨텐츠를 탐색합니다](../../tutorials/api/explore/cloud-storage.md)
- [Flow Service API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI에서 FTP 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/ftp.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
