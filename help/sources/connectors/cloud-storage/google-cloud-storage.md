---
keywords: Experience Platform;홈;인기 항목;Google 클라우드 스토리지;google 클라우드 스토리지
solution: Experience Platform
title: Google 클라우드 스토리지 커넥터
topic: overview
description: 아래 설명서는 API 또는 사용자 인터페이스를 사용하여 Google 클라우드 스토리지를 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---


# Google 클라우드 스토리지 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform] 및 [!DNL Azure] 같은 클라우드 제공업체를 위한 기본 연결을 제공하므로 이러한 시스템에서 데이터를 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 자신의 데이터를 [!DNL Platform]에 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공 마루 또는 구분된 형태로 포맷될 수 있습니다. 프로세스의 모든 단계가 소스 워크플로우에 통합됩니다. [!DNL Platform] 일괄로 데이터를 가져올 수  [!DNL Google Cloud Storage] 있습니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역 특정 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류 또는 비성능이 발생할 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## [!DNL Google Cloud Storage] 계정을 연결하기 위한 필수 설정

[!DNL Platform]에 연결하려면 먼저 [!DNL Google Cloud Storage] 계정에 대해 상호 운용성을 활성화해야 합니다. 상호 운용성 설정에 액세스하려면 [!DNL Google Cloud Platform]을 열고 탐색 패널의 **[!UICONTROL 스토리지]** 옵션에서 **[!UICONTROL 설정]**&#x200B;을 선택합니다.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

**[!UICONTROL 설정]** 페이지가 나타납니다. 여기에서 [!DNL Google] 프로젝트 ID에 대한 정보와 [!DNL Google Cloud Storage] 계정에 대한 세부 정보를 볼 수 있습니다. 상호 운용성 설정에 액세스하려면 상단 헤더에서 **[!UICONTROL 상호 운용성]**&#x200B;을 선택합니다.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

**[!UICONTROL 상호 운용성]** 페이지에는 인증, 액세스 키 및 사용자 계정과 연결된 기본 프로젝트에 대한 정보가 들어 있습니다. 상호 이용 가능한 액세스를 위한 기본 프로젝트를 아직 설정하지 않은 경우 상호 이용 가능한 액세스&#x200B;]**섹션에 대해**[!UICONTROL &#x200B;기본 프로젝트 내에서 설정할 수 있습니다. 기본 프로젝트가 이미 설정된 경우 이 섹션에는 프로젝트가 기본값으로 설정되었다는 확인이 표시됩니다.

사용자 계정에 대한 새 액세스 키 ID 및 비밀 액세스 키를 생성하려면 **[!UICONTROL 키 만들기]**&#x200B;를 선택합니다.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

새로 생성된 액세스 키 ID 및 비밀 액세스 키를 사용하여 [!DNL Google Cloud Storage] 계정을 [!DNL Platform]에 연결할 수 있습니다.

## 파일 및 디렉토리에 대한 이름 지정 제한

클라우드 스토리지 파일 또는 디렉토리의 이름을 지정할 때 고려해야 하는 제약 조건 목록은 다음과 같습니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공된 경우 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 제대로 이스케이프해야 합니다.`! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- 다음 문자는 허용되지 않습니다.`" \ / : | < > * ?`.
- 잘못된 URL 경로 문자는 사용할 수 없습니다. NTFS 파일 이름에서 유효하지만 `\uE000` 같은 코드 포인트는 유효한 유니코드 문자가 아닙니다. 또한 제어 문자(0x00~0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1에서 유니코드 문자열을 제어하는 규칙의 경우 [RFC 2616, 2.2섹션:기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 다음 파일 이름은 허용되지 않습니다.LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, COM9, COM9, PRN, AUX, NUL, CON, CLOCK$, 도트 문자(.) 및 두 도트 문자(..)가 있습니다.

## [!DNL Google Cloud Storage]을(를) [!DNL Platform]에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Google Cloud Storage]을 [!DNL Platform]에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

- [Flow Service API를 사용하여 Google 클라우드 스토리지 커넥터 만들기](../../tutorials/api/create/cloud-storage/google.md)
- [Flow Service API를 사용하여 클라우드 스토리지 시스템 살펴보기](../../tutorials/api/explore/cloud-storage.md)
- [Flow Service API를 사용하여 클라우드 스토리지 데이터 수집](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI에서 Google 클라우드 스토리지 소스 커넥터 만들기](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [UI에서 클라우드 스토리지 커넥터에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/batch/cloud-storage.md)