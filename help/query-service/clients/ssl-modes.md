---
keywords: Experience Platform;홈;자주 찾는 항목;쿼리 서비스;쿼리 서비스;연결;쿼리 서비스에 연결;SSL;SSL;SSLMODE;
title: 쿼리 서비스 SSL 옵션
description: Adobe Experience Platform 쿼리 서비스에 대한 서드파티 연결에 대한 SSL 지원과 전체 SSL 확인 모드를 사용하여 연결하는 방법에 대해 알아봅니다.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 37c30fc1a040efbce0c221c10b36e105d5b1a962
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 1%

---

# [!DNL Query Service] SSL 옵션

보안 강화를 위해 Adobe Experience Platform [!DNL Query Service]에서는 클라이언트/서버 통신을 암호화하기 위한 SSL 연결을 기본적으로 지원합니다. 이 문서에서는 [!DNL Query Service]에 대한 타사 클라이언트 연결에 사용할 수 있는 SSL 옵션과 `verify-full` SSL 매개 변수 값을 사용하여 연결하는 방법에 대해 설명합니다.

## 전제 조건

이 문서에서는 사용자가 플랫폼 데이터에 사용할 타사 데스크탑 클라이언트 애플리케이션을 이미 다운로드했다고 가정합니다. 타사 클라이언트와 연결할 때 SSL 보안을 통합하는 방법에 대한 특정 지침은 해당 연결 안내서 설명서에서 찾을 수 있습니다. 지원되는 모든 클라이언트 [!DNL Query Service]개의 목록에 대해서는 [클라이언트 연결 개요](./overview.md)를 참조하십시오.

## 사용 가능한 SSL 옵션 {#available-ssl-options}

플랫폼은 사용자의 데이터 보안 요구 사항에 맞게 다양한 SSL 옵션을 지원하며 암호화 및 키 교환의 처리 오버헤드를 조정합니다.

서로 다른 `sslmode` 매개 변수 값은 서로 다른 보호 수준을 제공합니다. SSL 인증서로 데이터를 암호화하면 &quot;중간자&quot;(MITM) 공격, 도청 및 가장을 방지하는 데 도움이 됩니다. 아래 표는 사용 가능한 다양한 SSL 모드와 이들이 제공하는 보호 수준에 대한 분류를 제공합니다.

>[!NOTE]
>
> 필수 데이터 보호 규정 준수로 인해 Adobe Experience Platform에서 SSL 값 `disable`을(를) 지원하지 않습니다.

