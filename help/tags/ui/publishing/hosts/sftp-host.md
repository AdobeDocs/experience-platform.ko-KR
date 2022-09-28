---
title: SFTP 호스트
description: 보안 자체 호스팅된 SFTP 서버에 라이브러리 빌드를 전달하도록 Adobe Experience Platform에서 태그를 구성하는 방법을 알아봅니다.
exl-id: 3c1dc43b-291c-4df4-94f7-a03b25dbb44c
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 18%

---

# SFTP 호스트

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Adobe Experience Platform을 사용하면 태그 라이브러리 빌드를 사용자가 호스트하는 보안 SFTP 서버에 전달하여 빌드의 저장 및 관리 방식을 보다 강력하게 제어할 수 있습니다. 이 안내서에서는 Experience Platform UI 또는 데이터 수집 UI에서 태그 속성에 대한 SFTP 호스트를 설정하는 방법을 다룹니다.

>[!NOTE]
>
>대신 Adobe에서 관리하는 호스트를 사용하도록 선택할 수도 있습니다. 다음 안내서를 참조하십시오. [Adobe 관리 호스트](./managed-by-adobe-host.md) 추가 정보.
>
>자체 호스팅 라이브러리의 이점 및 제한 사항에 대한 자세한 내용은 다음을 참조하십시오. [자체 호스팅 안내서](./self-hosting-libraries.md).

## 서버에 대한 액세스 키 설정 {#access-key}

플랫폼은 암호화된 키를 사용하여 SFTP 사이트에 연결합니다. 이를 올바르게 설정하려면 다음 몇 가지 단계를 수행해야 합니다.

### 공개/개인 키 쌍 만들기

SFTP 서버에 공개/개인 키 쌍이 설치되어 있어야 합니다. 이러한 키를 서버에 생성하거나 다른 곳에 생성한 후 서버에 설치할 수 있습니다. 다음 사항에 대해서는 GitHub 설명서 를 참조하십시오. [ssh 키를 생성하는 방법](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) 추가 정보.

### 키 암호화

개인 키는 공개 키를 암호화하는 데 사용됩니다. SFTP 호스트 생성 프로세스 중에 개인 키를 제공해야 합니다. 의 섹션을 참조하십시오. [값 암호화](../../../api/guides/encrypting-values.md) 공개 키 암호화에 대한 지침은 Reactor API 안내서 를 참조하십시오. 특정 키가 필요한지 알지 못하는 경우에는 프로덕션 환경의 GPG 키를 사용하십시오. 마지막으로, 모든 컴퓨터에서 개인 키를 암호화할 수 있으므로 이 단계를 완료하기 위해 서버에 GPG를 설치할 필요가 없습니다.

### 플랫폼 허용 목록에 추가하다 IP 주소

Platform이 SFTP 서버에 연결할 수 있도록 하기 위해 회사 방화벽 내에 사용할 IP 주소 세트를 승인해야 할 수 있습니다. 이러한 IP 주소는 다음과 같습니다.

* `184.72.239.68`
* `23.20.85.113`
* `54.226.193.184`

>[!NOTE]
>
>태그 빌드의 구조가 시간이 지남에 따라 변경되었습니다. 이전 임베드 코드는 최신 빌드 구조와 계속 작동할 수 있도록 내부적으로 symlink를 사용하여 이전 버전과의 호환성을 유지합니다. SFTP 서버는 태그 빌드의 올바른 대상으로 사용하기 위해 symlink 사용을 지원해야 합니다.

자세한 내용은 다음 미디어 문서를 참조하십시오. [sftp 서버를 설정하여 빌드를 제공하는 방법](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## SFTP 호스트 만들기 {#create}

선택 **[!UICONTROL 호스트]** 왼쪽 탐색에서 를 차례로 클릭하거나 **[!UICONTROL 호스트 추가]**.

![UI에서 선택한 호스트 추가 단추를 보여주는 이미지](../../../images/ui/publishing/sftp-hosts/add-host-button.png)

호스트 생성 대화 상자가 나타납니다. 호스트의 이름과 아래에 을 입력합니다. **[!UICONTROL 유형]**, 선택 **[!UICONTROL SFTP]**.

![선택 중인 SFTP 호스팅 옵션을 보여주는 이미지](../../../images/ui/publishing/sftp-hosts/select-sftp.png)

### SFTP 호스트 구성 {#configure}

이 대화 상자가 확장되어 SFTP 호스트에 대한 추가 구성 옵션이 포함됩니다. 이러한 내용은 아래에 설명되어 있습니다.

![SFTP 호스트 연결에 필요한 세부 정보를 보여주는 이미지](../../../images/ui/publishing/sftp-hosts/host-details.png)

| 구성 필드 | 설명 |
| --- | --- |
| [!UICONTROL Symlink 사용 안 함] | 기본적으로 모든 SFTP 호스트는 심볼 링크(symlink)를 사용하여 라이브러리를 참조합니다 [빌드](../builds.md) 서버에 저장됩니다. 그러나 모든 서버가 symlink 사용을 지원하는 것은 아닙니다. 이 옵션을 선택하면 호스트는 복사 작업을 사용하여 symlink를 사용하는 대신 직접 빌드 자산을 업데이트합니다. |
| [!UICONTROL SFTP 서버 URL] | 서버의 URL 기본 경로입니다. |
| [!UICONTROL 경로] | 이 호스트의 기본 서버 URL에 추가할 경로입니다. |
| [!UICONTROL 포트] | 포트는 다음 중 하나여야 합니다.<ul><li>`21`</li><li>`22`</li><li>`80`</li><li>`200-299`</li><li>`443`</li><li>`2000-2999`</li><li>`4343`</li><li>`8080`</li><li>`8888`</li></ul>보안 모범 사례로서 Adobe는 발신 트래픽에 사용할 수 있는 포트 수를 제한합니다. 선택한 포트는 일반적으로 회사 방화벽을 통해 허용되며 일부 범위의 유연성이 포함됩니다. |
| [!UICONTROL 사용자 이름] | 서버에 액세스할 때 사용할 사용자 이름입니다. |
| [!UICONTROL 암호화된 개인 키] | 사용자가 만든 암호화된 개인 키 [이전 단계](#access-key). |

선택 **[!UICONTROL 저장]** 선택한 구성으로 호스트를 생성합니다.

![저장되는 SFTP 호스트를 표시하는 이미지](../../../images/ui/publishing/sftp-hosts/save-host.png)

선택 시 **[!UICONTROL 저장]**&#x200B;를 설정하는 것이 좋습니다. Platform은 폴더를 만들고 이 폴더 내에 파일을 작성한 다음, 파일이 폴더에 있는지 확인한 후 삭제합니다. SFTP 서버의 사용자 계정(Platform에 제공한 보안 인증서에 첨부된 계정)에 이 작업을 수행하는 데 필요한 권한이 없는 경우 호스트가 &quot;실패&quot; 상태로 전환됩니다.

## 다음 단계

이 안내서에서는 태그에 사용할 자체 호스팅된 SFTP 서버를 설정하는 방법을 다룹니다. 호스트가 설정되면 이 호스트를 하나 이상의 사용자 [환경](../environments.md) 태그 라이브러리 게시용. 웹 또는 모바일 속성에서 태그 기능을 활성화하는 높은 수준의 프로세스에 대한 자세한 내용은 [게시 개요](../overview.md).
