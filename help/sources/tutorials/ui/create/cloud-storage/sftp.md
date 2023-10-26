---
title: UI에서 SFTP 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 SFTP 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: e92471b386b857fc21947d352f1c1b88431c68bc
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 만들기 [!DNL SFTP] UI의 소스 연결

이 튜토리얼에서는 [!DNL SFTP] Adobe Experience Platform UI를 사용한 소스 연결.

## 시작하기

이 자습서에서는 다음 플랫폼 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

>[!IMPORTANT]
>
>를 사용하여 JSON 개체를 수집할 때 줄바꿈 또는 캐리지 리턴을 피하는 것이 좋습니다. [!DNL SFTP] 소스 연결. 제한을 해결하려면 라인당 단일 JSON 개체를 사용하고 후속 파일에 여러 라인을 사용합니다.

이미 유효한 을(를) 가지고 있는 경우 [!DNL SFTP] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/batch/cloud-storage.md).

### 필요한 자격 증명 수집

에 연결하려면 [!DNL SFTP], 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 와(과) 연계된 이름 또는 IP 주소 [!DNL SFTP] 서버입니다. |
| `port` | 다음 [!DNL SFTP] 연결 중인 서버 포트입니다. 제공되지 않으면 기본값은 입니다. `22`. |
| `username` | 에 대한 액세스 권한이 있는 사용자 이름 [!DNL SFTP] 서버입니다. |
| `password` | 에 대한 암호 [!DNL SFTP] 서버입니다. |
| `privateKeyContent` | Base64로 인코딩된 SSH 개인 키 콘텐츠입니다. OpenSSH 키 유형은 RSA 또는 DSA로 분류되어야 합니다. |
| `passPhrase` | 키 파일 또는 키 콘텐츠가 암호로 보호되어 있는 경우 개인 키를 해독하기 위한 암호나 암호입니다. PrivateKeyContent가 암호로 보호된 경우 이 매개 변수는 PrivateKeyContent의 암호와 함께 값으로 사용해야 합니다. |
| `maxConcurrentConnections` | 이 매개 변수를 사용하면 SFTP 서버에 연결할 때 플랫폼이 생성하는 동시 연결 수에 대한 최대 제한을 지정할 수 있습니다. 이 값을 SFTP에서 설정한 제한보다 작게 설정해야 합니다. **참고**: 이 설정이 기존 SFTP 계정에 대해 활성화되면 향후 데이터 흐름에만 영향을 주고 기존 데이터 흐름에는 영향을 주지 않습니다. |
| 폴더 경로 | 액세스 권한을 제공할 폴더의 경로입니다. [!DNL SFTP] 소스 폴더 경로를 제공하여 선택한 하위 폴더에 대한 사용자 액세스를 지정할 수 있습니다. |

필요한 자격 증명을 수집했으면 아래 단계에 따라 새 자격 증명을 만들 수 있습니다 [!DNL SFTP] 플랫폼에 연결할 계정입니다.

## 다음에 연결 [!DNL SFTP] server

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 클라우드 스토리지] 범주, 선택 **[!UICONTROL SFTP]** 다음을 선택합니다. **[!UICONTROL 데이터 추가]**.

![SFTP 소스가 있는 Experience Platform 소스 카탈로그입니다.](../../../../images/tutorials/create/sftp/catalog.png)

다음 **[!UICONTROL SFTP에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 연결할 FTP 또는 SFTP 계정을 선택한 다음 를 선택합니다 **[!UICONTROL 다음]** 계속합니다.

![Experience Platform UI의 기존 SFTP 계정 목록입니다.](../../../../images/tutorials/create/sftp/existing.png)

### 새 계정

>[!TIP]
>
>* 만든 후에는 의 인증 유형을 변경할 수 없습니다. [!DNL SFTP] 기본 연결. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.
>
>* SFTP는 RSA 또는 DSA 유형 OpenSSH 키를 지원합니다. 키 파일 컨텐츠가 다음으로 시작하는지 확인합니다. `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 다음으로 끝남 `"-----END [RSA/DSA] PRIVATE KEY-----"`. 개인 키 파일이 PPK 형식 파일인 경우 PuTTY 도구를 사용하여 PPK에서 OpenSSH 형식으로 변환합니다.

새 계정을 만드는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**&#x200B;을 클릭하고 새 항목의 이름과 설명(선택 사항)을 입력합니다 [!DNL SFTP] 계정입니다.

![SFTP의 새 계정 화면](../../../../images/tutorials/create/sftp/new.png)

다음 [!DNL SFTP] 소스는 SSH 공개 키를 통해 기본 인증과 인증을 모두 지원합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증을 사용하려면 다음을 선택합니다 **[!UICONTROL 암호]** 그런 다음 연결할 호스트 및 포트 값을 사용자 이름 및 암호와 함께 제공합니다. 이 단계에서 액세스 권한을 제공할 하위 폴더의 경로를 지정할 수도 있습니다. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]**.

![기본 인증을 사용하는 SFTP 소스에 대한 새 계정 화면입니다](../../../../images/tutorials/create/sftp/password.png)

>[!TAB SSH 공개 키 인증]

SSH 공개 키 기반 자격 증명을 사용하려면 다음을 선택합니다. **[!UICONTROL SSH 공개 키]**  그런 다음 호스트 및 포트 값과 개인 키 콘텐츠 및 암호 조합을 제공합니다. 이 단계에서 액세스 권한을 제공할 하위 폴더의 경로를 지정할 수도 있습니다. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]**.

![SSH 공개 키를 사용하는 SFTP 소스에 대한 새 계정 화면입니다.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## 다음 단계

이 자습서에 따라 SFTP 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하여 [클라우드 스토리지에서 플랫폼으로 데이터를 가져오도록 데이터 흐름을 구성합니다.](../../dataflow/batch/cloud-storage.md).
