---
title: Acxiom 전망 데이터 가져오기
description: UI를 사용하여 Acxiom Prospecting Data를 Adobe Experience Platform 및 Adobe Real-time Customer Data Platform에 연결하는 방법을 알아봅니다.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# [!DNL Acxiom Prospecting Data Import]

>[!NOTE]
>
>다음 [!DNL Acxiom Prospecting Data Import] 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform은 데이터 파트너 애플리케이션에서 데이터를 수집할 수 있도록 지원합니다. 데이터 및 ID 파트너에 대한 지원은 다음과 같습니다 [!DNL Acxiom Prospecting Data Import].

[!DNL Acxiom]의 Adobe Real-time Customer Data Platform용 Prospect Data Import 는 잠재 고객을 최대한 활용하기 위한 프로세스입니다. [!DNL Acxiom] 안전한 내보내기를 통해 Real-Time CDP 자사 데이터를 가져오고 수상 경력에 빛나는 위생 및 id 해결 시스템을 통해 해당 데이터를 실행합니다. 비표시 목록으로 활용할 수 있는 데이터 파일이 생성됩니다. 그런 다음 이 데이터 파일은 [!DNL Acxiom Global] 데이터베이스를 사용하여 가져오기에 대해 잠재 고객 목록을 사용자 지정할 수 있습니다.

다음을 사용할 수 있습니다. [!DNL Acxiom] 소스에서 응답을 검색하고 매핑할 수 있습니다 [!DNL Acxiom] Prospect Service 사용 [!DNL Amazon S3] 드롭포인트입니다.

## 전제 조건

Experience Platform 시 버킷에 액세스하려면 다음 자격 증명에 대한 유효한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| [!DNL Acxiom] 인증 키 | 인증 키입니다. 다음 위치에서 이 값을 검색할 수 있습니다. [!DNL Acxiom] 팀. |
| [!DNL Amazon S3] 액세스 키 | 버킷에 대한 액세스 키 ID입니다. 다음 위치에서 이 값을 검색할 수 있습니다. [!DNL Acxiom] 팀. |
| [!DNL Amazon S3] 비밀 키 | 버킷의 비밀 키 ID. 다음 위치에서 이 값을 검색할 수 있습니다. [!DNL Acxiom] 팀. |
| 버킷 이름 | 파일을 공유할 버킷입니다. 다음 위치에서 이 값을 검색할 수 있습니다. [!DNL Acxiom] 팀. |

### 권한

둘 다 있어야 합니다. **[!UICONTROL 소스 보기]** 및 **[!UICONTROL 소스 관리]** 에 연결하기 위해 계정에 대해 활성화된 권한 [!DNL Acxiom Prospecting Data Import] Experience Platform 계정. 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/abac/ui/permissions.md).

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

## 파일 및 디렉터리에 대한 이름 지정 제약 조건

아래 나열된 제한 사항은 클라우드 스토리지 파일 또는 디렉토리의 이름을 지정할 때 고려해야 합니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`). 제공되면 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- 다음 문자는 허용되지 않습니다. `" \ / : | < > * ?`.
- 잘못된 URL 경로 문자는 허용되지 않습니다. 다음과 같은 코드 포인트 `\uE000`는 NTFS 파일 이름에서 유효하지만 은 유효한 유니코드 문자가 아닙니다. 또한 제어 문자(0x00 ~ 0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 다음을 참조하십시오. [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

## 다음 단계

이 문서를 읽고 데이터를 가져올 때 필요한 필수 구성 요소 설정을 완료했습니다. [!DNL Acxiom] Experience Platform 계정. 이제 의 안내서로 진행할 수 있습니다. [연결 중 [!DNL Acxiom Prospecting Data Import] 사용자 인터페이스를 사용하여 Experience Platform](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).