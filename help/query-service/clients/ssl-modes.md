---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;연결;쿼리 서비스에 연결;SSL;ssl;sslmode;
title: 쿼리 서비스 SSL 옵션
description: Adobe Experience Platform Query Service에 대한 타사 연결에 대한 SSL 지원 및 verify-full SSL 모드를 사용하여 연결하는 방법에 대해 알아봅니다.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# [!DNL Query Service] SSL 옵션

보안 강화를 위해 Adobe Experience Platform [!DNL Query Service] 는 클라이언트/서버 통신을 암호화하기 위해 SSL 연결을 기본적으로 지원합니다. 이 문서에서는 타사 클라이언트 연결에 사용할 수 있는 SSL 옵션을 다룹니다 [!DNL Query Service] 및 `verify-full` SSL 매개 변수 값입니다.

## 전제 조건

이 문서에서는 사용자가 플랫폼 데이터에 사용할 타사 데스크탑 클라이언트 응용 프로그램을 이미 다운로드했다고 가정합니다. 타사 클라이언트와 연결할 때 SSL 보안을 통합하는 방법에 대한 구체적인 지침은 해당 연결 안내서 설명서에서 확인할 수 있습니다. 모든 [!DNL Query Service] 지원되는 클라이언트는 [클라이언트 연결 개요](./overview.md).

## 사용 가능한 SSL 옵션 {#available-ssl-options}

플랫폼은 데이터 보안 요구 사항에 맞게 다양한 SSL 옵션을 지원하며 암호화 및 키 교환의 처리 오버헤드를 조정합니다.

다른 `sslmode` 매개 변수 값은 다양한 보호 수준을 제공합니다. SSL 인증서를 사용하여 데이터를 암호화하여 &quot;중간적&quot;(MITM) 공격, 도청 및 가장을 방지하는 데 도움이 됩니다. 아래 표에는 사용 가능한 다양한 SSL 모드 및 보호 수준이 표시되어 있습니다.

>[!NOTE]
>
> SSL 값 `disable` 는 필수 데이터 보호 규정 준수 때문에 Adobe Experience Platform에서 지원하지 않습니다.

