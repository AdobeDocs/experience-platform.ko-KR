---
keywords: Experience Platform;홈;인기 항목;FTP;ftp;
solution: Experience Platform
title: FTP 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 FTP 서버를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: a6186fad-8a7b-4103-80c7-a522ff69fe9e
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# (베타) FTP 커넥터

>[!NOTE]
>
>FTP 커넥터는 Beta 버전입니다. 다음을 참조하십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블이 지정된 커넥터 사용에 대한 자세한 정보를 제공합니다.

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform], 및 [!DNL Azure]를 사용하면 이러한 시스템에서 데이터를 가져올 수 있습니다.

클라우드 스토리지 소스는 고유한 데이터를으로 가져올 수 있습니다 [!DNL Platform] 를 다운로드하거나, 형식을 지정하거나, 업로드할 필요가 없습니다. 수집된 데이터는 XDM JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. [!DNL Platform] 에서는 일괄 처리를 통해 FTP 또는 SFTP 서버에서 데이터를 가져올 수 있습니다.

>[!IMPORTANT]
>
>FTP 소스 커넥터를 사용하여 데이터 흐름을 만들 때 FTP 서버 내에서 발생하는 증분 업데이트의 지속적인 문제로 인해 일회성 수집 일정에 대해 설정하는 것이 좋습니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

## 파일 및 디렉터리에 대한 이름 지정 제약 조건

다음은 클라우드 저장소 파일 또는 디렉터리의 이름을 지정할 때 고려해야 하는 제한 사항 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`). 제공되면 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 허용되지 않습니다. `" \ / : | < > * ?`.
- 잘못된 URL 경로 문자는 허용되지 않습니다. 다음과 같은 코드 포인트 `\uE000`는 NTFS 파일 이름에서 유효하지만 은 유효한 유니코드 문자가 아닙니다. 또한 제어 문자(0x00 ~ 0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 다음을 참조하십시오. [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

## FTP 연결 [!DNL Platform]

아래 설명서에서는 FTP 서버를 로 연결하는 방법에 대한 정보를 제공합니다 [!DNL Platform] api 또는 사용자 인터페이스 사용:

### API 사용

- [흐름 서비스 API를 사용하여 FTP 기본 연결 만들기](../../tutorials/api/create/cloud-storage/ftp.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스의 데이터 구조 및 콘텐츠 탐색](../../tutorials/api/explore/cloud-storage.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI에서 FTP 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/ftp.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
