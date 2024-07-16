---
keywords: Experience Platform;홈;인기 주제;쿼리 서비스;쿼리 서비스;연결;쿼리 서비스에 연결;aqua data studio;Aqua Data Studio;Looker;looker;Postico;Postico;Power BI;power bi;psql;studio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: 클라이언트를 쿼리 서비스에 연결
description: 이 문서에서는 다양한 데스크탑 클라이언트 응용 프로그램에서 쿼리 서비스에 연결하는 방법과 해당 연결을 확인하는 방법을 설명합니다.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 클라이언트를 [!DNL Query Service]에 연결

이 단원에서는 다양한 데스크톱 클라이언트 응용 프로그램에서 [!DNL Query Service]에 연결하는 방법과 해당 연결을 확인하는 방법에 대해 설명합니다. [!DNL Query Service]은(는) [!DNL PostgreSQL] 프로토콜을 사용하므로 이 섹션의 지침에서는 [!DNL PostgreSQL] 도구 및 드라이버를 사용하여 쿼리를 연결하고 작성하는 방법에 대해 설명합니다.

>[!IMPORTANT]
>
>Query Service 대화형 Postgres API에 대한 프로덕션 환경의 TLS/SSL 인증서는 2024년 1월 24일 수요일에 새로 고쳐졌습니다.<br>연간 요구 사항이지만 Adobe의 TLS/SSL 인증서 공급자가 인증서 계층 구조를 업데이트함에 따라 체인의 루트 인증서도 변경되었습니다. 인증서 기관 목록에 루트 인증서가 누락된 경우 특정 Postgres 클라이언트에 영향을 줄 수 있습니다. 예를 들어 PSQL CLI 클라이언트는 루트 인증서를 명시적 파일 `~/postgresql/root.crt`에 추가해야 할 수 있습니다. 그렇지 않으면 오류가 발생할 수 있습니다. 예, `psql: error: SSL error: certificate verify failed`. 이 문제에 대한 자세한 내용은 [공식 PostgreSQL 설명서](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES)를 참조하십시오.<br>추가할 루트 인증서를 [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem)에서 다운로드할 수 있습니다.

다음 클라이언트에 대한 지침이 제공됩니다.

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)

>[!IMPORTANT]
>
>Power BI 및 Tableau 사용자는 쿼리 서비스 자격 증명 탭에서 Customer Journey Analytics을 BI 도구에 연결할 수 있습니다. [BI 도구를 Customer Journey Analytics에 연결](../ui/credentials.md#connect-to-customer-journey-analytics)하는 방법에 대한 지침은 자격 증명 설명서를 참조하세요.
