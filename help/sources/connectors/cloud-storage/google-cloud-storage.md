---
keywords: Experience Platform;홈;인기 항목;Google 클라우드 스토리지;google 클라우드 스토리지
solution: Experience Platform
title: Google 클라우드 스토리지 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Google Cloud 저장소를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ae22e423119bf378a068349d481f0717a75171bb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Google 클라우드 스토리지 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform], 및 [!DNL Azure]를 사용하면 이러한 시스템에서 데이터를 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 고유한 데이터를 플랫폼으로 가져올 수 있습니다. 수집된 데이터는 Experience Data Model(XDM)과 호환되는 JSON 또는 Parquet 형식이나 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. Platform에서 데이터를 가져올 수 있습니다. [!DNL Google Cloud Storage] 배치 사용.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 연결 필수 구성 요소 설정 [!DNL Google Cloud Storage] account

Platform에 연결하려면 먼저 상호 운용성을 설정해야 합니다 [!DNL Google Cloud Storage] 계정이 필요합니다. 상호 운용성 설정에 액세스하려면 [!DNL Google Cloud Platform] 을(를) 선택합니다. **[!UICONTROL 설정]** 에서 **[!UICONTROL 클라우드 스토리지]** 옵션을 선택합니다.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

다음 **[!UICONTROL 설정]** 페이지가 나타납니다. 여기에서 [!DNL Google] 프로젝트 ID 및 세부 정보 [!DNL Google Cloud Storage] 계정이 필요합니다. 상호 운용성 설정에 액세스하려면 **[!UICONTROL 상호 운용성]** 상단 헤더에서

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

다음 **[!UICONTROL 상호 운용성]** 페이지에는 인증, 액세스 키 및 서비스 계정과 연결된 기본 프로젝트에 대한 정보가 들어 있습니다. 서비스 계정에 대한 새 액세스 키 ID와 비밀 액세스 키를 생성하려면 **[!UICONTROL 서비스 계정 키 만들기]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

새로 생성된 액세스 키 ID와 비밀 액세스 키를 사용하여 [!DNL Google Cloud Storage] Platform에 계정을 설정합니다.

자세한 내용은 다음 안내서를 참조하십시오. [서비스 계정 키 생성 및 관리](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) 에서 [!DNL Google Cloud] 설명서.

## 파일 및 디렉터리에 대한 이름 지정 제한

클라우드 저장소 파일 또는 디렉토리의 이름을 지정할 때 고려해야 하는 제한 사항 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`). 제공된 경우 자동으로 제거됩니다.
- 다음 예약된 URL 문자를 제대로 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 사용할 수 없습니다. `" \ / : | < > * ?`.
- 잘못된 URL 경로 문자를 사용할 수 없습니다. 다음과 같은 코드 포인트 `\uE000`NTFS 파일 이름에서 사용할 수 있지만 올바른 유니코드 문자는 아닙니다. 또한 제어 문자(0x00~0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 관리하는 규칙은 다음을 참조하십시오 [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 다음 파일 이름은 허용되지 않습니다. LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, UL, CON, CLOCK$, dot 문자(..) 및 두 개의 점 문자(.)가 있습니다.

## Connect [!DNL Google Cloud Storage] 플랫폼

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Google Cloud Storage] API 또는 사용자 인터페이스를 사용하여 플랫폼:

### API 사용

- [Flow Service API를 사용하여 Google Cloud Storage 기본 연결을 만듭니다](../../tutorials/api/create/cloud-storage/google.md)
- [Flow Service API를 사용하여 클라우드 스토리지 소스의 데이터 구조 및 컨텐츠를 탐색합니다](../../tutorials/api/explore/cloud-storage.md)
- [Flow Service API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI에서 Google 클라우드 스토리지 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
