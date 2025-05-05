---
description: Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식을 기반으로 대상 및 프로필 데이터를 엔드포인트 또는 스토리지 위치에 전달하도록 Experience Platform에 대한 대상 통합 패턴을 구성할 수 있는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 9c59f6edd51c61c1fe2ff69e0adea49e6efb8745
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식을 기반으로 대상과 프로필 데이터를 엔드포인트 또는 스토리지 위치에 제공하기 위해 Experience Platform에 대한 대상 통합 패턴을 구성할 수 있는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.

Destination SDK 설명서는 Adobe Experience Platform Destination SDK을 사용하여 Adobe Experience Platform과의 제품화된 대상 통합을 구성, 테스트 및 릴리스하고 대상을 지속적으로 성장하는 대상 카탈로그의 일부로 만드는 지침을 제공합니다. 또한 Destination SDK을 사용하여 사용자 지정 개인 대상을 만들어 요구 사항에 맞게 데이터를 내보낼 수도 있습니다.

대상 카탈로그를 표시하는 Experience Platform UI의 ![스크린샷입니다.](assets/destinations-catalog-overview.png)

## 빠른 시작 - 필수 정보 살펴보기 {#quick-start}

Destination SDK을 통해 대상 구성 및 제출을 빠르게 시작하려면 아래 링크에서 설명서를 검토하십시오.

>[!BEGINSHADEBOX]

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>구성 페이지</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/functionality/configuration-options.md">모든 구성 옵션 설명</a></li>
                <li> 대상 서버 구성 - <a href="/help/destinations/destination-sdk/functionality/destination-server/server-specs.md">서버 사양</a> 및 <a href="/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md">템플릿 사양</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md">고객 데이터 필드 및 기타 대상 구성 요소</a></li>
                <li><a href="https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">템플릿 및 매크로</a></li>
            </ul>
        </td>
        <td>
            <p><b>안내서</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/overview.md#process">높은 수준의 통합 프로세스</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">스트리밍 대상 구성</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">파일 기반 대상 구성</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md">잠재 고객 프로필을 내보내도록 대상 구성</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/submit-destination.md">게시할 대상 제출</a></li>
            </ul>
        </td>
                <td>
            <p><b>API 참조</b></p>
            <ul>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-servers-and-templates">대상 서버 끝점 API 참조</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-configurations">대상 끝점 API 참조</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Audience-metadata-templates">대상 메타데이터 API 참조</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-testing">API 참조 테스트</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-publishing">대상 게시 API 참조</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>스트리밍 대상 구성 - 치트 시트</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">스트리밍 대상 전체 안내서 구성</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-server/message-format.md">자갈 템플릿을 통한 데이터 변환 이해</a> 및 <a href="/help/destinations/destination-sdk/functionality/destination-server/supported-functions.md">지원되는 템플릿 함수 보기</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md">데이터 수집 정책 이해</a></li>
                <li><a href="https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">라이브 구성 예</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md">스트리밍 대상 테스트</a></li>
            </ul>
        </td>
        <td>
            <p><b>파일 기반 대상 구성 - 치트 시트</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">파일 기반 대상 전체 안내서 구성</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md">내보낸 파일의 파일 형식 구성</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md">Amazon S3 대상에 대한 라이브 구성 예</a></li>
                <li>파일 내보내기 일정 및 파일 이름을 위한 <a href="/help/destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md">일괄 구성</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md">파일 기반 대상 테스트</a></li>
            </ul>
        </td>
        <td>
            <p><b>기타 필수 정보</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/getting-started.md#obtain-authentication-credentials">API를 사용하는 데 필요한 인증 자격 증명 가져오기</a></li>
                <li><a href="/help/destinations/destination-sdk/integration-prerequisites.md">통합 사전 요구 사항</a></li>
                <li><a href="/help/destinations/destination-sdk/glossary.md">Destination SDK 용어 목록</a></li>                
                <li><a href="/help/destinations/destination-sdk/functionality/rate-limiting-retry-policy.md">비율 제한 및 재시도 정책</a></li>
                <li><a href="/help/destinations/destination-sdk/docs-framework/self-service-template.md">대상을 문서화할 셀프서비스 템플릿</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>


>[!ENDSHADEBOX]

## 프로덕션 및 사용자 정의 통합 {#productized-custom-integrations}

>[!IMPORTANT]
>
> 개인 사용자 지정 대상을 만드는 이 기능은 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html) 고객에게만 제공됩니다.

Destination SDK 파트너는 [Experience Platform 카탈로그](../catalog/overview.md)에 제품화된 대상을 추가할 수 있습니다.

1. 사전 구성된 매개 변수를 사용하여 고객 간의 통합 구성을 표준화하고 고객의 설정 환경을 간소화합니다.
2. Experience Platform 대상 카탈로그에 브랜드 대상 카드를 도입하여 고객 설정 및 인식을 간소화합니다.
3. Adobe Experience Platform 및 Adobe Real-time Customer Data Platform과의 제품화된 대상 통합으로 특화되어 있습니다.

Experience Platform 고객인 경우 활성화 요구 사항에 가장 적합한 자신만의 개인 사용자 지정 대상을 작성할 수도 있습니다.

