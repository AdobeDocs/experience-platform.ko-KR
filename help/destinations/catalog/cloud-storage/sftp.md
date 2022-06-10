---
keywords: SFTP;sftp
title: SFTP 연결
description: SFTP 서버에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 구분된 데이터 파일을 주기적으로 내보냅니다.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 715533352e84573f60f012504988595af6146e2f
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 1%

---

# SFTP 연결

## 개요 {#overview}

SFTP 서버에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 구분된 데이터 파일을 주기적으로 내보냅니다.

>[!IMPORTANT]
>
> Experience Platform은 SFTP 서버로 데이터 내보내기를 지원하지만 데이터를 내보내는 권장 클라우드 저장소 위치는 다음과 같습니다 [!DNL Amazon S3] 및 [!DNL Azure Blob].

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![SFTP 프로필 기반 내보내기 유형](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA 공개 키"
>abstract="선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 Base64 인코딩 문자열로 작성해야 합니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="개인 SSH 키"
>abstract="개인 SSH 키는 Base64로 인코딩된 문자열로 포맷해야 하며 암호로 보호되어서는 안 됩니다. "

When [연결](../../ui/connect-destination.md) 이 대상에 대해 다음 정보를 제공해야 합니다.

#### 인증 정보 {#authentication-information}

을(를) 선택하는 경우 **[!UICONTROL 기본 인증]** sftp 위치에 연결할 유형:

![SFTP 대상 기본 인증](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL 호스트]**: SFTP 저장소 위치의 주소입니다.
* **[!UICONTROL 사용자 이름]**: SFTP 저장소 위치에 로그인할 사용자 이름;
* **[!UICONTROL 암호]**: SFTP 저장소 위치에 로그인하는 암호입니다.
* **[!UICONTROL 암호화 키]**: 선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩된 문자열입니다.
   * 예: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. 간결성을 위해 중간 부분이 단축된 올바른 형식의 PGP 키의 예를 아래 를 참조하십시오.

      ![PGP 키](../..//assets/catalog/cloud-storage/sftp/pgp-key.png)


을(를) 선택하는 경우 **[!UICONTROL SSH 키가 있는 SFTP]** sftp 위치에 연결할 인증 유형:

![SFTP 대상 SSH 키 인증](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL 도메인]**: SFTP 계정의 IP 주소 또는 도메인 이름을 입력합니다
* **[!UICONTROL 포트]**: SFTP 저장소 위치에서 사용되는 포트입니다.
* **[!UICONTROL 사용자 이름]**: SFTP 저장소 위치에 로그인할 사용자 이름;
* **[!UICONTROL SSH 키]**: SFTP 저장소 위치에 로그인하는 데 사용되는 개인 SSH 키입니다. 개인 키는 Base64로 인코딩된 문자열로 포맷해야 하며 암호로 보호되어서는 안 됩니다.
* **[!UICONTROL 암호화 키]**: 선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩된 문자열입니다.
   * 예: `----BEGIN PGP PUBLIC KEY BLOCK---- {Base64-encoded string} ----END PGP PUBLIC KEY BLOCK----`. 간결성을 위해 중간 부분이 단축된 올바른 형식의 PGP 키의 예를 아래 를 참조하십시오.

      ![PGP 키](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### 대상 세부 사항 {#destination-details}

SFTP 위치에 인증 연결을 설정한 후 대상에 대해 다음 정보를 제공합니다.

![SFTP 대상에 사용할 수 있는 대상 세부 사항](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL 이름]**: Experience Platform 사용자 인터페이스에서 이 대상을 식별하는 데 도움이 되는 이름을 입력합니다.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 폴더 경로]**: 파일을 내보낼 SFTP 위치에 폴더의 경로를 입력합니다.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 내보낸 데이터 {#exported-data}

대상 [!DNL SFTP] 대상, 플랫폼에서 `.csv` 파일을 입력한 저장 위치에 저장합니다. 파일에 대한 자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 세그먼트 활성화 자습서에서 를 참조하십시오.

## IP 주소 허용 목록

을(를) 참조하십시오. [클라우드 스토리지 대상에 대한 IP 주소 허용 목록](ip-address-allow-list.md) Adobe IP를 허용 목록에 추가해야 하는 경우
