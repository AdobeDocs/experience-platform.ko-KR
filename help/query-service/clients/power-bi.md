---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;Power BI;power bi;쿼리 서비스에 연결;
solution: Experience Platform
title: 쿼리 서비스에 Power BI 연결
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스와 Power BI을 연결하는 단계를 안내합니다.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---

# 연결 [!DNL Power BI] 쿼리 서비스

이 문서에서는 다음 연결 단계를 다룹니다 [!DNL Power BI] Adobe Experience Platform 쿼리 서비스가 포함된 데스크탑.

## 시작하기

이 안내서를 사용하려면 이미 다음 항목에 대한 액세스 권한이 있어야 합니다. [!DNL Power BI] 데스크탑 앱으로 인터페이스를 탐색하는 방법을 잘 알고 있습니다. 다운로드하려면 [!DNL Power BI] 데스크탑 또는 자세한 내용은 [공식 [!DNL Power BI] 설명서](https://docs.microsoft.com/ko-kr/power-bi/).

>[!IMPORTANT]
>
> 다음 [!DNL Power BI] 데스크탑 애플리케이션 **전용** Windows 장치에서 사용할 수 있습니다.

연결에 필요한 자격 증명을 획득하려면 [!DNL Power BI] Experience Platform을 수행하려면 Platform UI에서 쿼리 작업 영역에 액세스할 수 있어야 합니다. 현재 쿼리 작업 영역에 대한 액세스 권한이 없는 경우 조직 관리자에게 문의하십시오.

설치 후 [!DNL Power BI]를 설치해야 합니다. `Npgsql`PostgreSQL용 .NET 드라이버 패키지 Npgsql에 대한 자세한 내용은 [Npgsql 설명서](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>새 버전의 경우 오류가 발생하므로 v4.0.10 이하를 다운로드해야 합니다.

아래에[!DNL Npgsql GAC Installation]사용자 정의 설정 화면에서 다음을 선택합니다. **[!DNL Will be installed on local hard drive]**.

Npgsql이 제대로 설치되었는지 확인하려면 다음 단계를 진행하기 전에 컴퓨터를 다시 시작하십시오.

## 연결 [!DNL Power BI] 쿼리 서비스 {#connect-power-bi}

연결하려면 [!DNL Power BI] Query Service를 열려면 를 엽니다. [!DNL Power BI] 및 선택 **[!DNL Get Data]** 상단 메뉴 리본에서 그런 다음 &quot;[!DNL PostgreSQL]검색 막대에서 &quot;&quot;를 눌러 데이터 소스 목록의 범위를 좁힙니다. 표시되는 결과에서 다음을 선택합니다. **[!DNL PostgreSQL database]**, 그 다음 **[!DNL Connect]**.

다음 [!DNL PostgreSQL] 서버 및 데이터베이스에 대한 값을 요청하는 데이터베이스 대화 상자가 나타납니다. 방법에 대한 추가 지침 [Power Query Desktop에서 PostgreSQL 데이터베이스에 연결](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) 공식 문서에서 찾을 수 있음 [!DNL PowerBI] 설명서를 참조하십시오.

이러한 필수 값은 Adobe Experience Platform 자격 증명에서 가져옵니다. 자격 증명을 찾으려면 Platform UI에 로그인하고 를 선택합니다 **[!UICONTROL 쿼리]** 왼쪽 탐색 후 **[!UICONTROL 자격 증명]**. 데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md).

>[!IMPORTANT]
>
>Power BI 또는 Tableau 사용자는 쿼리 서비스 자격 증명 탭에서 Customer Journey Analytics을 BI 도구에 연결할 수 있습니다. 방법에 대한 지침은 자격 증명 설명서 를 참조하십시오 [BI 도구를 Customer Journey Analytics에 연결](../ui/credentials.md#connect-to-customer-journey-analytics).

![자격 증명 탭과 만료 자격 증명이 강조 표시된 Experience Platform 쿼리 작업 영역입니다.](../images/clients/power-bi/query-service-credentials-page.png)

다음에서 **[!DNL Server]** 필드 [!DNL PostgreSQL database] 대화 상자에서 쿼리 서비스에 있는 호스트의 값을 입력합니다 [!UICONTROL 자격 증명] 섹션. 프로덕션의 경우 포트 추가 `:80` 호스트 문자열의 끝으로 이동합니다. 예: `made-up.platform-query.adobe.io:80`.

다음 **[!DNL Database]** 필드는 &quot;모두&quot; 또는 데이터 세트 테이블 이름일 수 있습니다. 예: `prod:all`.

>[!IMPORTANT]
>
>타사 BI 도구의 중첩된 데이터 구조를 병합하여 사용성을 개선하고 데이터를 검색, 분석, 변환 및 보고하는 데 필요한 워크로드를 줄일 수 있습니다. 다음에서 설명서를 참조하십시오.[`FLATTEN` 기능](../key-concepts/flatten-nested-data.md) 데이터베이스에 연결할 때 이 설정을 활성화하는 방법에 대한 지침입니다.

### 데이터 연결 모드 {#data-connectivity-mode}

다음으로, 다음을 선택할 수 있습니다. **[!DNL Data Connectivity mode]**. 다음에서 [!DNL PostgreSQL database] 대화 상자, 선택 **[!DNL Import]** 뒤에 오는 **[!DNL OK]** 사용 가능한 모든 테이블 목록을 표시하거나 **[!DNL DirectQuery]** 로 직접 데이터를 가져오거나 복사하지 않고 데이터 소스를 직접 쿼리하려면 [!DNL Power BI].

에 대해 자세히 알아보려면 **[!DNL Import]** 모드: 의 섹션을 읽으십시오. [테이블 가져오기](#import). 에 대해 자세히 알아보기 **[!DNL DirectQuery]** 모드: 의 섹션을 읽으십시오. [데이터를 가져오지 않고 데이터 세트 쿼리](#direct-query).

선택 **[!DNL OK]** 데이터베이스 세부 사항을 확인한 후

### 인증 {#authentication}

데이터 연결 모드를 확인하면 사용자 이름, 암호 및 애플리케이션 설정을 묻는 메시지가 나타납니다. 이 경우 사용자 이름은 조직 ID이고 암호는 인증 토큰입니다. 둘 다 [쿼리 서비스 자격 증명] 페이지에서 찾을 수 있습니다.

이 세부 정보를 입력한 다음 선택 **[!DNL Connect]** 을 클릭하여 다음 단계로 이동합니다.

## 표 가져오기 {#import}

을(를) 선택하여 **[!DNL Import]** [!DNL Data Connectivity mode]에서 선택한 테이블 및 열을 사용할 수 있도록 전체 데이터 세트를 가져옵니다. [!DNL Power BI] 데스크탑 애플리케이션 상태 그대로.

>[!IMPORTANT]
>
>초기 가져오기 이후 발생한 데이터 변경 사항을 보려면 내의 데이터를 새로 고쳐야 합니다 [!DNL Power BI] 전체 데이터 세트를 다시 가져와.

테이블을 가져오려면 서버 및 데이터베이스 세부 정보를 입력합니다 [위에서 설명한 바와 같이](#connect-power-bi) 및 선택 **[!DNL Import]** [!DNL Data Connectivity mode], 그 다음 **[!DNL OK]**. 다음 [!DNL Navigator] 사용 가능한 모든 테이블 목록을 표시하는 대화 상자가 나타납니다. 미리 보려는 테이블을 선택한 다음 **[!DNL Load]** Power BI으로 데이터 세트를 가져옵니다. 이제 표를 로 가져옵니다. [!DNL Power BI].

[PowerBi 데스크탑에서 데이터에 연결하는 방법에 대한 일반 정보](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) 앱은 공식 문서에서 찾을 수 있습니다.

### 사용자 지정 SQL을 사용하여 테이블 가져오기

[!DNL Power BI] 및 과 같은 기타 타사 도구 [!DNL Tableau] 현재 에서는 사용자가 Platform의 XDM 개체와 같은 중첩된 개체를 가져올 수 없습니다. 이 문제를 해결하려면, [!DNL Power BI] 사용자 지정 SQL을 사용하여 이러한 중첩된 필드에 액세스하고 데이터의 평면화된 보기를 만들 수 있습니다. [!DNL Power BI] 그런 다음 이전에 중첩된 데이터의 이 병합된 보기를 일반 테이블로 로드합니다.

다음에서 [!DNL PostgreSQL database] 대화 상자, 선택 **[!DNL Advanced options]** 사용자 지정 SQL 쿼리를 **[!DNL SQL statement]** 섹션. 이 사용자 지정 쿼리는 JSON 이름-값 쌍을 테이블 형식으로 병합하는 데 사용해야 합니다. 공식 설명서에서는 다음 방법에 대한 정보도 제공합니다. [고급 옵션에서 SQL 문을 사용하여 PowerBI 연결](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

사용자 정의된 쿼리를 입력한 후 다음을 선택합니다. **[!DNL OK]** 을 클릭하여 데이터베이스 연결을 계속합니다. 다음을 참조하십시오. [인증](#authentication) 위의 섹션 을 참조하여 이 워크플로우 부분에서 데이터베이스를 연결하는 방법을 확인하십시오.

인증이 완료되면 병합된 데이터의 미리보기가 [!DNL Power BI] 데스크탑 대시보드를 테이블로 표시합니다. 대화 상자 맨 위에 서버 및 데이터베이스 이름이 나열됩니다. 선택 **[!DNL Load]** 가져오기 프로세스를 완료합니다.

이제 시각화를 편집하고 내보내기에서 사용할 수 있습니다. [!DNL Power BI] 데스크탑 앱입니다.

## 데이터를 가져오지 않고 데이터 세트 쿼리 {#direct-query}

다음 **[!DNL DirectQuery]** [!DNL Data Connectivity mode] 로 데이터를 가져오거나 복사하지 않고 직접 데이터 소스 쿼리 [!DNL Power BI] 데스크탑 이 연결 모드를 사용하면 UI를 통해 현재 데이터로 모든 시각화를 새로 고칠 수 있습니다. 그러나 시각화를 생성하거나 새로 고치는 데 필요한 시간은 기본 데이터 소스의 성능에 따라 달라집니다.

다음에 대한 추가 정보: [사용 [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) 뿐만 아니라 그 문제에 대한 포괄적인 논의 [연결 옵션, 사용 사례 및 제한 사항](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) 공식 문서에서 찾을 수 있음 [!DNL PowerBI] 설명서를 참조하십시오.

사용 방법 [!DNL Data Connectivity mode]를 선택하고 **[!DNL DirectQuery]** 다음 전환 **[!DNL Advanced options]** 사용자 지정 SQL 쿼리를 **[!DNL SQL statement]** 섹션. 다음을 확인합니다. **[!DNL Include relationship columns]** 이(가) 선택되어 있습니다. 쿼리를 완료했으면 다음을 선택합니다 **[!DNL OK]** 계속합니다.

쿼리의 미리보기가 나타납니다. 선택 **[!DNL Load]** 을 클릭하여 쿼리 결과를 확인합니다.

## 다음 단계

이 문서를 읽으면 이제 [!DNL Power BI] 데스크탑 앱과 다양한 데이터 연결 모드를 사용할 수 있습니다. 쿼리 작성 및 실행 방법에 대한 자세한 내용은 [쿼리 실행 지침](../best-practices/writing-queries.md).
