---
title: 데이터 수집 개요
description: 이 문서에서는 보다 자세한 정보를 보려면 해당 개요 설명서에 대한 링크와 함께 Experience Platform으로 데이터를 수집하는 세 가지 주요 방법을 소개합니다.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 1%

---

# 데이터 수집 개요

Adobe Experience Platform에서 데이터 수집은 다양한 소스에서 조직에서 액세스, 사용 및 분석할 수 있는 저장 매체로 데이터를 전송하는 것입니다. Experience Platform의 데이터 수집은 **수집 스트리밍** 및 **수집 일괄 처리**&#x200B;의 두 가지 기본 범주로 그룹화할 수 있습니다.

스트리밍 및 일괄 처리 수집 아래에는 데이터를 Experience Platform에 수집하는 데 사용할 수 있는 여러 가지 방법이 있습니다. 이러한 방법에는 다양한 **소스**&#x200B;를 사용하고 이러한 소스에 연결하여 데이터를 Experience Platform으로 가져오는 방법이 포함됩니다.

Experience Platform에 데이터를 수집할 수 있는 다양한 방법에 대한 개요는 이 문서 를 참조하십시오.

<!-- Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Experience Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Experience Platform services. -->

## 스트리밍 수집 {#streaming}

스트리밍 수집 을 사용하여 클라이언트 및 서버측 장치에서 실시간으로 Experience Platform으로 데이터를 전송할 수 있습니다. Experience Platform은 데이터 입력 기능을 사용하여 들어오는 경험 데이터를 스트리밍할 수 있도록 지원하며, 이는 데이터 레이크 내의 스트리밍 지원 데이터 세트에서 유지됩니다. 데이터 입력 기능은 수집된 데이터를 자동으로 인증하도록 구성하여 신뢰할 수 있는 소스에서 데이터가 오는지 확인할 수 있습니다.

자세한 내용은 [스트리밍 수집 개요](./streaming-ingestion/overview.md)를 참조하십시오.

## 일괄 처리 수집 {#batch}

Experience Platform에서 일괄 처리는 일정 기간 동안 수집된 데이터 세트이며 단일 단위로 함께 처리됩니다. 데이터 세트는 배치로 구성됩니다. 일괄 처리 수집 을 사용하여 데이터를 일괄 처리 파일로 Experience Platform에 수집할 수 있습니다. 배치가 수집되면 배치는 성공적으로 수집된 레코드 수와 실패한 레코드 수 및 관련 오류 메시지를 설명하는 메타데이터를 제공합니다.

플랫 CSV 파일(XDM 스키마에 매핑됨) 및 Parquet 파일과 같이 수동으로 업로드한 데이터 파일은 이 방법을 사용하여 수집해야 합니다.

