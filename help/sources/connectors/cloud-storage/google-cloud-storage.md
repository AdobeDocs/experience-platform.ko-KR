---
keywords: Experience Platform;홈;인기 항목;Google 클라우드 스토리지;google 클라우드 스토리지
solution: Experience Platform
title: Google 클라우드 스토리지 Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Google Cloud Storage를 Adobe Experience Platform에 연결하는 방법에 대해 알아봅니다.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ee659ded9701132b12d5b93672b4c958e9720028
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Google 클라우드 스토리지 커넥터

>[!IMPORTANT]
>
>이제 Amazon Web Services(AWS)에서 Adobe Experience Platform을 실행할 때 [!DNL Google Cloud Storage] 소스를 사용할 수 있습니다. 현재 AWS에서 실행 중인 Experience Platform은 제한된 수의 고객이 사용할 수 있습니다. 지원되는 Experience Platform 인프라에 대한 자세한 내용은 [Experience Platform 멀티 클라우드 개요](../../../landing/multi-cloud.md)를 참조하세요.

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform] 및 [!DNL Azure]과(와) 같은 클라우드 공급업체에 기본 연결을 제공하므로 이러한 시스템에서 데이터를 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 포맷 또는 업로드 없이도 고유한 데이터를 플랫폼으로 가져올 수 있습니다. 수집된 데이터는 XDM(Experience 데이터 모델) 을 준수하는 JSON 또는 Parquet으로 포맷하거나 구분된 형식으로 포맷할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. 플랫폼을 사용하면 [!DNL Google Cloud Storage]에서 일괄 처리를 통해 데이터를 가져올 수 있습니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

## [!DNL Google Cloud Storage] 계정에 연결하기 위한 필수 구성 요소 설정

플랫폼에 연결하려면 먼저 [!DNL Google Cloud Storage] 계정에 대해 상호 운용성을 사용하도록 설정해야 합니다. 상호 운용성 설정에 액세스하려면 [!DNL Google Cloud Platform]을(를) 열고 탐색 패널의 **[!UICONTROL 클라우드 저장소]** 옵션에서 **[!UICONTROL 설정]**&#x200B;을(를) 선택하십시오.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

**[!UICONTROL 설정]** 페이지가 나타납니다. 여기에서 [!DNL Google] 프로젝트 ID에 대한 정보와 [!DNL Google Cloud Storage] 계정에 대한 세부 정보를 볼 수 있습니다. 상호 운용성 설정에 액세스하려면 상단 헤더에서 **[!UICONTROL 상호 운용성]**&#x200B;을 선택하십시오.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

**[!UICONTROL 상호 운용성]** 페이지에는 서비스 계정과 연결된 인증, 액세스 키 및 기본 프로젝트에 대한 정보가 포함되어 있습니다. 서비스 계정에 대한 새 액세스 키 ID와 비밀 액세스 키를 생성하려면 **[!UICONTROL 서비스 계정에 대한 키 만들기]**&#x200B;를 선택하십시오.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

새로 생성된 액세스 키 ID 및 비밀 액세스 키를 사용하여 [!DNL Google Cloud Storage] 계정을 플랫폼에 연결할 수 있습니다.

자세한 내용은 [!DNL Google Cloud] 설명서에서 [서비스 계정 키 만들기 및 관리](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)에 대한 안내서를 참조하십시오.

## 파일 및 디렉터리에 대한 이름 지정 제약 조건

다음은 클라우드 저장소 파일 또는 디렉터리의 이름을 지정할 때 고려해야 하는 제한 사항 목록입니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공되면 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- `" \ / : | < > * ?` 문자는 사용할 수 없습니다.
- 잘못된 URL 경로 문자는 허용되지 않습니다. `\uE000` 같은 코드 포인트는 NTFS 파일 이름에서 사용할 수 있지만 올바른 유니코드 문자가 아닙니다. 또한 제어 문자(0x00 ~ 0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)을 참조하십시오.
- LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

## [!DNL Google Cloud Storage]을(를) 플랫폼에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Google Cloud Storage]을(를) 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

- [흐름 서비스 API를 사용하여 Google 클라우드 스토리지 기본 연결 만들기](../../tutorials/api/create/cloud-storage/google.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스의 데이터 구조 및 콘텐츠 탐색](../../tutorials/api/explore/cloud-storage.md)
- [흐름 서비스 API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI에서 Google 클라우드 스토리지 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
