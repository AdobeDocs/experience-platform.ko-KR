---
title: SFTP Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 SFTP 서버를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 0%

---

# SFTP 커넥터

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL SFTP] 계정을 Experience Platform에 연결하기 위해 완료해야 하는 필수 구성 요소 단계는 이 문서를 참조하십시오.

>[!TIP]
>
>연결하기 전에 SFTP 서버 구성에서 키보드 대화형 인증을 비활성화해야 합니다. 이 설정을 비활성화하면 서비스나 프로그램을 통해 입력하는 것이 아니라 암호를 수동으로 입력할 수 있습니다.

## 전제 조건 {#prerequisites}

[!DNL SFTP] 원본을 Experience Platform에 연결하기 위해 완료해야 하는 필수 구성 요소 단계는 이 섹션을 참조하십시오.

### 허용 목록에 추가하다 IP 주소

소스 커넥터를 사용하기 전에 IP 주소 목록을 허용 목록에 추가하다에 추가해야 합니다. 영역별 IP 주소를 허용 목록에 추가하다에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 허용 목록에 추가하다 자세한 내용은 [IP 주소](../../ip-address-allow-list.md) 페이지를 참조하십시오.

### 파일 및 디렉터리에 대한 이름 지정 제약 조건

다음은 클라우드 저장소 파일 또는 디렉터리의 이름을 지정할 때 고려해야 하는 제한 사항 목록입니다.

