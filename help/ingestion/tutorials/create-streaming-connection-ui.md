---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI를 사용하여 스트리밍 연결 만들기
topic: tutorial
translation-type: tm+mt
source-git-commit: 181719e729748adcde62199c9406a97b7a807182

---


# UI를 사용하여 스트리밍 연결 만들기

이 UI 가이드는 Adobe Experience Platform을 사용하여 스트리밍 연결을 만드는 데 도움이 됩니다.

## 시작하기

Experience Platform에 데이터를 스트리밍하기 시작하려면 먼저 스트리밍 HTTP 연결을 만들어야 합니다. 스트리밍 연결을 만들 때 스트리밍 데이터의 소스, 신뢰할 수 있는(인증된) 소스 또는 신뢰할 수 없는(인증되지 않은) 소스에서 데이터를 전송할지 여부와 같은 주요 세부 정보를 제공해야 합니다.

스트리밍 연결을 등록한 후에는 데이터를 플랫폼에 스트리밍하는 데 사용할 수 있는 고유한 URL이 있습니다.

이 안내서를 완료하려면 Adobe Experience Platform에 액세스해야 합니다. 플랫폼에 대한 액세스 권한이 없는 경우 시스템 관리자에게 문의하여 계속 진행하십시오.

## 스트리밍 연결 만들기

Experience Platform UI에 로그인한 후 소스를 클릭하여 **카탈로그** *탭을 엽니다* . 이 페이지에는 사용 가능한 소스 유형이 개별 카드로 표시되며, 각 카드에는 스트리밍 연결에서 데이터 세트로 생성된 데이터 흐름 수가 표시되는 버블이 포함됩니다.

![](../images/streaming-ingestion/ui/click-sources.png)

소스 *페이지에서* HTTP **API**, **Connect**&#x200B;소스를차례로클릭합니다.

![](../images/streaming-ingestion/ui/click-connect-source.png)

HTTP *에 연결* 화면이 나타납니다. 서비스 *세부*&#x200B;사항에서 **새 스트리밍 연결에 대한** 이름과 **설명을** 모두 제공합니다.

계정 *인증*&#x200B;아래에서 스트리밍 연결에 대해 다음 구성 속성을 선택합니다.

- **인증:** 스트리밍 연결에 인증이 필요한지 여부입니다. 인증은 신뢰할 수 있는 소스에서 데이터를 수집합니다. PII(개인 식별 정보)를 처리하는 경우 이 기능을 사용하는 것이 좋습니다.
- **XDM 스키마 호환성:** 이 스트리밍 연결이 XDM 스키마와 호환되는 이벤트를 전송할지 여부입니다. 기본적으로 이 속성은 **켜져**&#x200B;있습니다.

구성 속성 선택이 끝나면 Connect를 **클릭합니다**. 이제 스트리밍 HTTP 연결이 생성되어 소스 작업 영역의 찾아보기 *탭 아래에서* 볼 수 *있습니다* .

![](../images/streaming-ingestion/ui/http-sources-details.png)

찾아보기 *탭에서* 새로 만든 스트리밍 HTTP 연결을 클릭하고 해당 연결의 세부 사항을 볼 수 있습니다.

![](../images/streaming-ingestion/ui/browse-sources.png)

연결 이름의 하이퍼링크를 클릭하면 연결된 데이터 세트를 구성하여 표시할 데이터를 선택할 수 *있습니다*.

![](../images/streaming-ingestion/ui/select-data.png)

새 데이터 집합을 [만들거나 기존 데이터](#create-a-new-dataset) 집합을 [사용할 수 있습니다](#use-an-existing-dataset).

### 새 데이터 집합 만들기

새 데이터 세트를 만들려면 데이터 **세트에**&#x200B;대한 **대상**&#x200B;스키마뿐만 아니라 **이름** , 설명을제공합니다.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

모든 세부 사항을 삽입하고 다음을 클릭하면 **마침을**&#x200B;클릭하기 전에 제공된 세부 사항을 검토하여 **데이터** 세트를 스트리밍 HTTP 연결에 연결할 수 있습니다.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### 기존 데이터 세트 사용

기존 데이터 집합을 사용하려면 출력 데이터 **집합 이름을**&#x200B;선택합니다.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

다음을 클릭한 **후**&#x200B;마침을 클릭하기 전에 세부 사항을 검토하여 **선택한** 데이터 세트를 스트리밍 HTTP 연결에 연결할 수 있습니다.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## 다음 단계

이 튜토리얼을 따라 스트리밍 HTTP 연결을 만들어 스트리밍 끝점을 사용하여 다양한 데이터 통합 API에 액세스할 수 있습니다. API에서 스트리밍 연결을 만들기 위한 지침은 스트리밍 연결 [만들기 자습서를](../tutorials/create-streaming-connection.md)참조하십시오.
