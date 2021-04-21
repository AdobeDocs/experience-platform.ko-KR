---
keywords: Experience Platform;홈;인기 항목;PSQL;쿼리 서비스;쿼리 서비스;메타데이터;명령;메타데이터 명령;메타데이터 명령
solution: Experience Platform
title: 쿼리 서비스의 메타데이터 PostgreSQL 명령
topic-legacy: metadata
description: Adobe Experience Platform 쿼리 서비스에서 메타데이터를 쿼리하는 데 현재 지원되는 PostgreSQL 명령 목록입니다.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 쿼리 서비스의 메타데이터 PostgreSQL 명령

데이터 세트에 대한 메타데이터의 경우 현재 쿼리를 위해 다음 PostgreSQL 명령이 지원됩니다.

>[!NOTE]
>
>아래 나열된 명령은 대/소문자를 구분합니다.

| 명령 | 설명 |
|------- | ------------|
| `\conninfo` | 현재 데이터베이스 연결에 대한 정보를 출력합니다. |
| `\d` | 보이는 모든 테이블, 뷰, 구체화된 뷰, 시퀀스 및 외래 테이블의 목록을 표시합니다. |
| `\dE` | 외래 테이블 목록을 표시합니다. |
| `\df or \df+` | 함수 목록을 표시합니다. |
| `\di` | 인덱스 목록을 표시합니다. |
| `\dm` | 구체화된 뷰 목록을 표시합니다. |
| `\dn` | 스키마(네임스페이스) 목록을 표시합니다. |
| `\ds` | 시퀀스 목록을 표시합니다. |
| `\dS` | PostgreSQL 정의 테이블 목록을 표시합니다. |
| `\dt` | 테이블 목록을 표시합니다. |
| `\dT` | 데이터 유형 목록을 표시합니다. |
| `\dv` | 보기 목록을 표시합니다. |
| `\encoding` | 현재 클라이언트 문자 집합 인코딩을 나열합니다. |
| `\errverbose` | 가장 최근 서버 오류 메시지를 최대 단위로 반복합니다. |
| `\l or \list` | 서버에 데이터베이스 목록을 표시합니다. |
| `\set` | 모든 현재 psql 변수의 이름 및 값을 표시합니다. |
| `\showtables` | 다음 정보를 표시합니다.<br>이름:테이블을 참조하는 이름입니다.<br>datasetId:저장되는 데이터 세트의 ID입니다.<br>데이터 세트:저장되는 데이터 세트의 이름입니다.<br>description:데이터 세트에 대한 설명입니다.<br>해결:현재 세션에서 데이터 세트를 확인할지 여부를 나타내는 부울 값입니다. |
| `\timing` | 표시 간을 전환합니다. 디스플레이는 밀리초 단위로 표시됩니다. 1초보다 긴 간격은 분:초 형식으로 표시되며 필요한 경우 시간 및 일 필드가 추가됩니다. |

`\d`으로 시작하는 모든 명령을 결합할 수 있습니다. 예를 들어 `\dtsn`을 발행하여 모든 테이블, 시퀀스 및 스키마 목록을 표시할 수 있습니다. `\d` 그 자체는 모든 보이는 테이블, 뷰, 구체화된 뷰 및 시퀀스를 보여줍니다.

위에 나열된 명령에 대한 자세한 내용은 [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html)의 설명서를 참조하십시오. 그러나 PostgreSQL 설명서에 표시된 일부 옵션은 [!DNL Experience Platform]에서 지원되지 않습니다.
