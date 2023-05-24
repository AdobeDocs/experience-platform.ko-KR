---
keywords: Experience Platform;홈;자주 찾는 항목;쿼리 서비스;쿼리 서비스;연결;쿼리 서비스에 연결;SSL;SSL;SSLMODE;
title: 쿼리 서비스 SSL 옵션
description: Adobe Experience Platform 쿼리 서비스에 대한 서드파티 연결에 대한 SSL 지원과 전체 SSL 확인 모드를 사용하여 연결하는 방법에 대해 알아봅니다.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# [!DNL Query Service] SSL 옵션

보안 강화를 위해 Adobe Experience Platform [!DNL Query Service] 는 클라이언트/서버 통신을 암호화하기 위한 SSL 연결에 대한 기본 지원을 제공합니다. 이 문서에서는 타사 클라이언트 연결에 사용할 수 있는 SSL 옵션에 대해 설명합니다. [!DNL Query Service] 및 을 사용하여 연결하는 방법 `verify-full` SSL 매개 변수 값입니다.

## 사전 요구 사항

이 문서에서는 사용자가 플랫폼 데이터에 사용할 타사 데스크탑 클라이언트 애플리케이션을 이미 다운로드했다고 가정합니다. 타사 클라이언트와 연결할 때 SSL 보안을 통합하는 방법에 대한 특정 지침은 해당 연결 안내서 설명서에서 찾을 수 있습니다. 모든 항목 목록 [!DNL Query Service] 지원되는 클라이언트는 다음을 참조하십시오. [클라이언트 연결 개요](./overview.md).

## 사용 가능한 SSL 옵션 {#available-ssl-options}

플랫폼은 사용자의 데이터 보안 요구 사항에 맞게 다양한 SSL 옵션을 지원하며 암호화 및 키 교환의 처리 오버헤드를 조정합니다.

다름 `sslmode` 매개 변수 값은 다양한 보호 수준을 제공합니다. SSL 인증서로 데이터를 암호화하면 &quot;중간자&quot;(MITM) 공격, 도청 및 가장을 방지하는 데 도움이 됩니다. 아래 표는 사용 가능한 다양한 SSL 모드와 이들이 제공하는 보호 수준에 대한 분류를 제공합니다.

>[!NOTE]
>
> SSL 값 `disable` 은(는) 필수 데이터 보호 규정 준수로 인해 Adobe Experience Platform에서 지원하지 않습니다.

| sslmode | 도청 보호 | MITM 보호 | 설명 |
|---|---|---|---|
| `allow` | 부분 | 아니요 | 보안은 우선순위가 아니며 속도와 낮은 처리 오버헤드가 더 중요합니다. 이 모드는 서버에서 요구하는 경우에만 암호화를 선택합니다. |
| `prefer` | 부분 | 아니요 | 암호화는 필요하지 않지만, 서버가 지원하는 경우 통신이 암호화됩니다. |
| `require` | 예 | 아니요 | 암호화는 모든 통신에 필요합니다. 네트워크가 올바른 서버에 연결할 수 있도록 트러스트됩니다. 서버 SSL 인증서 유효성 검사가 필요하지 않습니다. |
| `verify-ca` | 예 | CA 정책에 따라 다름 | 암호화는 모든 통신에 필요합니다. 데이터를 공유하려면 서버 유효성 검사가 필요합니다. 이렇게 하려면에서 루트 인증서를 설정해야 합니다. [!DNL PostgreSQL] 홈 디렉토리. [자세한 내용은 아래에 나와 있습니다](#instructions) |
| `verify-full` | 예 | 예 | 암호화는 모든 통신에 필요합니다. 데이터를 공유하려면 서버 유효성 검사가 필요합니다. 이렇게 하려면에서 루트 인증서를 설정해야 합니다. [!DNL PostgreSQL] 홈 디렉토리. [자세한 내용은 아래에 나와 있습니다](#instructions). |

>[!NOTE]
>
>차이점 `verify-ca` 및 `verify-full` 루트 CA(인증 기관)의 정책에 따라 다릅니다. 애플리케이션에 대한 개인 인증서를 발급하기 위해 고유한 로컬 CA를 만든 경우 다음을 사용하십시오. `verify-ca` 종종 충분한 보호 기능을 제공합니다. 공용 CA를 사용하는 경우 `verify-ca` 다른 사용자가 CA에 등록한 서버에 연결할 수 있도록 허용합니다. `verify-full` 항상 공용 루트 CA와 함께 사용해야 합니다.

Platform 데이터베이스에 대한 서드파티 연결을 설정할 때 다음을 사용하는 것이 좋습니다. `sslmode=require` 최소한 작동 중인 데이터에 대한 보안 연결을 보장합니다. 다음 `verify-full` SSL 모드는 대부분의 보안 중요 환경에서 사용하는 것이 좋습니다.

## 서버 확인을 위한 루트 인증서 설정 {#root-certificate}

보안 연결을 보장하려면 연결이 이루어지기 전에 클라이언트와 서버 모두에서 SSL 사용을 구성해야 합니다. SSL이 서버에만 구성된 경우 클라이언트는 서버가 높은 보안을 요구하도록 설정하기 전에 암호와 같은 중요한 정보를 전송할 수 있습니다.

기본적으로, [!DNL PostgreSQL] 은 서버 인증서의 확인을 수행하지 않습니다. 중요한 데이터가 전송되기 전에(SSL의 일부로) 서버 ID를 확인하고 보안 연결을 보장합니다 `verify-full` 모드), 로컬 컴퓨터에 루트(자체 서명된) 인증서를 배치해야 합니다(`root.crt`)와 서버의 루트 인증서로 서명된 리프 인증서.

다음과 같은 경우 `sslmode` 매개 변수가 로 설정되어 있습니다. `verify-full`, libpq는 클라이언트에 저장된 루트 인증서까지의 인증서 체인을 확인하여 서버를 신뢰할 수 있는지 확인합니다. 그런 다음 호스트 이름이 서버 인증서에 저장된 이름과 일치하는지 확인합니다.

서버 인증서 인증을 허용하려면 하나 이상의 루트 인증서( )를 배치해야 합니다.`root.crt`)에 있는 [!DNL PostgreSQL] 파일을 홈 디렉터리에 저장합니다. 파일 경로는 다음과 유사합니다. `~/.postgresql/root.crt`.

