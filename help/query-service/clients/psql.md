---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PSQL과 연결
topic: connect
translation-type: tm+mt
source-git-commit: 8310204071375a55329f661c9ac678f96979a594

---


# PSQL과 연결

PSQL 파섹 다음 지침에 따라 설치할 수 있습니다.

## Mac에 게시물 설치

터미널 창을 열고 다음 세 가지 명령을 실행합니다.

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

이러한 명령을 실행한 후 다음을 볼 수 있습니다.

```shell
/usr/local/bin/psql
```

## PC에 게시물 설치

이 [위치에서](https://www.postgresql.org/download/windows/)게시물을 다운로드하고 설치합니다.

경로 변수 편집:

![이미지](../images/clients/psql/path.png)

&quot;Postgres&quot;가 포함된 두 줄을 추가합니다.

업데이트를 저장한 다음 명령 프롬프트를 열고 다음을 입력합니다.

```shell
psql -V
```

다음과 같은 것이 표시됩니다.

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL 및 쿼리 서비스

&quot;Connect BI 도구&quot; 페이지에서 플랫폼 UI로 돌아갑니다.

&quot;PSQL 명령&quot;에 대한 **복사를** 클릭합니다.

![이미지](../images/clients/psql/connect-bi.png)

> [!IMPORTANT]:PC를 사용하는 경우 텍스트 편집기를 사용하여 명령 문자열에서 줄 바꿈을 제거한 다음 문자열을 복사합니다.

명령 문자열을 터미널 또는 명령 창에 붙여 넣고 Enter 키를 누릅니다.

다음과 같은 결과가 표시됩니다.

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

버전 10.5 이상이 표시되지 않으면 해당 버전 이상을 다운로드해야 합니다.