* 디렉터리 및 파일 구성 요소 이름은 255자를 초과할 수 없습니다.
* 디렉터리 및 파일 이름은 슬래시(`/`)로 끝날 수 없습니다. 제공되면 자동으로 제거됩니다.
* 다음 예약된 URL 문자는 올바르게 이스케이프해야 합니다. `! ' ( ) ; @ & = + $ , % # [ ]`
* `" \ / : | < > * ?` 문자는 사용할 수 없습니다.
* 잘못된 URL 경로 문자는 허용되지 않습니다. `\uE000` 같은 코드 포인트는 NTFS 파일 이름에서 사용할 수 있지만 올바른 유니코드 문자가 아닙니다. 또한 제어 문자(0x00 ~ 0x1F, \u0081 등)와 같은 일부 ASCII 또는 유니코드 문자도 사용할 수 없습니다. HTTP/1.1의 유니코드 문자열을 제어하는 규칙에 대해서는 [RFC 2616, 섹션 2.2: 기본 규칙](https://www.ietf.org/rfc/rfc2616.txt) 및 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt)을 참조하십시오.
* LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, 점 문자(.) 및 점 문자(..) 두 개를 사용할 수 없습니다.

### [!DNL SFTP]에 대한 Base64 인코딩 OpenSSH 개인 키 설정

[!DNL SFTP] 원본은 [!DNL Base64] 인코딩된 OpenSSH 개인 키를 사용하여 인증을 지원합니다. Base64로 인코딩된 OpenSSH 개인 키를 생성하고 [!DNL SFTP]을(를) Experience Platform에 연결하는 방법에 대한 자세한 내용은 아래 단계를 참조하십시오.

>[!BEGINTABS]

>[!TAB Windows]

### 사용자 [!DNL Windows]명

[!DNL Windows] 컴퓨터를 사용하는 경우 **시작** 메뉴를 연 다음 **설정**&#x200B;을 선택하세요.

![설정](../../images/tutorials/create/sftp/settings.png)

표시되는 **설정** 메뉴에서 **앱**&#x200B;을 선택합니다.

![앱](../../images/tutorials/create/sftp/apps.png)

**선택적 기능**&#x200B;을(를) 선택하십시오.

![선택적 기능](../../images/tutorials/create/sftp/optional-features.png)

선택적 기능 목록이 나타납니다. **OpenSSH Client**&#x200B;이(가) 컴퓨터에 이미 사전 설치된 경우 **선택적 기능**&#x200B;의 **설치된 기능** 목록에 포함됩니다.

![open-ssh](../../images/tutorials/create/sftp/open-ssh.png)

설치되지 않은 경우 **설치**&#x200B;를 선택한 다음 **[!DNL Powershell]**&#x200B;을(를) 열고 다음 명령을 실행하여 개인 키를 생성합니다.

```shell
PS C:\Users\lucy> ssh-keygen -t rsa -m pem
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\lucy/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\lucy/.ssh/id_rsa.
Your public key has been saved in C:\Users\lucy/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:osJ6Lg0TqK8nekNQyZGMoYwfyxNc+Wh0hYBtBylXuGk lucy@LAPTOP-FUJT1JEC
The key's randomart image is:
+---[RSA 3072]----+
|.=.*+B.o.        |
|=.O.O +          |
|+o+= B           |
|+o +E .          |
|.o=o  . S        |
|+... . .         |
| *o .            |
|o.B.             |
|=O..             |
+----[SHA256]-----+
```

그런 다음 개인 키의 파일 경로를 제공하는 동안 다음 명령을 실행하여 [!DNL Base64]에서 개인 키를 인코딩합니다.

```shell
C:\Users\lucy> [convert]::ToBase64String((Get-Content -path "C:\Users\lucy\.ssh\id_rsa" -Encoding byte)) > C:\Users\lucy\.ssh\id_rsa_base64
```

위의 명령은 지정한 파일 경로에 [!DNL Base64] 인코딩 개인 키를 저장합니다. 그런 다음 해당 개인 키를 사용하여 [!DNL SFTP]을(를) 인증하고 Experience Platform에 연결할 수 있습니다.

>[!TAB Mac]

### 사용자 [!DNL Mac]명

[!DNL Mac]을(를) 사용하는 경우 **터미널**&#x200B;을(를) 열고 다음 명령을 실행하여 개인 키를 생성합니다. 이 경우 개인 키는 `/Documents/id_rsa`에 저장됩니다.

```shell
ssh-keygen -t rsa -m pem -f ~/Documents/id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/vrana/Documents/id_rsa.
Your public key has been saved in /Users/vrana/Documents/id_rsa.pub.
The key fingerprint is:
SHA256:s49PCaO4a0Ee8I7OOeSyhQAGc+pSUQnRii9+5S7pp1M vrana@vrana-macOS
The key's randomart image is:
+---[RSA 2048]----+
|o ==..           |
|.+..o            |
|oo.+             |
|=.. +            |
|oo = .  S        |
|+.+ +E . = .     |
|o*..*.. . o      |
|.o*=.+   +       |
|.oo=Oo  ..o      |
+----[SHA256]-----+
```

그런 다음 [!DNL Base64]에서 개인 키를 인코딩하려면 다음 명령을 실행하십시오.

```shell
base64 ~/Documents/id_rsa > ~/Documents/id_rsa_base64
 
 
# Print Content of base64 encoded file
cat ~/Documents/id_rsa_base64
LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUJGd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFRRUF0cWFYczlXOUF1ZmtWazUwSXpwNXNLTDlOMU9VYklaYXVxbVM0Q0ZaenI1NjNxUGFuN244CmFxZWdvQTlCZnVnWDJsTVpGSFl5elEzbnp6NXdXMkdZa1hkdjFjakd0elVyNyt1NnBUeWRneGxrOGRXZWZsSzBpUlpYWW4KVFRwS0E5c2xXaHhjTXg3R2x5ejdGeDhWSzI3MmdNSzNqY1d1Q0VIU3lLSFR5SFFwekw0MEVKbGZJY1RGR1h1dW1LQjI5SwpEakhwT1grSDdGcG5Gd1pabTA4Uzc2UHJveTVaMndFalcyd1lYcTlyUDFhL0E4ejFoM1ZLdllzcG53c2tCcHFQSkQ1V3haCjczZ3M2OG9sVllIdnhWajNjS3ZsRlFqQlVFNWRNUnB2M0I5QWZ0SWlrYmNJeUNDaXV3UnJmbHk5eVNPQ2VlSEc0Z2tUcGwKL3V4YXNOT0h1d0FBQThqNnF6R1YrcXN4bFFBQUFBZHpjMmd0Y25OaEFBQUJBUUMycHBlejFiMEM1K1JXVG5Rak9ubXdvdgowM1U1UnNobHE2cVpMZ0lWbk92bnJlbzlxZnVmeHFwNkNnRDBGKzZCZmFVeGtVZGpMTkRlZlBQbkJiWVppUmQyL1Z5TWEzCk5TdnY2N3FsUEoyREdXVHgxWjUrVXJTSkZsZGlkTk9rb0QyeVZhSEZ3ekhzYVhMUHNYSHhVcmJ2YUF3cmVOeGE0SVFkTEkKb2RQSWRDbk12alFRbVY4aHhNVVplNjZZb0hiMG9PTWVrNWY0ZnNXbWNYQmxtYlR4THZvK3VqTGxuYkFTTmJiQmhlcjJzLwpWcjhEelBXSGRVcTlpeW1mQ3lRR21vOGtQbGJGbnZlQ3pyeWlWVmdlL0ZXUGR3cStVVkNNRlFUbDB4R20vY0gwQiswaUtSCnR3aklJS0s3Qkd0K1hMM0pJNEo1NGNiaUNST21YKzdGcXcwNGU3QUFBQUF3RUFBUUFBQVFBcGs0WllzMENSRnNRTk9WS0sKYWxjazlCVDdzUlRLRjFNenhrSGVydmpJYk9kL0lvRXpkcHlVa28rbm41RmpGK1hHRnNCUXZnOFdTaUlJTk1oU3BNYWI1agpvWXlka2gvd0ovWElOaDlZaE5QVXlURi9NNkFnMkNYd21KS2RxN1VKWjZyNjloV3V0VVN6U05QbkVYWTZLc29GeVUwTEFvCko0OHJMT1pMZldtMHFhWDBLNUgzNmJPaHFXSWJwMDNoZk94eno5M0MrSDM5MFJkRkp4bzJVZ0FVY3UvdHREb0REVldBdmEKVkVyMWEzak9LenVHbThrK21WeXpPZERjVFY4ckZIT0pwRnRBU3l6Q24yVld1MjV0TWtrcGRPRjNKcVdMZHdOY3loeG1URApXZGVDNWh4V0Fiano0WDZ5WXpHcFcwTmptVkFoWUVVZGNBSVlXWWM3OGEvQkFBQUFnRm8wakl4aGhwZkJ6QjF6b09FMDJBClpjTC9hcUNuYysrdmJ1a2V0aFg5Zzhlb0xQMTQyeUgzdlpLczl3c1RtbVVsZ0prZURaN2hUcklwOGY2eEwzdDRlMXByY1kKb2ZLd0gwckNGOTFyaldPbGZOUmxEempoR1NTTEVMczZoNlNzMEdBQXE2Z0ZQTVF2dTB4TDlQUTlGQ21YZVVKazJpRm1MWgpEWWJGc0NyVUxEQUFBQWdRRGF0a1pMamJaSTBFM0ZuY2dTOVF5Y3lVWmtkZ1dVNjBQcG9ud3BMQXdUdHRpOG1EQXE5cHYwClEvUlk1WE9UeGF3VXNHa0tYMjNtV1BYR0grdUlBSzhrelVVM2dGM1dRWGVkTWw4NHVCVFZCTEtUdStvVVAvZmIvMEE0dE0KSE9BSythbXZPMkZuYzFiSmVwd05USTE2cjZXWk9sZWV2ZklJQVpXcEgxVVpIdkVRQUFBSUVBMWNwcStDNUVXSFJwbnVPZQpiNHE4T0tKTlJhSUxIRUN6U0twWlFpZDFhRmJYWlVKUXpIQU85YzhINVZMcjBNUjFkcW1ORkNja2ZsZzI2Y3BEUEl3TjBYCm5HMFBxcmhKbXp0U3ZQZ3NGdkNPallncXF6U0RYUjkxd1JQTEN5cU8zcGMyM2kzZnp2WkhtMGhIdWdoNVJqV0loUlFZVkwKZUpDWHRqM08vY3p1SWdzQUFBQVJkbkpoYm1GQWRuSmhibUV0YldGalQxTUJBZz09Ci0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

[!DNL Base64] 인코딩 개인 키가 지정한 폴더에 저장되면 공개 키 파일의 내용을 [!DNL SFTP] 호스트 인증 키의 새 줄에 추가해야 합니다. 명령줄에서 다음 명령을 실행합니다.

```shell
cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

공개 키가 제대로 추가되었는지 확인하려면 명령줄에서 다음을 실행할 수 있습니다.

```shell
more ~/.ssh/authorized_keys
```

>[!ENDTABS]

### 필요한 자격 증명 수집 {#credentials}

[!DNL SFTP] 서버를 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증을 사용하여 [!DNL SFTP] 서버를 인증하려면 다음 자격 증명에 적절한 값을 제공하십시오.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | [!DNL SFTP] 서버와 연결된 이름 또는 IP 주소입니다. |
| `port` | 연결 중인 [!DNL SFTP] 서버 포트입니다. 지정하지 않으면 기본값은 `22`입니다. |
| `username` | [!DNL SFTP] 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | [!DNL SFTP] 서버의 암호입니다. |
| `maxConcurrentConnections` | 이 매개 변수를 사용하면 SFTP 서버에 연결할 때 Experience Platform에서 만드는 동시 연결 수의 최대 제한을 지정할 수 있습니다. 이 값을 SFTP에서 설정한 제한보다 작게 설정해야 합니다. **참고**: 기존 SFTP 계정에 대해 이 설정을 사용하면 향후 데이터 흐름에만 영향을 주고 기존 데이터 흐름에는 영향을 주지 않습니다. |
| `folderPath` | 액세스 권한을 제공할 폴더의 경로입니다. [!DNL SFTP] 원본, 폴더 경로를 제공하여 선택한 하위 폴더에 대한 사용자 액세스를 지정할 수 있습니다. |
| `disableChunking` | 데이터를 수집하는 동안 [!DNL SFTP] 원본은 먼저 파일 길이를 검색하고 파일을 여러 부분으로 나눈 다음 병렬로 읽을 수 있습니다. 이 값을 활성화하거나 비활성화하여 [!DNL SFTP] 서버가 파일 길이를 검색할 수 있는지 또는 특정 오프셋에서 데이터를 읽을 수 있는지 여부를 지정할 수 있습니다. |
| `connectionSpec.id` | (API 전용) 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL SFTP]의 연결 사양 ID는 `b7bf2577-4520-42c9-bae9-cad01560f7bc`입니다. |