| sslmode | 도청 보호 | MITM 보호 | 설명 |
|---|---|---|---|
| `allow` | 예 | 아니요 | 암호화는 모든 통신에 필요합니다. 네트워크가 올바른 서버에 연결할 수 있도록 트러스트됩니다. |
| `prefer` | 예 | 아니요 | 암호화는 모든 통신에 필요합니다. 네트워크가 올바른 서버에 연결할 수 있도록 트러스트됩니다. |
| `require` | 예 | 아니요 | 암호화는 모든 통신에 필요합니다. 네트워크가 올바른 서버에 연결할 수 있도록 트러스트됩니다. 서버 SSL 인증서 유효성 검사가 필요하지 않습니다. |
| `verify-ca` | 예 | CA 정책에 따라 다름 | 암호화는 모든 통신에 필요합니다. 데이터를 공유하려면 서버 유효성 검사가 필요합니다. [!DNL PostgreSQL] 홈 디렉터리에 루트 인증서를 설정해야 합니다. [자세한 내용은 아래에 있습니다](#instructions) |
| `verify-full` | 예 | 예 | 암호화는 모든 통신에 필요합니다. 데이터를 공유하려면 서버 유효성 검사가 필요합니다. [!DNL PostgreSQL] 홈 디렉터리에 루트 인증서를 설정해야 합니다. [자세한 내용은 아래에 있습니다](#instructions). |

>[!NOTE]
>
>`verify-ca`과(와) `verify-full`의 차이는 루트 CA(인증 기관)의 정책에 따라 다릅니다. 응용 프로그램에 대한 개인 인증서를 발급할 수 있도록 고유한 로컬 CA를 만든 경우 `verify-ca`을(를) 사용하면 충분한 보호 기능이 제공됩니다. 공용 CA를 사용하는 경우 `verify-ca`에서 다른 사람이 CA에 등록한 서버에 연결할 수 있습니다. `verify-full`은(는) 항상 공용 루트 CA와 함께 사용해야 합니다.

Platform 데이터베이스에 대한 서드파티 연결을 설정할 때는 최소한 `sslmode=require`을(를) 사용하여 동작 중인 데이터에 대한 보안 연결을 확인하는 것이 좋습니다. `verify-full` SSL 모드는 대부분의 보안 중요 환경에서 사용하는 것이 좋습니다.

## 서버 확인을 위한 루트 인증서 설정 {#root-certificate}

>[!IMPORTANT]
>
>Query Service 대화형 Postgres API에 대한 프로덕션 환경의 TLS/SSL 인증서는 2024년 1월 24일 수요일에 새로 고쳐졌습니다.<br>연간 요구 사항이지만 Adobe의 TLS/SSL 인증서 공급자가 인증서 계층 구조를 업데이트함에 따라 체인의 루트 인증서도 변경되었습니다. 인증서 기관 목록에 루트 인증서가 누락된 경우 특정 Postgres 클라이언트에 영향을 줄 수 있습니다. 예를 들어 PSQL CLI 클라이언트는 루트 인증서를 명시적 파일 `~/postgresql/root.crt`에 추가해야 할 수 있습니다. 그렇지 않으면 오류가 발생할 수 있습니다. 예, `psql: error: SSL error: certificate verify failed`. 이 문제에 대한 자세한 내용은 [공식 PostgreSQL 설명서](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES)를 참조하십시오.<br>추가할 루트 인증서를 [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem)에서 다운로드할 수 있습니다.

보안 연결을 보장하려면 연결이 이루어지기 전에 클라이언트와 서버 모두에서 SSL 사용을 구성해야 합니다. SSL이 서버에만 구성된 경우 클라이언트는 서버가 높은 보안을 요구하도록 설정하기 전에 암호와 같은 중요한 정보를 전송할 수 있습니다.

기본적으로 [!DNL PostgreSQL]은(는) 서버 인증서 확인을 수행하지 않습니다. SSL `verify-full` 모드의 일부로 중요한 데이터를 보내기 전에 서버 ID를 확인하고 보안 연결을 확인하려면 로컬 컴퓨터(`root.crt`)에 루트(자체 서명된) 인증서를 배치하고 서버에 루트 인증서로 서명된 리프 인증서를 배치해야 합니다.

`sslmode` 매개 변수가 `verify-full`(으)로 설정된 경우 libpq는 클라이언트에 저장된 루트 인증서까지의 인증서 체인을 확인하여 서버를 신뢰할 수 있는지 확인합니다. 그런 다음 호스트 이름이 서버 인증서에 저장된 이름과 일치하는지 확인합니다.

서버 인증서 확인을 허용하려면 홈 디렉터리의 [!DNL PostgreSQL] 파일에 하나 이상의 루트 인증서(`root.crt`)를 배치해야 합니다. 파일 경로는 `~/.postgresql/root.crt`과(와) 비슷합니다.

## 타사 [!DNL Query Service] 연결에 사용할 수 있도록 전체 확인 SSL 모드 활성화 {#instructions}

`sslmode=require`보다 엄격한 보안 제어가 필요한 경우 강조 표시된 단계에 따라 `verify-full` SSL 모드를 사용하여 [!DNL Query Service]에 타사 클라이언트를 연결할 수 있습니다.

>[!NOTE]
>
>SSL 인증서를 얻는 데 사용할 수 있는 옵션은 여러 가지가 있습니다. 악성 인증서의 증가 추세로 인해 DigiCert는 높은 보증 TLS/SSL, PKI, IoT 및 서명 솔루션의 신뢰할 수 있는 글로벌 공급자이므로 이 안내서에서 사용됩니다.

1. [사용 가능한 DigiCert 루트 인증서 목록으로 이동](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. 사용 가능한 인증서 목록에서 &quot;[!DNL DigiCert Global Root G2]&quot;을(를) 검색합니다.
1. [!DNL **PEM 다운로드**]를 선택하여 로컬 컴퓨터에 파일을 다운로드합니다.
   ![다운로드 PEM이 강조 표시된 사용 가능한 DigiCert 루트 인증서 목록입니다.](../images/clients/ssl-modes/digicert.png)
1. 보안 인증서 파일의 이름을 `root.crt`(으)로 바꾸십시오.
1. 파일을 [!DNL PostgreSQL] 폴더에 복사합니다. 필요한 파일 경로는 운영 체제에 따라 다릅니다. 폴더가 아직 존재하지 않는 경우 폴더를 만듭니다.
   - macOS을 사용하는 경우 경로는 `/Users/<username>/.postgresql`입니다.
   - Windows를 사용하는 경우 경로는 `%appdata%\postgresql`입니다.

>[!TIP]
>
>Windows 운영 체제에서 `%appdata%` 파일 위치를 찾으려면 ⊞ **Win + R**&#x200B;을 누르고 검색 필드에 `%appdata%`을(를) 입력하십시오.

[!DNL DigiCert Global Root G2] CRT 파일을 [!DNL PostgreSQL] 폴더에서 사용할 수 있게 되면 `sslmode=verify-full` 또는 `sslmode=verify-ca` 옵션을 사용하여 [!DNL Query Service]에 연결할 수 있습니다.

## 다음 단계

이 문서를 읽으면 타사 클라이언트를 [!DNL Query Service]에 연결하는 데 사용할 수 있는 SSL 옵션과 `verify-full` SSL 옵션을 활성화하여 사용 중인 데이터를 암호화하는 방법에 대해 더 잘 이해할 수 있습니다.

아직 수행하지 않았다면 [타사 클라이언트를  [!DNL Query Service]](./overview.md)에 연결하는 방법에 대한 지침을 따르십시오.