| sslmode | 도청 보호 | MITM 보호 | 설명 |
|---|---|---|---|
| `allow` | 부분 | 아니요 | 보안이 우선순위가 아니며, 속도가 빠르며 처리 오버헤드가 낮습니다. 이 모드는 서버에서 암호화를 고집하는 경우에만 작동합니다. |
| `prefer` | 부분 | 아니요 | 암호화는 필요하지 않지만 서버에서 지원하는 경우 통신이 암호화됩니다. |
| `require` | 예 | 아니요 | 모든 통신에서 암호화가 필요합니다. 올바른 서버에 연결하도록 네트워크를 신뢰할 수 있습니다. 서버 SSL 인증서 유효성 검사가 필요하지 않습니다. |
| `verify-ca` | 예 | CA 정책에 따라 다릅니다 | 모든 통신에서 암호화가 필요합니다. 데이터를 공유하려면 먼저 서버 유효성 검사가 필요합니다. 이렇게 하려면 루트 인증서를 [!DNL PostgreSQL] 홈 디렉토리. [자세한 내용은 아래에 나와 있습니다](#instructions) |
| `verify-full` | 예 | 예 | 모든 통신에서 암호화가 필요합니다. 데이터를 공유하려면 먼저 서버 유효성 검사가 필요합니다. 이렇게 하려면 루트 인증서를 [!DNL PostgreSQL] 홈 디렉토리. [자세한 내용은 아래에 나와 있습니다](#instructions). |

>[!NOTE]
>
>차이점 `verify-ca` 및 `verify-full` 루트 CA(인증 기관)의 정책에 따라 다릅니다. 고유한 로컬 CA를 만들어 `verify-ca` 종종 충분한 보호를 제공합니다. 공용 CA를 사용하는 경우, `verify-ca` 다른 사람이 CA에 등록한 서버에 대한 연결을 허용합니다. `verify-full` 는 항상 공개 루트 CA와 함께 사용해야 합니다.

Platform 데이터베이스에 타사 연결을 설정할 때는 `sslmode=require` 적어도 이동 중인 데이터의 보안 연결을 보장합니다. 다음 `verify-full` SSL 모드는 대부분의 보안에 민감한 환경에서 사용하는 것이 좋습니다.

## 서버 확인을 위한 루트 인증서 설정 {#root-certificate}

보안 연결을 보장하려면 연결을 수행하기 전에 클라이언트와 서버 모두에서 SSL 사용을 구성해야 합니다. SSL이 서버에만 구성된 경우, 서버가 높은 보안을 요구하도록 설정하기 전에 클라이언트가 암호와 같은 중요한 정보를 전송할 수 있습니다.

기본적으로 [!DNL PostgreSQL] 서버 인증서 확인을 수행하지 않습니다. 중요한 데이터가 전송되기 전에(SSL의 일부로) 서버의 ID를 확인하고 보안 연결을 확인합니다 `verify-full` 모드)이면 로컬 컴퓨터에 루트(자체 서명) 인증서를 배치해야 합니다(`root.crt`) 및 서버의 루트 인증서에 의해 서명된 리프 인증서

만약 `sslmode` 매개 변수가 `verify-full`, libpq는 클라이언트에 저장된 루트 인증서까지 인증서 체인을 확인하여 서버가 신뢰할 수 있는지 확인합니다. 그런 다음 호스트 이름이 서버 인증서에 저장된 이름과 일치하는지 확인합니다.

서버 인증서 확인을 허용하려면 하나 이상의 루트 인증서(`root.crt`)을 클릭하여 제품에서 사용할 수 있습니다. [!DNL PostgreSQL] 파일을 홈 디렉토리에 저장합니다. 파일 경로는 다음과 비슷합니다 `~/.postgresql/root.crt`.

## 타사에서 사용할 수 있도록 verify-full SSL 모드 활성화 [!DNL Query Service] 연결 {#instructions}

보다 엄격한 보안 관리가 필요한 경우 `sslmode=require`로 지정하는 경우 강조 표시된 단계에 따라 타사 클라이언트를 연결할 수 있습니다 [!DNL Query Service] 사용 `verify-full` SSL 모드.

>[!NOTE]
>
>SSL 인증서를 획득하기 위한 다양한 옵션이 있습니다. 불량 인증서의 트렌드가 점차 증가하고 있으므로 DigiCert는 높은 보증 TLS/SSL, PKI, IoT 및 서명 솔루션을 제공하는 신뢰할 수 있는 글로벌 공급자이므로 이 안내서에서 사용됩니다.

1. 다음으로 이동 [사용 가능한 DigiCert 루트 인증서 목록](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. &quot; 검색[!DNL DigiCert Global Root CA]사용 가능한 인증서 목록에서 &quot;를 클릭합니다.
1. 선택 [!DNL **PEM 다운로드**] 파일을 로컬 컴퓨터에 다운로드하려면 다음을 수행하십시오.
   ![다운로드 PEM이 강조 표시된 사용 가능한 DigiCert 루트 인증서 목록입니다.](../images/clients/ssl-modes/digicert.png)
1. 보안 인증서 파일의 이름을 다음으로 변경합니다. `root.crt`.
1. 파일에 복사 [!DNL PostgreSQL] 폴더를 입력합니다. 필요한 파일 경로는 운영 체제에 따라 다릅니다. 폴더가 아직 없으면 폴더를 만듭니다.
   - macOS을 사용하는 경우 경로는 입니다 `/Users/<username>/.postgresql`
   - Windows를 사용하는 경우 경로는 `%appdata%\postgresql`

>[!TIP]
>
>을(를) 찾으려면 `%appdata%` Windows 운영 체제의 파일 위치를 ⊞ **Win + R** 및 입력 `%appdata%` 검색 필드에 입력할 수 있습니다.

다음 이후 [!DNL DigiCert Global Root CA] CRT 파일은 [!DNL PostgreSQL] 폴더, 연결 [!DNL Query Service] 사용 `sslmode=verify-full` 또는 `sslmode=verify-ca` 선택 사항입니다.

## 다음 단계

이 문서를 읽은 후에는 타사 클라이언트를 연결할 수 있는 사용 가능한 SSL 옵션을 더 잘 이해할 수 있습니다 [!DNL Query Service], 및 를 사용하여 `verify-full` 움직임으로 데이터를 암호화하는 SSL 옵션.

아직 수행하지 않았다면 다음 지침을 따르십시오. [타사 클라이언트를에 연결 [!DNL Query Service]](./overview.md).
