---
title: 모세관 스트리밍 이벤트 개요
description: Capillary에서 Experience Platform으로 데이터를 스트리밍하는 방법에 대해 알아봅니다.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>[!DNL Capillary Streaming Events] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 소스 개요에서 [약관](../../home.md#terms-and-conditions)을 참조하십시오.

[!DNL Capillary Technologies]은(는) 전 세계 300개 이상의 브랜드에서 신뢰하는 선도적인 충성도 및 참여 플랫폼입니다. 비즈니스에서 [!DNL Capillary Streaming Events]의 고객 프로필, 충성도 데이터 및 트랜잭션 이벤트를 Adobe Experience Platform으로 원활하게 스트리밍할 수 있도록 하려면 [!DNL Capillary] 소스를 사용하십시오. [!DNL Capillary] 소스를 연결하여 실시간 개인화, 고급 대상자 세분화 및 옴니채널 캠페인 오케스트레이션을 사용할 수 있습니다.

[!DNL Capillary]을(를) Experience Platform과 통합하여 다음과 같은 작업을 수행할 수 있습니다.

* **충성도 포인트, 계층 및 보상**&#x200B;을 실시간으로 동기화합니다.
* 분석 및 활성화를 위해 **트랜잭션 데이터**&#x200B;를 Experience Platform으로 보냅니다.
* 세그멘테이션, 여정 오케스트레이션 및 개인화를 위해 Real-Time CDP, Experience Platform 및 Adobe Journey Optimizer을 활용합니다.

## 전제 조건

[!DNL Capillary]을(를) Adobe Experience Platform에 연결하기 전에 다음을 확인하십시오.

* 유효한 **Adobe 조직 ID** 및 활성화된 Experience Platform 샌드박스에 대한 액세스 권한.
* **[!UICONTROL 계정을 Experience Platform에 연결하려면 계정에 대해]**&#x200B;소스 보기&#x200B;**[!UICONTROL 및]**&#x200B;소스 관리[!DNL Capillary] 권한이 모두 활성화되어야 합니다. 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/ui/overview.md)를 참조하십시오.

### 스키마 만들기

[!DNL Capillary]에서 전송될 수 있는 필드 및 데이터 형식을 저장할 수 있는 데이터 집합을 설명하려면 XDM(경험 데이터 모델) 스키마를 만들어야 합니다.

1. Adobe Experience Platform에 로그인하고 조직의 로그인을 통해 Experience Platform에 액세스합니다.
2. 왼쪽 탐색 패널에서 **[!UICONTROL 스키마]**&#x200B;를 선택하여 [!UICONTROL 스키마] 작업 영역을 엽니다.
3. 오른쪽 상단에서 **[!UICONTROL 스키마 만들기]**&#x200B;를 선택합니다.
4. 스키마 만들기 대화 상자에서 **[!UICONTROL 수동 만들기]**(직접 필드 및 필드 그룹 추가) 또는 **[!UICONTROL ML 지원 만들기]**(CSV 파일을 업로드하고 머신 러닝을 사용하여 권장 스키마를 생성) 중에서 선택합니다.
5. 스키마의 기본 클래스(예: XDM 개인 프로필, XDM ExperienceEvent 또는 기타)를 선택합니다. **[!UICONTROL 기타]**&#x200B;를 선택하는 경우 사용 가능한 사용자 지정 또는 표준 클래스 중에서 선택할 수 있습니다.
6. 스키마에 대한 알기 쉬운 이름 및 설명을 입력합니다.
7. 스키마 편집기를 사용하여 다음과 같은 작업을 수행할 수 있습니다. 필드 그룹(재사용 가능한 필드 블록)을 추가하고, 개별 필드를 정의(이름, 데이터 유형 및 옵션 사용자 정의)하고, 필요한 경우 사용자 정의 데이터 유형 또는 필드 그룹을 생성합니다.
8. 캔버스에서 스키마 구조를 검토합니다. 스키마를 만들려면 **[!UICONTROL 완료]**&#x200B;를 선택하십시오.
9. (선택 사항) 스키마 편집기에서 필요에 따라 필드를 편집하고, 설명을 추가하고, 필드 그룹을 조정합니다.

XDM 스키마를 만드는 방법에 대한 자세한 지침은 [스키마 편집기를 사용하여 스키마 만들기](../../../xdm/tutorials/create-schema-ui.md)에 대한 안내서를 참조하십시오.

### 데이터 세트 만들기

그런 다음 방금 만든 스키마를 참조하는 데이터 세트를 만들어야 합니다.

1. Experience Platform UI의 왼쪽 탐색에서 [!UICONTROL 데이터 세트]를 선택하여 [!UICONTROL 데이터 세트] 작업 영역을 엽니다.
2. 오른쪽 상단에서 **[!UICONTROL 데이터 집합 만들기]**&#x200B;를 선택합니다.
3. 만들기 옵션에서 **[!UICONTROL 스키마에서 데이터 집합 만들기]**&#x200B;를 선택합니다.
4. 목록에서 이전에 만든 XDM 스키마를 검색하고 선택합니다. 스키마를 찾으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
5. 데이터 세트에 대해 고유한 수사적 이름을 입력합니다.
6. 필요한 경우 향후 사용자가 데이터 세트를 식별하는 데 도움이 되는 설명을 추가합니다.
7. 데이터 집합을 만들려면 **[!UICONTROL 완료]**&#x200B;를 선택하십시오.

데이터 집합을 만드는 방법에 대한 자세한 지침은 [데이터 집합 UI 안내서](../../../catalog/datasets/user-guide.md)를 참조하세요.

## Experience Platform에 [!DNL Capillary Streaming Events] 연결

[!DNL Capillary]에 대한 필수 구성 요소 설정을 완료했으면 [[!DNL Capillary Streaming Events] UI 자습서](../../tutorials/ui/create/loyalty/capillary.md)를 읽고 계정을 연결하고 데이터를 [!DNL Capillary]에서 Experience Platform으로 스트리밍하는 방법에 대해 알아보십시오.
