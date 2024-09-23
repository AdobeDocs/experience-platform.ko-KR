---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;Power BI;power bi;쿼리 서비스에 연결;
solution: Experience Platform
title: 쿼리 서비스에 Power BI 연결
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스와 Power BI을 연결하는 단계를 안내합니다.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 2b76b99d1e22d75faf8d758edd6cf08acdec7c21
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL Power BI] 연결

이 문서에서는 [!DNL Power BI] 데스크톱을 Adobe Experience Platform 쿼리 서비스와 연결하는 단계에 대해 설명합니다.

## 시작하기

이 안내서를 사용하려면 이미 [!DNL Power BI] 데스크톱 앱에 액세스할 수 있어야 하며 해당 인터페이스를 탐색하는 방법에 익숙해야 합니다. [!DNL Power BI] 데스크톱을 다운로드하거나 자세한 내용은 [공식 [!DNL Power BI] 설명서](https://docs.microsoft.com/ko-kr/power-bi/)를 참조하세요.

>[!IMPORTANT]
>
> [!DNL Power BI] 데스크톱 응용 프로그램은 Windows 장치에서 **전용**&#x200B;입니다.

[!DNL Power BI]을(를) Experience Platform에 연결하는 데 필요한 자격 증명을 획득하려면 Platform UI에서 쿼리 작업 영역에 액세스할 수 있어야 합니다. 현재 쿼리 작업 영역에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오.

## 쿼리 서비스에 [!DNL Power BI] 연결 {#connect-power-bi}

[!DNL Power BI]을(를) 쿼리 서비스에 연결하려면 [!DNL Power BI]을(를) 열고 상단 메뉴 리본에서 **[!DNL Get Data]**&#x200B;을(를) 선택하십시오. 그런 다음 검색 막대에 &quot;[!DNL PostgreSQL]&quot;을(를) 입력하여 데이터 원본 목록의 범위를 좁힙니다. 표시되는 결과에서 **[!DNL PostgreSQL database]**&#x200B;을(를) 선택한 후 **[!DNL Connect]**&#x200B;을(를) 선택합니다.

서버 및 데이터베이스에 대한 값을 요청하는 [!DNL PostgreSQL] 데이터베이스 대화 상자가 나타납니다. [Power Query Desktop에서 PostgreSQL 데이터베이스에 연결](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop)하는 방법에 대한 추가 지침은 공식 [!DNL PowerBI] 설명서에서 찾을 수 있습니다.

이러한 필수 값은 Adobe Experience Platform 자격 증명에서 가져옵니다. 자격 증명을 찾으려면 Platform UI에 로그인하고 왼쪽 탐색에서 **[!UICONTROL 쿼리]**&#x200B;를 선택한 다음 **[!UICONTROL 자격 증명]**&#x200B;을 선택하십시오. 데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오.

>[!IMPORTANT]
>
>Power BI 또는 Tableau 사용자는 쿼리 서비스 자격 증명 탭에서 Customer Journey Analytics을 BI 도구에 연결할 수 있습니다. [BI 도구를 Customer Journey Analytics에 연결](../ui/credentials.md#connect-to-customer-journey-analytics)하는 방법에 대한 지침은 자격 증명 설명서를 참조하세요.

![자격 증명 탭과 만료 자격 증명이 강조 표시된 Experience Platform 쿼리 작업 영역입니다.](../images/clients/power-bi/query-service-credentials-page.png)

[!DNL PostgreSQL database] 대화 상자의 **[!DNL Server]** 필드에 쿼리 서비스 [!UICONTROL 자격 증명] 섹션에 있는 호스트의 값을 입력하십시오. 프로덕션의 경우 호스트 문자열 끝에 `:80` 포트를 추가하십시오. 예: `made-up.platform-query.adobe.io:80`.

**[!DNL Database]** 필드는 &quot;all&quot; 또는 데이터 집합 테이블 이름일 수 있습니다. 예: `prod:all`.

>[!IMPORTANT]
>
>타사 BI 도구의 중첩된 데이터 구조를 병합하여 사용성을 개선하고 데이터를 검색, 분석, 변환 및 보고하는 데 필요한 워크로드를 줄일 수 있습니다. 데이터베이스에 연결할 때 이 설정을 활성화하는 방법에 대한 지침은 [`FLATTEN` 기능](../key-concepts/flatten-nested-data.md)에 대한 설명서를 참조하십시오.

### 데이터 연결 모드 {#data-connectivity-mode}

다음으로 **[!DNL Data Connectivity mode]**&#x200B;을(를) 선택할 수 있습니다. [!DNL PostgreSQL database] 대화 상자에서 **[!DNL Import]**, **[!DNL OK]**&#x200B;을(를) 차례로 선택하여 사용 가능한 모든 테이블 목록을 표시하거나 **[!DNL DirectQuery]**&#x200B;을(를) 선택하여 [!DNL Power BI](으)로 직접 데이터를 가져오거나 복사하지 않고 데이터 원본을 직접 쿼리합니다.

**[!DNL Import]** 모드에 대한 자세한 내용은 [테이블 가져오기](#import)에 대한 섹션을 참조하십시오. **[!DNL DirectQuery]** 모드에 대한 자세한 내용은 [데이터를 가져오지 않고 데이터 집합 쿼리](#direct-query)에 대한 섹션을 참조하십시오.

데이터베이스 세부 정보를 확인한 후 **[!DNL OK]**&#x200B;을(를) 선택하십시오.

### 인증 {#authentication}

데이터 연결 모드를 확인하면 사용자 이름, 암호 및 애플리케이션 설정을 묻는 메시지가 나타납니다. 이 경우 사용자 이름은 조직 ID이고 암호는 인증 토큰입니다. 둘 다 [쿼리 서비스 자격 증명] 페이지에서 찾을 수 있습니다.

이 세부 정보를 입력한 다음 **[!DNL Connect]**&#x200B;을(를) 선택하여 다음 단계로 진행합니다.

## 표 가져오기 {#import}

**[!DNL Import]** [!DNL Data Connectivity mode]을(를) 선택하면 [!DNL Power BI] 데스크톱 응용 프로그램에서 선택한 테이블 및 열을 그대로 사용할 수 있는 전체 데이터 집합을 가져옵니다.

>[!IMPORTANT]
>
>초기 가져오기 이후 발생한 데이터 변경 사항을 보려면 전체 데이터 세트를 다시 가져와서 [!DNL Power BI] 내의 데이터를 새로 고쳐야 합니다.

테이블을 가져오려면 서버 및 데이터베이스 세부 정보 [을(를) 위에서 설명한 대로 ](#connect-power-bi)입력하고 **[!DNL Import]** [!DNL Data Connectivity mode], **[!DNL OK]**&#x200B;을(를) 선택하십시오. 사용 가능한 모든 테이블 목록이 표시된 [!DNL Navigator] 대화 상자가 나타납니다. 미리 보려는 테이블을 선택한 다음 **[!DNL Load]**&#x200B;을(를) 선택하여 데이터 집합을 Power BI으로 가져옵니다. 이제 테이블을 [!DNL Power BI](으)로 가져왔습니다.

[PowerBi Desktop의 데이터에 연결하는 방법에 대한 일반 정보](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) 앱은 공식 문서에서 확인할 수 있습니다.

### 사용자 지정 SQL을 사용하여 테이블 가져오기

[!DNL Power BI] 및 [!DNL Tableau]과(와) 같은 다른 타사 도구는 현재 사용자가 플랫폼의 XDM 개체와 같은 중첩 개체를 가져올 수 없습니다. 이러한 문제를 해결하기 위해 [!DNL Power BI]에서는 사용자 지정 SQL을 사용하여 이러한 중첩 필드에 액세스하고 데이터의 병합된 보기를 만들 수 있습니다. 그런 다음 [!DNL Power BI]은(는) 이전에 중첩된 데이터의 이 병합된 보기를 일반 테이블로 로드합니다.

[!DNL PostgreSQL database] 대화 상자에서 **[!DNL Advanced options]**&#x200B;을(를) 선택하여 **[!DNL SQL statement]** 섹션에 사용자 지정 SQL 쿼리를 입력합니다. 이 사용자 지정 쿼리는 JSON 이름-값 쌍을 테이블 형식으로 병합하는 데 사용해야 합니다. 공식 설명서는 고급 옵션에서 SQL 문을 사용하여 [PowerBI를 연결](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options)하는 방법에 대한 정보도 제공합니다.

사용자 지정 쿼리를 입력한 후 **[!DNL OK]**&#x200B;을(를) 선택하여 데이터베이스 연결을 계속합니다. 이 워크플로우 부분에서 데이터베이스 연결에 대한 지침은 위의 [인증](#authentication) 섹션을 참조하십시오.

인증이 완료되면 병합된 데이터의 미리 보기가 [!DNL Power BI] 데스크톱 대시보드에 표로 나타납니다. 대화 상자 맨 위에 서버 및 데이터베이스 이름이 나열됩니다. 가져오기 프로세스를 완료하려면 **[!DNL Load]**&#x200B;을(를) 선택하십시오.

이제 [!DNL Power BI] 데스크톱 앱에서 시각화를 편집하고 내보낼 수 있습니다.

## 데이터를 가져오지 않고 데이터 세트 쿼리 {#direct-query}

**[!DNL DirectQuery]** [!DNL Data Connectivity mode]이(가) 데이터를 [!DNL Power BI] 데스크톱으로 가져오거나 복사하지 않고 데이터 원본을 직접 쿼리합니다. 이 연결 모드를 사용하면 UI를 통해 현재 데이터로 모든 시각화를 새로 고칠 수 있습니다. 그러나 시각화를 생성하거나 새로 고치는 데 필요한 시간은 기본 데이터 소스의 성능에 따라 달라집니다.

[사용 [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery)에 대한 자세한 정보와 [연결 옵션, 사용 사례 및 제한 사항에 대한 포괄적인 토론](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about)은 공식 [!DNL PowerBI] 문서에서 확인할 수 있습니다.

이 [!DNL Data Connectivity mode]을(를) 사용하려면 **[!DNL DirectQuery]** 토글을 선택한 다음 **[!DNL Advanced options]**&#x200B;을(를) 선택하여 **[!DNL SQL statement]** 섹션에 사용자 지정 SQL 쿼리를 입력하십시오. **[!DNL Include relationship columns]**&#x200B;을(를) 선택했는지 확인하십시오. 쿼리를 완료했으면 **[!DNL OK]**&#x200B;을(를) 선택하여 계속합니다.

쿼리의 미리보기가 나타납니다. 쿼리 결과를 보려면 **[!DNL Load]**&#x200B;을(를) 선택하십시오.

## 다음 단계

이 문서를 읽으면 이제 [!DNL Power BI] 데스크톱 앱에 연결하는 방법과 사용 가능한 여러 데이터 연결 모드를 이해할 수 있습니다. 쿼리를 작성하여 실행하는 방법에 대한 자세한 내용은 [쿼리 실행에 대한 지침](../best-practices/writing-queries.md)을 참조하세요.
