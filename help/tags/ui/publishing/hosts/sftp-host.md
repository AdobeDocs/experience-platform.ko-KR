---
title: SFTP 호스트
description: 보안 자체 호스팅된 SFTP 서버에 라이브러리 빌드를 전달하도록 Adobe Experience Platform에서 태그를 구성하는 방법을 알아봅니다.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 32%

---

# SFTP 호스트

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../../term-updates.md)을 참조하십시오.

호스팅된 라이브러리를 Adobe에서 관리하지 않도록 하려는 경우 다른 옵션은 Adobe Experience Platform에서 사용자가 호스트하는 보안 SFTP 서버에 빌드를 전달하도록 하는 것입니다.

플랫폼은 암호화된 키를 사용하여 SFTP 사이트에 연결합니다. 이를 올바르게 설정하려면 다음 몇 가지 단계를 수행해야 합니다.

1. SFTP 서버에 공개/개인 키 쌍이 설치되어 있어야 합니다. 이러한 키를 서버에 생성하거나 다른 곳에 생성한 후 서버에 설치할 수 있습니다. 자세한 내용은 [SSH 키를 생성하는 방법](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key)에 대한 GitHub 설명서를 참조하십시오.
1. 개인 키는 공개 GPG 키를 암호화하는 데 사용됩니다. SFTP 호스트 생성 프로세스 중에 개인 키를 제공해야 합니다. 공개 GPG 키 암호화에 대한 지침은 Reactor API 설명서의 [값 암호화](https://developer.adobelaunch.com/api/guides/encrypting_values/) 섹션을 참조하십시오. 특정 키가 필요한지 알지 못하는 경우에는 프로덕션 환경의 GPG 키를 사용하십시오. 마지막으로, 모든 컴퓨터에서 개인 키를 암호화할 수 있으므로 이 단계를 완료하기 위해 서버에 GPG를 설치할 필요가 없습니다.
1. Platform이 SFTP 서버에 연결할 수 있도록 하기 위해 회사 방화벽에 사용되는 IP 주소를 승인해야 할 수 있습니다. 그러한 IP 주소는 다음과 같습니다.
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>태그 빌드의 구조가 시간이 지남에 따라 변경되었습니다. 이전 임베드 코드는 최신 빌드 구조와 계속 작동할 수 있도록 내부적으로 symlink를 사용하여 이전 버전과의 호환성을 유지합니다. SFTP 서버는 태그 빌드의 올바른 대상으로 사용하기 위해 symlink 사용을 지원해야 합니다.

자세한 내용은 [SFTP 서버를 설정하여 빌드](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6)를 제공하는 방법에 대한 다음 미디어 문서를 참조하십시오.

## SFTP 호스트 만들기

1. [!UICONTROL 호스트] 탭을 엽니다.
1. 새 호스트를 만듭니다.
1. 호스트에 이름을 지정합니다.
1. **[!UICONTROL SFTP]** 를 호스트 유형으로 선택합니다.
1. 호스트, 경로, 포트, 사용자 이름 및 암호화된 개인 키를 입력합니다.

   포트는 다음 중 하나여야 합니다.

   * 21
   * 22
   * 80
   * 200-299
   * 443
   * 2000-2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >보안 모범 사례로서 Adobe는 발신 트래픽에 사용할 수 있는 포트 수를 제한합니다. 선택한 포트는 일반적으로 회사 방화벽을 통해 허용되며 일부 범위의 유연성이 포함됩니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

**[!UICONTROL 저장]**&#x200B;을 선택하면 SFTP 서버에 파일을 전달하는 연결 및 기능이 테스트됩니다. Platform은 폴더를 만들고 이 폴더 내에 파일을 작성한 다음, 파일이 폴더에 있는지 확인한 후 삭제합니다. SFTP 서버의 사용자 계정(Platform에 제공한 보안 인증서에 첨부된 계정)에 이 작업을 수행하는 데 필요한 권한이 없는 경우 호스트가 &quot;실패&quot; 상태로 전환됩니다.
