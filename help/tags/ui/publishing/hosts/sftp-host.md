---
title: SFTP 호스트
description: Adobe Experience Platform에서 태그를 구성하여 보안 및 자체 호스팅되는 SFTP 서버에 라이브러리 빌드를 전달하는 방법에 대해 알아봅니다.
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 10%

---

# SFTP 호스트

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Experience Platform을 사용하면 호스팅하는 보안 SFTP 서버에 태그 라이브러리 빌드를 전달할 수 있으므로, 빌드의 저장 및 관리 방법을 보다 세밀하게 제어할 수 있습니다. 이 안내서에서는 Experience Platform UI 또는 데이터 수집 UI에서 태그 속성에 대한 SFTP 호스트를 설정하는 방법을 다룹니다.

>[!NOTE]
>
>Adobe에서 관리하는 호스트를 대신 사용하도록 선택할 수도 있습니다. 자세한 내용은 [Adobe 관리 호스트](./managed-by-adobe-host.md)에 대한 안내서를 참조하십시오.
>
>자체 호스팅 라이브러리의 이점 및 제한 사항에 대한 자세한 내용은 [자체 호스팅 가이드](./self-hosting-libraries.md)를 참조하십시오.

## 서버에 대한 액세스 키 설정 {#access-key}

Experience Platform은 암호화된 키를 사용하여 SFTP 사이트에 연결합니다. 이를 올바르게 설정하려면 다음 몇 가지 단계를 수행해야 합니다.

### 공개/개인 키 쌍 만들기

SFTP 서버에 공개/개인 키 쌍이 설치되어 있어야 합니다. 이러한 키를 서버에 생성하거나 다른 곳에 생성한 후 서버에 설치할 수 있습니다. 자세한 내용은 [SSH 키를 생성하는 방법](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key)에 대한 GitHub 설명서를 참조하십시오.

### 키 암호화

개인 키는 공개 키를 암호화하는 데 사용됩니다. SFTP 호스트 생성 프로세스 중에 개인 키를 제공해야 합니다. 공개 키 암호화에 대한 지침은 Reactor API 안내서의 [암호 값](../../../api/guides/encrypting-values.md)에 대한 섹션을 참조하십시오. 특정 키가 필요한지 알지 못하는 경우에는 프로덕션 환경의 GPG 키를 사용하십시오. 마지막으로, 모든 컴퓨터에서 개인 키를 암호화할 수 있으므로 이 단계를 완료하기 위해 서버에 GPG를 설치할 필요가 없습니다.

### 허용 목록에 추가하다 Experience Platform IP 주소

>[!IMPORTANT]
>
> 2025년 6월 23일, Adobe Launch는 SFTP 호스트 유형 및 콜백 API 기능을 지원하는 데 사용되는 외부 IP 주소를 업데이트하고 있습니다. 이러한 기능을 계속 사용하려면 방화벽 규칙이 새 IP 주소에서 트래픽을 허용하는지 확인하십시오.
>
> 중단 없이 액세스를 유지하려면 지금 새 IP를 추가하고 2025년 6월 23일 이후에 이전 IP를 제거하는 것이 좋습니다.
>
>**이전 IP 주소:**
> * `184.72.239.68`
> * `23.20.85.113`
> * `54.226.193.184`
>
>**새 IP 주소:**
> * `34.227.138.75 `
> * `44.194.43.191`
> * `3.215.163.18`

Experience Platform이 SFTP 서버에 연결할 수 있도록 하기 위해 회사 방화벽 내에서 사용할 IP 주소 집합을 승인해야 할 수 있습니다. 이러한 IP 주소는 다음과 같습니다.

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>태그 빌드의 구조가 시간이 지남에 따라 변경되었습니다. 이전 포함 코드가 최신 빌드 구조와 계속 작동할 수 있도록 내부적으로 symlink를 사용하여 이전 버전과의 호환성을 유지합니다. SFTP 서버는 태그 빌드의 올바른 대상으로 사용하기 위해 symlink 사용을 지원해야 합니다.

자세한 내용은 [빌드를 전달하도록 SFTP 서버를 설정하는 방법](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6)에 대한 Medium 문서를 참조하십시오.

