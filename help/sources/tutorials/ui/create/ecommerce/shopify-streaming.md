---
title: Ui에서 Shopify 스트리밍 연결 및 데이터 흐름 만들기
description: Platform 사용자 인터페이스를 사용하여 Shopify 스트리밍 소스 연결 및 데이터 흐름을 만드는 방법을 알아봅니다
badge: Beta
exl-id: d53f4ab5-8bdc-4647-83d5-ee898abda0f2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---

# UI를 사용하여 [!DNL Shopify Streaming] 데이터에 대한 소스 연결 및 데이터 흐름을 만듭니다.

이 자습서에서는 Platform 사용자 인터페이스를 사용하여 [!DNL Shopify Streaming] 소스 연결 및 데이터 흐름을 만드는 단계를 제공합니다.

## 시작하기 {#getting-started}

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

>[!IMPORTANT]
>
>이 자습서에서는 [!DNL Shopify Streaming] 계정에 대한 필수 구성 요소 설정을 완료해야 합니다. 계정 설정 단계는 [[!DNL Shopify Streaming] 개요](../../../../connectors/ecommerce/shopify-streaming.md)를 참조하세요.

## [!DNL Shopify Streaming] 계정 연결

Platform UI의 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**eCommerce** 범주에서 [!DNL Shopify Streaming]을(를) 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![Experience Platform 원본 카탈로그](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## 데이터 선택

플랫폼으로 가져올 데이터를 선택할 수 있는 인터페이스를 제공하는 **[!UICONTROL 데이터 선택]** 단계가 나타납니다.

* 인터페이스의 왼쪽 부분은 계정 내에서 사용 가능한 데이터 스트림을 볼 수 있는 브라우저입니다.
* 인터페이스의 오른쪽 부분에서 JSON 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

로컬 시스템에서 JSON 파일을 업로드하려면 **[!UICONTROL 파일 업로드]**&#x200B;를 선택하십시오. 또는 업로드할 JSON 파일을 [!UICONTROL 파일 끌어다 놓기] 패널로 끌어다 놓을 수 있습니다.

![원본 워크플로의 데이터 추가 단계입니다.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

파일이 업로드되면 미리보기 인터페이스가 업데이트되어 업로드한 스키마의 미리보기가 표시됩니다. 미리보기 인터페이스를 사용하여 파일의 내용과 구조를 검사할 수 있습니다. [!UICONTROL 검색 필드] 유틸리티를 사용하여 스키마 내의 특정 항목에 액세스할 수도 있습니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![원본 워크플로의 미리 보기 단계입니다.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## 데이터 흐름 세부 정보

**데이터 흐름 세부 정보** 단계가 표시되어 기존 데이터 집합을 사용하거나 데이터 흐름의 새 데이터 집합을 설정하는 옵션을 제공하고 데이터 흐름의 이름과 설명을 제공할 수 있습니다. 이 단계에서는 프로필 수집, 오류 진단, 부분 수집 및 경고에 대한 설정을 구성할 수도 있습니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![원본 워크플로의 데이터 흐름 세부 단계입니다.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## 매핑

소스 스키마의 소스 필드를 대상 스키마의 해당 대상 XDM 필드에 매핑할 수 있는 인터페이스를 제공하는 [!UICONTROL 매핑] 단계가 나타납니다.

Platform은 사용자가 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑된 필드에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다. 필요에 따라 필드를 직접 매핑하도록 선택하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 파생할 수 있습니다. 매퍼 인터페이스 및 계산된 필드 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html)를 참조하십시오.

원본 데이터가 성공적으로 매핑되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![원본 워크플로의 매핑 단계입니다.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## 검토

새 데이터 흐름을 만들기 전에 검토할 수 있는 **[!UICONTROL 검토]** 단계가 나타납니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**: 원본 형식, 선택한 원본 파일의 관련 경로 및 해당 원본 파일에 있는 열의 수를 표시합니다.
* **[!UICONTROL 데이터 집합 및 맵 필드 할당]**: 데이터 집합이 준수하는 스키마를 포함하여 소스 데이터가 수집되는 데이터 집합을 표시합니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]**&#x200B;를 선택하고 데이터 흐름이 만들어지도록 잠시 기다립니다.

![원본 워크플로의 검토 단계입니다.](../../../../images/tutorials/create/shopify-streaming/review.png)

## 스트리밍 끝점 URL 가져오기

스트리밍 데이터 흐름이 만들어지면 이제 스트리밍 끝점 URL을 검색할 수 있습니다. 이 끝점은 Webhook에 가입하는 데 사용되며 스트리밍 소스에서 Experience Platform과 통신할 수 있습니다.

스트리밍 끝점을 검색하려면 방금 만든 데이터 흐름의 [!UICONTROL 데이터 흐름 활동] 페이지로 이동한 다음, [!UICONTROL 속성] 패널 아래쪽에서 끝점을 복사합니다.

![데이터 흐름 활동의 스트리밍 끝점입니다.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## 다음 단계

이 자습서를 따라 [!DNL Shopify Streaming] 계정에 대한 소스 연결 및 데이터 흐름을 설정했습니다. API를 사용하여 [!DNL Shopify Streaming] 계정을 연결하는 방법에 대한 지침은 [흐름 서비스 API를 사용하여 소스 연결 및 스트리밍에 대한 데이터 흐름 만들기 [!DNL Shopify] 에 대한 자습서를 참조하십시오](../../../api/create/ecommerce/shopify-streaming.md).
