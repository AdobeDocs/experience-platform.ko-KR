---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 데이터 랜딩 영역 소스
topic-legacy: overview
description: 데이터 랜딩 영역을 Adobe Experience Platform에 연결하는 방법 알아보기
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecc9bc603bfd7b56f5f232b0d6d91eb65a901510
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] is [!DNL Azure Blob] Adobe Experience Platform에서 프로비저닝한 스토리지 인터페이스로, Platform으로 파일을 가져올 수 있는 안전한 클라우드 기반 파일 스토리지 설비에 액세스할 수 있도록 합니다. 액세스 권한이 있습니다. [!DNL Data Landing Zone] 샌드박스당 컨테이너 및 모든 컨테이너의 총 데이터 볼륨은 Platform Products 및 Services 라이선스와 함께 제공된 총 데이터로 제한됩니다. Platform 및 Launch의 모든 애플리케이션 서비스(예: [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], 및 [!DNL Real-time Customer Data Platform] 하나의 [!DNL Data Landing Zone] 샌드박스당 컨테이너. 을 통해 컨테이너에 파일을 읽고 쓸 수 있습니다 [!DNL Azure Storage Explorer] 또는 명령줄 인터페이스를 사용할 수 있습니다.

[!DNL Data Landing Zone] 는 SAS 기반 인증을 지원하고 데이터는 표준으로 보호됩니다 [!DNL Azure Blob] 저장 보안 메커니즘이 휴지 및 전송 중입니다. SAS 기반 인증을 통해 [!DNL Data Landing Zone] 공용 인터넷 연결을 통한 컨테이너 사용자의 [!DNL Data Landing Zone] 컨테이너. 즉, 네트워크에 대한 허용 목록 또는 지역 간 설정을 구성할 필요가 없습니다. Platform에서는 [!DNL Data Landing Zone] 컨테이너. 7일 후 모든 파일이 삭제됩니다.

## 파일 및 디렉터리에 대한 이름 지정 제한

다음은 클라우드 저장소 파일 또는 디렉토리의 이름을 지정할 때 고려해야 하는 제한 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`). 제공된 경우 자동으로 제거됩니다.
- 다음 예약된 URL 문자를 제대로 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 사용할 수 없습니다. `" \ / : | < > * ?`.
- 잘못된 URL 경로 문자를 사용할 수 없습니다. 다음과 같은 코드 포인트 `\uE000`NTFS 파일 이름에서 사용할 수 있지만 올바른 유니코드 문자는 아닙니다. 또한 컨트롤 문자(예: `0x00` to `0x1F`, `\u0081`, 등)도 허용되지 않습니다. HTTP/1.1의 유니코드 문자열을 관리하는 규칙은 다음을 참조하십시오 [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 다음 파일 이름은 허용되지 않습니다. LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, UL, CON, CLOCK$, dot 문자(..) 및 두 개의 점 문자(.)가 있습니다.

## Connect [!DNL Data Landing Zone] to [!DNL Platform]

아래 설명서에서는 [!DNL Data Landing Zone] API 또는 사용자 인터페이스를 사용하여 Adobe Experience Platform에 컨테이너를 전송하는 것이 좋습니다.

### API 사용

- [만들기 [!DNL Data Landing Zone] 흐름 서비스 API를 사용한 소스 연결](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Flow Service API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [Connect [!DNL Data Landing Zone] UI를 사용하여 플랫폼 구현](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