## SFTP 호스트 만들기 {#create}

왼쪽 탐색에서 **[!UICONTROL 호스트]**&#x200B;를 선택한 다음 **[!UICONTROL 호스트 추가]**&#x200B;를 선택하십시오.

![UI에서 선택 중인 호스트 추가 단추를 보여 주는 이미지](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

호스트 생성 대화 상자가 나타납니다. 호스트의 이름을 입력하고 **[!UICONTROL 유형]**&#x200B;에서 **[!UICONTROL SFTP]**&#x200B;을(를) 선택합니다.

![선택 중인 SFTP 호스팅 옵션을 보여 주는 이미지](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### SFTP 호스트 구성 {#configure}

대화 상자가 확장되어 SFTP 호스트에 대한 추가 구성 옵션을 포함합니다. 이러한 내용은 아래에 설명되어 있습니다.

![SFTP 호스트 연결에 필요한 세부 정보를 표시하는 이미지](../../../images/ui/publishing/sftp-hosts/host-details.png)

| 구성 필드 | 설명 |
| --- | --- |
| [!UICONTROL 심볼릭 링크 사용 안 함] | 기본적으로 모든 SFTP 호스트는 기호 링크(symlink)를 사용하여 서버에 저장된 라이브러리 [빌드](../builds.md)를 참조합니다. 그러나 모든 서버가 symlink의 사용을 지원하는 것은 아닙니다. 이 옵션을 선택하면 호스트가 심볼릭 링크를 사용하는 대신 복사 작업을 사용하여 빌드 에셋을 직접 업데이트합니다. |
| [!UICONTROL SFTP 서버 URL] | 서버의 URL 기본 경로입니다. |
| [!UICONTROL 경로] | 이 호스트의 기본 서버 URL에 추가할 경로입니다. |
| [!UICONTROL 포트] | 포트는 다음 중 하나여야 합니다.<ul><li>`21`</li><li>`22`</li><li>`201`</li><li>`200`</li><li>`2002`</li><li>`2018`</li><li>`2022`</li><li>`2200`</li><li>`2222`</li><li>`2333`</li><li>`2939`</li><li>`443`</li><li>`4343`</li><li>`80`</li><li>`8080`</li><li>`8888`</li></ul>보안 모범 사례로서 Adobe는 발신 트래픽에 사용할 수 있는 포트 수를 제한합니다. 선택한 포트는 일반적으로 회사 방화벽을 통해 허용되며 일부 범위의 유연성을 포함합니다. |
| [!UICONTROL 사용자 이름] | 서버에 액세스할 때 사용할 사용자 이름입니다. |
| [!UICONTROL 암호화된 개인 키] | [이전 단계](#access-key)에서 만든 암호화된 개인 키입니다. |

선택한 구성으로 호스트를 만들려면 **[!UICONTROL 저장]**&#x200B;을 선택하십시오.

![저장 중인 SFTP 호스트를 보여 주는 이미지](../../../images/ui/publishing/sftp-hosts/save-host.png)

**[!UICONTROL 저장]**&#x200B;을 선택하면 SFTP 서버에 파일을 전달할 수 있는 연결 및 기능이 테스트됩니다. Experience Platform은 폴더를 만들고 해당 폴더 내에 파일을 작성한 다음, 파일이 폴더에 있는지 확인한 후 삭제합니다. SFTP 서버의 사용자 계정(Experience Platform에 제공한 보안 인증서에 첨부된 계정)에 이 작업을 수행하는 데 필요한 권한이 없는 경우 호스트가 &quot;실패&quot; 상태로 전환됩니다.

## 다음 단계

이 안내서에서는 태그에 사용할 자체 호스팅 SFTP 서버를 설정하는 방법을 다룹니다. 호스트가 설정되면 태그 라이브러리를 게시하기 위해 이 호스트를 하나 이상의 [환경](../environments.md)과 연결할 수 있습니다. 웹 또는 모바일 속성에서 태그 기능을 활성화하는 고급 프로세스에 대한 자세한 내용은 [게시 개요](../overview.md)를 참조하십시오.
