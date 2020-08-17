---
keywords: Experience Platform;home;popular topics;PSQL;psql
solution: Experience Platform
title: 메타데이터 명령
topic: metadata
description: 메타데이터 쿼리를 위해 현재 지원되는 PSQL 명령 목록입니다.
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 메타데이터 명령

데이터 세트에 대한 메타데이터의 경우 현재 쿼리를 위해 다음 PSQL 명령이 지원됩니다.

>[!NOTE]
>
>아래 나열된 명령은 대/소문자를 구분합니다.

| 명령 | 설명 |
|------- | ------------|
| `\conninfo` | 현재 데이터베이스 연결에 대한 정보를 출력합니다. |
| `\d` | 보이는 모든 테이블, 뷰, 구체화된 뷰, 시퀀스 및 외래 테이블 목록을 표시합니다. |
| `\dE` | 외래 테이블 목록을 표시합니다. |
| `\df or \df+` | 함수 목록을 표시합니다. |
| `\di` | 인덱스 목록을 표시합니다. |
| `\dm` | 구체화된 뷰 목록을 표시합니다. |
| `\dn` | 스키마(네임스페이스) 목록을 표시합니다. |
| `\ds` | 시퀀스 목록을 표시합니다. |
| `\dS` | PostgreSQL 정의 테이블 목록을 표시합니다. |
| `\dt` | 표 목록을 표시합니다. |
| `\dT` | 데이터 유형 목록을 표시합니다. |
| `\dv` | 보기 목록을 표시합니다. |
| `\encoding` | 현재 클라이언트 문자 집합 인코딩을 나열합니다. |
| `\errverbose` | 가장 최근 서버 오류 메시지를 최대 단위로 반복합니다. |
| `\l or \list` | 서버의 데이터베이스 목록을 표시합니다. |
| `\set` | 모든 현재 psql 변수의 이름과 값을 표시합니다. |
| `\showtables` | 다음 정보를 표시합니다. <br>name:테이블을 참조할 이름입니다.<br>datasetId:저장된 데이터 세트의 ID입니다.<br>dataset:저장된 데이터 세트의 이름입니다.<br>description:데이터 세트에 대한 설명입니다.<br>해결됨:현재 세션에서 데이터 세트를 해결할지 여부를 나타내는 부울 값입니다. |
| `\timing` | 표시 간을 전환합니다. 디스플레이는 밀리초 단위로 표시됩니다. 1초를 초과하는 간격은 분:초 형식으로 표시되며 필요한 경우 시간 및 일 필드가 추가됩니다. |

로 시작하는 모든 명령을 결합할 `\d` 수 있습니다. 예를 들어 모든 테이블, 시퀀스 및 스키마 목록 `\dtsn` 을 표시하는 문제를 해결할 수 있습니다. `\d` 기본적으로 표시되는 모든 테이블, 뷰, 구체화된 뷰 및 시퀀스를 보여줍니다.

위에 나열된 명령에 대한 자세한 내용은 [postgresql.org의 설명서를 참조하십시오](https://www.postgresql.org/docs/10/app-psql.html). 그러나 PostgreSQL 설명서에 표시된 일부 옵션은 지원되지 않습니다 [!DNL Experience Platform].

