---
title: Acxiom 데이터 수집
description: ' [!DNL Acxiom] 데이터를 Real-time Customer Data Platform으로 수집하고, 자사 프로필을 보강하고, 대상자를 개선하고, 마케팅 채널 전반에서 활성화하는 방법을 알아봅니다.'
badge: Beta
exl-id: 3bbbe4e1-5e34-4104-bf39-2c452865b807
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# [!DNL Acxiom Data Ingestion]

>[!NOTE]
>
>[!DNL Acxiom Prospecting Data Import] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

[!DNL Acxiom Data Ingestion] 소스를 사용하여 [!DNL Acxiom] 데이터를 Real-time Customer Data Platform으로 수집하고 자사 프로필을 보강합니다. 그런 다음 [!DNL Acxiom]이(가) 보강된 자사 프로필을 사용하여 대상자를 개선하고 마케팅 채널 전반에서 활성화할 수 있습니다.

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

[!DNL Acxiom Data Ingestion] 소스 계정을 설정하는 방법에 대한 자세한 내용은 아래 문서를 참조하십시오.

## 전제 조건 {#prerequisites}

[!DNL Acxiom Data Ingestion] 계정을 Experience Platform에 연결하려면 다음 인증 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| [!DNL Acxiom] 인증 키 | 인증 키입니다. [!DNL Acxiom] 팀에서 이 값을 검색할 수 있습니다. |
| [!DNL Amazon S3] 액세스 키 | 버킷에 대한 액세스 키 ID입니다. [!DNL Acxiom] 팀에서 이 값을 검색할 수 있습니다. |
| [!DNL Amazon S3] 비밀 키 | 버킷의 비밀 키 ID. [!DNL Acxiom] 팀에서 이 값을 검색할 수 있습니다. |
| 버킷 이름 | 파일을 공유할 버킷입니다. [!DNL Acxiom] 팀에서 이 값을 검색할 수 있습니다. |

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

### Experience Platform에 대한 권한 구성

[!DNL Acxiom Data Ingestion] 계정을 Experience Platform에 연결하려면 계정에 대해 **[!UICONTROL 소스 보기]** 및 **[!UICONTROL 소스 관리]** 사용 권한이 모두 활성화되어 있어야 합니다. 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/ui/overview.md)를 참조하십시오.

### 파일 및 디렉터리에 대한 이름 지정 제약 조건

아래 나열된 제한 사항은 클라우드 스토리지 파일 또는 디렉토리의 이름을 지정할 때 고려해야 합니다.

- 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
- 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공되면 자동으로 제거됩니다.
- 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
- `" \ / : | < > * ?` 문자는 사용할 수 없습니다.
- 잘못된 URL 경로 문자는 허용되지 않습니다. `\uE000` 같은 코드 포인트는 NTFS 파일 이름에서 사용할 수 있지만 올바른 유니코드 문자가 아닙니다. 또한 제어 문자(0x00 ~ 0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)을 참조하십시오.
- LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

## 다음 단계

이 문서를 읽고 [!DNL Acxiom] 계정의 데이터를 Experience Platform 상태로 만드는 데 필요한 필수 구성 요소 설정을 완료했습니다. 이제 사용자 인터페이스를 사용하여 [연결 [!DNL Acxiom Data Ingestion] Experience Platform에 연결](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md)에 대한 안내서로 진행할 수 있습니다.
