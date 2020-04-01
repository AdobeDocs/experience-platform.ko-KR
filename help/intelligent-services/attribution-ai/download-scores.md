---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: 기여도 AI에서 점수 액세스
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 689b4c7a96856e1167ee435a6740fed006136256

---


# 기여도 AI에서 점수 액세스

>[!IMPORTANT] 데이터 대량 내보내기를 위한 원시 점수 다운로드에 대한 자세한 내용은 attributionai-support@adobe.com에 문의하십시오.

기여도 AI에 대한 점수에 액세스하는 작업은 Snowflake를 통해 수행됩니다. 현재, Adobe 지원을 attributionai-support@adobe.com에서 이메일로 전송하여 Snowflake에 대한 자격 증명을 설정하고 귀하의 리더 계정에 수신해야 합니다.

Adobe 지원이 요청을 처리하면 Snowflake에 대한 Reader 계정 및 아래 해당 자격 증명에 대한 URL이 제공됩니다.

- 눈송이 URL
- 사용자 이름
- 암호

>[!NOTE] Reader 계정은 JDBC 커넥터를 지원하는 SQL 클라이언트, 워크시트 및 BI 솔루션을 사용하여 데이터를 쿼리하는 것입니다.

자격 증명과 URL이 있으면 모델 테이블을 원시 형식(터치포인트 날짜 또는 전환 날짜별로 집계됨)으로 질의할 수 있습니다.

## Snowflake에서 스키마 찾기

제공된 자격 증명을 사용하여 Snowflake에 로그인합니다. 왼쪽 **위** 주 탐색에서 워크시트 탭을 클릭한 다음 왼쪽 패널에서 데이터베이스 디렉토리로 이동합니다.

![워크시트 및 탐색](./images/download-scores/edited_snowflake_1.png)

그런 다음 **화면의 오른쪽** 상단 모서리에서 스키마 선택을 클릭합니다. 이 팝업 창에서 올바른 데이터베이스를 선택했는지 확인합니다. 그런 다음 스키마 *드롭다운을* 클릭하고 나열된 스키마 중 하나를 선택합니다. 선택한 스키마 아래에 나열된 점수 테이블에서 직접 쿼리할 수 있습니다.

![스키마 찾기](./images/download-scores/edited_snowflake_2.png)

## Raw 스코어 다운로드

원시 점수 다운로드에 대한 자세한 내용은 attributionai-support@adobe.com에 문의하십시오.

## PowerBI를 Snowflake에 연결(선택 사항)

Snowflake 자격 증명을 사용하여 PowerBI Desktop 및 Snowflake 데이터베이스 간의 연결을 설정할 수 있습니다.

먼저 서버 *상자 아래에* Snowflake URL을 입력합니다. 그런 다음 *웨어하우스에서*&quot;XSMALL&quot;을 입력합니다. 그런 다음 사용자 이름과 암호를 입력합니다.

![powerbi 예](./images/download-scores/powerbi-snowflake.png)

연결이 설정되면 Snowflake 데이터베이스를 선택한 다음 적절한 스키마를 선택합니다. 이제 모든 테이블을 로드할 수 있습니다.

스키마를 선택하면 속성 점수가 포함된 테이블이 나타납니다.

| 표 | 설명 |
| ----- | ----------- |
| APP_{APP_ID} | 원시 속성 점수. |
| APP_{APP_ID}_BY_CONV_DATE | 전환 날짜 수준에서 집계된 원시 속성 점수입니다. |
| APP_{APP_ID}_BY_TP_DATE | 터치포인트 날짜 수준에서 집계된 원시 속성 점수입니다. |

## 다음 단계

이 문서에서는 데이터를 쿼리하고 속성 AI에 대한 점수를 액세스하는 데 필요한 단계에 대해 간략하게 설명합니다. 이제 제공되는 다른 [지능형 서비스](../home.md) 및 가이드를 계속 검색할 수 있습니다.