![대상 개발자가 Destination SDK과 상호 작용하는 방법과 Real-Time CDP 고객이 제품화된 대상 및 개인 대상의 이점을 활용하는 방법을 보여 주는 개요 다이어그램](assets/destination-sdk-visual.png)

## 지원되는 통합 유형 {#supported-integration-types}

### 실시간(스트리밍) 통합 {#real-time-integrations}

Adobe Experience Platform은 Destination SDK을 통해 REST API 끝점이 있는 대상과 실시간(스트리밍이라고도 함) 통합을 지원합니다. Experience Platform과 실시간 통합은 다음과 같은 기능을 지원합니다.

* 메시지 변환 및 집계
* 프로필 채우기
* 대상 설정 및 데이터 전송을 초기화하기 위한 구성 가능한 메타데이터 통합
* 구성 가능한 인증
* 대상 구성을 테스트하고 반복할 수 있는 테스트 및 유효성 검사 API 세트입니다

### 파일 기반 통합 {#file-based-integrations}

Destination SDK을 통해 통합을 설정하여 정기적으로 파일을 원하는 저장소 위치로 내보낼 수도 있습니다. Experience Platform과 파일 기반의 통합은 다음과 같은 기능을 지원합니다.

* 여러 지원되는 형식(CSV, Parquet, JSON)으로 파일 내보내기
* 다운스트림 요구 사항을 충족하도록 내보낸 파일의 형식을 구성할 수 있는 구성 가능한 파일 형식 옵션

[통합 필수 구성 요소](integration-prerequisites.md) 문서에서 대상 쪽의 기술 요구 사항을 읽어보고 [구성 옵션](functionality/configuration-options.md) 문서에서 지원되는 모든 구성에 대해 읽어 보십시오

## Destination SDK 액세스 권한 얻기 {#get-access}

Destination SDK 액세스 권한은 Real-Time CDP 고객인 파트너 또는 Experience Platform의 상태에 따라 다릅니다. 자세한 내용은 아래 표를 참조하십시오.

| 파트너 또는 고객 유형 | Destination SDK 액세스 방법 |
---------|----------|
| ISV(Independent Software Vendor) | [Adobe 기술 파트너 프로그램](https://partners.adobe.com/technologyprogram/experiencecloud.html)에 참여하고 Destination SDK에 액세스할 수 있도록 프로비저닝된 Experience Platform 샌드박스를 가져오도록 요청하십시오. |
| 시스템 통합자(SI) | Experience Platform 샌드박스를 프로비저닝하고 Destination SDK에 액세스하려면 [Adobe 솔루션 파트너 프로그램](https://solutionpartners.adobe.com/home.html)에서 Gold 또는 Platinum 수준이어야 합니다. |
| [Real-Time CDP Ultimate 패키지](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html)에서 고객 Experience Platform | 기본적으로 Experience Platform 샌드박스 및 Destination SDK에 액세스하여 조직의 개인 대상을 구축할 수 있습니다. |

{style="table-layout:auto"}

## 고급 프로세스 {#process}

Experience Platform에서 대상을 구성하는 프로세스는 아래에 요약되어 있습니다.

1. ISV 또는 SI인 경우 위의 섹션에서 [액세스 가져오기](#get-access) 정보를 참조하십시오. [Real-Time CDP Ultimate 패키지](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html) 고객은 이 단계를 건너뛸 수 있습니다.
2. [Experience Platform 샌드박스를 프로비저닝하고 대상 작성 권한을 사용하도록 요청](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support)합니다.
3. 통합을 빌드합니다. [스트리밍 대상](guides/configure-destination-instructions.md) 또는 [파일 기반 대상](guides/configure-file-based-destination-instructions.md)을 구성하려면 제품 설명서의 지침을 따르십시오.
4. 통합을 테스트합니다. [스트리밍 대상](testing-api/streaming-destinations/streaming-destination-testing-overview.md) 또는 [파일 기반 대상](testing-api/batch-destinations/file-based-destination-testing-overview.md)을 테스트하려면 제품 설명서의 지침을 따르십시오.
5. [제품화된 통합을 만드는 ISV 또는 SI인 경우](./overview.md#productized-custom-integrations)Adobe 검토를 위해 [통합을 제출](guides/submit-destination.md)하십시오(표준 응답 시간은 5영업일).
6. 제품화된 통합을 만드는 ISV 또는 SI인 경우 [셀프서비스 설명서 프로세스](docs-framework/documentation-instructions.md)를 사용하여 대상 Experience League에 대한 제품 설명서 페이지를 만드십시오.
7. 제품화된 통합의 경우 Adobe이 승인하면 통합이 [Experience Platform 카탈로그](../catalog/overview.md)에 표시됩니다.
8. 통합을 업데이트하려면 동일한 프로세스를 따르십시오.

## 참조 {#reference}

Adobe은 다음 Experience Platform 설명서를 읽고 이해할 것을 권장합니다.

* [Adobe Experience Platform 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=ko)
* [XDM 스키마 컴포지션의 기준](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ko-KR)
* [ID 네임스페이스 개요](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=ko)
