---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 데이터 랜딩 영역 소스
topic-legacy: overview
description: 데이터 랜딩 영역을 Adobe Experience Platform에 연결하는 방법 알아보기
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] 는 Adobe Experience Platform에서 제공하는  [!DNL Azure Blob] 스토리지 인터페이스로, Platform으로 파일을 가져올 수 있도록 안전한 클라우드 기반 파일 스토리지 기능에 액세스할 수 있도록 합니다. 샌드박스당 하나의 [!DNL Data Landing Zone] 컨테이너에 액세스할 수 있으며 모든 컨테이너의 총 데이터 볼륨은 플랫폼 프로덕션 및 서비스 라이센스와 함께 제공된 총 데이터로 제한됩니다. Platform 및 해당 애플리케이션 서비스(예: [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] 및 [!DNL Real-time Customer Data Platform])의 모든 고객은 샌드박스당 하나의 [!DNL Data Landing Zone] 컨테이너를 사용할 수 있습니다. [!DNL Azure Storage Explorer] 또는 명령줄 인터페이스를 통해 컨테이너에 파일을 읽고 쓸 수 있습니다.

[!DNL Data Landing Zone] 은 SAS 기반 인증을 지원하며, 데이터는  [!DNL Azure Blob] 저장 및 전송 중에 표준 스토리지 보안 메커니즘으로 보호됩니다. SAS 기반 인증을 사용하면 공용 인터넷 연결을 통해 [!DNL Data Landing Zone] 컨테이너에 안전하게 액세스할 수 있습니다. [!DNL Data Landing Zone] 컨테이너에 액세스하는 데 필요한 네트워크 변경 사항이 없습니다. 즉, 네트워크에 대한 허용 목록 또는 영역 간 설정을 구성할 필요가 없습니다. Platform에서는 [!DNL Data Landing Zone] 컨테이너에 업로드된 모든 파일에 대해 엄격한 7일 TTL(Time-to-Live)을 적용합니다. 7일 후 모든 파일이 삭제됩니다.

## 파일 및 디렉터리에 대한 이름 지정 제한

다음은 클라우드 저장소 파일 또는 디렉토리의 이름을 지정할 때 고려해야 하는 제한 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공된 경우 자동으로 제거됩니다.
- 다음 예약된 URL 문자를 제대로 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 사용할 수 없습니다. `" \ / : | < > * ?`
- 잘못된 URL 경로 문자를 사용할 수 없습니다. `\uE000` 같은 코드 포인트는 NTFS 파일 이름에서 유효하지만 올바른 유니코드 문자는 아닙니다. 또한 제어 문자(예: `0x00` ~ `0x1F`, `\u0081` 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙은 [RFC 2616, 섹션 2.2를 참조하십시오. 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 다음 파일 이름은 허용되지 않습니다. LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, UL, CON, CLOCK$, dot 문자(..) 및 두 개의 점 문자(.)가 있습니다.

## [!DNL Data Landing Zone]을 [!DNL Platform]에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Data Landing Zone] 컨테이너에서 Adobe Experience Platform으로 데이터를 가져오는 방법에 대한 정보를 제공합니다.

### API 사용

- [Flow Service API를 사용하여 [!DNL Data Landing Zone] 소스 연결을 만듭니다](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Flow Service API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI를 사용하여 [!DNL Data Landing Zone] 플랫폼에 연결](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
