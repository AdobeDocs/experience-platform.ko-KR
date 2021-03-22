---
keywords: Experience Platform;홈;인기 항목;물방울;Azure Blob;azure blob
solution: Experience Platform
title: Azure Blob 소스 커넥터 개요
topic: 개요
description: API 또는 사용자 인터페이스를 사용하여 Azure Blob을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 7fc99214272d2ce743b3666826c66f5d65e4d2ca
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Azure Blob 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform] 및 [!DNL Azure] 같은 클라우드 공급자에 대한 기본 연결을 제공합니다. 이러한 시스템의 데이터를 [!DNL Platform]으로 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 자신의 데이터를 [!DNL Platform]에 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공 마루 또는 구분된 형태로 포맷될 수 있습니다. 프로세스의 모든 단계가 소스 워크플로우에 통합됩니다. [!DNL Platform] 일괄로 데이터를 가져올 수  [!DNL Azure Blob] 있습니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역 특정 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류 또는 비성능이 발생할 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

>[!IMPORTANT]
>
>현재 [!DNL Azure Blob] 소스 커넥터는 플랫폼에 동일한 영역 연결을 지원하지 않습니다. 즉, Azure 인스턴스가 플랫폼과 동일한 네트워크 영역을 사용하는 경우 플랫폼 소스에 대한 연결을 설정할 수 없습니다. 현재 교차 영역 연결만 지원됩니다. 자세한 내용은 Adobe 계정 관리자에게 문의하십시오.

## 파일 및 디렉토리에 대한 이름 지정 제한

클라우드 스토리지 파일 또는 디렉토리의 이름을 지정할 때 고려해야 하는 제약 조건 목록은 다음과 같습니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공된 경우 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 제대로 이스케이프해야 합니다.`! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 허용되지 않습니다.`" \ / : | < > * ?`.
- 잘못된 URL 경로 문자는 사용할 수 없습니다. NTFS 파일 이름에서 유효하지만 `\uE000` 같은 코드 포인트는 유효한 유니코드 문자가 아닙니다. 또한 제어 문자(0x00~0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1에서 유니코드 문자열을 제어하는 규칙의 경우 [RFC 2616, 2.2섹션:기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 다음 파일 이름은 허용되지 않습니다.LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, COM9, COM9, PRN, AUX, NUL, CON, CLOCK$, 도트 문자(.) 및 두 도트 문자(..)가 있습니다.

## [!DNL Azure Blob]을(를) [!DNL Platform]에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 Azure Blob을 Adobe Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

- [흐름 서비스 API를 사용하여 Azure Blob 소스 연결 만들기](../../tutorials/api/create/cloud-storage/blob.md)
- [Flow Service API를 사용하여 클라우드 스토리지 시스템 살펴보기](../../tutorials/api/explore/cloud-storage.md)
- [Flow Service API를 사용하여 클라우드 스토리지 데이터 수집](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI에서 Azure Blob 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/blob.md)
- [UI에서 클라우드 스토리지 연결에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/batch/cloud-storage.md)