>[!TAB SSH 공개 키 인증]

SSH 공개 키 인증을 사용하여 [!DNL SFTP] 서버를 인증하려면 다음 자격 증명에 적절한 값을 제공하십시오.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | [!DNL SFTP] 서버와 연결된 이름 또는 IP 주소입니다. |
| `port` | 연결 중인 [!DNL SFTP] 서버 포트입니다. 지정하지 않으면 기본값은 `22`입니다. |
| `username` | [!DNL SFTP] 서버에 액세스할 수 있는 사용자 이름입니다. |
| `password` | [!DNL SFTP] 서버의 암호입니다. |
| `privateKeyContent` | Base64로 인코딩된 SSH 개인 키 콘텐츠입니다. 지원되는 OpenSSH 키 유형은 `ed25519`, `RSA` 및 `DSA`입니다. |
| `passPhrase` | 키 파일 또는 키 콘텐츠가 암호로 보호되어 있는 경우 개인 키를 해독하기 위한 암호나 암호입니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수는 PrivateKeyContent의 암호와 함께 값으로 사용해야 합니다. |
| `maxConcurrentConnections` | 이 매개 변수를 사용하면 SFTP 서버에 연결할 때 Experience Platform에서 만드는 동시 연결 수의 최대 제한을 지정할 수 있습니다. 이 값을 SFTP에서 설정한 제한보다 작게 설정해야 합니다. **참고**: 기존 SFTP 계정에 대해 이 설정을 사용하면 향후 데이터 흐름에만 영향을 주고 기존 데이터 흐름에는 영향을 주지 않습니다. |
| `folderPath` | 액세스 권한을 제공할 폴더의 경로입니다. [!DNL SFTP] 원본, 폴더 경로를 제공하여 선택한 하위 폴더에 대한 사용자 액세스를 지정할 수 있습니다. |
| `disableChunking` | 데이터를 수집하는 동안 [!DNL SFTP] 원본은 먼저 파일 길이를 검색하고 파일을 여러 부분으로 나눈 다음 병렬로 읽을 수 있습니다. 이 값을 활성화하거나 비활성화하여 [!DNL SFTP] 서버가 파일 길이를 검색할 수 있는지 또는 특정 오프셋에서 데이터를 읽을 수 있는지 여부를 지정할 수 있습니다. |
| `connectionSpec.id` | (API 전용) 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL SFTP]의 연결 사양 ID는 `b7bf2577-4520-42c9-bae9-cad01560f7bc`입니다. |

>[!ENDTABS]

## SFTP를 Experience Platform에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 SFTP 서버를 Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

* [흐름 서비스 API를 사용하여 SFTP 기본 연결 만들기](../../tutorials/api/create/cloud-storage/sftp.md)
* [흐름 서비스 API를 사용하여 클라우드 스토리지 소스의 데이터 구조 및 콘텐츠 탐색](../../tutorials/api/explore/cloud-storage.md)
* [흐름 서비스 API를 사용하여 클라우드 스토리지 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

* [UI에서 SFTP 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/sftp.md)
* [UI에서 클라우드 스토리지 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/batch/cloud-storage.md)
