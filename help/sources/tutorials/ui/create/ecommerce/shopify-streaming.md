---
title: Ui에서 Shopify 스트리밍 연결 및 데이터 흐름 만들기
description: Platform 사용자 인터페이스를 사용하여 Shopify 스트리밍 소스 연결 및 데이터 흐름을 만드는 방법을 알아봅니다
badge: Beta
exl-id: d53f4ab5-8bdc-4647-83d5-ee898abda0f2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# 소스 연결 및 데이터 흐름 만들기 [!DNL Shopify Streaming] UI를 사용하는 데이터

이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL Shopify Streaming] 플랫폼 사용자 인터페이스를 사용한 소스 연결 및 데이터 흐름.

## 시작하기 {#getting-started}

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

>[!IMPORTANT]
>
>이 자습서에서는 의 사전 요구 사항 설정을 완료해야 합니다. [!DNL Shopify Streaming] 계정입니다. 계정 설정 단계는 [[!DNL Shopify Streaming] 개요](../../../../connectors/ecommerce/shopify-streaming.md).

## 연결 [!DNL Shopify Streaming] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 **전자 상거래** 범주, 선택 [!DNL Shopify Streaming]을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

![Experience Platform 소스 카탈로그](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## 데이터 선택

다음 **[!UICONTROL 데이터 선택]** 플랫폼으로 가져올 데이터를 선택할 수 있는 인터페이스를 제공하는 단계가 나타납니다.

* 인터페이스의 왼쪽 부분은 계정 내에서 사용 가능한 데이터 스트림을 볼 수 있는 브라우저입니다.
* 인터페이스의 오른쪽 부분에서 JSON 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

선택 **[!UICONTROL 파일 업로드]** 로컬 시스템에서 JSON 파일을 업로드합니다. 또는 업로드할 JSON 파일을 [!UICONTROL 파일 드래그 앤 드롭] 패널.

![소스 워크플로우의 데이터 추가 단계입니다.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

파일이 업로드되면 미리보기 인터페이스가 업데이트되어 업로드한 스키마의 미리보기가 표시됩니다. 미리보기 인터페이스를 사용하여 파일의 내용과 구조를 검사할 수 있습니다. 다음을 사용할 수도 있습니다 [!UICONTROL 검색 필드] 스키마 내의 특정 항목에 액세스하는 유틸리티입니다.

완료되면 다음을 선택합니다. **[!UICONTROL 다음]**.

![소스 워크플로우의 미리보기 단계입니다.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## 데이터 흐름 세부 정보

다음 **데이터 흐름 세부 정보** 데이터 흐름의 이름과 설명을 제공할 수 있는 기회와 함께 기존 데이터 세트를 사용하거나 데이터 흐름의 새 데이터 세트를 설정할 수 있는 옵션이 제공되는 단계가 나타납니다. 이 단계에서는 프로필 수집, 오류 진단, 부분 수집 및 경고에 대한 설정을 구성할 수도 있습니다.

완료되면 다음을 선택합니다. **[!UICONTROL 다음]**.

![소스 워크플로우의 데이터 흐름 세부 단계.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## 매핑

다음 [!UICONTROL 매핑] 소스 스키마의 소스 필드를 타겟 스키마의 해당 타겟 XDM 필드에 매핑하는 인터페이스를 제공하는 단계가 나타납니다.

Platform은 사용자가 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑된 필드에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다. 필요에 따라 필드를 직접 매핑하도록 선택하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 파생할 수 있습니다. 매퍼 인터페이스 및 계산된 필드 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

소스 데이터가 성공적으로 매핑되면 다음을 선택합니다. **[!UICONTROL 다음]**.

![소스 워크플로우의 매핑 단계입니다.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## 검토

다음 **[!UICONTROL 리뷰]** 새 데이터 흐름을 만들기 전에 검토할 수 있는 단계가 나타납니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**: 소스 유형, 선택한 소스 파일의 관련 경로 및 해당 소스 파일 내의 열 수를 표시합니다.
* **[!UICONTROL 데이터 세트 할당 및 필드 매핑]**: 데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집되는 데이터 세트를 표시합니다.

데이터 흐름을 검토한 후 다음을 선택합니다 **[!UICONTROL 완료]** 데이터 흐름이 만들어지는 데 시간이 걸릴 수 있습니다.

![소스 워크플로우의 검토 단계입니다.](../../../../images/tutorials/create/shopify-streaming/review.png)

## 스트리밍 끝점 URL 가져오기

스트리밍 데이터 흐름이 만들어지면 이제 스트리밍 끝점 URL을 검색할 수 있습니다. 이 끝점은 Webhook에 가입하는 데 사용되며 스트리밍 소스에서 Experience Platform과 통신할 수 있습니다.

스트리밍 끝점을 검색하려면 [!UICONTROL 데이터 흐름 활동] 방금 만든 데이터 흐름의 페이지이며 끝점을 아래쪽에서 복사합니다. [!UICONTROL 속성] 패널.

![데이터 흐름 활동의 스트리밍 종단점입니다.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## 다음 단계

이 자습서를 따라 소스 연결 및 데이터 흐름을 [!DNL Shopify Streaming] 계정입니다. 에 연결하는 방법에 대한 지침은 [!DNL Shopify Streaming] API를 사용하는 계정은에 대한 자습서를 참조하십시오. [소스 연결 및 스트리밍할 데이터 흐름 만들기 [!DNL Shopify] 흐름 서비스 API를 사용하는 데이터](../../../api/create/ecommerce/shopify-streaming.md).