## 서드파티와 함께 사용하기 위해 확인-전체 SSL 모드 활성화 [!DNL Query Service] 연결 {#instructions}

보다 엄격한 보안 관리가 필요한 경우 `sslmode=require`, 강조 표시된 단계에 따라 서드파티 클라이언트를 [!DNL Query Service] 사용 `verify-full` SSL 모드.

>[!NOTE]
>
>SSL 인증서를 얻는 데 사용할 수 있는 옵션은 여러 가지가 있습니다. 악성 인증서의 증가 추세로 인해 DigiCert는 높은 보증 TLS/SSL, PKI, IoT 및 서명 솔루션의 신뢰할 수 있는 글로벌 공급자이므로 이 안내서에서 사용됩니다.

1. 다음으로 이동 [사용 가능한 DigiCert 루트 인증서 목록](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. 검색 대상[!DNL DigiCert Global Root CA]사용 가능한 인증서 목록에서 &quot;를 클릭합니다.
1. 선택 [!DNL **PEM 다운로드**] 로컬 컴퓨터에 파일을 다운로드합니다.
   ![다운로드 PEM이 강조 표시된 사용 가능한 DigiCert 루트 인증서 목록입니다.](../images/clients/ssl-modes/digicert.png)
1. 보안 인증서 파일 이름을 다음으로 변경 `root.crt`.
1. 파일을 [!DNL PostgreSQL] 폴더를 삭제합니다. 필요한 파일 경로는 운영 체제에 따라 다릅니다. 폴더가 아직 존재하지 않는 경우 폴더를 만듭니다.
   - macOS을 사용하는 경우 경로는 다음과 같습니다. `/Users/<username>/.postgresql`
   - Windows를 사용하는 경우 경로는 다음과 같습니다. `%appdata%\postgresql`

>[!TIP]
>
>를 찾으려면 `%appdata%` windows 운영 체제의 파일 위치입니다. 키를 누릅니다⊞ **Win + R** 및 입력 `%appdata%` 을 검색 필드에 추가합니다.

다음 이후 [!DNL DigiCert Global Root CA] CRT 파일은 [!DNL PostgreSQL] 폴더에 연결할 수 있습니다. [!DNL Query Service] 사용 `sslmode=verify-full` 또는 `sslmode=verify-ca` 옵션을 선택합니다.

## 다음 단계

이 문서를 읽고 타사 클라이언트를에 연결하는 데 사용할 수 있는 SSL 옵션을 이해합니다 [!DNL Query Service]및 을 활성화하는 방법 `verify-full` 이동 중인 데이터를 암호화하는 SSL 옵션입니다.

아직 수행하지 않았다면 의 지침을 따르십시오. [타사 클라이언트 연결 [!DNL Query Service]](./overview.md).