자세한 내용은 [일괄 처리 수집 개요](./batch-ingestion/overview.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform 소스에 연결하여 데이터를 수집할 수도 있습니다. Experience Platform은 연결하고 데이터를 수집할 수 있는 다양한 데이터 소스의 카탈로그를 유지 관리합니다. 이러한 소스는 Adobe Analytics 소스 또는 Marketo Engage 소스와 같은 기본 Adobe 애플리케이션일 수 있습니다. [!DNL Amazon S3] 원본 및 [!DNL Google Cloud Storage] 원본과 같은 타사 원본에 연결할 수도 있습니다.

소스는 클라우드 저장소, 데이터베이스 및 CRM 시스템과 같은 다양한 카테고리로 그룹화됩니다. 지정된 소스는 일괄 처리 또는 스트리밍 수집을 지원할 수 있습니다.

소스를 사용하면 다양한 데이터 소스 및 다양한 사용 사례 범주의 데이터를 수집할 수 있습니다. 또한 소스를 통한 데이터 수집을 통해 외부 데이터 소스에 대해 인증하고 수집 일정을 구성하고 수집 처리량을 관리할 수 있습니다.

자세한 내용은 [소스 개요](../sources/home.md)를 참조하십시오.

### ML 지원 스키마 만들기 {#ml-assisted-schema-creation}

이제 새로운 데이터 소스를 빠르게 통합하기 위해 머신 러닝 알고리즘을 사용하여 샘플 데이터에서 스키마를 생성할 수 있습니다. 이러한 자동화는 정확한 스키마 생성을 단순화하고 오류를 줄이며 데이터 수집에서 분석 및 통찰력에 이르는 프로세스의 속도를 높입니다.

이 워크플로에 대한 자세한 내용은 [ML 지원 스키마 만들기 안내서](../xdm/ui/ml-assisted-schema-creation.md)를 참조하십시오.

## 데이터 준비 {#data-prep}

데이터 준비는 수집 방법이 아니지만 데이터 수집 과정에서 중요한 부분입니다. 데이터를 Experience Platform에 수집하기 위한 데이터 흐름을 생성하기 전에 데이터 준비 기능을 사용하여 XDM(Experience Data Model)과 데이터를 매핑, 변환 및 검증할 수 있습니다. 데이터 준비는 데이터 수집 프로세스 동안 Experience Platform 사용자 인터페이스에서 &quot;매핑&quot; 단계로 표시됩니다.

자세한 내용은 [데이터 준비 개요](../data-prep/home.md)를 참조하십시오.

## 스트리밍 수집 방법 {#streaming-ingestion-methods}

다음 표에서는 Experience Platform으로 스트리밍 데이터를 수집하는 데 사용할 수 있는 다양한 방법에 대해 설명합니다.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1123px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:31px; vertical-align:top; width:1123px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">스트리밍 소스</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">메서드</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:401px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">일반적인 사용 사례</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">프로토콜</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">고려 사항</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko-KR" style="color:#0563c1; text-decoration:underline">Adobe 웹/모바일 SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">웹 사이트 및 모바일 앱에서 데이터 수집.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">클라이언트측 수집에 기본 설정된 방법입니다.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">푸시, HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">단일 Adobe을 활용하여 여러 SDK 애플리케이션을 구현합니다.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/streaming/http" style="color:#0563c1; text-decoration:underline">HTTP API 커넥터</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">스트리밍 소스, 트랜잭션, 관련 고객 이벤트 및 신호에서 수집.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">푸시, REST API, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">원시 또는 XDM 데이터는 실시간 Edge 세그멘테이션 또는 이벤트 전달 없이 허브로 직접 스트리밍됩니다.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=en" style="color:#0563c1; text-decoration:underline">[!DNL Edge Network] API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">전 세계에 배포된 [!DNL Edge Network]에서 스트리밍 소스, 트랜잭션, 관련 고객 이벤트 및 신호의 컬렉션입니다.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">푸시, REST API, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">데이터는 [!DNL Edge Network]을(를) 통해 스트리밍됩니다. Edge에서 실시간 세그멘테이션 및 이벤트 전달을 지원합니다. </span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en" style="color:#0563c1; text-decoration:underline">Adobe 애플리케이션</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Adobe Analytics, Marketo Engage, Adobe Campaign Managed Services, Adobe Target, Adobe Audience Manager과 같은 애플리케이션에서 데이터 수집</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">푸시, Source 커넥터 및 API</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">권장되는 접근 방법은 기존 애플리케이션 SDK를 사용하는 대신 웹/모바일 SDK으로 마이그레이션하는 것입니다.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">스트리밍 소스</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">엔터프라이즈 이벤트 스트림 수집, 일반적으로 엔터프라이즈 데이터를 여러 다운스트림 애플리케이션에 공유하는 데 사용됩니다. </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">푸시, REST API, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">데이터는 JSON 형식으로 스트리밍되며 XDM 스키마에 매핑될 수 있습니다.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/sdk/streaming-sdk/getting-started" style="color:#0563c1; text-decoration:underline">스트리밍 소스 SDK</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">SDK 스트리밍 셀프 서비스 소스의 셀프 서비스 기능을 사용하여 고유한 데이터 소스를 Experience Platform 소스 카탈로그에 통합합니다.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">푸시, HTTP API, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">파트너 통합 스트리밍 소스의 예로는 Braze, Pendo 및 RainFocus가 있습니다.</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

## 일괄 처리 수집 방법 {#batch-ingestion-methods}

다음 표에서는 배치 데이터를 Experience Platform으로 수집하는 데 사용할 수 있는 다양한 방법에 대해 설명합니다.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1105px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:37px; vertical-align:top; width:1105px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">일괄 처리 소스</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">메서드</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:397px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">일반적인 사용 사례</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">프로토콜</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">고려 사항</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/batch/overview" style="color:#0563c1; text-decoration:underline">일괄 처리 수집 API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">엔터프라이즈 관리 큐에서 수집. 수집 전에 데이터를 준비하고 서식을 지정해야 하는 경우 일괄 처리 수집을 사용합니다.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">푸시, JSON 또는 Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">수집할 배치 및 파일을 관리해야 합니다.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/home" style="color:#0563c1; text-decoration:underline">일괄 처리 소스</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">클라우드 스토리지, CRM 및 마케팅 자동화 애플리케이션에서 데이터를 수집하기 위한 일반적인 접근 방식</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">대량의 이전 데이터를 수집하는 데 이상적입니다.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">풀, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">사전 구성된 예약 간격을 기반으로 한 Source 수집.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/data-landing-zone.html?lang=en" style="color:#0563c1; text-decoration:underline">데이터 랜딩 구역</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Adobe 프로비저닝된 클라우드 기반 파일 스토리지. 샌드박스당 하나의 데이터 랜딩 영역 컨테이너에 액세스할 수 있습니다.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">나중에 Experience Platform으로 수집하려면 파일을 데이터 랜딩 영역에 푸시합니다.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">푸시, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Experience Platform에서는 데이터 랜딩 영역 컨테이너에 업로드된 모든 파일 및 폴더에 대해 엄격한 7일 만료 시간을 적용합니다. 모든 파일과 폴더는 7일 후에 삭제됩니다.</span></span></span></li>
</ul>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/sdk/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">일괄 처리 소스 SDK</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">셀프 서비스 소스 일괄 처리 SDK의 셀프 서비스 기능을 사용하여 고유한 데이터 소스를 Experience Platform 소스 카탈로그와 통합합니다.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">파트너 커넥터 또는 엔터프라이즈 커넥터 설정에 적합한 워크플로 환경에 적합합니다.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">풀, REST API, CSV 또는 JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">파트너 통합 배치 소스의 예로는 Mailchimp, OneTrust, Zendesk 등이 있습니다.</span></span></span></li>
</ul>

<p> </p>
</td>
</tr>
</tbody>
</table>

## 다음 단계 및 추가 리소스

이 문서에서는 [!DNL Experience Platform]의 [!DNL Data Ingestion]에 대한 다양한 측면을 간략하게 소개합니다. 각 수집 방법에 대한 개요 설명서 를 계속 읽으면서 다양한 기능, 사용 사례 및 모범 사례를 숙지하십시오. 또한 아래 수집 개요 비디오를 시청하여 학습을 보완할 수도 있습니다. [!DNL Experience Platform]이(가) 수집된 레코드의 메타데이터를 추적하는 방법에 대한 자세한 내용은 [카탈로그 서비스 개요](../catalog/home.md)를 참조하십시오.

>[!WARNING]
>
>다음 비디오에 사용된 &quot;통합 프로필&quot;이라는 용어가 최신 상태가 아닙니다. [!DNL "Profile"] 또는 [!DNL "Real-Time Customer Profile"] 용어는 [!DNL Experience Platform] 설명서에 사용된 올바른 용어입니다. 최신 기능은 설명서 를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
