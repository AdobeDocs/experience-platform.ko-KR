---
title: Merkury Enterprise Identity Resolution 소스 개요
description: 사용자 인터페이스를 사용하여 Merkury Enterprise Identity Resolution을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2023-12-12T00:00:00Z
badge: Beta
source-git-commit: 2f277e835333343ea22e52e05aa84a63f1d3d8ec
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>다음 [!DNL Merkury Enterprise Identity Resolution] 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform은 데이터 파트너 애플리케이션에서 데이터를 수집할 수 있도록 지원합니다. 데이터 파트너에 대한 지원은 다음과 같습니다 [!DNL Merkury Enterprise Identity Resolution].

다음을 사용할 수 있습니다. [!DNL Merkury] 작성자: [!DNL Merkle] 쿠키를 사용하지 않더라도 더 많은 디지털 방문자를 인식하고 고객에게 필요한 연관성 있고 개인화된 경험을 제공할 수 있습니다.

다음을 활용할 수 있습니다. **개인 ID** 의 일부로 [!DNL Merkury] 소스 - 조직에서 개인에 대해 알고 있는 모든 것을 하나의 포괄적인 프로필로 결합합니다. 이러한 세부 사항은 다음과 같습니다.

- 디지털 동작
- 구매 환경 설정
- 이름, 이메일 주소, 실제 주소 또는 장치 ID 등 식별 정보.

수집된 데이터의 형식을 XDM(Experience Data Model) JSON, XDM Parquet 또는 구분된 형식으로 지정할 수 있습니다. 프로세스의 모든 단계는 소스 작업에 통합됩니다

![Merkury 소스의 데이터 처리 워크플로우에 대한 일러스트레이션입니다.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

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

## 전제 조건

다음 전제 조건을 충족해야 다음 사용을 시작할 수 있습니다. [!DNL Merkury] 소스:

- 다음을 완료해야 합니다. [!DNL Merkury] 로 설정 [!DNL Merkury] 팀.
- 에서 자격 증명(액세스 키, 비밀 키 및 버킷 이름)을 검색해야 합니다. [!DNL Merkury] 팀. 

>[!NOTE]
>
>다음과 같은 파일 경로 `myBucket/folder/subfolder/subsubfolder/abc.csv` 은(는) 귀하에게 액세스 권한만 부여할 수 있습니다. `subsubfolder/abc.csv`. 하위 폴더에 액세스하려면 버킷 매개 변수를 myBucket으로 지정하고 folderPath를 folder/subfolder로 지정하여 파일 탐색이 하위 폴더에서 시작되도록 할 수 있습니다 `subsubfolder/abc.csv`.

## 다음 단계

이 문서를 읽고 데이터를 가져올 수 있는 필수 구성 요소 설정을 완료했습니다. [!DNL Merkury] Experience Platform 계정. 이제 의 안내서로 진행할 수 있습니다. [연결 중 [!DNL Merkury] 사용자 인터페이스를 사용하여 Experience Platform](../../tutorials/ui/create/data-partners/merkury.md).
