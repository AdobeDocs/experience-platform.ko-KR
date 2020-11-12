---
keywords: Experience Platform;home;popular topics;Blob;blob;Azure Blob;azure blob
solution: Experience Platform
title: Azure Blob 커넥터
topic: overview
description: 아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 Azure Blob를 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: e0a0b7fc28b8cc85c5140d3840e06e5c7078c307
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Azure Blob 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform]및 AWS와 같은 클라우드 제공업체를 위한 기본 연결을 [!DNL Azure]제공합니다. 이러한 시스템에서 얻은 데이터를 [!DNL Platform]

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 [!DNL Platform] 없이 고유한 데이터를 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공식 또는 구분 기호로 형식을 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. [!DNL Platform] 배치에서 데이터를 가져올 수 [!DNL Azure Blob] 있습니다.

## IP 주소 허용 목록

소스 커넥터를 사용하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역 특정 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 파일 및 디렉토리 이름 지정 제한

클라우드 스토리지 파일 또는 디렉토리의 이름을 지정할 때 고려해야 하는 제한 사항의 목록은 다음과 같습니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(슬래시)로 끝날 수`/`없습니다. 제공된 경우 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 적절하게 이스케이프되어야 합니다. `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- 다음 문자는 허용되지 않습니다. `" \ / : | < > * ?`.
- 잘못된 URL 경로 문자는 사용할 수 없습니다. NTFS 파일 이름에 `\uE000`유효한 코드 포인트는 올바른 유니코드 문자가 아닙니다. 또한 컨트롤 문자(0x00~0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1에서 유니코드 문자열을 제어하는 규칙은 [RFC 2616, 섹션 2.2를 참조하십시오.기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 다음 파일 이름은 허용되지 않습니다.LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM8, COM9, COM9, prn, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 두 점 문자(..)가 있습니다.

## 연결 [!DNL Azure Blob] 을 [!DNL Platform]

아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 Azure Blob를 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

- [Flow Service API를 사용하여 Azure Blob 커넥터 만들기](../../tutorials/api/create/cloud-storage/blob.md)
- [Flow Service API를 사용하여 클라우드 스토리지 시스템 살펴보기](../../tutorials/api/explore/cloud-storage.md)
- [Flow Service API를 사용하여 클라우드 스토리지 데이터 수집](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI에서 Azure Blob 소스 커넥터 만들기](../../tutorials/ui/create/cloud-storage/blob.md)
- [UI에서 클라우드 스토리지 커넥터에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/batch/cloud-storage.md)